---
title: "Azure 自動化中的 aaaMy 第一個 PowerShell runbook |Microsoft 文件"
description: "教學課程會引導您進行 hello 建立、 測試和發佈的簡單的 PowerShell runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: 
keywords: "azure powershell, powershell 指令碼教學課程, powershell 自動化"
ms.assetid: a43b395a-e740-41a3-ae62-40eac9d0ec00
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/26/2017
ms.author: magoedte;sngun
ms.openlocfilehash: abff94abe666cd8423c35b970b4162ba9247bcf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="my-first-powershell-runbook"></a>我的第一個 PowerShell Runbook

> [!div class="op_single_selector"]
> * [圖形化](automation-first-runbook-graphical.md)
> * [PowerShell](automation-first-runbook-textual-powershell.md)
> * [PowerShell 工作流程](automation-first-runbook-textual.md)
> 
> 

本教學課程將引導您完成建立 hello [PowerShell runbook](automation-runbook-types.md#powershell-runbooks) Azure 自動化中。 我們會開始的簡單 runbook，我們測試發行時，我們會說明如何 tootrack hello hello runbook 工作的狀態。 然後我們修改 hello runbook tooactually 管理在此情況下啟動 Azure 虛擬機器的 Azure 資源。 最後，我們要新增 runbook 參數 hello 更強固的 runbook。

## <a name="prerequisites"></a>必要條件
toocomplete 本教學課程中，您需要遵循的 hello:

* Azure 訂用帳戶。 如果您沒有這類帳戶，可以[啟用自己的 MSDN 訂戶權益<a href="/pricing/free-account/" target="_blank">或](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)[註冊免費帳戶](https://azure.microsoft.com/free/)。
* [自動化帳戶](automation-sec-configure-azure-runas-account.md)toohold hello runbook 並驗證 tooAzure 資源。  此帳戶必須具有權限 toostart，停止 hello 虛擬機器。
* Azure 虛擬機器。 我們會停止並啟動這部電腦，因此它不該是生產 VM。

## <a name="step-1---create-new-runbook"></a>步驟 1 - 建立新的 Runbook
我們會先建立輸出的 hello 文字的簡單 runbook *Hello World*。

1. 在 hello Azure 入口網站，開啟您的自動化帳戶。  
   hello 自動化帳戶 頁面可讓您快速檢視 hello 資源此帳戶中。 您應該已經有一些資產。 其中大部分都是會自動包含在新的自動化帳戶的 hello 模組。 您也應該擁有 hello 認證資產中所述 hello[必要條件](#prerequisites)。
2. 按一下 hello **Runbook**磚 tooopen hello runbook 的清單。<br><br> ![RunbooksControl](media/automation-first-runbook-textual-powershell/runbooks-control-tiles.png)  
3. 建立新的 runbook，依序按一下 hello**新增 runbook**  按鈕，然後**建立新的 runbook**。
4. Hello runbook hello 命名*MyFirstRunbook PowerShell*。
5. 在此情況下，我們會 toocreate [PowerShell runbook](automation-runbook-types.md#powershell-runbooks)因此選取**Powershell**如**Runbook 類型**。<br><br> ![Runbook 類型](media/automation-first-runbook-textual-powershell/automation-runbook-type.png)  
6. 按一下**建立**toocreate hello runbook 和開啟 hello 文字編輯器。

## <a name="step-2---add-code-toohello-runbook"></a>步驟 2-加入程式碼 toohello runbook
您可以直接在 hello runbook 的其中一個類型程式碼或您可以從程式庫控制項 hello 選取 cmdlet、 runbook 和資產，但它們已加入 toohello runbook 與任何相關的參數。 這個逐步解說中，我們直接輸入 hello runbook。

1. 我們的 Runbook 目前是空白的，輸入「Write-Output "Hello World."」 。<br><br> ![](media/automation-first-runbook-textual-powershell/automation-helloworld.png)  
2. 按一下以儲存 hello runbook**儲存**。<br><br> ![儲存按鈕](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-save.png)  

## <a name="step-3---test-hello-runbook"></a>步驟 3-測試 hello runbook
我們發行 hello runbook toomake 之前它可用在生產環境中，我們想要 tootest 它 toomake 確定它是否正常運作。 測試 Runbook 時，您會執行其 **草稿** 版本，並以互動方式檢視其輸出。

1. 按一下**測試窗格**tooopen hello 測試窗格。<br><br> ![Test Pane](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-test.png)  
2. 按一下**啟動**toostart hello 測試。 這應該是 hello 才啟用選項。
3. 隨即會建立 [Runbook 工作](automation-runbook-execution.md) ，並顯示其狀態。  
   做為啟動 hello 作業狀態*排入佇列*表示它正在等待在 hello 雲端 toocome 可用的 runbook worker。 它會接著進入太*起始*背景工作宣告 hello 作業時，然後*執行*hello runbook 實際開始執行時。  
4. 當 hello runbook 作業完成時，會顯示其輸出。 在我們的情況中，我們應該會看到 Hello World。<br><br> ![測試窗格輸出](media/automation-first-runbook-textual-powershell/automation-testpane-output.png)  
5. 關閉 hello 測試窗格 tooreturn toohello 畫布。

## <a name="step-4---publish-and-start-hello-runbook"></a>步驟 4-發佈和啟動 hello runbook
我們建立的 hello runbook 仍處於草稿模式。 我們需要 toopublish 前我們可以在生產環境中執行它。  當您發行的 runbook 時，您以覆寫現有已發佈版本 hello hello 草稿版本。  在我們的案例中，我們已發佈版本還沒有因為我們剛才建立 hello runbook。

1. 按一下**發行**toopublish hello runbook，然後**是**出現提示時。<br><br> ![發佈按鈕](media/automation-first-runbook-textual-powershell/automation-runbook-edit-controls-publish.png)  
2. 當您捲動左的 tooview hello runbook 在 hello **Runbook**窗格現在，它會顯示**撰寫狀態**的**發佈**。
3. 捲軸背景 toohello 右 tooview hello 窗格**MyFirstRunbook PowerShell**。  
   hello hello 頂端的選項讓我們 toostart hello runbook、 檢視 hello runbook、 排程在未來，hello toostart 或建立[webhook](automation-webhooks.md)讓它可以啟動透過 HTTP 呼叫。
4. 我們想 toostart hello runbook，因此請按**啟動**，然後按一下**確定**hello 啟動 Runbook 刀鋒視窗開啟時。<br><br> ![開始按鈕](media/automation-first-runbook-textual-powershell/automation-runbook-controls-start.png)<br>    
5. 工作窗格會開啟供我們建立的 hello runbook 工作。 我們可以關閉此窗格中，但在此情況下我們維持開啟，因此我們可以觀看 hello 作業的進度。
6. 中會顯示 hello 作業狀態**工作摘要**和相符項目 hello 我們了解我們所測試 hello runbook 時的狀態。<br><br> ![工作摘要](media/automation-first-runbook-textual-powershell/job-pane-status-blade-jobsummary.png)<br>  
7. 一次 hello runbook 狀態顯示*已完成*，按一下 **輸出**。 hello [輸出] 窗格會開啟，而且我們可以看到我們*Hello World*。<br><br> ![工作輸出](media/automation-first-runbook-textual-powershell/job-pane-status-blade-outputtile.png)<br> 
8. 關閉 hello 輸出窗格。
9. 按一下**所有記錄檔**hello runbook 工作的 tooopen hello 資料流 窗格。 我們應該只會看到*Hello World*在 hello 輸出資料流，但這會顯示 runbook 作業，例如 Verbose 和錯誤的其他資料流 hello runbook 是否寫入 toothem。<br><br> ![](media/automation-first-runbook-textual-powershell/job-pane-status-blade-alllogstile.png)<br>   
10. 關閉 hello 資料流窗格和 hello 工作窗格 tooreturn toohello MyFirstRunbook PowerShell 窗格。
11. 按一下**作業**tooopen hello [工作] 窗格，針對此 runbook。 這樣就會列出所有 hello 這個 runbook 所建立的工作。 我們只能看到列出因為我們只執行 hello 作業一次一項作業。<br><br> ![作業清單](media/automation-first-runbook-textual-powershell/runbook-control-job-tile.png)  
12. 您可以按一下此工作 tooopen hello 我們開始 hello runbook 時，我們會檢視的相同 [工作] 窗格。 這可讓您 toogo 回時間和檢視 hello 詳細資料中針對特定 runbook 所建立的任何作業。

## <a name="step-5---add-authentication-toomanage-azure-resources"></a>步驟 5 – 新增驗證 toomanage Azure 資源
我們已經測試並發行我們 Runbook，但是到目前為止，它似乎並不實用。 我們想要 toohave 它管理的 Azure 資源。 不是能 toodo 雖然除非我們驗證使用 hello 認證稱為 tooin hello[必要條件](#prerequisites)。 這是以 hello**新增 AzureRmAccount** cmdlet。

1. 開啟的 hello 文字編輯器，依序按一下**編輯**hello MyFirstRunbook PowerShell 窗格上。<br><br> ![編輯 Runbook](media/automation-first-runbook-textual-powershell/automation-runbook-controls-edit.png)<br>   
2. 我們不需要 hello **Write-output**不再行，因此請繼續進行和刪除。
3. 輸入或複製並貼上下列程式碼會處理 hello 驗證與自動化執行身分帳戶的 hello:
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationId $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   ```
   <br>
4. 按一下**測試窗格**，以便我們可以測試 hello runbook。
5. 按一下**啟動**toostart hello 測試。 在完成時，您應該會收到類似輸出 toohello 之後，顯示您的帳戶的基本資訊。 這可確認該 hello 認證有效。<br><br> ![驗證](media/automation-first-runbook-textual-powershell/runbook-auth-output.png)

## <a name="step-6---add-code-toostart-a-virtual-machine"></a>步驟 6-加入程式碼 toostart 虛擬機器
既然我們 runbook 驗證 tooour Azure 訂用帳戶，我們可以管理資源。 我們加入命令 toostart 虛擬機器。 您可以挑選您 Azure 訂用帳戶中的任何虛擬機器，而且現在我們將硬 hello runbook 中的該名稱。

1. 之後*新增 AzureRmAccount*，型別*開始 AzureRmVM-名稱 '為 VMName' ResourceGroupName 'NameofResourceGroup'*提供 hello 名稱和 hello 虛擬機器 toostart 資源群組名稱。  
   
   ```
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name 'VMName' -ResourceGroupName 'ResourceGroupName'
   ```
   <br>
2. 儲存 hello runbook，然後按一下**測試窗格**，以便我們可以測試它。
3. 按一下**啟動**toostart hello 測試。 在完成時，請檢查該 hello 虛擬機器已啟動。

## <a name="step-7---add-an-input-parameter-toohello-runbook"></a>步驟 7-加入的輸入的參數 toohello runbook
我們 runbook 目前開始 hello 虛擬機器，我們 hello runbook 中的硬式編碼，但如果我們在 hello runbook 啟動時，指定 hello 虛擬機器會是更有用。 我們現在會將輸入的參數 toohello runbook tooprovide 該功能。

1. 加入參數*VMName*和*ResourceGroupName* toohello runbook，並使用這些變數與 hello**開始 AzureRmVM** cmdlet，如下列的 hello 範例所示。  
   
   ```
   Param(
    [string]$VMName,
    [string]$ResourceGroupName
   )
   $Conn = Get-AutomationConnection -Name AzureRunAsConnection
   Add-AzureRMAccount -ServicePrincipal -Tenant $Conn.TenantID `
   -ApplicationID $Conn.ApplicationID -CertificateThumbprint $Conn.CertificateThumbprint
   Start-AzureRmVM -Name $VMName -ResourceGroupName $ResourceGroupName
   ```
   <br>
2. 儲存 hello runbook 並開啟 hello 測試窗格。 您可以現在提供值給 hello hello 測試中使用的兩個輸入的變數。
3. 關閉 hello 測試窗格。
4. 按一下**發行**toopublish hello 新版 hello runbook。
5. 停止 hello hello 上一個步驟中啟動的虛擬機器。
6. 按一下**啟動**toostart hello runbook。 型別在 hello **VMName**和**ResourceGroupName**要 toostart hello 虛擬機器。<br><br> ![傳遞參數](media/automation-first-runbook-textual-powershell/automation-pass-params.png)<br>  
7. Hello runbook 完成時，請檢查該 hello 虛擬機器已啟動。

## <a name="differences-from-powershell-workflow"></a>與 PowerShell 工作流程的差異
PowerShell runbook 有 hello 相同生命週期、 功能和管理 PowerShell 工作流程 runbook，但有一些差異和限制：

1. 執行快速比較的 tooPowerShell 工作流程 runbook，因為它們不需要編譯步驟的 PowerShell runbook。
2. PowerShell 工作流程 runbook 支援檢查點，使用檢查點，PowerShell 工作流程 runbook 可以繼續從 hello runbook 中的任何時間點，而 PowerShell runbook 只能從 hello 開頭繼續。
3. PowerShell 工作流程 Runbook 支援平行和序列執行，而 PowerShell Runbook 只能以序列方式執行命令。
4. 在 PowerShell 工作流程 Runbook 中，活動、命令或指令碼區塊可以有它自己的 Runspace，而在 PowerShell Runbook 中，指令碼中的所有項目會在單一的 Runspace 中執行。 原生 PowerShell Runbook 與 PowerShell 工作流程 Runbook 之間還有一些 [語法差異](https://technet.microsoft.com/magazine/dn151046.aspx) 。

## <a name="next-steps"></a>後續步驟
* tooget 開始使用圖形化 runbook，請參閱[我的第一個圖形化 runbook](automation-first-runbook-graphical.md)
* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)
* tooknow 深入了解 runbook 類型、 其優點和限制，請參閱[Azure 自動化 runbook 類型](automation-runbook-types.md)
* 如需 PowerShell 指令碼支援功能的詳細資訊，請參閱 [Azure 自動化中的原生 PowerShell 指令碼支援](https://azure.microsoft.com/blog/announcing-powershell-script-support-azure-automation-2/)

