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
# <a name="scheduling-a-runbook-in-azure-automation"></a>在 Azure 自動化中排程 Runbook
tooschedule runbook 在 Azure 自動化 toostart 在指定的時間，您將它連結 tooone 或多個排程。 排程可以設定的 tooeither 執行一次或重複每小時或每日排程 hello Azure 傳統入口網站中的 runbook 和 runbook hello Azure 入口網站中，您可以另外排定它們 hello 一週的每週、 每月、 特定天數或天數hello 月份或 hello 月份的某一天。  一個 runbook 可以連結的 toomultiple 排程和排程也可以有多個連結的 runbook tooit。

## <a name="creating-a-schedule"></a>建立排程
在 hello 傳統入口網站，或使用 Windows PowerShell，您可以建立 hello Azure 入口網站中 runbook 的新排程。 您也可以建立新的排程，當您將連結使用 hello Azure 傳統 runbook tooa 排程或 Azure 入口網站的 hello 選項。

> [!NOTE]
> 當您將排程與 runbook 產生關聯時，自動化帳戶中儲存的 hello 模組的 hello 目前版本，並連結 toothat 排程。  這表示如果在您建立排程時，在您的帳戶已有同名的模組版本 1.0，然後更新 hello 模組 tooversion 2.0 hello 排程會繼續 toouse 1.0。  在順序 toouse hello 更新的模組版本，您必須建立新的排程。 
> 
> 

### <a name="toocreate-a-new-schedule-in-hello-azure-classic-portal"></a>toocreate hello Azure 傳統入口網站中的新排程
1. 在 hello Azure 傳統入口網站，選取 自動化，然後再選取 hello 自動化帳戶名稱。
2. 選取 hello**資產** 索引標籤。
3. 在 hello hello 視窗底部，按一下 **加入設定**。
4. 按一下 [ **加入排程**]。
5. 輸入**名稱**並選擇性地**描述**hello 新 schedule.your 排程將執行**一次**，**每小時**， **每日**，**每週**，或**每月**。
6. 指定**開始時間**和其他選項，視您選取的排程 hello 類型而定。

### <a name="toocreate-a-new-schedule-in-hello-azure-portal"></a>toocreate hello Azure 入口網站中的新排程
1. 在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello**資產**磚 tooopen hello**資產**刀鋒視窗。
2. 按一下 hello**排程**磚 tooopen hello**排程**刀鋒視窗。
3. 按一下**加入排程**在 hello hello 刀鋒視窗最上方。
4. 在 hello**新排程**刀鋒視窗中，輸入**名稱**並選擇性地**描述**hello 新排程。
5. 選取以選取 hello 排程將執行一次，或重複發生的排程上**一次**或**循環**。  如果選取 一次，請指定 開始時間，然後按一下建立。  如果您選取**循環**，指定**開始時間**和 hello 頻率的頻率 hello runbook toorepeat-由**小時**，**天**，**週**，或由**月份**。  如果您選取**週**或**月份**hello 下拉式清單中，從 hello**的週期選項**會出現在 hello 刀鋒視窗中，並在選取項目後, hello**循環選項**刀鋒視窗會提供，而且如果您選取，您可以選取一週天數 hello**週**。  如果您選取**月份**，您可以選擇**星期幾**或 hello 月的特定幾天 hello 行事曆和最後，您想 toorun 上或不 hello hello 當月最後一天，然後按一下 **[確定]**.   

### <a name="toocreate-a-new-schedule-with-windows-powershell"></a>toocreate 使用 Windows PowerShell 的新排程
您可以使用 hello [New-azureautomationschedule](http://msdn.microsoft.com/library/azure/dn690271.aspx) cmdlet toocreate 傳統的 runbook，在 Azure 自動化中的新排程或[新增 AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603577.aspx) hello Azure 中的 runbook 的 cmdlet入口網站。 您必須指定 hello hello 排程與 hello 頻率應該執行的開始時間。

hello，下列命令範例顯示如何 toocreate 新的排程執行每日下午 3:30 於 2015 年 1 月 20 日起的 Azure 服務管理 cmdlet。

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    New-AzureAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName –StartTime "1/20/2016 15:30:00" –DayInterval 1

hello 下列範例命令顯示如何 toocreate hello 的排程第 15 和 30，每個月使用 Azure 資源管理員 cmdlet。

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    New-AzureRMAutomationSchedule –AutomationAccountName $automationAccountName –Name `
    $scheduleName -StartTime "7/01/2016 15:30:00" -MonthInterval 1 `
    -DaysOfMonth Fifteenth,Thirtieth -ResourceGroupName "ResourceGroup01"


## <a name="linking-a-schedule-tooa-runbook"></a>連結排程 tooa runbook
一個 runbook 可以連結的 toomultiple 排程和排程也可以有多個連結的 runbook tooit。 如果 Runbook 有參數，您可以為它們提供值。 您必須為任何必要參數提供值，並可以提供任何選擇性參數的值。  每次透過這個排程啟動 hello runbook 時，會使用這些值。  您可以將附加 hello 相同 runbook tooanother 排程，並指定不同的參數值。

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-classic-portal"></a>toolink 排程 tooa runbook 以 hello Azure 傳統入口網站
1. 在 hello Azure 傳統入口網站，選取 **自動化**，然後按一下 hello 自動化帳戶名稱。
2. 選取 hello **Runbook**  索引標籤。
3. 按一下 hello runbook tooschedule hello 名稱。
4. 按一下 hello**排程** 索引標籤。
5. 如果 hello runbook 不是目前連結的 tooa 排程，則您會獲得 hello 選項太**連結 tooa 新排程**或**連結 tooan 現有排程**。  如果 hello runbook 目前連結的 tooa 排程，請按一下**連結**在 hello 底部 hello 視窗 tooaccess 這些選項。
6. 如果 hello runbook 有參數，系統會提示您提供值。  

### <a name="toolink-a-schedule-tooa-runbook-with-hello-azure-portal"></a>toolink 排程 tooa runbook 以 hello Azure 入口網站
1. 在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello **Runbook**磚 tooopen hello **Runbook**刀鋒視窗。
2. 按一下 hello runbook tooschedule hello 名稱。
3. 如果 hello runbook 不是目前連結的 tooa 排程，然後您將會是給定的 hello 選項 toocreate 的新排程或連結現有的排程 tooan。  
4. 如果 hello runbook 有參數，您可以選取 hello 選項**修改回合的設定 (預設： Azure)**和 hello**參數**刀鋒視窗會顯示，您可以據此輸入 hello 資訊。  

### <a name="toolink-a-schedule-tooa-runbook-with-windows-powershell"></a>toolink 排程 tooa runbook 使用 Windows PowerShell
您可以使用 hello [Register-azureautomationscheduledrunbook](http://msdn.microsoft.com/library/azure/dn690265.aspx) toolink 排程 tooa 傳統 runbook 或[暫存器 AzureRmAutomationScheduledRunbook](https://msdn.microsoft.com/library/mt603575.aspx) hello Azure 入口網站中 runbook 的 cmdlet。  您可以指定 hello runbook 參數的值與 hello 參數參數。 請參閱 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) ，以取得指定參數值的詳細資訊。

hello 下列範例命令顯示如何 toolink 排程，使用 Azure 服務管理 cmdlet 搭配參數。

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params

hello 下列範例命令顯示如何 toolink 排程 tooa runbook 使用的 Azure 資源管理員 cmdlet 搭配參數。

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Test-Runbook"
    $scheduleName = "Sample-DailySchedule"
    $params = @{"FirstName"="Joe";"LastName"="Smith";"RepeatCount"=2;"Show"=$true}
    Register-AzureRmAutomationScheduledRunbook –AutomationAccountName $automationAccountName `
    –Name $runbookName –ScheduleName $scheduleName –Parameters $params `
    -ResourceGroupName "ResourceGroup01"

## <a name="disabling-a-schedule"></a>停用排程
當您停用排程時，任何連結的 runbook tooit 將無法再執行該排程。 您可以手動停用排程，或在建立排程時為具有頻率的排程設定到期時間。 當達到 hello 到期時間時，就會停用 hello 排程。

### <a name="toodisable-a-schedule-from-hello-azure-classic-portal"></a>toodisable 從 hello Azure 傳統入口網站的排程
您可以停用 hello hello hello 排程的排程詳細資料頁面從 Azure 傳統入口網站中的排程。

1. 在 hello Azure 傳統入口網站，選取 自動化，然後再按一下 hello 自動化帳戶名稱。
2. 選取 hello 資產 索引標籤。
3. 按一下排程 tooopen hello 名稱及其詳細資料頁面。
4. 變更**啟用**太**否**。

### <a name="toodisable-a-schedule-from-hello-azure-portal"></a>toodisable 從 hello Azure 入口網站的排程
1. 在 hello Azure 入口網站，從您的自動化帳戶，按一下 hello**資產**磚 tooopen hello**資產**刀鋒視窗。
2. 按一下 hello**排程**磚 tooopen hello**排程**刀鋒視窗。
3. 按一下排程 tooopen hello 詳細資料 刀鋒視窗的 hello 名稱。
4. 變更**啟用**太**否**。

### <a name="toodisable-a-schedule-with-windows-powershell"></a>toodisable 排程與 Windows PowerShell
您可以使用 hello [Set-azureautomationschedule](http://msdn.microsoft.com/library/azure/dn690270.aspx)傳統 runbook 的現有排程的 cmdlet toochange hello 屬性或[組 AzureRmAutomationSchedule](https://msdn.microsoft.com/library/mt603566.aspx) hello Azure 中的 runbook 的 cmdlet入口網站。 toodisable hello 排程、 指定**false** hello **IsEnabled**參數。

hello 下列命令範例示範如何排程使用 toodisable hello Azure 服務管理 cmdlet。

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-DailySchedule"
    Set-AzureAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false

hello 下列範例命令顯示如何 toodisable runbook 使用的 Azure 資源管理員 cmdlet 的排程。

    $automationAccountName = "MyAutomationAccount"
    $scheduleName = "Sample-MonthlyDaysOfMonthSchedule"
    Set-AzureRmAutomationSchedule –AutomationAccountName $automationAccountName `
    –Name $scheduleName –IsEnabled $false -ResourceGroupName "ResourceGroup01"


## <a name="next-steps"></a>後續步驟
* toolearn 進一步了解使用排程，請參閱[在 Azure 自動化排程資產](http://msdn.microsoft.com/library/azure/dn940016.aspx)
* 請參閱 < 開始使用 Azure 自動化中的 runbook tooget [Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) 

