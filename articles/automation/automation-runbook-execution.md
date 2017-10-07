---
title: "在 Azure 自動化中的 aaaRunbook 執行 |Microsoft 文件"
description: "描述如何在 Azure 自動化 runbook 處理的 hello 詳細資料。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d10c8ce2-2c0b-4ea7-ba3c-d20e09b2c9ca
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2017
ms.author: bwren
ms.openlocfilehash: bdb535675443353d44640bc7773de3f9dac5e42c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-execution-in-azure-automation"></a>Azure 自動化中的 Runbook 執行
當您在 Azure 自動化中啟動 Runbook 時即會建立一個工作。 工作是 Runbook 的單一執行個體。 Azure 自動化背景工作會指派 toorun 每項工作。 雖然背景工作是由多個 Azure 帳戶共用，來自不同自動化帳戶的工作會彼此隔離。 適用於您作業沒有控制哪一個背景工作服務 hello 要求。  單一 Runbook 一次可以執行多個工作。 當您在 hello Azure 入口網站中檢視 runbook 的 hello 清單時，它會列出 hello 的每個 runbook 已啟動的所有工作的狀態。 您可以檢視 hello 每個 runbook 的工作清單中的每個訂單 tootrack hello 狀態。 如需 hello 不同工作狀態的說明，請參閱[作業狀態](#job-statuses)。

hello 下列圖表顯示 hello 生命週期的 runbook 工作的[圖形化 runbook](automation-runbook-types.md#graphical-runbooks)和[PowerShell 工作流程 runbook](automation-runbook-types.md#powershell-workflow-runbooks)。

![工作狀態 -PowerShell 工作流程](./media/automation-runbook-execution/job-statuses.png)

hello 下列圖表顯示 hello 生命週期的 runbook 工作的[PowerShell runbook](automation-runbook-types.md#powershell-runbooks)。

![工作狀態 - PowerShell 指令碼](./media/automation-runbook-execution/job-statuses-script.png)

您的工作具有存取 tooyour Azure 藉由連接 tooyour Azure 訂用帳戶的資源。 它們才有存取 tooresources 在資料中心，這些資源可供從 hello 公用雲端存取。

## <a name="job-statuses"></a>工作狀態
hello 下表描述作業可能會有的 hello 不同狀態。

| 狀態 | 說明 |
|:--- |:--- |
| Completed |hello 作業已順利完成。 |
| Failed |如[圖形化和 PowerShell 工作流程 runbook](automation-runbook-types.md)，hello runbook 失敗 toocompile。  如[PowerShell 指令碼 runbook](automation-runbook-types.md)、 hello runbook 失敗 toostart 或 hello 工作時發生例外狀況。 |
| 處理失敗，正在等候資源 |hello 工作失敗，因為它已達到 hello[公平分享](#fairshare)限制三次，並從啟動 hello 相同的檢查點或從 hello hello runbook 的每次啟動。 |
| 已排入佇列 |hello 工作正在等候資源上提供自動化背景工作 toocome，讓它可以啟動。 |
| 啟動中 |hello 作業已指派 tooa 工作者、 hello 系統處於啟動它的 hello 程序。 |
| 繼續中 |hello 系統是處於 hello 的暫停後繼續 hello 工作的程序。 |
| 執行中 |hello 作業正在執行。 |
| 執行中，正在等候資源 |hello 作業已卸載，因為它已達到 hello[公平分享](#fairshare)限制。 作業很快會從其上一個檢查點繼續。 |
| 已停止 |在完成前 hello 使用者 hello 作業已停止。 |
| 停止中 |hello 系統是處於停止 hello 作業的 hello 程序。 |
| 暫止 |hello 作業已暫停 hello 使用者、 hello 系統或 hello runbook 中的命令。 已暫停的作業能重新啟動，並從其最後一個檢查點或是 hello 開頭 hello runbook 如果它沒有檢查點繼續。 例外狀況發生時，hello runbook 只會暫停 hello 系統。 根據預設，ErrorActionPreference 設定太**繼續**，這表示該 hello 作業會繼續執行在發生錯誤。 如果此喜好設定變數設定得**停止**，然後 hello 作業會發生錯誤時暫停。  適用於太[圖形化和 PowerShell 工作流程 runbook](automation-runbook-types.md)只。 |
| 暫停中 |hello 系統嘗試進行 toosuspend hello hello hello 使用者要求作業。 在暫停之前 hello runbook 必須達到其下一個檢查點。 如果它已通過其最後一個檢查點，則可在暫停之前完成。  適用於太[圖形化和 PowerShell 工作流程 runbook](automation-runbook-types.md)只。 |

## <a name="viewing-job-status-from-hello-azure-portal"></a>檢視工作狀態從 hello Azure 入口網站
您可以檢視所有 runbook 工作的摘要的狀態或向下鑽研到特定 runbook 工作 hello Azure 入口網站中，或藉由設定整合與您 Microsoft Operations Management Suite (OMS) 的記錄分析工作區 tooforward runbook 的作業狀態的詳細資料，工作資料流。  如需整合與 OMS 記錄分析的詳細資訊，請參閱[自動化 tooLog 分析 (OMS) 從轉寄工作狀態和作業資料流](automation-manage-send-joblogs-log-analytics.md)。  

### <a name="automation-runbook-jobs-summary"></a>自動化 Runbook 作業摘要
在您選取的自動化帳戶的權限的 hello，您可以看到所有選取的自動化帳戶下的 hello runbook 工作的摘要**工作統計資料**磚。<br><br> ![[作業統計資料] 圖格](./media/automation-runbook-execution/automation-account-job-status-summary.png)。<br> 這個磚會顯示計數和執行所有作業的 hello 作業狀態的圖形表示。  

按一下 hello 磚顯示 hello**作業**刀鋒視窗，其中包含所有已執行的工作、 狀態、 工作執行與開始與完成時間的彙總的清單。<br><br> ![自動化帳戶的 [作業] 刀鋒視窗](./media/automation-runbook-execution/automation-account-jobs-status-blade.png)<br><br>  您可以篩選 hello 工作清單中選取**篩選作業**和篩選之特定 runbook 工作狀態、 或 hello 下拉式清單中，從 hello 日期/時間範圍 toosearch 內。<br><br> ![篩選作業狀態](./media/automation-runbook-execution/automation-account-jobs-filter.png)

或者，您可以檢視特定 runbook 工作摘要詳細資料，從 hello 選取該 runbook **Runbook**刀鋒視窗，然後選取 hello 與自動化帳戶中的**作業**磚。  這顯現出 hello**作業**刀鋒視窗中，並從該處您可以按一下 hello 作業記錄 tooview 其詳細資料與輸出。<br><br> ![自動化帳戶的 [作業] 刀鋒視窗](./media/automation-runbook-execution/automation-runbook-job-summary-blade.png)<br> 

### <a name="job-summary"></a>工作摘要
您可以檢視所有已針對特定 runbook 和最新狀態建立的 hello 工作的清單。 您可以篩選此清單依工作狀態及 hello hello 的日期範圍將 toohello 作業最後變更。 tooview 其詳細的資訊及輸出，請按一下 hello 作業名稱。 hello hello 工作的詳細的檢視包含 hello hello 提供 toothat 工作的 runbook 參數的值。

您可以使用下列步驟執行 runbook 的 tooview hello 作業 hello。

1. 在 hello Azure 入口網站，選取 **自動化**，然後選取 hello 的自動化帳戶的名稱。
2. 從 hello 中樞，選取**Runbook**然後在 hello **Runbook**刀鋒視窗從 hello 清單中選取 runbook。
3. 在 hello 刀鋒視窗中的 hello 選取 runbook，按一下 hello**作業**磚。
4. 按一下其中一個 hello 清單中的 hello 作業，然後在 hello runbook 工作的詳細資料 刀鋒視窗，您可以檢視其詳細資料與輸出。

## <a name="retrieving-job-status-using-windows-powershell"></a>使用 Windows PowerShell 擷取工作狀態
您可以使用 hello [Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx) runbook 和 hello 詳細資料的特定作業所建立的 tooretrieve hello 作業。 如果您使用 Windows PowerShell 啟動 runbook[開始 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx)，則它會傳回 hello 產生的作業。 使用[Get AzureRmAutomationJob](https://msdn.microsoft.com/library/mt619440.aspx)輸出 tooget 工作的輸出。

hello 下列範例命令擷取範例 runbook 的 hello 最後一個作業並顯示其狀態、 hello 值為 hello runbook 參數，提供與 hello 來自 hello 工作的輸出。

    $job = (Get-AzureRmAutomationJob –AutomationAccountName "MyAutomationAccount" `
    –RunbookName "Test-Runbook" -ResourceGroupName "ResourceGroup01" | sort LastModifiedDate –desc)[0]
    $job.Status
    $job.JobParameters
    Get-AzureRmAutomationJobOutput -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAcct" -Id $job.JobId –Stream Output

## <a name="fair-share"></a>公平共用
在 hello 雲端中的所有 runbook 之間的順序 tooshare 資源，Azure 自動化會暫時卸除任何作業已執行三個小時之後。  在此期間，[以 PowerShell 為基礎的 Runbook](automation-runbook-types.md#powershell-runbooks) 的作業會停止，而且不會重新啟動。  hello 作業狀態顯示**已停止**。  這種類型的 runbook 永遠重新啟動從 hello 開頭因為它們不支援檢查點。  

[以 PowerShell 工作流程為基礎的 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 將會從其最後一個[檢查點](https://docs.microsoft.com/system-center/sma/overview-powershell-workflows#bk_Checkpoints)繼續。  執行三個小時之後, hello 將會暫止 runbook 工作 hello 服務和其狀態顯示**執行，等待資源**。  可以使用沙箱時，hello runbook 將會自動重新啟動 hello 自動化服務並繼續從 hello 最後一個檢查點。  這是 PowerShell 工作流程的正常暫停/重新啟動行為。  如果 hello runbook 再次超過三個小時的執行階段，hello 程序會重複，toothree 時間。  Hello 第三個重新啟動之後，如果 hello runbook 仍有未完成三個小時內，則 hello runbook 工作已失敗，而且 hello 作業狀態顯示**失敗，等待資源**。  在此情況下，您會收到 hello 遵循 hello 失敗的例外狀況。

*hello 作業無法繼續執行，因為它已重複收回 hello 從相同的檢查點。請確定您的 Runbook 在未保存其狀態的情況下，不會長時間執行作業。*

這會是無限期而無法完成，runbook 執行的 tooprotect hello 服務，它們並非能夠 toomake 它 toohello 再次卸載，否則下一個檢查點。

如果 hello runbook 沒有檢查點，或者 hello 作業在卸載之前未到達 hello 第一個檢查點，然後重新啟動從 hello 開頭。  

當您建立 runbook 時，您應該確保兩個檢查點之間的任何活動不會超過三小時一次該 hello 時間 toorun。 您可能需要 tooadd 檢查點 tooyour runbook tooensure，它不會達到這三個小時的限制或分解長時間執行的作業。 例如，您的 Runbook 可能在大型 SQL 資料庫上執行重新索引。 如果此單一操作未完成內 hello 公平共用限制 hello 作業會卸載然後 hello 從頭重新啟動。 在此情況下，您應該 hello 重新索引操作分成多個步驟，例如一次重新一個資料表分割，然後再插入檢查點之後每個作業，以便 hello 作業無法繼續 hello 最後一個作業 toocomplete 之後。

## <a name="next-steps"></a>後續步驟
* toolearn hello 不同的方法可以使用的 toostart 在 Azure 自動化 runbook 詳細資料請參閱[Azure 自動化中啟動 runbook](automation-starting-a-runbook.md)

