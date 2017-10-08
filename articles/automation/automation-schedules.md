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
# <a name="scheduling-a-runbook-in-azure-automation"></a>在 Azure 自動化中排程 Runbook
tooschedule runbook 在 Azure 自動化 toostart 在指定的時間，您將它連結 tooone 或多個排程。 排程可以設定的 tooeither 執行一次，或在發生每小時或每日排程 hello Azure 傳統入口網站中的 runbook 和 runbook hello Azure 入口網站中，您也可以排定它們的 hello 一週的每週、 每月、 特定天數或天數的 hello月份或特定 hello 月份天數。  一個 runbook 可以連結的 toomultiple 排程和排程也可以有多個連結的 runbook tooit。

> [!NOTE]
> 排程目前不支援 Azure Automation DSC 組態。
> 
> 

## <a name="windows-powershell-cmdlets"></a>Windows PowerShell Cmdlet
hello 下表中的 hello cmdlet 會使用的 toocreate 和管理使用 Windows PowerShell 在 Azure 自動化中排程。 這些 cmdlet 隨附 hello [Azure PowerShell 模組](/powershell/azure/overview)。

| Cmdlet | 說明 |
|:--- |:--- |
| **Azure Resource Manager 的 Cmdlet** | |
| [Get-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/get-azurermautomationschedule) |擷取排程。 |
| [New-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) |建立新排程。 |
| [Remove-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/remove-azurermautomationschedule) |移除排程。 |
| [Set-AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) |設定現有排程的 hello 屬性。 |
| [Get-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/set-azurermautomationscheduledrunbook) |擷取排程的 Runbook。 |
| [Register-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) |將 Runbook 與排程相關聯。 |
| [Unregister-AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/unregister-azurermautomationscheduledrunbook) |從排程分離 Runbook。 |
| **Azure 服務管理的 Cmdlet** | |
| [Get-AzureAutomationSchedule](/powershell/module/azure/get-azureautomationschedule?view=azuresmps-3.7.0) |擷取排程。 |
| [New-AzureAutomationSchedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) |建立新排程。 |
| [Remove-AzureAutomationSchedule](/powershell/module/azure/remove-azureautomationschedule?view=azuresmps-3.7.0) |移除排程。 |
| [Set-AzureAutomationSchedule](/powershell/module/azure/set-azureautomationschedule?view=azuresmps-3.7.0) |設定現有排程的 hello 屬性。 |
| [Get-AzureAutomationScheduledRunbook](/powershell/module/azure/get-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |擷取排程的 Runbook。 |
| [Register-AzureAutomationScheduledRunbook](/powershell/module/azure/register-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |將 Runbook 與排程相關聯。 |
| [Unregister-AzureAutomationScheduledRunbook](/powershell/module/azure/unregister-azureautomationscheduledrunbook?view=azuresmps-3.7.0) |從排程分離 Runbook。 |

## <a name="creating-a-schedule"></a>建立排程
在 hello 傳統入口網站，或使用 Windows PowerShell，您可以建立 hello Azure 入口網站中 runbook 的新排程。 您也可以建立新的排程，當您將連結使用 hello Azure 傳統 runbook tooa 排程或 Azure 入口網站的 hello 選項。

> [!NOTE]
> Azure 自動化會使用 hello 最新的模組，您的自動化帳戶中，新的排程的工作執行時。  影響您的 runbook 和 hello tooavoid 自動化程序，您應該先測試的任何 runbook 都有專用的測試自動化帳戶連結排程。  這將會驗證您排程的 runbook 繼續 toowork 正確，如果不是，您可以進一步疑難排解並套用任何變更之前需要移轉的 hello 更新 runbook 版本 tooproduction。  
>  您的自動化帳戶不會自動收到任何新版本的模組除非您已更新這些手動選取 hello[更新 Azure 模組](automation-update-azure-modules.md)選項從 hello**模組**刀鋒視窗。 
>  

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate hello Azure 入口網站中的新排程
1. 在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello**資產**磚 tooopen hello**資產**刀鋒視窗。
2. 按一下 hello**排程**磚 tooopen hello**排程**刀鋒視窗。
3. 按一下**加入排程**在 hello hello 刀鋒視窗最上方。
4. 在 hello**新排程**刀鋒視窗中，輸入**名稱**並選擇性地**描述**hello 新排程。
5. 選取以選取 hello 排程將執行一次，或重複發生的排程上**一次**或**循環**。  如果選取 一次，請指定 開始時間，然後按一下建立。  如果您選取**循環**，指定**開始時間**和 hello 頻率的頻率 hello runbook toorepeat-由**小時**，**天**，**週**，或由**月份**。  如果您選取**週**或**月份**hello 下拉式清單中，從 hello**的週期選項**會出現在 hello 刀鋒視窗中，並在選取項目後, hello**循環選項**刀鋒視窗會提供，而且如果您選取，您可以選取一週天數 hello**週**。  如果您選取**月份**，您可以選擇**工作日**或 hello 月的特定幾天 hello 行事曆和最後，您想 toorun 上或不 hello hello 當月最後一天，然後按一下 **[確定]**.   

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate hello Azure 傳統入口網站中的新排程
1. 在 hello Azure 傳統入口網站，選取 自動化，然後選取 hello 自動化帳戶名稱。
2. 選取 hello**資產** 索引標籤。
3. 在 hello hello 視窗底部，按一下 **加入設定**。
4. 按一下 [ **加入排程**]。
5. 輸入**名稱**並選擇性地**描述**hello 新 schedule.your 排程將執行**一次**，**每小時**， **每日**，**每週**，或**每月**。
6. 指定**開始時間**和其他選項，視您選取的排程 hello 類型而定。

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate 使用 Windows PowerShell 的新排程
您可以使用 hello [New-azureautomationschedule](/powershell/module/azure/new-azureautomationschedule?view=azuresmps-3.7.0) cmdlet toocreate 傳統的 runbook，在 Azure 自動化中的新排程或[新增 AzureRmAutomationSchedule](/powershell/module/azurerm.automation/new-azurermautomationschedule) hello Azure 中的 runbook 的 cmdlet入口網站。 您必須指定 hello hello 排程與 hello 頻率應該執行的開始時間。

hello 下列範例命令顯示如何 toocreate hello 的排程第 15 和 30，每個月使用 Azure 資源管理員 cmdlet。

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"

hello，下列命令範例顯示如何 toocreate 新的排程執行每日下午 3:30 於 2015 年 1 月 20 日起的 Azure 服務管理 cmdlet。

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

## <a name="linking-a-schedule-tooa-runbook"></a>連結排程 tooa runbook
一個 runbook 可以連結的 toomultiple 排程和排程也可以有多個連結的 runbook tooit。 如果 Runbook 有參數，您可以為它們提供值。 您必須為任何必要參數提供值，並可以提供任何選擇性參數的值。  每次透過這個排程啟動 hello runbook 時，會使用這些值。  您可以將附加 hello 相同 runbook tooanother 排程，並指定不同的參數值。

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink 排程 tooa runbook 以 hello Azure 入口網站
1. 在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello **Runbook**磚 tooopen hello **Runbook**刀鋒視窗。
2. 按一下 hello runbook tooschedule hello 名稱。
3. 如果 hello runbook 不是目前連結的 tooa 排程，然後您將會是給定的 hello 選項 toocreate 的新排程或連結現有的排程 tooan。  
4. 如果 hello runbook 有參數，您可以選取 hello 選項**修改回合的設定 (預設： Azure)**和 hello**參數**刀鋒視窗會顯示，您可以據此輸入 hello 資訊。  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink 排程 tooa runbook 以 hello Azure 傳統入口網站
1. 在 hello Azure 傳統入口網站，選取 **自動化**，然後按一下 hello 的自動化帳戶的名稱。
2. 選取 hello **Runbook**  索引標籤。
3. 按一下 hello runbook tooschedule hello 名稱。
4. 按一下 hello**排程** 索引標籤。
5. 如果 hello runbook 不是目前連結的 tooa 排程，則您會獲得 hello 選項太**連結 tooa 新排程**或**連結 tooan 現有排程**。  如果 hello runbook 目前連結的 tooa 排程，請按一下**連結**在 hello 底部 hello 視窗 tooaccess 這些選項。
6. 如果 hello runbook 有參數，系統會提示您提供值。  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink 排程 tooa runbook 使用 Windows PowerShell
您可以使用 hello [Register-azureautomationscheduledrunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink 排程 tooa 傳統 runbook 或[暫存器 AzureRmAutomationScheduledRunbook](/powershell/module/azurerm.automation/register-azurermautomationscheduledrunbook) hello Azure 入口網站中 runbook 的 cmdlet。  您可以指定 hello runbook 參數的值與 hello 參數參數。 請參閱 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) ，以取得指定參數值的詳細資訊。

hello 下列範例命令顯示如何 toolink 排程 tooa runbook 使用的 Azure 資源管理員 cmdlet 搭配參數。

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"
hello 下列範例命令顯示如何 toolink 排程，使用 Azure 服務管理 cmdlet 搭配參數。

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

## <a name="disabling-a-schedule"></a>停用排程
當您停用排程時，任何連結的 runbook tooit 將無法再執行該排程。 您可以手動停用排程，或在建立排程時為具有頻率的排程設定到期時間。 當達到 hello 到期時間時，就會停用 hello 排程。

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable 從 hello Azure 入口網站的排程
1. 在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello**資產**磚 tooopen hello**資產**刀鋒視窗。
2. 按一下 hello**排程**磚 tooopen hello**排程**刀鋒視窗。
3. 按一下排程 tooopen hello 詳細資料 刀鋒視窗的 hello 名稱。
4. 變更**啟用**太**否**。

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable 從 hello Azure 傳統入口網站的排程
您可以停用 hello hello hello 排程的排程詳細資料頁面從 Azure 傳統入口網站中的排程。

1. 在 hello Azure 傳統入口網站，選取 自動化，然後按一下 hello 自動化帳戶名稱。
2. 選取 hello 資產 索引標籤。
3. 按一下排程 tooopen hello 名稱及其詳細資料頁面。
4. 變更**啟用**太**否**。

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable 排程與 Windows PowerShell
您可以使用 hello [Set-azureautomationschedule](http://msdn.microsoft.com/library/azure/dn690270.aspx)傳統 runbook 的現有排程的 cmdlet toochange hello 屬性或[組 AzureRmAutomationSchedule](/powershell/module/azurerm.automation/set-azurermautomationschedule) hello Azure 中的 runbook 的 cmdlet入口網站。 toodisable hello 排程、 指定**false** hello **IsEnabled**參數。

hello 下列範例命令顯示如何 toodisable runbook 使用的 Azure 資源管理員 cmdlet 的排程。

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"

hello 下列命令範例示範如何排程使用 toodisable hello Azure 服務管理 cmdlet。

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

## <a name="next-steps"></a>後續步驟
* 請參閱 < 開始使用 Azure 自動化中的 runbook tooget [Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) 

