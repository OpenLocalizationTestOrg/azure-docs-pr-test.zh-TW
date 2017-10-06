---
title: "自動化 Runbook 類型 aaaAzure |Microsoft 文件"
description: "描述 hello 不同類型的 runbook，您可以使用 Azure 自動化，您應該考慮判斷哪些類型 toouse 時的考量中。 "
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 9265c975-4281-4819-a84f-d86641277f36
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 06/01/2017
ms.author: bwren
ms.openlocfilehash: c28aa57c77025764b16784372308a4ff2f596914
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-runbook-types"></a>Azure 自動化 Runbook 類型
Azure 自動化 hello 下表中支援四種類型的簡短描述的 runbook。  hello 以下各節提供每個型別，包括時的考量的進一步資訊每個 toouse。

| 類型 | 說明 |
|:--- |:--- |
| [圖形化](#graphical-runbooks) |以 Windows PowerShell 為基礎，而且完全在 Azure 入口網站的圖形化編輯器中建立和編輯。 |
| [圖形化 PowerShell 工作流程](#graphical-runbooks) |根據 Windows PowerShell 工作流程和 Azure 入口網站中的建立及編輯完全在 hello 圖形化編輯器。 |
| [PowerShell](#powershell-runbooks) |以 Windows PowerShell 指令碼為基礎的文字 Runbook。 |
| [PowerShell 工作流程](#powershell-workflow-runbooks) |以 Windows PowerShell 工作流程為基礎的文字 Runbook。 |

## <a name="graphical-runbooks"></a>圖形化 Runbook
[圖形化](automation-runbook-types.md#graphical-runbooks)及圖形化 PowerShell 工作流程 runbook 建立和編輯與 hello hello Azure 入口網站中的圖形化編輯器。  您可以將它們匯出 tooa 檔案，然後匯入另一個自動化帳戶，但您無法建立或編輯這些其他工具。  圖形化 runbook 產生 PowerShell 程式碼，但您無法直接檢視或修改 hello 程式碼。 圖形化 runbook 不能轉換的 hello tooone[文字格式](automation-runbook-types.md)，也不可以是轉換的 toographical 格式文字 runbook。 圖形化 runbook 可以轉換的 tooGraphical PowerShell 工作流程 runbook 在匯入，反之亦然。

### <a name="advantages"></a>優點
* 虛擬插入連結設定撰寫模型  
* 專注於資料如何流經 hello 程序  
* 以視覺方式呈現管理程序  
* 子 runbook toocreate 高等級的工作流程中包含其他 runbook  
* 建議您採用模組化的程式設計  


### <a name="limitations"></a>限制
* 無法在 Azure 入口網站之外編輯 Runbook。
* 可能需要包含 PowerShell 程式碼 tooperform 複雜邏輯的程式碼活動。
* 無法檢視或直接編輯 hello PowerShell 程式碼所建立的 hello 圖形化工作流程。 請注意，您可以檢視您在任何程式碼活動中建立的 hello 程式碼。

## <a name="powershell-runbooks"></a>PowerShell Runbook
PowerShell Runbook 以 Windows PowerShell 為基礎。  您直接編輯 hello 的 hello runbook 使用 hello Azure 入口網站中的 hello 文字編輯器的程式碼。  您也可以使用任何離線的文字編輯器和[匯入 hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx)至 Azure 自動化。

### <a name="advantages"></a>優點
* 實作所有的複雜邏輯與 hello 額外複雜的 PowerShell 工作流程沒有 PowerShell 程式碼。 
* Runbook 便會啟動 PowerShell 工作流程 runbook 速度，因為它不需要再執行編譯 toobe。

### <a name="limitations"></a>限制
* 必須熟悉 PowerShell 指令碼處理。
* 無法使用[平行處理](automation-powershell-workflow.md#parallel-processing)tooperform 多個平行的動作。
* 無法使用[檢查點](automation-powershell-workflow.md#checkpoints)tooresume runbook，如果發生錯誤。
* PowerShell 工作流程 runbook 和圖形化 runbook 只能包含以子 runbook 使用 hello Start-azureautomationrunbook cmdlet，此 cmdlet 會建立新的工作。

### <a name="known-issues"></a>已知問題
以下是 PowerShell Runbook 目前已知的問題。

* PowerShell Runbook 無法擷取具有 Null 值的未加密 [變數資產](automation-variables.md) 。
* 無法擷取 PowerShell runbook[變數資產](automation-variables.md)與 *~*  hello 名稱中。
* PowerShell Runbook 中落入迴圈的 Get-Process 大約在 80 次反覆運算之後就會損毀。 
* 如果它一次嘗試 toowrite 資料 toohello 輸出資料流的數量極大，PowerShell runbook 可能會失敗。   您通常可以解決這個問題，藉由輸出只會 hello 使用大型物件時所需的資訊。  例如，而不是輸出類似*Get-process*，您可以將輸出只具有所需的 hello 欄位*Get-process |選取 ProcessName，CPU*。

## <a name="powershell-workflow-runbooks"></a>PowerShell 工作流程 Runbook
PowerShell Workflow Runbook 是以 [Windows PowerShell 工作流程](automation-powershell-workflow.md)為基礎的文字 Runbook。  您直接編輯 hello 的 hello runbook 使用 hello Azure 入口網站中的 hello 文字編輯器的程式碼。  您也可以使用任何離線的文字編輯器和[匯入 hello runbook](http://msdn.microsoft.com/library/azure/dn643637.aspx)至 Azure 自動化。

### <a name="advantages"></a>優點
* 使用 PowerShell 工作流程程式碼實作所有複雜的邏輯。
* 使用[檢查點](automation-powershell-workflow.md#checkpoints)tooresume runbook，如果發生錯誤。
* 使用[平行處理](automation-powershell-workflow.md#parallel-processing)tooperform 多個平行的動作。
* 可以包含其他圖形化 runbook 和 PowerShell 工作流程 runbook 做為子 runbook toocreate 高等級的工作流程。

### <a name="limitations"></a>限制
* 作者必須熟悉 PowerShell 工作流程。
* Runbook 必須這類處理 hello 的 PowerShell 工作流程的其他複雜度[還原序列化物件](automation-powershell-workflow.md#code-changes)。
* Runbook 採取長 toostart 比 PowerShell runbook，因為它需要 toobe 才執行編譯。
* PowerShell runbook 只能包含以子 runbook 使用 hello Start-azureautomationrunbook cmdlet，此 cmdlet 會建立新的工作。

## <a name="considerations"></a>考量
您應該考慮到帳戶 hello 時判斷特定 runbook 的型別 toouse 下列其他考量。

* 您無法將 runbook 轉換從圖形化 tootextual 型別，反之亦然。
* 使用不同類型的 Runbook 作為子 Runbook 時有所限制。  如需詳細資訊，請參閱 [Azure 自動化中的子 Runbook](automation-child-runbooks.md) 。

## <a name="next-steps"></a>後續步驟
* toolearn 進一步了解撰寫圖形化 runbook，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)
* toounderstand hello PowerShell 和 PowerShell 之間的差異工作流程中的 runbook，請參閱[學習 Windows PowerShell 工作流程](automation-powershell-workflow.md)
* 如需有關如何 toocreate 或匯入 Runbook，請參閱[建立或匯入 Runbook](automation-creating-importing-runbook.md)

