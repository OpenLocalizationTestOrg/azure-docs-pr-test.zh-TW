---
title: "Azure 自動化中的 aaaChild runbook |Microsoft 文件"
description: "描述 hello 不同方法在 Azure 自動化中啟動 runbook，從另一個 runbook 並分享兩者之間的資訊。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 919887b9-43e2-4c16-883c-f81807fe37db
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d3d06818d344b565d53cc4f4705b41dcfcf9a376
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="child-runbooks-in-azure-automation"></a>Azure 自動化中的子 Runbook
它是在 Azure 自動化 toowrite 可重複使用、 模組化 runbook 具備可供其他 runbook 的不同功能的最佳作法。 父 runbook 通常會呼叫一或多個子 runbook tooperform 所需的功能。 有兩種方式 toocall 子系 runbook，而且每個具有不同差異，您應該了解，以便決定，將會最適合您不同的案例。

## <a name="invoking-a-child-runbook-using-inline-execution"></a>使用內嵌執行叫用子 Runbook
tooinvoke runbook 內嵌從另一個 runbook，方法，您可以使用 hello hello runbook 名稱，並提供其參數的值，如同您使用活動或 cmdlet。  中的所有 runbook 都 hello 相同自動化帳戶都可用 tooall toobe 用於這種方式的其他項目。 hello 父 runbook 將會等到 hello 子 runbook toocomplete 日前 toohello 下一行，並將任何輸出傳回直接 toohello 父代。

當您叫用 runbook 內嵌時，它會在 hello hello 父 runbook 相同作業中執行。 有不會指示 hello 作業記錄中的 hello 已執行的子系 runbook。 任何例外狀況及任何資料流從 hello 子 runbook 的輸出會與 hello 父系相關聯。 這導致較少的工作，並讓它們更容易 tootrack 且 tootroubleshoot 自 hello 子 runbook 擲回任何例外狀況，及其任何資料流輸出都與 hello 父工作相關聯。

發佈 Runbook 時，其呼叫的所有子 Runbook 都必須是已發佈的。 這是因為在編譯 Runbook 時，Azure 自動化會建置與任何子 Runbook 的關聯。 不是，如果 hello 父 runbook 會出現 toopublish 正常運作，但啟動時，會產生例外狀況。 如果發生這種情況，您可以重新發佈順序 tooproperly 參考 hello 子 runbook 中的 hello 父 runbook。 如果任何 hello 子 runbook 變更 hello 關聯將已經建立，因為不需要 toorepublish hello 父 runbook。

hello 內嵌方式呼叫子 runbook 參數可以是任何資料類型，包括複雜的物件，而且沒有任何[JSON 序列化](automation-starting-a-runbook.md#runbook-parameters)因為，所以當您開始使用 Azure 管理入口網站 hello hello runbook，或以 hello開始 AzureRmAutomationRunbook cmdlet。

### <a name="runbook-types"></a>Runbook 類型
哪些類型可以彼此呼叫：

* [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks) 和[圖形化 Runbook](automation-runbook-types.md#graphical-runbooks) 可以內嵌方式呼叫彼此 (這兩者都是 PowerShell)。
* [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks) 和圖形化 PowerShell 工作流程 Runbook 可以內嵌方式呼叫彼此 (這兩者都是 PowerShell 工作流程)。
* hello PowerShell 類型並 hello PowerShell 工作流程類型不能彼此內嵌方式呼叫，必須使用開始 AzureRmAutomationRunbook。

何時會與發行順序有關：

* hello 發行的 runbook 只會有影響的 PowerShell 工作流程和圖形化 PowerShell 工作流程 runbook 中的順序。

當您呼叫使用內嵌執行圖形或 PowerShell 工作流程子系 runbook 時，只會使用 hello hello runbook 名稱。  當您呼叫 PowerShell 子系 runbook 時，您必須前面有其名稱與*。\\* hello 指令碼的 toospecify 位於 hello 本機目錄中。 

### <a name="example"></a>範例
hello 下列範例會叫用接受三個參數、 複雜物件、 整數和布林值的測試子 runbook。 hello hello 子 runbook 的輸出會指派 tooa 變數。  在此情況下，hello 子系 runbook 是 PowerShell 工作流程 runbook

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = PSWF-ChildRunbook –VM $vm –RepeatCount 2 –Restart $true

以下是 hello 做 hello 子系使用 PowerShell runbook 的相同範例。

    $vm = Get-AzureRmVM –ResourceGroupName "LabRG" –Name "MyVM"
    $output = .\PS-ChildRunbook.ps1 –VM $vm –RepeatCount 2 –Restart $true


## <a name="starting-a-child-runbook-using-cmdlet"></a>使用 Cmdlet 啟動子 Runbook
您可以使用 hello[開始 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603661.aspx) cmdlet toostart runbook 中所述[toostart 使用 Windows PowerShell runbook](automation-starting-a-runbook.md#starting-a-runbook-with-windows-powershell)。 使用這個 Cmdlet 的模式有兩種。  一種模式，在 hello cmdlet 就會傳回 hello 作業識別碼 hello 子 runbook 建立 hello 子工作。  在 hello 其他模式，您可以指定 hello 啟用**-等候**hello cmdlet 會等待直到 hello 子參數，作業結束，而且會傳回從 hello 子 runbook 的 hello 輸出。

從 cmdlet 啟動子 runbook 的 hello 作業會從 hello 父 runbook 執行的個別工作中。 這會產生比叫用 hello runbook 內嵌更多工作，並使其更加困難 tootrack。 hello 父代可以以非同步方式啟動多個子系 runbook，而不等候每個 toocomplete。 以相同類型的平行呼叫 hello 子 runbook 內嵌，hello 父 runbook 將需要 toouse hello[平行關鍵字](automation-powershell-workflow.md#parallel-processing)。

使用 Cmdlet 啟動之子 Runbook 的參數是以雜湊表方式提供，如 [Runbook 參數](automation-starting-a-runbook.md#runbook-parameters)中所述。 只能使用簡單資料類型。 如果 hello runbook 有複雜資料型別參數，然後必須內嵌呼叫它。

### <a name="example"></a>範例
hello 下列範例會啟動子 runbook 的參數，然後等候 toocomplete 使用 hello 開始 AzureRmAutomationRunbook-等候參數。 完成後，從 hello 子 runbook 會收集其輸出。

    $params = @{"VMName"="MyVM";"RepeatCount"=2;"Restart"=$true} 
    $joboutput = Start-AzureRmAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Test-ChildRunbook" -ResourceGroupName "LabRG" –Parameters $params –wait


## <a name="comparison-of-methods-for-calling-a-child-runbook"></a>子 Runbook 的呼叫方法比較
hello 下表摘要說明 hello 差異 hello 兩種方法，從另一個 runbook 呼叫某個 runbook。

|  | 內嵌 | Cmdlet |
|:--- |:--- |:--- |
| 作業 |子 runbook hello 與 hello 父系相同作業中執行。 |Hello 子 runbook 建立不同的工作。 |
| 執行 |父 runbook 會等到 hello 子 runbook toocomplete 才能繼續。 |父 runbook 會繼續執行，啟動子 runbook 之後，立即*或*父 runbook 會等到 hello 子工作 toofinish。 |
| 輸出 |父 Runbook 可以直接從子 Runbook 取得輸出。 |父 Runbook 必須擷取子 Runbook 作業的輸出，或  父 Runbook 可以直接從子 Runbook 取得輸出。 |
| 參數 |Hello 子 runbook 參數的值會個別指定，而且可以使用任何資料類型。 |值為 hello 子 runbook 參數必須結合成單一雜湊表，而且只可包含簡單、 陣列，及運用 JSON 序列化的資料類型的物件。 |
| 自動化帳戶 |父系 runbook 只能使用 hello 中的子系 runbook 相同自動化帳戶。 |父 runbook 可以使用任何自動化帳戶 hello 的子系 runbook 相同的 Azure 訂用帳戶和甚至不同訂用帳戶有連線 tooit。 |
| 發佈 |發佈父 Runbook 之前必須先發佈子 Runbook。 |啟動父 Runbook 之前必須先發佈子 Runbook。 |

## <a name="next-steps"></a>後續步驟
* [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md)
* [Azure 自動化中的 Runbook 輸出與訊息](automation-runbook-output-and-messages.md)

