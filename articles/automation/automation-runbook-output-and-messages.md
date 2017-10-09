---
title: "aaaRunbook 輸出和在 Azure 自動化中的訊息 |Microsoft 文件"
description: "描述如何 toocreate 並擷取輸出和錯誤訊息從 Azure 自動化中的 runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 13a414f5-0e2c-4be2-9558-a3e3ec84b6b2
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: magoedte;bwren
ms.openlocfilehash: c1505fa889473766bfa47e43aaed2449d60ad851
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-output-and-messages-in-azure-automation"></a>Azure 自動化中的 Runbook 輸出與訊息
大部分的 Azure 自動化 runbook 將會有某種形式的輸出，例如錯誤訊息 toohello 使用者，或供其他工作流程使用 toobe 的複雜物件。 Windows PowerShell 提供[多個資料流](http://blogs.technet.com/heyscriptingguy/archive/2014/03/30/understanding-streams-redirection-and-write-host-in-powershell.aspx)toosend 輸出指令碼或工作流程。 Azure 自動化以不同的運作與每個資料流，以及您應該遵循最佳作法 toouse 每個當您建立 runbook。

hello 下表提供簡短描述每個 hello 資料流和 hello Azure 管理入口網站中的行為在執行已發佈的 runbook 和[測試 runbook](automation-testing-runbook.md)。 後續各節將提供每個資料流的進一步詳細資料。

| Stream | 說明 | Published | 測試 |
|:--- |:--- |:--- |:--- |
| 輸出 |供 toobe 其他 runbook 使用的物件。 |寫入 toohello 作業歷程記錄。 |顯示在 hello 測試輸出窗格中。 |
| 警告 |適用於 hello 使用者的警告訊息。 |寫入 toohello 作業歷程記錄。 |顯示在 hello 測試輸出窗格中。 |
| 錯誤 |適用於 hello 使用者的錯誤訊息。 不同於例外狀況，hello runbook 預設會繼續執行之後錯誤訊息。 |寫入 toohello 作業歷程記錄。 |顯示在 hello 測試輸出窗格中。 |
| 詳細資訊 |提供一般或偵錯資訊的訊息。 |如果詳細資訊記錄已為 hello runbook 撰寫只 toojob 歷程記錄。 |Hello 測試輸出窗格中顯示，只有當 $VerbosePreference tooContinue hello runbook 中設定。 |
| Progress |自動產生 hello runbook 中每個活動之前和之後的記錄。 hello runbook 不應嘗試 toocreate 它自己的進度記錄因為它們供互動式使用者。 |如果進度記錄已為 hello runbook 撰寫只 toojob 歷程記錄。 |不會顯示在 hello 測試輸出窗格。 |
| 偵錯 |適用於互動式使用者的訊息。 不應在 Runbook 中使用。 |不會寫入 toojob 歷程記錄。 |不會寫入 tooTest 輸出窗格。 |

## <a name="output-stream"></a>輸出資料流
hello 輸出資料流適用於正確執行時，指令碼或工作流程所建立之物件的輸出。 在 Azure 自動化中，這個資料流主要用於所耗用的主要物件 toobe[父呼叫 hello 目前 runbook 的 runbook](automation-child-runbooks.md)。 當您[呼叫 runbook 內嵌](automation-child-runbooks.md#invoking-a-child-runbook-using-inline-execution)從父 runbook，它會傳回資料從 hello 輸出資料流 toohello 父代。 如果您知道 hello runbook 永遠不會被另一個 runbook 呼叫，您應該只使用 hello 輸出資料流 toocommunicate 的一般資訊後 toohello 使用者。 最佳做法，不過，您通常應該使用 hello [Verbose Stream](#Verbose) toocommunicate 的一般資訊 toohello 使用者。

您可以撰寫資料 toohello 輸出資料流使用[Write-output](http://technet.microsoft.com/library/hh849921.aspx)或將 hello 物件放入的 hello runbook 中的那一行。

    #hello following lines both write an object toohello output stream.
    Write-Output –InputObject $object
    $object

### <a name="output-from-a-function"></a>從函式輸出
當您撰寫 toohello 輸出資料流中包括您在 runbook 中的函式時，hello 輸出會傳遞後 toohello runbook。 如果 hello runbook 將指派該輸出 tooa 變數，然後不會寫入 toohello 輸出資料流。 撰寫 tooany hello 函式內來自其他資料流將寫入 toohello hello runbook 的對應資料流。

請考慮下列 runbook 範例的 hello。

    Workflow Test-Runbook
    {
        Write-Verbose "Verbose outside of function" -Verbose
        Write-Output "Output outside of function"
        $functionOutput = Test-Function
        $functionOutput

    Function Test-Function
     {
        Write-Verbose "Verbose inside of function" -Verbose
        Write-Output "Output inside of function"
      }
    }


hello hello runbook 工作的輸出資料流將是：

    Output inside of function
    Output outside of function

hello hello runbook 工作的詳細資訊資料流將是：

    Verbose outside of function
    Verbose inside of function

一旦發行 hello runbook 和您在開始之前，您也必須開啟登入順序 tooget hello 詳細資料流輸出中的 hello runbook 設定的詳細資訊。

### <a name="declaring-output-data-type"></a>宣告輸出資料類型
工作流程可以指定其輸出使用 hello hello 資料型別[OutputType 屬性](http://technet.microsoft.com/library/hh847785.aspx)。 這個屬性在執行階段中，沒有任何作用，但是它提供指示 toohello runbook 作者在設計階段的 hello runbook 的 hello 預期輸出。 隨著 hello runbook 工具組的持續 tooevolve，hello 重要性的設計階段宣告輸出資料型別提升的重要性。 如此一來，它會是最佳作法 tooinclude 這個宣告中您所建立的任何 runbook。

以下是範例輸出類型清單：

* System.String
* System.Int32
* System.Collections.Hashtable
* Microsoft.Azure.Commands.Compute.Models.PSVirtualMachine

hello 下列 runbook 範例輸出字串物件，並包含其輸出類型的宣告。 如果您的 runbook 會輸出特定類型的陣列，則您仍應指定 hello 類型為相對於的 tooan hello 類型陣列。

    Workflow Test-Runbook
    {
       [OutputType([string])]

       $output = "This is some string output."
       Write-Output $output
    }

toodeclare Grapical 或圖形化 PowerShell 工作流程 runbook 中的輸出類型，您可以選取 hello**輸入和輸出**功能表選項，並輸入 hello 名稱 hello 的輸出類型。  我們建議您改用 hello 完整.NET 類別名稱 toomake 參考從父 runbook 時容易辨識它。  這會公開該類別 toohello 資料匯流排的 hello runbook 中的所有 hello 屬性，並提供很大的彈性，它們使用的條件式邏輯記錄，並參考做為 hello runbook 中的其他活動的值時。<br> ![Runbook 輸入和輸出選項](media/automation-runbook-output-and-messages/runbook-menu-input-and-output-option.png)

在下列範例的 hello，我們有兩個圖形化 runbook toodemonstrate 這項功能。  如果我們套用 hello 模組化 runbook 設計模型時，我們有一個 runbook 會做為 hello*驗證 Runbook 範本*管理與 Azure 中，使用驗證 hello 執行身分帳戶。  我們第二個 runbook，通常會執行 hello 的核心邏輯 tooautomate 特定案例，在此情況下即將 tooexecute hello*驗證 Runbook 範本*並顯示 hello 結果 tooyour**測試**輸出窗格。  在一般情況下，我們必須執行一些動作根據資源運用 hello 輸出 hello 子系 runbook 從這個 runbook。    

以下是 hello 基本邏輯的 hello **AuthenticateTo Azure** runbook。<br> ![驗證 Runbook 範本範例](media/automation-runbook-output-and-messages/runbook-authentication-template時的行為。png)時的行為。  

它包含 hello 輸出類型*Microsoft.Azure.Commands.Profile.Models.PSAzureContext*，這會傳回 hello 驗證設定檔屬性。<br> ![Runbook 輸出類型範例](media/automation-runbook-output-and-messages/runbook-input-and-output-add-blade.png) 

雖然此 runbook 是很直接的還有一個組態項目 toocall 這裡。  hello 最後一個活動執行 hello **Write-output** cmdlet，並寫入 hello 設定檔資料 tooa $_ 變數使用的 PowerShell 運算式 hello **Inputobject**參數，所需的指令程式。  

Hello 第二個 runbook 在這個範例中，名為*測試 ChildOutputType*，我們只需要兩個活動。<br> ![範例子輸出類型 Runbook](media/automation-runbook-output-and-messages/runbook-display-authentication-results-example.png) 

hello 第一個活動呼叫 hello **AuthenticateTo Azure** runbook 和 hello 的第二個活動執行 hello **Write-verbose** cmdlet 搭配 hello**資料來源**的**活動輸出**和 hello 值**欄位路徑**是**Context.Subscription.SubscriptionName**，這指定 hello hello 內容輸出**AuthenticateTo Azure** runbook。<br> ![Write-Verbose Cmdlet 參數的資料來源](media/automation-runbook-output-and-messages/runbook-write-verbose-parameters-config.png)    

hello 產生的輸出是 hello hello 訂用帳戶名稱。<br> ![Test-ChildOutputType Runbook 結果](media/automation-runbook-output-and-messages/runbook-test-childoutputtype-results.png)

一個注意事項 hello hello 輸出型別控制行為的詳細資訊。  當您輸入中的 hello 輸入 hello 輸出型別欄位中的值與輸出屬性刀鋒視窗時，輸入，為了讓您 hello 控制項所辨識的項目 toobe 之後有 tooclick hello 控制之外。  

## <a name="message-streams"></a>訊息資料流
不同於 hello 輸出資料流，訊息資料流是預定的 toocommunicate 資訊 toohello 使用者。 有多個訊息資料流適用於不同類型的資訊，且 Azure 自動化以不同的方式處理每個資料流。

### <a name="warning-and-error-streams"></a>警告和錯誤資料流
hello 警告和錯誤資料流是 runbook 中發生的預定的 toolog 問題。 當 runbook 執行時，並測試 runbook 時包含 hello Azure 管理入口網站中的 hello 測試輸出窗格中將它們寫入 toohello 作業歷程記錄。 根據預設，hello runbook 將會繼續在警告或錯誤後執行。 您可以指定該 hello runbook 應該在警告或錯誤暫停藉由設定[喜好設定變數](#PreferenceVariables)建立 hello 訊息之前的 hello runbook 中。 例如，toocause runbook toosuspend 在發生錯誤一樣例外狀況，設定**$ErrorActionPreference** tooStop。

建立警告或錯誤訊息，使用 hello [Write-warning](https://technet.microsoft.com/library/hh849931.aspx)或[Write-error](http://technet.microsoft.com/library/hh849962.aspx) cmdlet。 活動也可能會撰寫 toothese 資料流。

    #hello following lines create a warning message and then an error message that will suspend hello runbook.

    $ErrorActionPreference = "Stop"
    Write-Warning –Message "This is a warning message."
    Write-Error –Message "This is an error message that will stop hello runbook because of hello preference variable."

### <a name="verbose-stream"></a>詳細資訊資料流
hello 詳細資訊訊息串流是 hello runbook 作業的相關的一般資訊。 因為 hello[偵錯資料流](#Debug)無法在 runbook 中使用，詳細訊息應該使用偵錯資訊。 根據預設，已發佈 runbook 的詳細訊息不會儲存在 hello 作業歷程記錄。 toostore 詳細訊息，hello hello Azure 管理入口網站中的 hello runbook 的 [設定] 索引標籤上設定已發行的 runbook tooLog 詳細記錄。 在大部分情況下，您應該保留 hello 預設設定，不記錄 runbook 基於效能考量的詳細資訊記錄。 開啟這個選項只有 tootroubleshoot 或偵錯 runbook。

當[測試 runbook](automation-testing-runbook.md)，即使 hello runbook 設定的 toolog 詳細資訊記錄，不會顯示詳細訊息。 toodisplay 時的詳細資訊訊息[測試 runbook](automation-testing-runbook.md)，您必須設定 hello $VerbosePreference 變數 tooContinue。 設定該變數會在 hello 的 hello Azure 入口網站的 [測試輸出] 窗格中顯示詳細訊息。

建立使用 hello 的詳細資訊訊息[Write-verbose](http://technet.microsoft.com/library/hh849951.aspx) cmdlet。

    #hello following line creates a verbose message.

    Write-Verbose –Message "This is a verbose message."

### <a name="debug-stream"></a>偵錯資料流
hello 偵錯資料流適用於互動式使用者，並且不應該在 runbook 中使用。

## <a name="progress-records"></a>進度記錄
如果您設定 runbook toolog 進度記錄 （在 hello 的 hello Azure 入口網站中的 hello runbook 設定索引標籤），則記錄會將寫入 toohello 作業歷程記錄之前和之後每個活動執行。 在大部分情況下，您應該保留不記錄 runbook 的進度記錄順序 toomaximize 效能的 hello 預設設定。 開啟這個選項只有 tootroubleshoot 或偵錯 runbook。 在測試 runbook 時，即使 hello runbook 設定的 toolog 進度記錄，將不會顯示進度訊息。

hello [Write-progress](http://technet.microsoft.com/library/hh849902.aspx)指令程式中不是有效的 runbook，因為這供互動式使用者。

## <a name="preference-variables"></a>喜好設定變數
Windows PowerShell 會使用[喜好設定變數](http://technet.microsoft.com/library/hh847796.aspx)toodetermine toorespond toodata 傳送 toodifferent 輸出資料流的方式。 您可以設定這些變數在它將如何回應傳送到不同的資料流的 toodata runbook toocontrol。

hello 下表列出可用於 runbook 及其有效值和預設值的 hello 喜好設定變數。 請注意，本表只包含 runbook 中有效的 hello 值。 其他的值為 hello 喜好設定變數在 Azure 自動化之外的 Windows PowerShell 中使用時的有效值。

| 變數 | 預設值 | 有效值 |
|:--- |:--- |:--- |
| WarningPreference |Continue |Stop<br>Continue<br>SilentlyContinue |
| ErrorActionPreference |Continue |Stop<br>Continue<br>SilentlyContinue |
| VerbosePreference |SilentlyContinue |Stop<br>Continue<br>SilentlyContinue |

hello 下表列出 hello 喜好設定變數值 runbook 中有效的 hello 行為。

| 值 | 行為 |
|:--- |:--- |
| Continue |Hello 訊息記錄，並繼續執行 hello runbook。 |
| SilentlyContinue |繼續執行 hello runbook 而不記錄 hello 訊息。 這有 hello 作法會忽略 hello 訊息。 |
| 停止 |Hello 訊息記錄，並擱置 hello runbook。 |

## <a name="retrieving-runbook-output-and-messages"></a>擷取 Runbook 輸出和訊息
### <a name="azure-portal"></a>Azure 入口網站
您可以在 hello hello runbook 的 [工作] 索引標籤從 Azure 入口網站中檢視 runbook 工作的 hello 詳細資料。 hello hello 工作的摘要會顯示 hello 輸入的參數和 hello[輸出資料流](#Output)在加法 toogeneral hello 工作和資訊任何發生的例外狀況。 hello 歷程記錄會包含來自 hello 訊息[輸出資料流](#Output)和[Warning and Error Streams](#WarningError)中新增 toohello [Verbose Stream](#Verbose)和[進度記錄](#Progress)hello runbook 是否已設定的 toolog 詳細資訊和進度記錄。

### <a name="windows-powershell"></a>Windows PowerShell
在 Windows PowerShell 中擷取輸出和訊息從 runbook 使用 hello [Get-azureautomationjoboutput](https://msdn.microsoft.com/library/mt603476.aspx) cmdlet。 此 cmdlet 需要 hello hello 作業的識別碼，而且具有參數稱為您用來指定哪些資料流 tooreturn 資料流。 您可以指定任何 tooreturn hello 作業的所有資料流。

下列範例中的 hello 範例 runbook，然後等候它開始 toocomplete。 完成後，從 hello 工作收集其輸出資料流。

    $job = Start-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "Test-Runbook"

    $doLoop = $true
    While ($doLoop) {
       $job = Get-AzureRmAutomationJob -ResourceGroupName "ResourceGroup01" `
       –AutomationAccountName "MyAutomationAccount" -Id $job.JobId
       $status = $job.Status
       $doLoop = (($status -ne "Completed") -and ($status -ne "Failed") -and ($status -ne "Suspended") -and ($status -ne "Stopped")
    }

    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" -Id $job.JobId –Stream Output

### <a name="graphical-authoring"></a>圖形化編寫
圖形化 runbook，額外的記錄會提供活動層級追蹤 hello 形式。  追蹤有兩種等級：基本及詳細。  在基本追蹤中，您可以查看 hello 啟動以及 hello runbook 會加上資訊中每個活動的結束時間相關 tooany 活動重試嘗試次數等 hello 活動開始時間。  在詳細追蹤中，您會得到基本追蹤的結果，加上每個活動的輸入及輸出資料。  請注意，目前 hello 追蹤記錄會寫入使用 hello 詳細資料流，因此您必須啟用詳細資訊記錄，當您啟用追蹤。  啟用追蹤的圖形化 runbook 無須 toolog 進度記錄，因為 hello 基本追蹤做 hello 相同的目的，而且更有用的資訊。

![圖形化編寫的工作串流檢視](media/automation-runbook-output-and-messages/job-streams-view-blade.png)

您可以從上述螢幕擷取畫面的 hello 了，當您啟用記錄和追蹤的圖形化 runbook 的詳細資訊，更多的資訊會顯示在 hello 實際執行的工作資料流檢視。  這些額外的資訊在您排解 Runbook 相關的生產問題時是不可或缺的，因此您應該只為這個目的來啟用該功能，而不是隨時啟用。    
hello 追蹤記錄可以是許多特別。  使用圖形化 runbook 追蹤您可以取得每個活動，根據是否您有設定基本或詳細追蹤的兩個 toofour 記錄。  除非您需要資訊 tootrack hello 處理 runbook 的疑難排解時，您可能想的 tookeep 追蹤已關閉。

**tooenable 活動層級追蹤，執行下列步驟的 hello。**

1. 在 hello Azure 入口網站，開啟您的自動化帳戶。
2. 按一下 hello **Runbook**磚 tooopen hello runbook 的清單。
3. 在 hello Runbook 刀鋒視窗中，按一下 tooselect 從您的 runbook 清單圖形化 runbook。
4. 在 hello 設定刀鋒視窗中的 hello 選取 runbook，按一下  **Logging and Tracing**。
5. 在 hello Logging and Tracing 刀鋒視窗中，在記錄檔的詳細資訊記錄，按一下 **上**tooenable 詳細資訊記錄和 udner 活動層級追蹤變更 hello 追蹤層級太**基本**或**詳細資料**根據 hello 您要求的追蹤層級。<br>
   
   ![圖形化編寫的 [記錄和追蹤] 刀鋒視窗](media/automation-runbook-output-and-messages/logging-and-tracing-settings-blade.png)

### <a name="microsoft-operations-management-suite-oms-log-analytics"></a>Microsoft Operations Management Suite (OMS) Log Analytics
自動化可以傳送 runbook 工作狀態和作業資料流 tooyour Microsoft Operations Management Suite (OMS) 記錄分析工作區。  透過 Log Analytics，您可以：

* 針對自動化工作取得深入解析 
* 根據您的 Runbook 工作狀態 (例如已失敗或已暫停) 觸發電子郵件或警示 
* 撰寫工作資料流之間的進階查詢 
* 在自動化帳戶之間相互關聯工作 
* 視覺化一段時間的工作歷程記錄    

如需有關如何使用記錄分析 toocollect tooconfigure 整合相互關聯，並處理的作業資料的詳細資訊，請參閱[自動化 tooLog 分析 (OMS) 從轉寄工作狀態和作業資料流](automation-manage-send-joblogs-log-analytics.md)。

## <a name="next-steps"></a>後續步驟
* 深入了解 runbook 執行時，如何 toomonitor runbook 作業和其他技術的詳細資訊，請參閱 toolearn[追蹤 runbook 工作](automation-runbook-execution.md)
* 如何 toodesign 和使用的子系 runbook，請參閱的 toounderstand [Azure 自動化中的子 runbook](automation-child-runbooks.md)

