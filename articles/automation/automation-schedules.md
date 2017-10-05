---
title: "Azure 自動化中的排程 | Microsoft Docs"
description: "自動化排程是用來排程讓 Azure 自動化中的 Runbook 自動啟動。 描述如何建立和管理排程，以便以特定時間或循環排程來自動啟動 Runbook。"
services: automation
documentationcenter: 
author: MGoedtel
manager: jwhit
editor: tysonn
ms.assetid: 1c2da639-ad20-4848-920b-88e471b2e1d9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/13/2016
ms.author: magoedte
ms.openlocfilehash: 140bea93c4563666e8cfdf356eaf87500c1aca8e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="7242f-104">在 Azure 自動化中排程 Runbook</span><span class="sxs-lookup"><span data-stu-id="7242f-104">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="7242f-105">若要排程在指定時間啟動 Azure 自動化中的 Runbook，您會將它連結到一個或多個排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-105">To schedule a runbook in Azure Automation to start at a specified time, you link it to one or more schedules.</span></span> <span data-ttu-id="7242f-106">在 Azure 傳統入口網站和 Azure 入口網站中，Runbook 的排程可以設定為執行一次，或以每小時或每日重複發生的排程來執行，您也可以將 Runbook 排程為每週、每月、一週或一個月當中的特定幾天，或每月的特定一天來執行。</span><span class="sxs-lookup"><span data-stu-id="7242f-106">A schedule can be configured to either run once or on a reoccurring hourly or daily schedule for runbooks in the Azure classic portal and for runbooks in the Azure portal,  you can also schedule them for weekly, monthly, specific days of the week or days of the month, or a particular day of the month.</span></span>  <span data-ttu-id="7242f-107">Runbook 可以連結至多個排程，而排程可以有多個與其連結的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7242f-107">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span>

> [!NOTE]
> <span data-ttu-id="7242f-108">排程目前不支援 Azure Automation DSC 組態。</span><span class="sxs-lookup"><span data-stu-id="7242f-108">Schedules do not currently support Azure Automation DSC configurations.</span></span>
> 
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="7242f-109">Windows PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="7242f-109">Windows PowerShell Cmdlets</span></span>
<span data-ttu-id="7242f-110">下表中的 Cmdlet 是用來在 Azure 自動化中透過 Windows PowerShell 建立和管理排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-110">The cmdlets in the following table are used to create and manage schedules with Windows PowerShell in Azure Automation.</span></span> <span data-ttu-id="7242f-111">它們是隨著 [Azure PowerShell 模組](/powershell/azure/overview)的一部分推出。</span><span class="sxs-lookup"><span data-stu-id="7242f-111">They ship as part of the [Azure PowerShell module](/powershell/azure/overview).</span></span>

| <span data-ttu-id="7242f-112">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="7242f-112">Cmdlets</span></span> | <span data-ttu-id="7242f-113">說明</span><span class="sxs-lookup"><span data-stu-id="7242f-113">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="7242f-114">**Azure Resource Manager 的 Cmdlet**</span><span class="sxs-lookup"><span data-stu-id="7242f-114">**Azure Resource Manager cmdlets**</span></span> | |
| [<span data-ttu-id="7242f-115">Get-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="7242f-115">Get-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/get-azurermautomationschedule) |<span data-ttu-id="7242f-116">擷取排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-116">Retrieves a schedule.</span></span> |
| [<span data-ttu-id="7242f-117">New-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="7242f-117">New-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/new-azurermautomationschedule) |<span data-ttu-id="7242f-118">建立新排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-118">Creates a new schedule.</span></span> |
| [<span data-ttu-id="7242f-119">Remove-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="7242f-119">Remove-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |<span data-ttu-id="7242f-120">移除排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-120">Removes a schedule.</span></span> |
| [<span data-ttu-id="7242f-121">Set-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="7242f-121">Set-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/set-azurermautomationschedule) |<span data-ttu-id="7242f-122">設定現有排程的屬性。</span><span class="sxs-lookup"><span data-stu-id="7242f-122">Sets the properties for an existing schedule.</span></span> |
| [<span data-ttu-id="7242f-123">Get-AzureRmAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="7242f-123">Get-AzureRmAutomationScheduledRunbook</span></span>](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |<span data-ttu-id="7242f-124">擷取排程的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7242f-124">Retrieves scheduled runbooks.</span></span> |
| [<span data-ttu-id="7242f-125">Register-AzureRmAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="7242f-125">Register-AzureRmAutomationScheduledRunbook</span></span>](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |<span data-ttu-id="7242f-126">將 Runbook 與排程相關聯。</span><span class="sxs-lookup"><span data-stu-id="7242f-126">Associates a runbook with a schedule.</span></span> |
| [<span data-ttu-id="7242f-127">Unregister-AzureRmAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="7242f-127">Unregister-AzureRmAutomationScheduledRunbook</span></span>](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |<span data-ttu-id="7242f-128">從排程分離 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7242f-128">Dissociates a runbook from a schedule.</span></span> |
| <span data-ttu-id="7242f-129">**Azure 服務管理的 Cmdlet**</span><span class="sxs-lookup"><span data-stu-id="7242f-129">**Azure Service Management cmdlets**</span></span> | |
| [<span data-ttu-id="7242f-130">Get-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="7242f-130">Get-AzureAutomationSchedule</span></span>](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="7242f-131">擷取排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-131">Retrieves a schedule.</span></span> |
| [<span data-ttu-id="7242f-132">New-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="7242f-132">New-AzureAutomationSchedule</span></span>](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="7242f-133">建立新排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-133">Creates a new schedule.</span></span> |
| [<span data-ttu-id="7242f-134">Remove-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="7242f-134">Remove-AzureAutomationSchedule</span></span>](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="7242f-135">移除排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-135">Removes a schedule.</span></span> |
| [<span data-ttu-id="7242f-136">Set-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="7242f-136">Set-AzureAutomationSchedule</span></span>](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="7242f-137">設定現有排程的屬性。</span><span class="sxs-lookup"><span data-stu-id="7242f-137">Sets the properties for an existing schedule.</span></span> |
| [<span data-ttu-id="7242f-138">Get-AzureAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="7242f-138">Get-AzureAutomationScheduledRunbook</span></span>](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |<span data-ttu-id="7242f-139">擷取排程的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7242f-139">Retrieves scheduled runbooks.</span></span> |
| [<span data-ttu-id="7242f-140">Register-AzureAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="7242f-140">Register-AzureAutomationScheduledRunbook</span></span>](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |<span data-ttu-id="7242f-141">將 Runbook 與排程相關聯。</span><span class="sxs-lookup"><span data-stu-id="7242f-141">Associates a runbook with a schedule.</span></span> |
| [<span data-ttu-id="7242f-142">Unregister-AzureAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="7242f-142">Unregister-AzureAutomationScheduledRunbook</span></span>](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |<span data-ttu-id="7242f-143">從排程分離 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7242f-143">Dissociates a runbook from a schedule.</span></span> |

## <a name="creating-a-schedule"></a><span data-ttu-id="7242f-144">建立排程</span><span class="sxs-lookup"><span data-stu-id="7242f-144">Creating a schedule</span></span>
<span data-ttu-id="7242f-145">您可以在 Azure 入口網站、傳統入口網站或使用 Windows PowerShell 為 Runbook 建立新排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-145">You can create a new schedule for runbooks in the Azure portal, in the classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="7242f-146">當您使用 Azure 傳統入口網站或 Azure 入口網站將 Runbook 連結至排程時，也可以選擇建立新的排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-146">You also have the option of creating a new schedule when you link a runbook to a schedule using the Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="7242f-147">執行新的排程工作時，Azure 自動化會使用自動化帳戶中的最新模組。</span><span class="sxs-lookup"><span data-stu-id="7242f-147">Azure Automation will use the latest modules in your Automation account when a new scheduled job is run.</span></span>  <span data-ttu-id="7242f-148">為了避免影響 Runbook 和它們所自動化的處理序，您應該先使用專用於測試的自動化帳戶測試任何具有連結排程的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7242f-148">To avoid impacting your runbooks and the processes they automate, you should first test any runbooks that have linked schedules with an Automation account dedicated for testing.</span></span>  <span data-ttu-id="7242f-149">這將會驗證您排程的 Runbook 會持續正確運作，否則，您可以進一步進行疑難排解，並套用任何必要變更，再將已更新的 Runbook 版本移轉至生產環境。</span><span class="sxs-lookup"><span data-stu-id="7242f-149">This will validate your scheduled runbooks continue to work correctly and if not, you can further troubleshoot and apply any changes required before migrating the updated runbook version to production.</span></span>  
>  <span data-ttu-id="7242f-150">除非您已選取 [模組] 刀鋒視窗中的[更新 Azure 模組](automation-update-azure-modules.md)選項進行手動更新，否則自動化帳戶不會自動取得任何新版本的模組。</span><span class="sxs-lookup"><span data-stu-id="7242f-150">Your Automation account will not automatically get any new versions of modules unless you have updated them manually by selecting the [Update Azure Modules](automation-update-azure-modules.md) option from the **Modules** blade.</span></span> 
>  

### <a name="to-create-a-new-schedule-in-the-azure-portal"></a><span data-ttu-id="7242f-151">在 Azure 入口網站中建立新排程</span><span class="sxs-lookup"><span data-stu-id="7242f-151">To create a new schedule in the Azure portal</span></span>
1. <span data-ttu-id="7242f-152">在 Azure 入口網站中，從您的自動化帳戶按一下 [資產] 圖格以開啟 [資產] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7242f-152">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="7242f-153">按一下 [排程] 圖格以開啟 [排程] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7242f-153">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="7242f-154">在刀鋒視窗的頂端按一下 [加入排程]  。</span><span class="sxs-lookup"><span data-stu-id="7242f-154">Click **Add a schedule** at the top of the blade.</span></span>
4. <span data-ttu-id="7242f-155">在 [新增排程] 刀鋒視窗中，為新排程輸入 [名稱] 並選擇性地輸入 [描述]。</span><span class="sxs-lookup"><span data-stu-id="7242f-155">On the **New schedule** blade, type a **Name** and optionally a **Description** for the new schedule.</span></span>
5. <span data-ttu-id="7242f-156">選取 [一次] 或 [週期]，以選取排程將會執行一次或以週期性的排程執行。</span><span class="sxs-lookup"><span data-stu-id="7242f-156">Select whether the schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="7242f-157">如果選取 [一次]，請指定 [開始時間]，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="7242f-157">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="7242f-158">如果選取 [週期]，則請指定 [開始時間] 和所需的 Runbook 重複頻率：依 [小時]、[天]、[週] 還是 [月] 執行。</span><span class="sxs-lookup"><span data-stu-id="7242f-158">If you select **Recurrence**, specify a **Start time** and the frequency for how often you want the runbook to repeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="7242f-159">如果您在下拉式清單中選取 [週] 或 [月]，刀鋒視窗將會出現 [週期選項]，一經選取，就會顯示 [週期選項] 刀鋒視窗，如果您選取了 [週]，將可以進一步選取星期幾。</span><span class="sxs-lookup"><span data-stu-id="7242f-159">If you select **week** or **month** from the drop-down list, the **Recurrence option** will appear in the blade and upon selection, the **Recurrence option** blade will be presented and you can select the day of week if you selected **week**.</span></span>  <span data-ttu-id="7242f-160">如果您已選取 [月]，則可以在行事曆上選擇要依 [工作日] 或當月的特定幾天，最後則是您是否要在當月最後一天執行，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7242f-160">If you selected **month**, you can choose by **weekdays** or specific days of the month on the calendar and finally, do you want to run it on the last day of the month or not and then click **OK**.</span></span>   

### <a name="to-create-a-new-schedule-in-the-azure-classic-portal"></a><span data-ttu-id="7242f-161">在 Azure 傳統入口網站中建立新排程</span><span class="sxs-lookup"><span data-stu-id="7242f-161">To create a new schedule in the Azure classic portal</span></span>
1. <span data-ttu-id="7242f-162">在 Azure 傳統入口網站中，選取 [自動化]，然後選取自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="7242f-162">In the Azure classic portal, select Automation and then select the name of an Automation account.</span></span>
2. <span data-ttu-id="7242f-163">選取 [ **資產** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7242f-163">Select the **Assets** tab.</span></span>
3. <span data-ttu-id="7242f-164">在視窗的底端按一下 [ **加入設定**]。</span><span class="sxs-lookup"><span data-stu-id="7242f-164">At the bottom of the window, click **Add Setting**.</span></span>
4. <span data-ttu-id="7242f-165">按一下 [ **加入排程**]。</span><span class="sxs-lookup"><span data-stu-id="7242f-165">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="7242f-166">為新排程輸入 [名稱] 並選擇性地輸入 [描述]。您的排程將會以 [一次]、[每小時]、[每日]、[每週] 或 [每月] 的方式執行。</span><span class="sxs-lookup"><span data-stu-id="7242f-166">Type a **Name** and optionally a **Description** for the new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="7242f-167">視您選取的排程類型而定，指定 [ **開始時間** ] 和其他選項。</span><span class="sxs-lookup"><span data-stu-id="7242f-167">Specify a **Start Time** and other options depending on the type of schedule that you selected.</span></span>

### <a name="to-create-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="7242f-168">使用 Windows PowerShell 建立新排程</span><span class="sxs-lookup"><span data-stu-id="7242f-168">To create a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="7242f-169">您可以使用 [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) Cmdlet 在 Azure 自動化中為傳統 Runbook 建立新的排程，或使用 [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) Cmdlet 在 Azure 入口網站中為 Runbook 建立新的排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-169">You can use the [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) cmdlet to create a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="7242f-170">您必須指定排程的開始時間，以及其應該執行的頻率。</span><span class="sxs-lookup"><span data-stu-id="7242f-170">You must specify the start time for the schedule and the frequency it should run.</span></span>

<span data-ttu-id="7242f-171">下列範例命令顯示如何使用 Azure Resource Manager Cmdlet，建立會在每月 15 號到 30 號執行的排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-171">The following sample commands show how to create a schedule for the 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

<span data-ttu-id="7242f-172">下列範例命令顯示如何使用 Azure 服務管理 Cmdlet 建立新的排程，從 2015 年 1 月 20 日起於每日下午 3:30 執行。</span><span class="sxs-lookup"><span data-stu-id="7242f-172">The following sample commands show how to create a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-to-a-runbook"></a><span data-ttu-id="7242f-173">將排程連結至 Runbook</span><span class="sxs-lookup"><span data-stu-id="7242f-173">Linking a schedule to a runbook</span></span>
<span data-ttu-id="7242f-174">Runbook 可以連結至多個排程，而排程可以有多個與其連結的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7242f-174">A runbook can be linked to multiple schedules, and a schedule can have multiple runbooks linked to it.</span></span> <span data-ttu-id="7242f-175">如果 Runbook 有參數，您可以為它們提供值。</span><span class="sxs-lookup"><span data-stu-id="7242f-175">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="7242f-176">您必須為任何必要參數提供值，並可以提供任何選擇性參數的值。</span><span class="sxs-lookup"><span data-stu-id="7242f-176">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="7242f-177">每次此排程啟動 Runbook 時將會使用這些值。</span><span class="sxs-lookup"><span data-stu-id="7242f-177">These values will be used each time the runbook is started by this schedule.</span></span>  <span data-ttu-id="7242f-178">您可以將相同的 Runbook 附加到另一個排程，並指定不同的參數值。</span><span class="sxs-lookup"><span data-stu-id="7242f-178">You can attach the same runbook to another schedule and specify different parameter values.</span></span>

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-portal"></a><span data-ttu-id="7242f-179">使用 Azure 入口網站將排程連結至 Runbook</span><span class="sxs-lookup"><span data-stu-id="7242f-179">To link a schedule to a runbook with the Azure portal</span></span>
1. <span data-ttu-id="7242f-180">在 Azure 入口網站中，從您的自動化帳戶按一下 [Runbook] 圖格，以開啟 [Runbook] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7242f-180">In the Azure portal, from your automation account, click the **Runbooks** tile to open the **Runbooks** blade.</span></span>
2. <span data-ttu-id="7242f-181">按一下要排程的 Runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="7242f-181">Click on the name of the runbook to schedule.</span></span>
3. <span data-ttu-id="7242f-182">如果 Runbook 目前未連結至排程，則將提供您建立新排程或連結至現有排程的選項。</span><span class="sxs-lookup"><span data-stu-id="7242f-182">If the runbook is not currently linked to a schedule, then you will be given the option to create a new schedule or link to an existing schedule.</span></span>  
4. <span data-ttu-id="7242f-183">如果 Runbook 有參數，您可以選取 [修改執行設定 (預設值: Azure)] 選項，隨即便會顯示 [參數] 刀鋒視窗供您據以輸入資訊。</span><span class="sxs-lookup"><span data-stu-id="7242f-183">If the runbook has parameters, you can select the option **Modify run settings (Default:Azure)** and the **Parameters** blade is presented where you can enter the information accordingly.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-the-azure-classic-portal"></a><span data-ttu-id="7242f-184">使用 Azure 傳統入口網站將排程連結至 Runbook</span><span class="sxs-lookup"><span data-stu-id="7242f-184">To link a schedule to a runbook with the Azure classic portal</span></span>
1. <span data-ttu-id="7242f-185">在 Azure 傳統入口網站中，選取 [自動化]，然後按一下自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="7242f-185">In the Azure classic portal, select **Automation** and then click the name of an Automation account.</span></span>
2. <span data-ttu-id="7242f-186">選取 [ **Runbook** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7242f-186">Select the **Runbooks** tab.</span></span>
3. <span data-ttu-id="7242f-187">按一下要排程的 Runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="7242f-187">Click on the name of the runbook to schedule.</span></span>
4. <span data-ttu-id="7242f-188">按一下 [ **排程** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7242f-188">Click the **Schedule** tab.</span></span>
5. <span data-ttu-id="7242f-189">如果 Runbook 目前未連結至排程，則將提供您 [連結至新排程] 或 [連結至現有排程] 選項。</span><span class="sxs-lookup"><span data-stu-id="7242f-189">If the runbook is not currently linked to a schedule, then you will be given the option to **Link to a New Schedule** or **Link to an Existing Schedule**.</span></span>  <span data-ttu-id="7242f-190">如果 Runbook 目前連結至排程，請按一下視窗底部的 **連結** 來存取這些選項。</span><span class="sxs-lookup"><span data-stu-id="7242f-190">If the runbook is currently linked to a schedule, click **Link** at the bottom of the window to access these options.</span></span>
6. <span data-ttu-id="7242f-191">如果 Runbook 有參數，系統會提示您輸入它們的值。</span><span class="sxs-lookup"><span data-stu-id="7242f-191">If the runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="to-link-a-schedule-to-a-runbook-with-windows-powershell"></a><span data-ttu-id="7242f-192">使用 Windows PowerShell 將排程連結至 Runbook</span><span class="sxs-lookup"><span data-stu-id="7242f-192">To link a schedule to a runbook with Windows PowerShell</span></span>
<span data-ttu-id="7242f-193">您可以使用 [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) 將排程連結至傳統 Runbook，或使用 [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) Cmdlet 將排程連結至 Azure 入口網站中的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7242f-193">You can use the [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) to link a schedule to a classic runbook or [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) cmdlet for runbooks in the Azure portal.</span></span>  <span data-ttu-id="7242f-194">您可以使用 Parameters 參數來指定 Runbook 參數的值。</span><span class="sxs-lookup"><span data-stu-id="7242f-194">You can specify values for the runbook’s parameters with the Parameters parameter.</span></span> <span data-ttu-id="7242f-195">請參閱 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) ，以取得指定參數值的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7242f-195">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="7242f-196">下列範例命令顯示如何使用 Azure Resource Manager Cmdlet 與參數，將排程連結至 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7242f-196">The following sample commands show how to link a schedule to a runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
<span data-ttu-id="7242f-197">下列範例命令顯示如何使用 Azure 服務管理 Cmdlet 與參數來連結排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-197">The following sample commands show how to link a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a><span data-ttu-id="7242f-198">停用排程</span><span class="sxs-lookup"><span data-stu-id="7242f-198">Disabling a schedule</span></span>
<span data-ttu-id="7242f-199">停用排程時，與其連結的任何 Runbook 將無法再依該排程執行。</span><span class="sxs-lookup"><span data-stu-id="7242f-199">When you disable a schedule, any runbooks linked to it will no longer run on that schedule.</span></span> <span data-ttu-id="7242f-200">您可以手動停用排程，或在建立排程時為具有頻率的排程設定到期時間。</span><span class="sxs-lookup"><span data-stu-id="7242f-200">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="7242f-201">當到達到期時間時，就會停用排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-201">When the expiration time is reached, the schedule will be disabled.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-portal"></a><span data-ttu-id="7242f-202">從 Azure 入口網站停用排程</span><span class="sxs-lookup"><span data-stu-id="7242f-202">To disable a schedule from the Azure portal</span></span>
1. <span data-ttu-id="7242f-203">在 Azure 入口網站中，從您的自動化帳戶按一下 [資產] 圖格以開啟 [資產] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7242f-203">In the Azure portal, from your automation account, click the **Assets** tile to open the **Assets** blade.</span></span>
2. <span data-ttu-id="7242f-204">按一下 [排程] 圖格以開啟 [排程] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7242f-204">Click the **Schedules** tile to open the **Schedules** blade.</span></span>
3. <span data-ttu-id="7242f-205">按一下排程的名稱以開啟詳細資料刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="7242f-205">Click the name of a schedule to open the details blade.</span></span>
4. <span data-ttu-id="7242f-206">將 [已啟用] 變更為 [否]。</span><span class="sxs-lookup"><span data-stu-id="7242f-206">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-from-the-azure-classic-portal"></a><span data-ttu-id="7242f-207">從 Azure 傳統入口網站停用排程</span><span class="sxs-lookup"><span data-stu-id="7242f-207">To disable a schedule from the Azure classic portal</span></span>
<span data-ttu-id="7242f-208">您可以在 Azure 傳統入口網站中從排程的 [排程詳細資料] 頁面停用排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-208">You can disable a schedule in the Azure classic portal from the Schedule Details page for the schedule.</span></span>

1. <span data-ttu-id="7242f-209">在 Azure 傳統入口網站中，選取 [自動化]，然後按一下自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="7242f-209">In the Azure classic portal, select Automation and then click the name of an Automation account.</span></span>
2. <span data-ttu-id="7242f-210">選取 [資產] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7242f-210">Select the Assets tab.</span></span>
3. <span data-ttu-id="7242f-211">按一下排程的名稱以開啟其詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="7242f-211">Click the name of a schedule to open its detail page.</span></span>
4. <span data-ttu-id="7242f-212">將 [已啟用] 變更為 [否]。</span><span class="sxs-lookup"><span data-stu-id="7242f-212">Change **Enabled** to **No**.</span></span>

### <a name="to-disable-a-schedule-with-windows-powershell"></a><span data-ttu-id="7242f-213">使用 Windows PowerShell 停用排程</span><span class="sxs-lookup"><span data-stu-id="7242f-213">To disable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="7242f-214">您可以使用 [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) Cmdlet 為傳統 Runbook 變更現有排程的屬性，或使用 [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) Cmdlet 為 Azure 入口網站中的 Runbook 變更現有排程的屬性。</span><span class="sxs-lookup"><span data-stu-id="7242f-214">You can use the [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet to change the properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) cmdlet for runbooks in the Azure portal.</span></span> <span data-ttu-id="7242f-215">若要停用排程，請為 **IsEnabled** 參數指定 **false**。</span><span class="sxs-lookup"><span data-stu-id="7242f-215">To disable the schedule, specify **false** for the **IsEnabled** parameter.</span></span>

<span data-ttu-id="7242f-216">下列範例命令顯示如何使用 Azure Resource Manager Cmdlet 來停用 Runbook 的排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-216">The following sample commands show how to disable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

<span data-ttu-id="7242f-217">下列範例命令顯示如何使用 Azure 服務管理 Cmdlet 來停用排程。</span><span class="sxs-lookup"><span data-stu-id="7242f-217">The following sample commands show how to disable a schedule using the Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a><span data-ttu-id="7242f-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7242f-218">Next steps</span></span>
* <span data-ttu-id="7242f-219">若要在 Azure 自動化中開始使用 Runbook，請參閱 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="7242f-219">To get started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 

