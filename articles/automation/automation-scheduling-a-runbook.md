---
title: "在 Azure 自動化中排程 Runbook | Microsoft Docs"
description: "描述如何在 Azure 自動化中建立排程，以便以特定時間或循環排程來自動啟動 Runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 710979ff-99d8-41e4-ac6d-6bf26b8ea654
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 12/09/2016
ms.author: bwren
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 52f1d55f141bb1b3948e3b7039cfc131a5e407b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="aa14f-103">在 Azure 自動化中排程 Runbook</span><span class="sxs-lookup"><span data-stu-id="aa14f-103">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="aa14f-104">若要排程在指定時間啟動 Azure 自動化中的 Runbook，您會將它連結到一個或多個排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-104">To schedule a runbook in Azure Automation to start at a specified time, you link it to one or more schedules.</span></span> <span data-ttu-id="aa14f-105">在 Azure 傳統入口網站和 Azure 入口網站中，Runbook 的排程可以設定為執行一次，或以每小時或每日重複發生的排程來執行，另外，您也可以將 Runbook 排程為每週、每月、一週或一個月當中的特定幾天，或每月的特定一天來執行。</span><span class="sxs-lookup"><span data-stu-id="aa14f-105">A schedule can be configured to either run once or on a reoccurring hourly or daily schedule for runbooks in the Azure classic portal and for runbooks in the Azure portal,  you can additionally schedule them for weekly, monthly, specific days of the week or days of the month, or a particular day of the month.</span></span>  <span data-ttu-id="aa14f-106">Runbook 可以連結至多個排程，而排程可以有多個與其連結的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="aa14f-106">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span>

## <a name="creating-a-schedule"></a><span data-ttu-id="aa14f-107">建立排程</span><span class="sxs-lookup"><span data-stu-id="aa14f-107">Creating a schedule</span></span>
<span data-ttu-id="aa14f-108">您可以在 Azure 入口網站、傳統入口網站或使用 Windows PowerShell 為 Runbook 建立新排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-108">You can create a new schedule for runbooks in the Azure portal, in the classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="aa14f-109">當您使用 Azure 傳統入口網站或 Azure 入口網站將 Runbook 連結至排程時，也可以選擇建立新的排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-109">You also have the option of creating a new schedule when you link a runbook to a schedule using the Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="aa14f-110">當您將排程與 Runbook 產生關聯時，自動化會在您的帳戶中儲存目前的模組版本，並將它們連結到該排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-110">When you associate a schedule with a runbook, Automation stores the current versions of the modules in your account and links them to that schedule.</span></span>  <span data-ttu-id="aa14f-111">這表示如果在建立排程時，您的帳戶中有 1.0 版的模組，而後將模組更新為 2.0 版，則此排程會繼續使用 1.0。</span><span class="sxs-lookup"><span data-stu-id="aa14f-111">This means that if you had a module with version 1.0 in your account when you created a schedule and then update the module to version 2.0, the schedule will continue to use 1.0.</span></span>  <span data-ttu-id="aa14f-112">若要使用更新後的模組版本，您必須建立新的排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-112">In order to use the updated module version, you must create a new schedule.</span></span> 
> 
> 

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a><span data-ttu-id="aa14f-113">在 Azure 傳統入口網站中建立新排程</span><span class="sxs-lookup"><span data-stu-id="aa14f-113">To create a new schedule in the Azure classic portal</span></span>
1. <span data-ttu-id="aa14f-114">在 Azure 傳統入口網站中選取 [自動化]，然後選取自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="aa14f-114">In the Azure classic portal, select Automation and then then select the name of an automation account.</span></span>
2. <span data-ttu-id="aa14f-115">選取 [ **資產** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="aa14f-115">Select the **Assets** tab.</span></span>
3. <span data-ttu-id="aa14f-116">在視窗的底端按一下 [ **加入設定**]。</span><span class="sxs-lookup"><span data-stu-id="aa14f-116">At the bottom of the window, click **Add Setting**.</span></span>
4. <span data-ttu-id="aa14f-117">按一下 [ **加入排程**]。</span><span class="sxs-lookup"><span data-stu-id="aa14f-117">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="aa14f-118">為新排程輸入 [名稱] 並選擇性地輸入 [描述]。您的排程將會以 [一次]、[每小時]、[每日]、[每週] 或 [每月] 的方式執行。</span><span class="sxs-lookup"><span data-stu-id="aa14f-118">Type a **Name** and optionally a **Description** for the new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="aa14f-119">視您選取的排程類型而定，指定 [ **開始時間** ] 和其他選項。</span><span class="sxs-lookup"><span data-stu-id="aa14f-119">Specify a **Start Time** and other options depending on the type of schedule that you selected.</span></span>

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a><span data-ttu-id="aa14f-120">在 Azure 入口網站中建立新排程</span><span class="sxs-lookup"><span data-stu-id="aa14f-120">To create a new schedule in the Azure portal</span></span>
1. <span data-ttu-id="aa14f-121">在 Azure 入口網站中，從您的自動化帳戶按一下 [資產] 圖格以開啟 [資產] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="aa14f-121">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="aa14f-122">按一下 [排程] 圖格以開啟 [排程] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="aa14f-122">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="aa14f-123">在刀鋒視窗的頂端按一下 [加入排程]  。</span><span class="sxs-lookup"><span data-stu-id="aa14f-123">Click **Add a schedule** at the top of the blade.</span></span>
4. <span data-ttu-id="aa14f-124">在 [新增排程] 刀鋒視窗中，為新排程輸入 [名稱] 並選擇性地輸入 [描述]。</span><span class="sxs-lookup"><span data-stu-id="aa14f-124">On the **New schedule** blade, type a **Name** and optionally a **Description** for the new schedule.</span></span>
5. <span data-ttu-id="aa14f-125">選取 [一次] 或 [週期]，以選取排程將會執行一次或以週期性的排程執行。</span><span class="sxs-lookup"><span data-stu-id="aa14f-125">Select whether the schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="aa14f-126">如果選取 [一次]，請指定 [開始時間]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="aa14f-126">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="aa14f-127">如果選取 [週期]，則請指定 [開始時間] 和所需的 Runbook 重複頻率：依 [小時]、[天]、[週] 還是 [月] 執行。</span><span class="sxs-lookup"><span data-stu-id="aa14f-127">If you select **Recurrence**, specify a **Start time** and the frequency for how often you want the runbook to repeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="aa14f-128">如果您在下拉式清單中選取 [週] 或 [月]，刀鋒視窗將會出現 [週期選項]，一經選取，就會顯示 [週期選項] 刀鋒視窗，如果您選取了 [週]，將可以進一步選取星期幾。</span><span class="sxs-lookup"><span data-stu-id="aa14f-128">If you select **week** or **month** from the drop-down list, the **Recurrence option** will appear in the blade and upon selection, the **Recurrence option** blade will be presented and you can select the day of week if you selected **week**.</span></span>  <span data-ttu-id="aa14f-129">如果您選取了 [月]，則可以在行事曆上選擇要依 [工作日] 或當月的特定幾天，最後則是您是否要在當月最後一天執行，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="aa14f-129">If you selected **month**, you can choose by **week days** or specific days of the month on the calendar and finally, do you want to run it on the last day of the month or not and then click **OK**.</span></span>   

### <a name="to-create-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="aa14f-130">使用 Windows PowerShell 建立新排程</span><span class="sxs-lookup"><span data-stu-id="aa14f-130">To create a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="aa14f-131">您可以使用 [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) Cmdlet 在 Azure 自動化中為傳統 Runbook 建立新的排程，或使用 [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) Cmdlet 在 Azure 入口網站中為 Runbook 建立新的排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-131">You can use the [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet to create a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="aa14f-132">您必須指定排程的開始時間，以及其應該執行的頻率。</span><span class="sxs-lookup"><span data-stu-id="aa14f-132">You must specify the start time for the schedule and the frequency it should run.</span></span>

<span data-ttu-id="aa14f-133">下列範例命令顯示如何使用 Azure 服務管理 Cmdlet 建立新的排程，從 2015 年 1 月 20 日起於每日下午 3:30 執行。</span><span class="sxs-lookup"><span data-stu-id="aa14f-133">The following sample commands show how to create a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

<span data-ttu-id="aa14f-134">下列範例命令顯示如何使用 Azure Resource Manager Cmdlet，建立會在每月 15 號到 30 號執行的排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-134">The following sample commands shows how to create a schedule for the 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-to-a-runbook"></a><span data-ttu-id="aa14f-135">將排程連結至 Runbook</span><span class="sxs-lookup"><span data-stu-id="aa14f-135">Linking a schedule to a runbook</span></span>
<span data-ttu-id="aa14f-136">Runbook 可以連結至多個排程，而排程可以有多個與其連結的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="aa14f-136">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span> <span data-ttu-id="aa14f-137">如果 Runbook 有參數，您可以為它們提供值。</span><span class="sxs-lookup"><span data-stu-id="aa14f-137">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="aa14f-138">您必須為任何必要參數提供值，並可以提供任何選擇性參數的值。</span><span class="sxs-lookup"><span data-stu-id="aa14f-138">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="aa14f-139">每次此排程啟動 Runbook 時將會使用這些值。</span><span class="sxs-lookup"><span data-stu-id="aa14f-139">These values will be used each time the runbook is started by this schedule.</span></span>  <span data-ttu-id="aa14f-140">您可以將相同的 Runbook 附加到另一個排程，並指定不同的參數值。</span><span class="sxs-lookup"><span data-stu-id="aa14f-140">You can attach the same runbook to another schedule and specify different parameter values.</span></span>

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a><span data-ttu-id="aa14f-141">使用 Azure 傳統入口網站將排程連結至 Runbook</span><span class="sxs-lookup"><span data-stu-id="aa14f-141">To link a schedule to a runbook with the Azure classic portal</span></span>
1. <span data-ttu-id="aa14f-142">在 Azure 傳統入口網站中，選取 [自動化]  ，然後按一下自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="aa14f-142">In the Azure classic portal, select **Automation** and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="aa14f-143">選取 [ **Runbook** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="aa14f-143">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="aa14f-144">按一下要排程的 Runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="aa14f-144">Click on the name of the runbook to schedule.</span></span>
4. <span data-ttu-id="aa14f-145">按一下 [ **排程** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="aa14f-145">Click the **Schedule** tab.</span></span>
5. <span data-ttu-id="aa14f-146">如果 Runbook 目前未連結至排程，則將提供您 [連結至新排程] 或 [連結至現有排程] 選項。</span><span class="sxs-lookup"><span data-stu-id="aa14f-146">If the runbook is not currently linked to a schedule, then you will be given the option to **Link to a New Schedule** or **Link to an Existing Schedule**.</span></span>  <span data-ttu-id="aa14f-147">如果 Runbook 目前連結至排程，請按一下視窗底部的 **連結** 來存取這些選項。</span><span class="sxs-lookup"><span data-stu-id="aa14f-147">If the runbook is currently linked to a schedule, click **Link** at the bottom of the window to access these options.</span></span>
6. <span data-ttu-id="aa14f-148">如果 Runbook 有參數，系統會提示您輸入它們的值。</span><span class="sxs-lookup"><span data-stu-id="aa14f-148">If the runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a><span data-ttu-id="aa14f-149">使用 Azure 入口網站將排程連結至 Runbook</span><span class="sxs-lookup"><span data-stu-id="aa14f-149">To link a schedule to a runbook with the Azure portal</span></span>
1. <span data-ttu-id="aa14f-150">在 Azure 入口網站中，從您的自動化帳戶按一下 [Runbook] 圖格，以開啟 [Runbook] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="aa14f-150">In the Azure portal, from your automation account, click the **Runbooks** tile to open the **Runbooks** blade.</span></span>
2. <span data-ttu-id="aa14f-151">按一下要排程的 Runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="aa14f-151">Click on the name of the runbook to schedule.</span></span>
3. <span data-ttu-id="aa14f-152">如果 Runbook 目前未連結至排程，則將提供您建立新排程或連結至現有排程的選項。</span><span class="sxs-lookup"><span data-stu-id="aa14f-152">If the runbook is not currently linked to a schedule, then you will be given the option to create a new schedule or link to an existing schedule.</span></span>  
4. <span data-ttu-id="aa14f-153">如果 Runbook 有參數，您可以選取 [修改執行設定 (預設值: Azure)] 選項，隨即便會顯示 [參數] 刀鋒視窗供您據以輸入資訊。</span><span class="sxs-lookup"><span data-stu-id="aa14f-153">If the runbook has parameters, you can select the option **Modify run settings (Default:Azure)** and the **Parameters** blade is presented where you can enter the information accordingly.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a><span data-ttu-id="aa14f-154">使用 Windows PowerShell 將排程連結至 Runbook</span><span class="sxs-lookup"><span data-stu-id="aa14f-154">To link a schedule to a runbook with Windows PowerShell</span></span>
<span data-ttu-id="aa14f-155">您可以使用 [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) 將排程連結至傳統 Runbook，或使用 [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) Cmdlet 將排程連結至 Azure 入口網站中的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="aa14f-155">You can use the [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) to link a schedule to a classic runbook or [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet for runbooks in the Azure portal.</span></span>  <span data-ttu-id="aa14f-156">您可以使用 Parameters 參數來指定 Runbook 參數的值。</span><span class="sxs-lookup"><span data-stu-id="aa14f-156">You can specify values for the runbook’s parameters with the Parameters parameter.</span></span> <span data-ttu-id="aa14f-157">請參閱 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) ，以取得指定參數值的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="aa14f-157">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="aa14f-158">下列範例命令顯示如何使用 Azure 服務管理 Cmdlet 與參數來連結排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-158">The following sample commands show how to link a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

<span data-ttu-id="aa14f-159">下列範例命令顯示如何使用 Azure Resource Manager Cmdlet 與參數，將排程連結至 Runbook。</span><span class="sxs-lookup"><span data-stu-id="aa14f-159">The following sample commands show how to link a schedule to a runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a><span data-ttu-id="aa14f-160">停用排程</span><span class="sxs-lookup"><span data-stu-id="aa14f-160">Disabling a schedule</span></span>
<span data-ttu-id="aa14f-161">停用排程時，與其連結的任何 Runbook 將無法再依該排程執行。</span><span class="sxs-lookup"><span data-stu-id="aa14f-161">When you disable a schedule, any runbooks linked to it will no longer run on that schedule.</span></span> <span data-ttu-id="aa14f-162">您可以手動停用排程，或在建立排程時為具有頻率的排程設定到期時間。</span><span class="sxs-lookup"><span data-stu-id="aa14f-162">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="aa14f-163">當到達到期時間時，就會停用排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-163">When the expiration time is reached, the schedule will be disabled.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a><span data-ttu-id="aa14f-164">從 Azure 傳統入口網站停用排程</span><span class="sxs-lookup"><span data-stu-id="aa14f-164">To disable a schedule from the Azure classic portal</span></span>
<span data-ttu-id="aa14f-165">您可以在 Azure 傳統入口網站中從排程的 [排程詳細資料] 頁面停用排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-165">You can disable a schedule in the Azure classic portal from the Schedule Details page for the schedule.</span></span>

1. <span data-ttu-id="aa14f-166">在 Azure 傳統入口網站中，選取 [自動化]，然後按一下自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="aa14f-166">In the Azure classic portal, select Automation and then then click the name of an automation account.</span></span>
2. <span data-ttu-id="aa14f-167">選取 [資產] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="aa14f-167">Select the Assets tab.</span></span>
3. <span data-ttu-id="aa14f-168">按一下排程的名稱以開啟其詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="aa14f-168">Click the name of a schedule to open its detail page.</span></span>
4. <span data-ttu-id="aa14f-169">將 [已啟用] 變更為 [否]。</span><span class="sxs-lookup"><span data-stu-id="aa14f-169">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-portal"></a><span data-ttu-id="aa14f-170">從 Azure 入口網站停用排程</span><span class="sxs-lookup"><span data-stu-id="aa14f-170">To disable a schedule from the Azure portal</span></span>
1. <span data-ttu-id="aa14f-171">在 Azure 入口網站中，從您的自動化帳戶按一下 [資產] 圖格以開啟 [資產] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="aa14f-171">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="aa14f-172">按一下 [排程] 圖格以開啟 [排程] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="aa14f-172">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="aa14f-173">按一下排程的名稱以開啟詳細資料刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="aa14f-173">Click the name of a schedule to open the details blade.</span></span>
4. <span data-ttu-id="aa14f-174">將 [已啟用] 變更為 [否]。</span><span class="sxs-lookup"><span data-stu-id="aa14f-174">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-with-windows-powershell"></a><span data-ttu-id="aa14f-175">使用 Windows PowerShell 停用排程</span><span class="sxs-lookup"><span data-stu-id="aa14f-175">To disable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="aa14f-176">您可以使用 [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) Cmdlet 為傳統 Runbook 變更現有排程的屬性，或使用 [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) Cmdlet 為 Azure 入口網站中的 Runbook 變更現有排程的屬性。</span><span class="sxs-lookup"><span data-stu-id="aa14f-176">You can use the [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet to change the properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="aa14f-177">若要停用排程，請為 **IsEnabled** 參數指定 **false**。</span><span class="sxs-lookup"><span data-stu-id="aa14f-177">To disable the schedule, specify **false** for the **IsEnabled** parameter.</span></span>

<span data-ttu-id="aa14f-178">下列範例命令顯示如何使用 Azure 服務管理 Cmdlet 來停用排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-178">The following sample commands show how to disable a schedule using the Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

<span data-ttu-id="aa14f-179">下列範例命令顯示如何使用 Azure Resource Manager Cmdlet 來停用 Runbook 的排程。</span><span class="sxs-lookup"><span data-stu-id="aa14f-179">The following sample commands show how to disable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a><span data-ttu-id="aa14f-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="aa14f-180">Next steps</span></span>
* <span data-ttu-id="aa14f-181">若要深入了解如何使用排程，請參閱 [Azure 自動化中的排程資產](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span><span class="sxs-lookup"><span data-stu-id="aa14f-181">To learn more about working with schedules, see [Schedule Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span></span>
* <span data-ttu-id="aa14f-182">若要在 Azure 自動化中開始使用 Runbook，請參閱 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="aa14f-182">To get started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 

