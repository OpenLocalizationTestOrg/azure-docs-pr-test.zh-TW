---
title: "Azure 自動化的 PowerShell 工作流程 aaaLearning |Microsoft 文件"
description: "本文旨在作為快速課程的作者熟悉 PowerShell 和 PowerShell 工作流程與概念適用 tooAutomation runbook 之間的 PowerShell toounderstand hello 特定差異。"
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: tysonn
ms.assetid: 84bf133e-5343-4e0e-8d6c-bb14304a70db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/21/2017
ms.author: magoedte;bwren
ms.openlocfilehash: 362c504eb96d31b99a826b128e6a591beecaa084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="learning-key-windows-powershell-workflow-concepts-for-automation-runbooks"></a>了解適用於自動化 Runbook 的重要 Windows PowerShell 工作流程概念 
Azure 自動化中的 Runbook 會實作為 Windows PowerShell 工作流程。  Windows PowerShell 工作流程為類似 tooa Windows PowerShell 指令碼，但有一些顯著的差異可能會造成混淆的 tooa 新的使用者。  您撰寫使用 PowerShell 工作流程 runbook 的預期的 toohelp 本文時，我們建議您撰寫使用 PowerShell，除非您需要檢查點的 runbook。  有幾個語法差異撰寫 PowerShell 工作流程 runbook 時，這些差異需要更多工作 toowrite 有效工作流程。  

工作流程是一系列經過程式設計、 相互連結的步驟執行長時間執行工作，或需要多個裝置或受管理的節點上的 hello 協調多個步驟。 hello 一般指令碼工作流程的好處包括 hello 能力 toosimultaneously 執行多個裝置的動作和 hello 能力 tooautomatically 從失敗中復原。 Windows PowerShell 工作流程是使用 Windows Workflow Foundation 的 Windows PowerShell 指令碼。 雖然 hello 工作流程是使用 Windows PowerShell 語法撰寫，並由 Windows PowerShell 啟動，它會由 Windows Workflow Foundation 進行處理。

如這篇文章中的 hello 主題的詳細資訊，請參閱[開始使用 Windows PowerShell 工作流程](http://technet.microsoft.com/library/jj134242.aspx)。

## <a name="basic-structure-of-a-workflow"></a>工作流程的基本結構
hello 第一個步驟 tooconverting PowerShell 指令碼 tooa PowerShell 工作流程括以 hello**工作流程**關鍵字。  工作流程啟動以 hello**工作流程**關鍵字後面接著括在大括弧的 hello 指令碼的 hello 主體。 hello hello 工作流程名稱遵循 hello**工作流程**關鍵字 hello 語法如下所示：

    Workflow Test-Workflow
    {
       <Commands>
    }

hello hello 工作流程名稱必須符合 hello hello 自動化 runbook 名稱。 如果正在匯入 hello runbook，則 hello 檔案名稱必須符合 hello 工作流程名稱，而且必須以結尾*.ps1*。

tooadd 參數 toohello 工作流程，使用 hello **Param**關鍵字就像 tooa 指令碼一樣。

## <a name="code-changes"></a>程式碼變更
PowerShell 工作流程程式碼看起來幾乎完全相同的 tooPowerShell 指令碼，除了少數的重大變更。  hello 下列各節描述您需要 toomake tooa PowerShell 指令碼為其 toorun 工作流程中的變更。

### <a name="activities"></a>活動
活動是工作流程中的特定工作。 就像指令碼是由一或多個命令所組成，工作流程是由序列中執行的一或多個活動所組成。 Windows PowerShell 工作流程，自動轉換許多 Windows PowerShell cmdlet tooactivities hello 執行工作流程時。 當您在 runbook 中指定其中一個指令程式時，hello 對應的活動是由 Windows Workflow Foundation 中執行。 針對沒有相應動作這些 cmdlet，Windows PowerShell 工作流程會自動執行中的 hello cmdlet [InlineScript](#inlinescript)活動。 有一組 Cmdlet 被排除，除非您明確在 InlineScript 區塊中將其納入，否則無法用在工作流程中。 如需這些概念的詳細資訊，請參閱 [在指令碼工作流程中使用活動](http://technet.microsoft.com/library/jj574194.aspx)。

工作流程活動共用一組通用參數 tooconfigure 其作業。 如需 hello 工作流程一般參數的詳細資訊，請參閱[about_WorkflowCommonParameters](http://technet.microsoft.com/library/jj129719.aspx)。

### <a name="positional-parameters"></a>位置參數
您無法對活動和工作流程中的 Cmdlet 使用位置參數。  這都表示您必須使用參數名稱。

例如，請考慮下列程式碼可取得所有執行中服務的 hello。

     Get-Service | Where-Object {$_.Status -eq "Running"}

如果您嘗試 toorun 這個相同的程式碼工作流程中，您收到訊息像 「 無法使用指定的 hello 解析集參數具名參數 」。  toocorrect，提供 hello 參數名稱，如 hello 下列所示。

    Workflow Get-RunningServices
    {
        Get-Service | Where-Object -FilterScript {$_.Status -eq "Running"}
    }

### <a name="deserialized-objects"></a>已還原序列化的物件
工作流程中的物件會還原序列化。  這表示其屬性都仍然可用，而不是它們的方法。  例如，請考慮 hello 下列 PowerShell 程式碼會停止服務，使用 hello 停止方法的 hello 服務物件。

    $Service = Get-Service -Name MyService
    $Service.Stop()

如果您嘗試 toorun 此工作流程中，您會收到的錯誤訊息 「 方法引動過程不支援在 Windows PowerShell 工作流程 」。  

其中一個選項是 toowrap 這兩行程式中的程式碼[InlineScript](#inlinescript)封鎖在這種情況下 $Service 會 hello 區塊內的服務物件。

    Workflow Stop-Service
    {
        InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
        }
    }

另一個選項是 toouse 執行的另一個 cmdlet hello 與 hello 方法相同的功能，如果有的話。  在我們的範例，hello Stop-service cmdlet 提供 hello 與 hello 停止方法之外，相同的功能無法使用 hello 下列工作流程。

    Workflow Stop-MyService
    {
        $Service = Get-Service -Name MyService
        Stop-Service -Name $Service.Name
    }


## <a name="inlinescript"></a>InlineScript
hello **InlineScript**活動時，您需要 toorun 一或多個命令做為傳統的 PowerShell 指令碼，而不是 PowerShell 工作流程。  工作流程中的命令會傳送 tooWindows Workflow Foundation 進行處理，而 Windows PowerShell 會處理 InlineScript 區塊中的命令。

InlineScript 會使用下列語法如下所示的 hello。

    InlineScript
    {
      <Script Block>
    } <Common Parameters>

您可以從 InlineScript 傳回輸出，透過將 hello 輸出 tooa 變數指派。 hello 下列範例會停止服務，並再將輸出 hello 服務名稱。

    Workflow Stop-MyService
    {
        $Output = InlineScript {
            $Service = Get-Service -Name MyService
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


您可以將值傳入 InlineScript 區塊，但必須使用 **$Using** 範圍修飾詞。  hello 下列範例是相同的 toohello 前一個範例不同之處在於 hello 服務提供名稱的變數。

    Workflow Stop-MyService
    {
        $ServiceName = "MyService"

        $Output = InlineScript {
            $Service = Get-Service -Name $Using:ServiceName
            $Service.Stop()
            $Service
        }

        $Output.Name
    }


雖然 InlineScript 活動可以在特定工作流程中重要，它們不支援工作流程建構，並應該只用於時所需的 hello 下列原因：

* 您不能在 InlineScript 區塊內使用[檢查點](#checkpoints)。 如果 hello 區塊內發生失敗，它必須從 hello 區塊的 hello 開頭繼續。
* 您不能在 InlineScriptBlock 內使用[平行執行](#parallel-processing)。
* InlineScript 會影響 hello 工作流程的延展性，因為它會保留 hello hello hello InlineScript 區塊完整長度的 Windows PowerShell 工作階段。

如需使用 InlineScript 的詳細資訊，請參閱[在工作流程中執行 Windows PowerShell 命令](http://technet.microsoft.com/library/jj574197.aspx)和 [about_InlineScript](http://technet.microsoft.com/library/jj649082.aspx)。

## <a name="parallel-processing"></a>平行處理
Windows PowerShell 工作流程的其中一個優點是 hello 能力 tooperform 一組命令，以平行方式，而不是以循序方式就如同一般的指令碼。

您可以使用 hello**平行**關鍵字 toocreate 同時執行的多個命令與指令碼區塊。 這會使用下列語法如下所示的 hello。 在此情況下，Activity1 和 Activity2 開始 hello 相同的時間。 只有在 Activity1 和 Activity2 都已完成之後，Activity3 才會開始。

    Parallel
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>


例如，請考慮下列 PowerShell 命令，複製多個檔案 tooa 網路目的地的 hello。  這些命令會以循序方式執行，因此該檔案必須完成複製之前 hello 接下來會啟動。     

    Copy-Item -Path C:\LocalPath\File1.txt -Destination \\NetworkPath\File1.txt
    Copy-Item -Path C:\LocalPath\File2.txt -Destination \\NetworkPath\File2.txt
    Copy-Item -Path C:\LocalPath\File3.txt -Destination \\NetworkPath\File3.txt

hello 下列工作流程來執行這些相同命令以平行方式，讓他們所有啟動複製 hello 在相同的時間。  它們只是所有之後複製 hello 完成訊息隨即出現。

    Workflow Copy-Files
    {
        Parallel
        {
            Copy-Item -Path "C:\LocalPath\File1.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File2.txt" -Destination "\\NetworkPath"
            Copy-Item -Path "C:\LocalPath\File3.txt" -Destination "\\NetworkPath"
        }

        Write-Output "Files copied."
    }


您可以使用 hello **ForEach-Parallel**同時建構 tooprocess 命令，每個項目集合中。 hello hello 集合中的項目會處理以平行方式，而 hello 指令碼區塊中的 hello 命令以循序方式執行。 這會使用下列語法如下所示的 hello。 在此情況下，Activity1 啟動 hello 相同時間 hello 集合中的所有項目。 針對每個項目，Activity2 會在 Activity1 完成之後開始。 只有在 Activity1 和 Activity2 已完成所有項目之後，Activity3 才會開始。

    ForEach -Parallel ($<item> in $<collection>)
    {
      <Activity1>
      <Activity2>
    }
    <Activity3>

下列範例中的 hello 是類似 toohello 上例平行複製檔案。  在此情況下，複製之後會對每個檔案顯示訊息。  它們只是所有之後完全複製 hello 最後完成的訊息隨即出現。

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach -Parallel ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
        }

        Write-Output "All files copied."
    }

> [!NOTE]
> 我們不建議以平行方式執行子系 runbook，因為這已顯示 toogive 不可靠的結果。  hello 有時 hello 子系 runbook 的輸出不會顯示，並設定一個子系 runbook 中的可能會影響 hello 其他平行子 runbook
>

## <a name="checkpoints"></a>檢查點
A*檢查點*是 hello hello 工作流程包含 hello 目前變數值的目前狀態的快照集並將任何輸出產生的 toothat 點。 如果工作流程以錯誤結束，或已暫停，然後 hello 下一次執行它將會開始從其最後一個檢查點，而不是 hello 開頭 hello 工作。  您可以在 hello 的工作流程中設定檢查點**Checkpoint-workflow**活動。

在下列範例程式碼的 hello，Activity2 造成 hello tooend 工作流程之後，就會發生例外狀況。 再次執行 hello 工作流程時，會從執行 Activity2 因為這是之後在 hello 最後一個檢查點設定。

    <Activity1>
    Checkpoint-Workflow
    <Activity2>
    <Exception>
    <Activity3>

活動可能容易出錯的 tooexception 且不應重複如果繼續 hello 工作流程之後，您應該在工作流程中設定檢查點。 例如，您的工作流程可能會建立虛擬機器。 您可以設定檢查點之前和之後 hello 命令 toocreate hello 虛擬機器。 如果 hello 建立失敗，然後 hello 命令可能會重複一次啟動 hello 工作流程時。 如果 hello 工作失敗之後 hello 建立成功，然後 hello 虛擬機器將不會建立一次時繼續 hello 工作流程。

下列範例中的 hello 複製多個檔案 tooa 網路位置，並設定檢查點之後的每個檔案。  如果失去 hello 網路位置，則 hello 工作流程結束錯誤。  當重新啟動時，它將會繼續在 hello 最後一個檢查點，這表示只有 hello 已複製的檔案會略過。

    Workflow Copy-Files
    {
        $files = @("C:\LocalPath\File1.txt","C:\LocalPath\File2.txt","C:\LocalPath\File3.txt")

        ForEach ($File in $Files)
        {
            Copy-Item -Path $File -Destination \\NetworkPath
            Write-Output "$File copied."
            Checkpoint-Workflow
        }

        Write-Output "All files copied."
    }

因為使用者名稱認證不永久變更之後呼叫 hello [Suspend-workflow](https://technet.microsoft.com/library/jj733586.aspx)活動或 hello 最後一個檢查點之後, 您需要 tooset hello 認證 toonull，然後再擷取一次從 hello 資產存放區之後**暫停工作流程**或稱為檢查點。  否則，您可能會收到下列錯誤訊息的 hello: *hello 工作流程工作無法繼續執行，可能是因為持續性資料無法完整地儲存或儲存持續性資料已損毀。您必須重新啟動 hello 工作流程。*

hello 遵循相同的程式碼示範如何 toohandle 這在您的 PowerShell 工作流程 runbook。

    workflow CreateTestVms
    {
       $Cred = Get-AzureAutomationCredential -Name "MyCredential"
       $null = Add-AzureRmAccount -Credential $Cred

       $VmsToCreate = Get-AzureAutomationVariable -Name "VmsToCreate"

       foreach ($VmName in $VmsToCreate)
         {
          # Do work first toocreate hello VM (code not shown)

          # Now add hello VM
          New-AzureRmVm -VM $Vm -Location "WestUs" -ResourceGroupName "ResourceGroup01"

          # Checkpoint so that VM creation is not repeated if workflow suspends
          $Cred = $null
          Checkpoint-Workflow
          $Cred = Get-AzureAutomationCredential -Name "MyCredential"
          $null = Add-AzureRmAccount -Credential $Cred
         }
     }


如果您使用以服務主體設定的執行身分帳戶進行驗證，則不必這麼做。  

如需有關檢查點的詳細資訊，請參閱[新增檢查點 tooa 指令碼工作流程](http://technet.microsoft.com/library/jj574114.aspx)。

## <a name="next-steps"></a>後續步驟
* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)
