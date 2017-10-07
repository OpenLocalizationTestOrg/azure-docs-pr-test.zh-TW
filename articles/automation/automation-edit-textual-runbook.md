---
title: "Azure 自動化中的 aaaEditing 文字 runbook"
description: "本文提供不同的程序使用 PowerShell 和 PowerShell 工作流程在 Azure 自動化中 runbook 使用 hello 文字編輯器。"
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: 6f5b48fb-6f30-4e99-9e14-9061b5554b08
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 3fd87d457838f300ca6c94bc345e82c679a0e011
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="editing-textual-runbooks-in-azure-automation"></a>在 Azure 自動化中編輯文字式 Runbook
hello Azure 自動化中的文字編輯器可使用的 tooedit [PowerShell runbook](automation-runbook-types.md#powershell-runbooks)和[PowerShell 工作流程 runbook](automation-runbook-types.md#powershell-workflow-runbooks)。 這會有 hello 的 intellisense 和色彩編碼與額外的特殊功能 tooassist 您在存取資源的一般 toorunbooks 等其他程式碼編輯器的一般功能。  本文提供執行與此編輯器不同的功能的詳細步驟。

hello 文字編輯器包含至 runbook 的活動、 資產和子系 runbook 的功能 tooinsert 程式碼。 而不是輸入 hello 程式碼本身，您可以從可用資源的清單中選取，然後利用 hello 適當的程式碼插入 hello 的 runbook。

Azure 自動化中的每個 Runbook 有兩個版本，「草稿」和「已發佈」。 編輯 hello hello runbook 草稿版本，並執行它，按一下此處。 無法編輯 hello 已發佈版本。 如需詳細資訊，請參閱 [發佈 Runbook](automation-creating-importing-runbook.md#publishing-a-runbook) 。

與 toowork[圖形化 Runbook](automation-runbook-types.md#graphical-runbooks)，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)。

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit runbook 以 hello Azure 入口網站
使用下列程序 tooopen runbook 進行編輯 hello 文字編輯器中的 hello。

1. 在 hello Azure 入口網站，選取您的自動化帳戶。
2. 按一下 hello **Runbook**磚 tooopen hello runbook 的清單。
3. 按一下 hello 名稱 hello runbook 的方法，您可以想 tooedit，，然後按一下hello**編輯** 按鈕。
4. 執行所需編輯 hello。
5. 當您完成編輯時，按一下 [儲存]  。
6. 按一下**發行**如果您想發行的 hello runbook toobe 的 hello 最新草稿版本。

### <a name="tooinsert-a-cmdlet-into-a-runbook"></a>tooinsert cmdlet 至 runbook
1. Hello 游標 hello 畫布的 hello 文字編輯器，在您在要 tooplace hello 指令程式的位置。
2. 展開 hello **Cmdlet** hello 控制項程式庫中的節點。
3. 展開包含您想要 toouse hello cmdlet hello 模組。
4. 以滑鼠右鍵按一下 hello cmdlet tooinsert，然後選取**新增 toocanvas**。  如果 hello cmdlet 有一個以上的參數集，將會加入 hello 預設集。  您也可以展開 hello cmdlet tooselect 不同的參數設定。
5. hello hello 指令程式的程式碼會插入與它的參數的完整清單。
6. 提供適當的值取代以大括號 <> 的任何必要參數的 hello 資料型別。  移除您不需要的任何參數。

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>tooinsert 至 runbook 的子 runbook 的程式碼
1. Hello 畫布的 hello 文字編輯器，在 hello 游標位置所在的程式碼 tooplace hello hello[子系 runbook](automation-child-runbooks.md)。
2. 展開 hello **Runbook** hello 控制項程式庫中的節點。
3. 以滑鼠右鍵按一下 hello runbook tooinsert，然後選取**新增 toocanvas**。
4. hello hello 子 runbook 的程式碼會插入其中任何含有任何 runbook 參數的預留位置。
5. Hello 預留位置取代為適當的每個參數的值。

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert 資產至 runbook
1. Hello 資料指標在 hello 畫布的 hello 文字編輯器，在您要 tooplace hello 程式碼 hello 子 runbook 的位置。
2. 展開 hello**資產**hello 控制項程式庫中的節點。
3. 展開您想要的資產的 hello 類型 hello 節點。
4. 以滑鼠右鍵按一下 hello 資產 tooinsert，然後選取**新增 toocanvas**。  如[變數資產](automation-variables.md)，選取 **新增 「 取得變數 」 toocanvas**或**新增 「 設定變數 」 toocanvas**根據您想 tooget 還是設定 hello 變數。
5. hello hello 資產的程式碼會插入至 hello runbook。

## <a name="tooedit-a-runbook-with-hello-azure-portal"></a>tooedit runbook 以 hello Azure 入口網站
使用下列程序 tooopen runbook 進行編輯 hello 文字編輯器中的 hello。

1. 在 hello Azure 入口網站，選取 **自動化**，然後按一下 hello 自動化帳戶名稱。
2. 選取 hello **Runbook**  索引標籤。
3. 按一下 hello 名稱 hello runbook 的方法，您可以想 tooedit，，然後選取 [hello**作者**] 索引標籤。
4. 按一下 hello**編輯**在 hello 囉 」 畫面底部的按鈕。
5. 執行所需編輯 hello。
6. 當您完成編輯時，按一下 [儲存]  。
7. 按一下**發行**如果您想發行的 hello runbook toobe 的 hello 最新草稿版本。

### <a name="tooinsert-an-activity-into-a-runbook"></a>tooinsert 至 Runbook 活動
1. Hello 資料指標在 hello 畫布的 hello 文字編輯器，在您要 tooplace hello 活動的位置。
2. 在 hello 囉 」 畫面底部，按一下 **插入**然後**活動**。
3. 在 hello**整合模組**資料行中，選取 hello 模組包含 hello 活動。
4. 在 [hello**活動**] 窗格中，選取一個活動。
5. 在 hello**描述**資料行中，注意 hello hello 活動描述。 或者，您可以按一下 檢視詳細的說明 toolaunch hello hello 瀏覽器中的活動。
6. 按一下向右箭號 hello。  如果 hello 活動有參數，它們會列出供您的資訊。
7. 按一下 hello 核取記號按鈕。  程式碼 toorun hello 活動會將插入 hello runbook。
8. 如果 hello 活動需要參數，提供適當的值取代以大括號 <> hello 資料型別。

### <a name="tooinsert-code-for-a-child-runbook-into-a-runbook"></a>tooinsert 至 runbook 的子 runbook 的程式碼
1. Hello 畫布的 hello 文字編輯器，在游標的位置 hello 想 tooplace hello[子系 runbook](automation-child-runbooks.md)。
2. 在 hello 囉 」 畫面底部，按一下 **插入**然後**Runbook**。
3. 選取 hello runbook tooinsert 從 hello 中心資料行，然後按一下向右箭號 hello。
4. 如果 hello runbook 有參數，它們會列出供您的資訊。
5. 按一下 hello 核取記號按鈕。  程式碼 toorun hello 選取 runbook 會將插入 hello 目前的 runbook。
6. 如果 hello runbook 需要參數，提供適當的值取代以大括號 <> hello 資料型別。

### <a name="tooinsert-an-asset-into-a-runbook"></a>tooinsert 資產至 runbook
1. Hello 游標 hello 畫布的 hello 文字編輯器，在您想 tooplace hello 活動 tooretrieve hello 資產所在的位置。
2. 在 hello 囉 」 畫面底部，按一下 **插入**然後**設定**。
3. 在 hello**設定動作**資料行中，選取 hello 您想要的動作。
4. 選取從 hello hello 中心資料行中的可用資產。
5. 按一下 hello 核取記號按鈕。  程式碼 tooget 或組 hello 資產會將插入 hello runbook。

## <a name="tooedit-an-azure-automation-runbook-using-windows-powershell"></a>tooedit 使用 Windows PowerShell 的 Azure 自動化 runbook
tooedit runbook 讓您使用 Windows PowerShell，使用您選擇的 hello 編輯器並儲存 tooa.ps1 檔案。 您可以使用 hello [Get-azureautomationrunbookdefinition](http://aka.ms/runbookauthor/cmdlet/getazurerunbookdefinition) hello runbook cmdlet tooretrieve hello 內容，然後[Set-azureautomationrunbookdefinition](http://aka.ms/runbookauthor/cmdlet/setazurerunbookdefinition) cmdlet tooreplace hello 現有草稿 runbook 以 hello 修改其中一個。

### <a name="tooretrieve-hello-contents-of-a-runbook-using-windows-powershell"></a>tooRetrieve hello Runbook Using Windows PowerShell 的內容
hello，下列命令範例顯示如何 tooretrieve hello runbook 指令碼，並將它儲存 tooa 指令碼檔案。 在此範例中，會擷取 hello 草稿版本。 它也是可能 tooretrieve hello 已發佈版本 hello runbook 但無法變更此版本。

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    $runbookDefinition = Get-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Slot Draft
    $runbookContent = $runbookDefinition.Content

    Out-File -InputObject $runbookContent -FilePath $scriptPath

### <a name="toochange-hello-contents-of-a-runbook-using-windows-powershell"></a>tooChange hello Runbook Using Windows PowerShell 的內容
hello 下列命令範例示範如何 tooreplace hello hello 的指令碼檔案的內容與現有的 runbook 內容。 請注意，這是 hello 相同範例中的程序[tooimport 從使用 Windows PowerShell 指令碼檔案 runbook](automation-creating-importing-runbook.md)。

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $scriptPath = "c:\runbooks\Sample-TestRunbook.ps1"

    Set-AzureAutomationRunbookDefinition -AutomationAccountName $automationAccountName -Name $runbookName -Path $scriptPath -Overwrite
    Publish-AzureAutomationRunbook –AutomationAccountName $automationAccountName –Name $runbookName

## <a name="related-articles"></a>相關文章
* [在 Azure 自動化中建立或匯入 Runbook](automation-creating-importing-runbook.md)
* [了解 PowerShell 工作流程](automation-powershell-workflow.md)
* [Azure 自動化中的圖形化編寫](automation-graphical-authoring-intro.md)
* [憑證](automation-certificates.md)
* [連線](automation-connections.md)
* [認證](automation-credentials.md)
* [排程](automation-schedules.md)
* [變數](automation-variables.md)
