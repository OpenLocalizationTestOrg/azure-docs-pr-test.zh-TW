---
title: "Azure 自動化中 runbook aaaScheduling |Microsoft 文件"
description: "描述如何在 Azure 自動化中排程 toocreate 以便在特定時間或週期性排程，您可以自動啟動 runbook。"
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
ms.openlocfilehash: c215b7ff6aa200466f3be566facba3c0cffcc924
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="scheduling-a-runbook-in-azure-automation"></a><span data-ttu-id="cbf5c-103">在 Azure 自動化中排程 Runbook</span><span class="sxs-lookup"><span data-stu-id="cbf5c-103">Scheduling a runbook in Azure Automation</span></span>
<span data-ttu-id="cbf5c-104">tooschedule runbook 在 Azure 自動化 toostart 在指定的時間，您將它連結 tooone 或多個排程。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-104">tooschedule a runbook in Azure Automation toostart at a specified time, you link it tooone or more schedules.</span></span> <span data-ttu-id="cbf5c-105">排程可以設定的 tooeither 執行一次或重複每小時或每日排程 hello Azure 傳統入口網站中的 runbook 和 runbook hello Azure 入口網站中，您可以另外排定它們 hello 一週的每週、 每月、 特定天數或天數hello 月份或 hello 月份的某一天。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-105">A schedule can be configured tooeither run once or on a reoccurring hourly or daily schedule for runbooks in hello Azure classic portal and for runbooks in hello Azure portal,  you can additionally schedule them for weekly, monthly, specific days of hello week or days of hello month, or a particular day of hello month.</span></span>  <span data-ttu-id="cbf5c-106">一個 runbook 可以連結的 toomultiple 排程和排程也可以有多個連結的 runbook tooit。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-106">A runbook can be linked toomultiple schedules, and a schedule can have multiple runbooks linked tooit.</span></span>

## <a name="creating-a-schedule"></a><span data-ttu-id="cbf5c-107">建立排程</span><span class="sxs-lookup"><span data-stu-id="cbf5c-107">Creating a schedule</span></span>
<span data-ttu-id="cbf5c-108">在 hello 傳統入口網站，或使用 Windows PowerShell，您可以建立 hello Azure 入口網站中 runbook 的新排程。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-108">You can create a new schedule for runbooks in hello Azure portal, in hello classic portal, or with Windows PowerShell.</span></span> <span data-ttu-id="cbf5c-109">您也可以建立新的排程，當您將連結使用 hello Azure 傳統 runbook tooa 排程或 Azure 入口網站的 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-109">You also have hello option of creating a new schedule when you link a runbook tooa schedule using hello Azure classic or Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="cbf5c-110">當您將排程與 runbook 產生關聯時，自動化帳戶中儲存的 hello 模組的 hello 目前版本，並連結 toothat 排程。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-110">When you associate a schedule with a runbook, Automation stores hello current versions of hello modules in your account and links them toothat schedule.</span></span>  <span data-ttu-id="cbf5c-111">這表示如果在您建立排程時，在您的帳戶已有同名的模組版本 1.0，然後更新 hello 模組 tooversion 2.0 hello 排程會繼續 toouse 1.0。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-111">This means that if you had a module with version 1.0 in your account when you created a schedule and then update hello module tooversion 2.0, hello schedule will continue toouse 1.0.</span></span>  <span data-ttu-id="cbf5c-112">在順序 toouse hello 更新的模組版本，您必須建立新的排程。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-112">In order toouse hello updated module version, you must create a new schedule.</span></span> 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a><span data-ttu-id="cbf5c-113">toocreate hello Azure 傳統入口網站中的新排程</span><span class="sxs-lookup"><span data-stu-id="cbf5c-113">toocreate a new schedule in hello Azure classic portal</span></span>
1. <span data-ttu-id="cbf5c-114">在 hello Azure 傳統入口網站，選取 自動化，然後再選取 hello 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-114">In hello Azure classic portal, select Automation and then then select hello name of an automation account.</span></span>
2. <span data-ttu-id="cbf5c-115">選取 hello**資產** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-115">Select hello **Assets** tab.</span></span>
3. <span data-ttu-id="cbf5c-116">在 hello hello 視窗底部，按一下 **加入設定**。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-116">At hello bottom of hello window, click **Add Setting**.</span></span>
4. <span data-ttu-id="cbf5c-117">按一下 [ **加入排程**]。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-117">Click **Add Schedule**.</span></span>
5. <span data-ttu-id="cbf5c-118">輸入**名稱**並選擇性地**描述**hello 新 schedule.your 排程將執行**一次**，**每小時**， **每日**，**每週**，或**每月**。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-118">Type a **Name** and optionally a **Description** for hello new schedule.your schedule will run **One Time**, **Hourly**, **Daily**, **Weekly**, or **Monthly**.</span></span>
6. <span data-ttu-id="cbf5c-119">指定**開始時間**和其他選項，視您選取的排程 hello 類型而定。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-119">Specify a **Start Time** and other options depending on hello type of schedule that you selected.</span></span>

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a><span data-ttu-id="cbf5c-120">toocreate hello Azure 入口網站中的新排程</span><span class="sxs-lookup"><span data-stu-id="cbf5c-120">toocreate a new schedule in hello Azure portal</span></span>
1. <span data-ttu-id="cbf5c-121">在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello**資產**磚 tooopen hello**資產**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-121">In hello Azure portal, from your automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
2. <span data-ttu-id="cbf5c-122">按一下 hello**排程**磚 tooopen hello**排程**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-122">Click hello **Schedules** tile tooopen hello **Schedules** blade.</span></span>
3. <span data-ttu-id="cbf5c-123">按一下**加入排程**在 hello hello 刀鋒視窗最上方。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-123">Click **Add a schedule** at hello top of hello blade.</span></span>
4. <span data-ttu-id="cbf5c-124">在 hello**新排程**刀鋒視窗中，輸入**名稱**並選擇性地**描述**hello 新排程。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-124">On hello **New schedule** blade, type a **Name** and optionally a **Description** for hello new schedule.</span></span>
5. <span data-ttu-id="cbf5c-125">選取以選取 hello 排程將執行一次，或重複發生的排程上**一次**或**循環**。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-125">Select whether hello schedule will run one time, or on a reoccurring schedule by selecting **Once** or **Recurrence**.</span></span>  <span data-ttu-id="cbf5c-126">如果選取 一次，請指定 開始時間，然後按一下建立。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-126">If you select **Once** specify a **Start time** and then click **Create**.</span></span>  <span data-ttu-id="cbf5c-127">如果您選取**循環**，指定**開始時間**和 hello 頻率的頻率 hello runbook toorepeat-由**小時**，**天**，**週**，或由**月份**。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-127">If you select **Recurrence**, specify a **Start time** and hello frequency for how often you want hello runbook toorepeat - by **hour**, **day**, **week**, or by **month**.</span></span>  <span data-ttu-id="cbf5c-128">如果您選取**週**或**月份**hello 下拉式清單中，從 hello**的週期選項**會出現在 hello 刀鋒視窗中，並在選取項目後, hello**循環選項**刀鋒視窗會提供，而且如果您選取，您可以選取一週天數 hello**週**。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-128">If you select **week** or **month** from hello drop-down list, hello **Recurrence option** will appear in hello blade and upon selection, hello **Recurrence option** blade will be presented and you can select hello day of week if you selected **week**.</span></span>  <span data-ttu-id="cbf5c-129">如果您選取**月份**，您可以選擇**星期幾**或 hello 月的特定幾天 hello 行事曆和最後，您想 toorun 上或不 hello hello 當月最後一天，然後按一下 **[確定]**.</span><span class="sxs-lookup"><span data-stu-id="cbf5c-129">If you selected **month**, you can choose by **week days** or specific days of hello month on hello calendar and finally, do you want toorun it on hello last day of hello month or not and then click **OK**.</span></span>   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a><span data-ttu-id="cbf5c-130">toocreate 使用 Windows PowerShell 的新排程</span><span class="sxs-lookup"><span data-stu-id="cbf5c-130">toocreate a new schedule with Windows PowerShell</span></span>
<span data-ttu-id="cbf5c-131">您可以使用 hello [New-azureautomationschedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet toocreate 傳統的 runbook，在 Azure 自動化中的新排程或[新增 AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) hello Azure 中的 runbook 的 cmdlet入口網站。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-131">You can use hello [New-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet toocreate a new schedule in Azure Automation for classic runbooks, or [New-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) cmdlet for runbooks in hello Azure portal.</span></span> <span data-ttu-id="cbf5c-132">您必須指定 hello hello 排程與 hello 頻率應該執行的開始時間。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-132">You must specify hello start time for hello schedule and hello frequency it should run.</span></span>

<span data-ttu-id="cbf5c-133">hello，下列命令範例顯示如何 toocreate 新的排程執行每日下午 3:30 於 2015 年 1 月 20 日起的 Azure 服務管理 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-133">hello following sample commands show how toocreate a new schedule that runs each day at 3:30 PM starting on January 20, 2015 with an Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

<span data-ttu-id="cbf5c-134">hello 下列範例命令顯示如何 toocreate hello 的排程第 15 和 30，每個月使用 Azure 資源管理員 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-134">hello following sample commands shows how toocreate a schedule for hello 15th and 30th of every month using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a><span data-ttu-id="cbf5c-135">連結排程 tooa runbook</span><span class="sxs-lookup"><span data-stu-id="cbf5c-135">Linking a schedule tooa runbook</span></span>
<span data-ttu-id="cbf5c-136">一個 runbook 可以連結的 toomultiple 排程和排程也可以有多個連結的 runbook tooit。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-136">A runbook can be linked toomultiple schedules, and a schedule can have multiple runbooks linked tooit.</span></span> <span data-ttu-id="cbf5c-137">如果 Runbook 有參數，您可以為它們提供值。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-137">If a runbook has parameters, then you can provide values for them.</span></span> <span data-ttu-id="cbf5c-138">您必須為任何必要參數提供值，並可以提供任何選擇性參數的值。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-138">You must provide values for any mandatory parameters and may provide values for any optional parameters.</span></span>  <span data-ttu-id="cbf5c-139">每次透過這個排程啟動 hello runbook 時，會使用這些值。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-139">These values will be used each time hello runbook is started by this schedule.</span></span>  <span data-ttu-id="cbf5c-140">您可以將附加 hello 相同 runbook tooanother 排程，並指定不同的參數值。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-140">You can attach hello same runbook tooanother schedule and specify different parameter values.</span></span>

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a><span data-ttu-id="cbf5c-141">toolink 排程 tooa runbook 以 hello Azure 傳統入口網站</span><span class="sxs-lookup"><span data-stu-id="cbf5c-141">toolink a schedule tooa runbook with hello Azure classic portal</span></span>
1. <span data-ttu-id="cbf5c-142">在 hello Azure 傳統入口網站，選取 **自動化**，然後按一下 hello 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-142">In hello Azure classic portal, select **Automation** and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="cbf5c-143">選取 hello **Runbook**  索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-143">Select hello **Runbooks** tab.</span></span>
3. <span data-ttu-id="cbf5c-144">按一下 hello runbook tooschedule hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-144">Click on hello name of hello runbook tooschedule.</span></span>
4. <span data-ttu-id="cbf5c-145">按一下 hello**排程** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-145">Click hello **Schedule** tab.</span></span>
5. <span data-ttu-id="cbf5c-146">如果 hello runbook 不是目前連結的 tooa 排程，則您會獲得 hello 選項太**連結 tooa 新排程**或**連結 tooan 現有排程**。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-146">If hello runbook is not currently linked tooa schedule, then you will be given hello option too**Link tooa New Schedule** or **Link tooan Existing Schedule**.</span></span>  <span data-ttu-id="cbf5c-147">如果 hello runbook 目前連結的 tooa 排程，請按一下**連結**在 hello 底部 hello 視窗 tooaccess 這些選項。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-147">If hello runbook is currently linked tooa schedule, click **Link** at hello bottom of hello window tooaccess these options.</span></span>
6. <span data-ttu-id="cbf5c-148">如果 hello runbook 有參數，系統會提示您提供值。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-148">If hello runbook has parameters, you will be prompted for their values.</span></span>  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a><span data-ttu-id="cbf5c-149">toolink 排程 tooa runbook 以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="cbf5c-149">toolink a schedule tooa runbook with hello Azure portal</span></span>
1. <span data-ttu-id="cbf5c-150">在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello **Runbook**磚 tooopen hello **Runbook**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-150">In hello Azure portal, from your automation account, click hello **Runbooks** tile tooopen hello **Runbooks** blade.</span></span>
2. <span data-ttu-id="cbf5c-151">按一下 hello runbook tooschedule hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-151">Click on hello name of hello runbook tooschedule.</span></span>
3. <span data-ttu-id="cbf5c-152">如果 hello runbook 不是目前連結的 tooa 排程，然後您將會是給定的 hello 選項 toocreate 的新排程或連結現有的排程 tooan。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-152">If hello runbook is not currently linked tooa schedule, then you will be given hello option toocreate a new schedule or link tooan existing schedule.</span></span>  
4. <span data-ttu-id="cbf5c-153">如果 hello runbook 有參數，您可以選取 hello 選項**修改回合的設定 (預設： Azure)**和 hello**參數**刀鋒視窗會顯示，您可以據此輸入 hello 資訊。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-153">If hello runbook has parameters, you can select hello option **Modify run settings (Default:Azure)** and hello **Parameters** blade is presented where you can enter hello information accordingly.</span></span>  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a><span data-ttu-id="cbf5c-154">toolink 排程 tooa runbook 使用 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbf5c-154">toolink a schedule tooa runbook with Windows PowerShell</span></span>
<span data-ttu-id="cbf5c-155">您可以使用 hello [Register-azureautomationscheduledrunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink 排程 tooa 傳統 runbook 或[暫存器 AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) hello Azure 入口網站中 runbook 的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-155">You can use hello [Register-AzureAutomationScheduledRunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink a schedule tooa classic runbook or [Register-AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) cmdlet for runbooks in hello Azure portal.</span></span>  <span data-ttu-id="cbf5c-156">您可以指定 hello runbook 參數的值與 hello 參數參數。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-156">You can specify values for hello runbook’s parameters with hello Parameters parameter.</span></span> <span data-ttu-id="cbf5c-157">請參閱 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) ，以取得指定參數值的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-157">See [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md) for more information on specifying parameter values.</span></span>

<span data-ttu-id="cbf5c-158">hello 下列範例命令顯示如何 toolink 排程，使用 Azure 服務管理 cmdlet 搭配參數。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-158">hello following sample commands show how toolink a schedule using an Azure Service Management cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

<span data-ttu-id="cbf5c-159">hello 下列範例命令顯示如何 toolink 排程 tooa runbook 使用的 Azure 資源管理員 cmdlet 搭配參數。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-159">hello following sample commands show how toolink a schedule tooa runbook using an Azure Resource Manager cmdlet with parameters.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a><span data-ttu-id="cbf5c-160">停用排程</span><span class="sxs-lookup"><span data-stu-id="cbf5c-160">Disabling a schedule</span></span>
<span data-ttu-id="cbf5c-161">當您停用排程時，任何連結的 runbook tooit 將無法再執行該排程。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-161">When you disable a schedule, any runbooks linked tooit will no longer run on that schedule.</span></span> <span data-ttu-id="cbf5c-162">您可以手動停用排程，或在建立排程時為具有頻率的排程設定到期時間。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-162">You can manually disable a schedule or set an expiration time for schedules with a frequency when you create them.</span></span> <span data-ttu-id="cbf5c-163">當達到 hello 到期時間時，就會停用 hello 排程。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-163">When hello expiration time is reached, hello schedule will be disabled.</span></span>

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a><span data-ttu-id="cbf5c-164">toodisable 從 hello Azure 傳統入口網站的排程</span><span class="sxs-lookup"><span data-stu-id="cbf5c-164">toodisable a schedule from hello Azure classic portal</span></span>
<span data-ttu-id="cbf5c-165">您可以停用 hello hello hello 排程的排程詳細資料頁面從 Azure 傳統入口網站中的排程。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-165">You can disable a schedule in hello Azure classic portal from hello Schedule Details page for hello schedule.</span></span>

1. <span data-ttu-id="cbf5c-166">在 hello Azure 傳統入口網站，選取 自動化，然後再按一下 hello 自動化帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-166">In hello Azure classic portal, select Automation and then then click hello name of an automation account.</span></span>
2. <span data-ttu-id="cbf5c-167">選取 hello 資產 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-167">Select hello Assets tab.</span></span>
3. <span data-ttu-id="cbf5c-168">按一下排程 tooopen hello 名稱及其詳細資料頁面。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-168">Click hello name of a schedule tooopen its detail page.</span></span>
4. <span data-ttu-id="cbf5c-169">變更**啟用**太**否**。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-169">Change **Enabled** too**No**.</span></span>

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a><span data-ttu-id="cbf5c-170">toodisable 從 hello Azure 入口網站的排程</span><span class="sxs-lookup"><span data-stu-id="cbf5c-170">toodisable a schedule from hello Azure portal</span></span>
1. <span data-ttu-id="cbf5c-171">在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello**資產**磚 tooopen hello**資產**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-171">In hello Azure portal, from your automation account, click hello **Assets** tile tooopen hello **Assets** blade.</span></span>
2. <span data-ttu-id="cbf5c-172">按一下 hello**排程**磚 tooopen hello**排程**刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-172">Click hello **Schedules** tile tooopen hello **Schedules** blade.</span></span>
3. <span data-ttu-id="cbf5c-173">按一下排程 tooopen hello 詳細資料 刀鋒視窗的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-173">Click hello name of a schedule tooopen hello details blade.</span></span>
4. <span data-ttu-id="cbf5c-174">變更**啟用**太**否**。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-174">Change **Enabled** too**No**.</span></span>

### <a name="toodisable-a-schedule-with-windows-powershell"></a><span data-ttu-id="cbf5c-175">toodisable 排程與 Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="cbf5c-175">toodisable a schedule with Windows PowerShell</span></span>
<span data-ttu-id="cbf5c-176">您可以使用 hello [Set-azureautomationschedule](http://msdn.microsoft.com/library/azure/dn690270.aspx)傳統 runbook 的現有排程的 cmdlet toochange hello 屬性或[組 AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) hello Azure 中的 runbook 的 cmdlet入口網站。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-176">You can use hello [Set-AzureAutomationSchedule](http://msdn.microsoft.com/library/azure/dn690270.aspx) cmdlet toochange hello properties of an existing schedule for a classic runbook or [Set-AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) cmdlet for runbooks in hello Azure portal.</span></span> <span data-ttu-id="cbf5c-177">toodisable hello 排程、 指定**false** hello **IsEnabled**參數。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-177">toodisable hello schedule, specify **false** for hello **IsEnabled** parameter.</span></span>

<span data-ttu-id="cbf5c-178">hello 下列命令範例示範如何排程使用 toodisable hello Azure 服務管理 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-178">hello following sample commands show how toodisable a schedule using hello Azure Service Management cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

<span data-ttu-id="cbf5c-179">hello 下列範例命令顯示如何 toodisable runbook 使用的 Azure 資源管理員 cmdlet 的排程。</span><span class="sxs-lookup"><span data-stu-id="cbf5c-179">hello following sample commands show how toodisable a schedule for a runbook using an Azure Resource Manager cmdlet.</span></span>

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a><span data-ttu-id="cbf5c-180">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cbf5c-180">Next steps</span></span>
* <span data-ttu-id="cbf5c-181">toolearn 進一步了解使用排程，請參閱[在 Azure 自動化排程資產](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span><span class="sxs-lookup"><span data-stu-id="cbf5c-181">toolearn more about working with schedules, see [Schedule Assets in Azure Automation](http://msdn.microsoft.com/library/azure/dn940016.aspx)</span></span>
* <span data-ttu-id="cbf5c-182">請參閱 < 開始使用 Azure 自動化中的 runbook tooget [Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md)</span><span class="sxs-lookup"><span data-stu-id="cbf5c-182">tooget started with runbooks in Azure Automation, see [Starting a Runbook in Azure Automation](automation-starting-a-runbook.md)</span></span> 

