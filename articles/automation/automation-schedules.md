---
title: "在 Azure 自動化中的 aaaSchedules |Microsoft 文件"
description: "自動化排程將會自動在 Azure 自動化 toostart 使用的 tooschedule runbook。 描述如何 toocreate 及管理中的排程，以便在特定時間或週期性排程，您可以自動啟動 runbook。"
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
ms.openlocfilehash: 888a5d15fd3442a2b8ab18dd8b0eb4ab9ad0c0d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="6e55a-104">在 Azure 自動化中排程 Runbook</span><span class="sxs-lookup"><span data-stu-id="6e55a-104">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="6e55a-105">tooschedule runbook 在 Azure 自動化 toostart 在指定的時間，您將它連結 tooone 或多個排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-105">tooschedule a runbook in Azure Automation toostart at a specified time, you link it tooone or more schedules.</span></span> <span data-ttu-id="6e55a-106">排程可以設定的 tooeither 執行一次，或在發生每小時或每日排程 hello Azure 傳統入口網站中的 runbook 和 runbook hello Azure 入口網站中，您也可以排定它們的 hello 一週的每週、 每月、 特定天數或天數的 hello月份或特定 hello 月份天數。</span><span class="sxs-lookup"><span data-stu-id="6e55a-106">A schedule can be configured tooeither run once or on a reoccurring hourly or daily schedule for runbooks in hello Azure classic portal and for runbooks in hello Azure portal,  you can also schedule them for weekly, monthly, specific days of hello week or days of hello month, or a particular day of hello month.</span></span>  <span data-ttu-id="6e55a-107">一個 runbook 可以連結的 toomultiple 排程和排程也可以有多個連結的 runbook tooit。</span><span class="sxs-lookup"><span data-stu-id="6e55a-107">A runbook can be linked toomultiple schedules, and a schedule can have multiple runbooks linked tooit.</span></span>

> [!NOTE]
> <span data-ttu-id="6e55a-108">排程目前不支援 Azure Automation DSC 組態。</span><span class="sxs-lookup"><span data-stu-id="6e55a-108">Schedules do not currently support Azure Automation DSC configurations.</span></span>
> 
> 

## <a name="windows-powershell-cmdlets"></a><span data-ttu-id="6e55a-109">Windows PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="6e55a-109">Windows PowerShell Cmdlets</span></span>
<span data-ttu-id="6e55a-110">hello 下表中的 hello cmdlet 會使用的 toocreate 和管理使用 Windows PowerShell 在 Azure 自動化中排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-110">hello cmdlets in hello following table are used toocreate and manage schedules with Windows PowerShell in Azure Automation.</span></span> <span data-ttu-id="6e55a-111">這些 cmdlet 隨附 hello [Azure PowerShell 模組](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6e55a-111">They ship as part of hello [Azure PowerShell module](/powershell/azure/overview).</span></span>

| <span data-ttu-id="6e55a-112">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="6e55a-112">Cmdlets</span></span> | <span data-ttu-id="6e55a-113">說明</span><span class="sxs-lookup"><span data-stu-id="6e55a-113">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="6e55a-114">**Azure Resource Manager 的 Cmdlet**</span><span class="sxs-lookup"><span data-stu-id="6e55a-114">**Azure Resource Manager cmdlets**</span></span> | |
| [<span data-ttu-id="6e55a-115">Get-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="6e55a-115">Get-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/get-azurermautomationschedule) |<span data-ttu-id="6e55a-116">擷取排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-116">Retrieves a schedule.</span></span> |
| [<span data-ttu-id="6e55a-117">New-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="6e55a-117">New-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/new-azurermautomationschedule) |<span data-ttu-id="6e55a-118">建立新排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-118">Creates a new schedule.</span></span> |
| [<span data-ttu-id="6e55a-119">Remove-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="6e55a-119">Remove-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |<span data-ttu-id="6e55a-120">移除排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-120">Removes a schedule.</span></span> |
| [<span data-ttu-id="6e55a-121">Set-AzureRmAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="6e55a-121">Set-AzureRmAutomationSchedule</span></span>](/powershell/module/azurerm.automation/set-azurermautomationschedule) |<span data-ttu-id="6e55a-122">設定現有排程的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="6e55a-122">Sets hello properties for an existing schedule.</span></span> |
| [<span data-ttu-id="6e55a-123">Get-AzureRmAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="6e55a-123">Get-AzureRmAutomationScheduledRunbook</span></span>](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |<span data-ttu-id="6e55a-124">擷取排程的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="6e55a-124">Retrieves scheduled runbooks.</span></span> |
| [<span data-ttu-id="6e55a-125">Register-AzureRmAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="6e55a-125">Register-AzureRmAutomationScheduledRunbook</span></span>](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |<span data-ttu-id="6e55a-126">將 Runbook 與排程相關聯。</span><span class="sxs-lookup"><span data-stu-id="6e55a-126">Associates a runbook with a schedule.</span></span> |
| [<span data-ttu-id="6e55a-127">Unregister-AzureRmAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="6e55a-127">Unregister-AzureRmAutomationScheduledRunbook</span></span>](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |<span data-ttu-id="6e55a-128">從排程分離 Runbook。</span><span class="sxs-lookup"><span data-stu-id="6e55a-128">Dissociates a runbook from a schedule.</span></span> |
| <span data-ttu-id="6e55a-129">**Azure 服務管理的 Cmdlet**</span><span class="sxs-lookup"><span data-stu-id="6e55a-129">**Azure Service Management cmdlets**</span></span> | |
| [<span data-ttu-id="6e55a-130">Get-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="6e55a-130">Get-AzureAutomationSchedule</span></span>](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="6e55a-131">擷取排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-131">Retrieves a schedule.</span></span> |
| [<span data-ttu-id="6e55a-132">New-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="6e55a-132">New-AzureAutomationSchedule</span></span>](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="6e55a-133">建立新排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-133">Creates a new schedule.</span></span> |
| [<span data-ttu-id="6e55a-134">Remove-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="6e55a-134">Remove-AzureAutomationSchedule</span></span>](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="6e55a-135">移除排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-135">Removes a schedule.</span></span> |
| [<span data-ttu-id="6e55a-136">Set-AzureAutomationSchedule</span><span class="sxs-lookup"><span data-stu-id="6e55a-136">Set-AzureAutomationSchedule</span></span>](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |<span data-ttu-id="6e55a-137">設定現有排程的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="6e55a-137">Sets hello properties for an existing schedule.</span></span> |
| [<span data-ttu-id="6e55a-138">Get-AzureAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="6e55a-138">Get-AzureAutomationScheduledRunbook</span></span>](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |<span data-ttu-id="6e55a-139">擷取排程的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="6e55a-139">Retrieves scheduled runbooks.</span></span> |
| [<span data-ttu-id="6e55a-140">Register-AzureAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="6e55a-140">Register-AzureAutomationScheduledRunbook</span></span>](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |<span data-ttu-id="6e55a-141">將 Runbook 與排程相關聯。</span><span class="sxs-lookup"><span data-stu-id="6e55a-141">Associates a runbook with a schedule.</span></span> |
| [<span data-ttu-id="6e55a-142">Unregister-AzureAutomationScheduledRunbook</span><span class="sxs-lookup"><span data-stu-id="6e55a-142">Unregister-AzureAutomationScheduledRunbook</span></span>](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |<span data-ttu-id="6e55a-143">從排程分離 Runbook。</span><span class="sxs-lookup"><span data-stu-id="6e55a-143">Dissociates a runbook from a schedule.</span></span> |

## <a name="creating-a-schedule"></a><span data-ttu-id="6e55a-144">建立排程</span><span class="sxs-lookup"><span data-stu-id="6e55a-144">Creating a schedule</span></span>
<span data-ttu-id="6e55a-145">在 hello 傳統入口網站，或使用 Windows PowerShell，您可以建立 hello Azure 入口網站中 runbook 的新排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-145">You can create a new schedule for runbooks in hello Azure portal, in hello classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="6e55a-146">您也可以建立新的排程，當您將連結使用 hello Azure 傳統 runbook tooa 排程或 Azure 入口網站的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="6e55a-146">You also have hello option of creating a new schedule when you link a runbook tooa schedule using hello Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6e55a-147">Azure 自動化會使用 hello 最新的模組，您的自動化帳戶中，新的排程的工作執行時。</span><span class="sxs-lookup"><span data-stu-id="6e55a-147">Azure Automation will use hello latest modules in your Automation account when a new scheduled job is run.</span></span>  <span data-ttu-id="6e55a-148">影響您的 runbook 和 hello tooavoid 自動化程序，您應該先測試的任何 runbook 都有專用的測試自動化帳戶連結排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-148">tooavoid impacting your runbooks and hello processes they automate, you should first test any runbooks that have linked schedules with an Automation account dedicated for testing.</span></span>  <span data-ttu-id="6e55a-149">這將會驗證您排程的 runbook 繼續 toowork 正確，如果不是，您可以進一步疑難排解並套用任何變更之前需要移轉的 hello 更新 runbook 版本 tooproduction。</span><span class="sxs-lookup"><span data-stu-id="6e55a-149">This will validate your scheduled runbooks continue toowork correctly and if not, you can further troubleshoot and apply any changes required before migrating hello updated runbook version tooproduction.</span></span>  
>  <span data-ttu-id="6e55a-150">您的自動化帳戶不會自動收到任何新版本的模組除非您已更新這些手動選取 hello[更新 Azure 模組](automation-update-azure-modules.md)選項從 hello**模組**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6e55a-150">Your Automation account will not automatically get any new versions of modules unless you have updated them manually by selecting hello [Update Azure Modules](automation-update-azure-modules.md) option from hello **Modules** blade.</span></span> 
>  

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a><span data-ttu-id="6e55a-151">toocreate hello Azure 入口網站中的新排程</span><span class="sxs-lookup"><span data-stu-id="6e55a-151">toocreate a new schedule in hello Azure portal</span></span>
1. <span data-ttu-id="6e55a-152">在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello**資產**磚 tooopen hello**資產**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6e55a-152">In hello Azure portal, from your automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
2. <span data-ttu-id="6e55a-153">按一下 hello**排程**磚 tooopen hello**排程**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6e55a-153">Click hello **Schedules** tile tooopen hello **Schedules** blade.</span></span>
3. <span data-ttu-id="6e55a-154">按一下**加入排程**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="6e55a-154">Click **Add a schedule** at hello top of hello blade.</span></span>
4. <span data-ttu-id="6e55a-155">在 hello**新排程**刀鋒視窗中，輸入**名稱**並選擇性地**描述**hello 新排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-155">On hello **New schedule** blade, type a **Name** and optionally a **Description** for hello new schedule.</span></span>
5. <span data-ttu-id="6e55a-156">選取以選取 hello 排程將執行一次，或重複發生的排程上**一次**或**循環**。</span><span class="sxs-lookup"><span data-stu-id="6e55a-156">Select whether hello schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="6e55a-157">如果選取 一次，請指定 開始時間，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="6e55a-157">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="6e55a-158">如果您選取**循環**，指定**開始時間**和 hello 頻率的頻率 hello runbook toorepeat-由**小時**，**天**，**週**，或由**月份**。</span><span class="sxs-lookup"><span data-stu-id="6e55a-158">If you select **Recurrence**, specify a **Start time** and hello frequency for how often you want hello runbook toorepeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="6e55a-159">如果您選取**週**或**月份**hello 下拉式清單中，從 hello**的週期選項**會出現在 hello 刀鋒視窗中，並在選取項目後, hello**循環選項**刀鋒視窗會提供，而且如果您選取，您可以選取一週天數 hello**週**。</span><span class="sxs-lookup"><span data-stu-id="6e55a-159">If you select **week** or **month** from hello drop-down list, hello **Recurrence option** will appear in hello blade and upon selection, hello **Recurrence option** blade will be presented and you can select hello day of week if you selected **week**.</span></span>  <span data-ttu-id="6e55a-160">如果您選取**月份**，您可以選擇**工作日**或 hello 月的特定幾天 hello 行事曆和最後，您想 toorun 上或不 hello hello 當月最後一天，然後按一下 **[確定]**.</span><span class="sxs-lookup"><span data-stu-id="6e55a-160">If you selected **month**, you can choose by **weekdays** or specific days of hello month on hello calendar and finally, do you want toorun it on hello last day of hello month or not and then click **OK**.</span></span>   

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a><span data-ttu-id="6e55a-161">toocreate hello Azure 傳統入口網站中的新排程</span><span class="sxs-lookup"><span data-stu-id="6e55a-161">toocreate a new schedule in hello Azure classic portal</span></span>
1. <span data-ttu-id="6e55a-162">在 hello Azure 傳統入口網站，選取 自動化，然後選取 hello 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="6e55a-162">In hello Azure classic portal, select Automation and then select hello name of an Automation account.</span></span>
2. <span data-ttu-id="6e55a-163">選取 hello**資產** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6e55a-163">Select hello **Assets** tab.</span></span>
3. <span data-ttu-id="6e55a-164">在 hello hello 視窗底部，按一下 **加入設定**。</span><span class="sxs-lookup"><span data-stu-id="6e55a-164">At hello bottom of hello window, click **Add Setting**.</span></span>
4. <span data-ttu-id="6e55a-165">按一下 [ **加入排程**]。</span><span class="sxs-lookup"><span data-stu-id="6e55a-165">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="6e55a-166">輸入**名稱**並選擇性地**描述**hello 新 schedule.your 排程將執行**一次**，**每小時**， **每日**，**每週**，或**每月**。</span><span class="sxs-lookup"><span data-stu-id="6e55a-166">Type a **Name** and optionally a **Description** for hello new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="6e55a-167">指定**開始時間**和其他選項，視您選取的排程 hello 類型而定。</span><span class="sxs-lookup"><span data-stu-id="6e55a-167">Specify a **Start Time** and other options depending on hello type of schedule that you selected.</span></span>

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="6e55a-168">toocreate 使用 Windows PowerShell 的新排程</span><span class="sxs-lookup"><span data-stu-id="6e55a-168">toocreate a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="6e55a-169">您可以使用 hello [New-azureautomationschedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) cmdlet toocreate 傳統的 runbook，在 Azure 自動化中的新排程或[新增 AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) hello Azure 中的 runbook 的 cmdlet入口網站。</span><span class="sxs-lookup"><span data-stu-id="6e55a-169">You can use hello [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) cmdlet toocreate a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) cmdlet for runbooks in hello Azure portal.</span></span> <span data-ttu-id="6e55a-170">您必須指定 hello hello 排程與 hello 頻率應該執行的開始時間。</span><span class="sxs-lookup"><span data-stu-id="6e55a-170">You must specify hello start time for hello schedule and hello frequency it should run.</span></span>

<span data-ttu-id="6e55a-171">hello 下列範例命令顯示如何 toocreate hello 的排程第 15 和 30，每個月使用 Azure 資源管理員 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6e55a-171">hello following sample commands show how toocreate a schedule for hello 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

<span data-ttu-id="6e55a-172">hello，下列命令範例顯示如何 toocreate 新的排程執行每日下午 3:30 於 2015 年 1 月 20 日起的 Azure 服務管理 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6e55a-172">hello following sample commands show how toocreate a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-tooa-runbook"></a><span data-ttu-id="6e55a-173">連結排程 tooa runbook</span><span class="sxs-lookup"><span data-stu-id="6e55a-173">Linking a schedule tooa runbook</span></span>
<span data-ttu-id="6e55a-174">一個 runbook 可以連結的 toomultiple 排程和排程也可以有多個連結的 runbook tooit。</span><span class="sxs-lookup"><span data-stu-id="6e55a-174">A runbook can be linked toomultiple schedules, and a schedule can have multiple runbooks linked tooit.</span></span> <span data-ttu-id="6e55a-175">如果 Runbook 有參數，您可以為它們提供值。</span><span class="sxs-lookup"><span data-stu-id="6e55a-175">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="6e55a-176">您必須為任何必要參數提供值，並可以提供任何選擇性參數的值。</span><span class="sxs-lookup"><span data-stu-id="6e55a-176">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="6e55a-177">每次透過這個排程啟動 hello runbook 時，會使用這些值。</span><span class="sxs-lookup"><span data-stu-id="6e55a-177">These values will be used each time hello runbook is started by this schedule.</span></span>  <span data-ttu-id="6e55a-178">您可以將附加 hello 相同 runbook tooanother 排程，並指定不同的參數值。</span><span class="sxs-lookup"><span data-stu-id="6e55a-178">You can attach hello same runbook tooanother schedule and specify different parameter values.</span></span>

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a><span data-ttu-id="6e55a-179">toolink 排程 tooa runbook 以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="6e55a-179">toolink a schedule tooa runbook with hello Azure portal</span></span>
1. <span data-ttu-id="6e55a-180">在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello **Runbook**磚 tooopen hello **Runbook**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6e55a-180">In hello Azure portal, from your automation account, click hello **Runbooks** tile tooopen hello **Runbooks** blade.</span></span>
2. <span data-ttu-id="6e55a-181">按一下 hello runbook tooschedule hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="6e55a-181">Click on hello name of hello runbook tooschedule.</span></span>
3. <span data-ttu-id="6e55a-182">如果 hello runbook 不是目前連結的 tooa 排程，然後您將會是給定的 hello 選項 toocreate 的新排程或連結現有的排程 tooan。</span><span class="sxs-lookup"><span data-stu-id="6e55a-182">If hello runbook is not currently linked tooa schedule, then you will be given hello option toocreate a new schedule or link tooan existing schedule.</span></span>  
4. <span data-ttu-id="6e55a-183">如果 hello runbook 有參數，您可以選取 hello 選項**修改回合的設定 (預設： Azure)**和 hello**參數**刀鋒視窗會顯示，您可以據此輸入 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="6e55a-183">If hello runbook has parameters, you can select hello option **Modify run settings (Default:Azure)** and hello **Parameters** blade is presented where you can enter hello information accordingly.</span></span>  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a><span data-ttu-id="6e55a-184">toolink 排程 tooa runbook 以 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="6e55a-184">toolink a schedule tooa runbook with hello Azure classic portal</span></span>
1. <span data-ttu-id="6e55a-185">在 hello Azure 傳統入口網站，選取 **自動化**，然後按一下 hello 的自動化帳戶的名稱。</span><span class="sxs-lookup"><span data-stu-id="6e55a-185">In hello Azure classic portal, select **Automation** and then click hello name of an Automation account.</span></span>
2. <span data-ttu-id="6e55a-186">選取 hello **Runbook**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6e55a-186">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="6e55a-187">按一下 hello runbook tooschedule hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="6e55a-187">Click on hello name of hello runbook tooschedule.</span></span>
4. <span data-ttu-id="6e55a-188">按一下 hello**排程** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6e55a-188">Click hello **Schedule** tab.</span></span>
5. <span data-ttu-id="6e55a-189">如果 hello runbook 不是目前連結的 tooa 排程，則您會獲得 hello 選項太**連結 tooa 新排程**或**連結 tooan 現有排程**。</span><span class="sxs-lookup"><span data-stu-id="6e55a-189">If hello runbook is not currently linked tooa schedule, then you will be given hello option too**Link tooa New Schedule** or **Link tooan Existing Schedule**.</span></span>  <span data-ttu-id="6e55a-190">如果 hello runbook 目前連結的 tooa 排程，請按一下**連結**在 hello 底部 hello 視窗 tooaccess 這些選項。</span><span class="sxs-lookup"><span data-stu-id="6e55a-190">If hello runbook is currently linked tooa schedule, click **Link** at hello bottom of hello window tooaccess these options.</span></span>
6. <span data-ttu-id="6e55a-191">如果 hello runbook 有參數，系統會提示您提供值。</span><span class="sxs-lookup"><span data-stu-id="6e55a-191">If hello runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a><span data-ttu-id="6e55a-192">toolink 排程 tooa runbook 使用 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e55a-192">toolink a schedule tooa runbook with Windows PowerShell</span></span>
<span data-ttu-id="6e55a-193">您可以使用 hello [Register-azureautomationscheduledrunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink 排程 tooa 傳統 runbook 或[暫存器 AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) hello Azure 入口網站中 runbook 的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6e55a-193">You can use hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink a schedule tooa classic runbook or [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) cmdlet for runbooks in hello Azure portal.</span></span>  <span data-ttu-id="6e55a-194">您可以指定 hello runbook 參數的值與 hello 參數參數。</span><span class="sxs-lookup"><span data-stu-id="6e55a-194">You can specify values for hello runbook’s parameters with hello Parameters parameter.</span></span> <span data-ttu-id="6e55a-195">請參閱 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) ，以取得指定參數值的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6e55a-195">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="6e55a-196">hello 下列範例命令顯示如何 toolink 排程 tooa runbook 使用的 Azure 資源管理員 cmdlet 搭配參數。</span><span class="sxs-lookup"><span data-stu-id="6e55a-196">hello following sample commands show how toolink a schedule tooa runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
<span data-ttu-id="6e55a-197">hello 下列範例命令顯示如何 toolink 排程，使用 Azure 服務管理 cmdlet 搭配參數。</span><span class="sxs-lookup"><span data-stu-id="6e55a-197">hello following sample commands show how toolink a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a><span data-ttu-id="6e55a-198">停用排程</span><span class="sxs-lookup"><span data-stu-id="6e55a-198">Disabling a schedule</span></span>
<span data-ttu-id="6e55a-199">當您停用排程時，任何連結的 runbook tooit 將無法再執行該排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-199">When you disable a schedule, any runbooks linked tooit will no longer run on that schedule.</span></span> <span data-ttu-id="6e55a-200">您可以手動停用排程，或在建立排程時為具有頻率的排程設定到期時間。</span><span class="sxs-lookup"><span data-stu-id="6e55a-200">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="6e55a-201">當達到 hello 到期時間時，就會停用 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-201">When hello expiration time is reached, hello schedule will be disabled.</span></span>

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a><span data-ttu-id="6e55a-202">toodisable 從 hello Azure 入口網站的排程</span><span class="sxs-lookup"><span data-stu-id="6e55a-202">toodisable a schedule from hello Azure portal</span></span>
1. <span data-ttu-id="6e55a-203">在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello**資產**磚 tooopen hello**資產**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6e55a-203">In hello Azure portal, from your automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
2. <span data-ttu-id="6e55a-204">按一下 hello**排程**磚 tooopen hello**排程**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="6e55a-204">Click hello **Schedules** tile tooopen hello **Schedules** blade.</span></span>
3. <span data-ttu-id="6e55a-205">按一下排程 tooopen hello 詳細資料 刀鋒視窗的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="6e55a-205">Click hello name of a schedule tooopen hello details blade.</span></span>
4. <span data-ttu-id="6e55a-206">變更**啟用**太**否**。</span><span class="sxs-lookup"><span data-stu-id="6e55a-206">Change **Enabled** too**No**.</span></span>

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a><span data-ttu-id="6e55a-207">toodisable 從 hello Azure 傳統入口網站的排程</span><span class="sxs-lookup"><span data-stu-id="6e55a-207">toodisable a schedule from hello Azure classic portal</span></span>
<span data-ttu-id="6e55a-208">您可以停用 hello hello hello 排程的排程詳細資料頁面從 Azure 傳統入口網站中的排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-208">You can disable a schedule in hello Azure classic portal from hello Schedule Details page for hello schedule.</span></span>

1. <span data-ttu-id="6e55a-209">在 hello Azure 傳統入口網站，選取 自動化，然後按一下 hello 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="6e55a-209">In hello Azure classic portal, select Automation and then click hello name of an Automation account.</span></span>
2. <span data-ttu-id="6e55a-210">選取 hello 資產 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="6e55a-210">Select hello Assets tab.</span></span>
3. <span data-ttu-id="6e55a-211">按一下排程 tooopen hello 名稱及其詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="6e55a-211">Click hello name of a schedule tooopen its detail page.</span></span>
4. <span data-ttu-id="6e55a-212">變更**啟用**太**否**。</span><span class="sxs-lookup"><span data-stu-id="6e55a-212">Change **Enabled** too**No**.</span></span>

### <a name="toodisable-a-schedule-with-windows-powershell"></a><span data-ttu-id="6e55a-213">toodisable 排程與 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="6e55a-213">toodisable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="6e55a-214">您可以使用 hello [Set-azureautomationschedule](http://msdn.microsoft.com/library/azure/dn690270.aspx)傳統 runbook 的現有排程的 cmdlet toochange hello 屬性或[組 AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) hello Azure 中的 runbook 的 cmdlet入口網站。</span><span class="sxs-lookup"><span data-stu-id="6e55a-214">You can use hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet toochange hello properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) cmdlet for runbooks in hello Azure portal.</span></span> <span data-ttu-id="6e55a-215">toodisable hello 排程、 指定**false** hello **IsEnabled**參數。</span><span class="sxs-lookup"><span data-stu-id="6e55a-215">toodisable hello schedule, specify **false** for hello **IsEnabled** parameter.</span></span>

<span data-ttu-id="6e55a-216">hello 下列範例命令顯示如何 toodisable runbook 使用的 Azure 資源管理員 cmdlet 的排程。</span><span class="sxs-lookup"><span data-stu-id="6e55a-216">hello following sample commands show how toodisable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

<span data-ttu-id="6e55a-217">hello 下列命令範例示範如何排程使用 toodisable hello Azure 服務管理 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="6e55a-217">hello following sample commands show how toodisable a schedule using hello Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a><span data-ttu-id="6e55a-218">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6e55a-218">Next steps</span></span>
* <span data-ttu-id="6e55a-219">請參閱 < 開始使用 Azure 自動化中的 runbook tooget [Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="6e55a-219">tooget started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 

