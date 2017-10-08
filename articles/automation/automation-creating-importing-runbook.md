---
title: "aaaCreating 或匯入在 Azure 自動化 runbook"
description: "本文說明如何 toocreate Azure 自動化中的檔案從一個匯入新的 runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 24414362-b690-4474-8ca7-df18e30fc31d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/07/2017
ms.author: magoedte;bwren
ms.openlocfilehash: d45f44cf15fbcacdd0de2977668502c2e1671063
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-or-importing-a-runbook-in-azure-automation"></a>在 Azure 自動化中建立或匯入 Runbook
您可以加入由 runbook tooAzure 自動化[建立一個新](#creating-a-new-runbook)或匯入現有的 runbook，從檔案或從 hello [Runbook 庫](automation-runbook-gallery.md)。 本文提供從檔案建立和匯入 Runbook 的資訊。  您可以取得所有上存取社群的 runbook 和模組中的 hello 詳細[Azure 自動化 Runbook 和模組組件庫](automation-runbook-gallery.md)。

## <a name="creating-a-new-runbook"></a>建立新的 Runbook
您可以建立新的 runbook 在 Azure 自動化中使用其中一種 hello Azure 入口網站或 Windows PowerShell。 一旦建立 hello runbook 之後，您可以使用編輯中的資訊[學習 PowerShell 工作流程](automation-powershell-workflow.md)和[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)。

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-classic-portal"></a>toocreate hello Azure 傳統入口網站使用新的 Azure 自動化 runbook
您只能搭配[PowerShell 工作流程 runbook](automation-runbook-types.md#powershell-workflow-runbooks) hello Azure 入口網站中。

1. Hello Azure 傳統入口網站中按一下，**新增**，**應用程式服務**，**自動化**， **Runbook**，**快速建立**.
2. 輸入所需的 hello 的詳細資訊，然後再按一下**建立**。 hello runbook 名稱必須以字母開頭，而且可以有字母、 數字、 底線和連字號。
3. 如果您現在想 tooedit hello runbook，然後按一下**編輯 Runbook**。 否則，請按一下 [確定] 。
4. 新的 runbook 會出現在 hello **Runbook**  索引標籤。

### <a name="toocreate-a-new-azure-automation-runbook-with-hello-azure-portal"></a>toocreate hello Azure 入口網站使用新的 Azure 自動化 runbook
1. 在 hello Azure 入口網站，開啟您的自動化帳戶。
2. 從 hello 中樞，選取**Runbook** tooopen hello 的 runbook 的清單。
3. 按一下 hello**新增 runbook**  按鈕，然後**建立新的 runbook**。
4. 輸入**名稱**hello runbook 並選取其[類型](automation-runbook-types.md)。 hello runbook 名稱必須以字母開頭，而且可以有字母、 數字、 底線和連字號。
5. 按一下**建立**toocreate hello runbook 和開啟 hello 編輯器。

### <a name="toocreate-a-new-azure-automation-runbook-with-windows-powershell"></a>toocreate 使用 Windows PowerShell 新的 Azure 自動化 runbook
您可以使用 hello[新增 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt619376.aspx) cmdlet toocreate 空[PowerShell 工作流程 runbook](automation-runbook-types.md#powershell-workflow-runbooks)。 您可以指定 hello**名稱**參數 toocreate 空的 runbook，您可以稍後編輯，或者您可以指定 hello**路徑**參數 tooimport runbook 檔案。 hello**類型**參數也應該包含的 toospecify hello 四個 runbook 類型之一。

hello 下列範例命令顯示如何 toocreate 新的空白 rubbook。

    New-AzureRmAutomationRunbook -AutomationAccountName MyAccount `
    -Name NewRunbook -ResourceGroupName MyResourceGroup -Type PowerShell

## <a name="importing-a-runbook-from-a-file-into-azure-automation"></a>將 Runbook 從檔案匯入 Azure 自動化
您可以在 Azure 自動化中建立新的 Runbook，方法是匯入 PowerShell 指令碼或 PowerShell 工作流程 (.ps1 延伸模組)，或匯入已匯出的圖形化 Runbook (.graphrunbook)。  您必須指定 hello[的 runbook 類型](automation-runbook-types.md)，會建立下列帳戶 hello 下列考量因素納入 hello 匯入。

* .graphrunbook 檔案只能匯入至新的 [圖形化 Runbook](automation-runbook-types.md#graphical-runbooks)，圖形化 Runbook 只能從 .graphrunbook 檔案建立。
* 包含 PowerShell 工作流程的 .ps1 檔案只能匯入至 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)。  如果 hello 檔案包含多個 PowerShell 工作流程，hello 匯入將會失敗。 您必須儲存每個工作流程 tooits 自己的檔案，並分別匯入每個。
* 未包含工作流程的 .ps1 檔案可以匯入至 [PowerShell Runbook](automation-runbook-types.md#powershell-runbooks) 或 [PowerShell 工作流程 Runbook](automation-runbook-types.md#powershell-workflow-runbooks)。  如果匯入到 PowerShell 工作流程 runbook，然後它會轉換的 tooa 工作流程，並註解將會包含在 hello runbook 指定 hello 所做的變更。

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-classic-portal"></a>tooimport hello Azure 傳統入口網站的檔案從 runbook
您可以使用下列程序 tooimport 指令碼檔案到 Azure 自動化的 hello。  請注意，您只能使用此入口網站將 .ps1 檔案匯入 PowerShell 工作流程 Runbook。  您必須使用其他類型 hello Azure 入口網站。

1. 在 hello Azure 管理入口網站中，選取 **自動化**，然後選取 自動化帳戶。
2. 按一下 [匯入] 。
3. 按一下**瀏覽檔案**並找出 hello 指令碼檔案 tooimport。
4. 如果您現在想 tooedit hello runbook，然後按一下**編輯 Runbook**。 否則，請按一下 [確定]。
5. hello 新 runbook 會出現在 hello **Runbook** hello 自動化帳戶 索引標籤。
6. 您必須[發行 hello runbook](#publishing-a-runbook)才能執行它。

### <a name="tooimport-a-runbook-from-a-file-with-hello-azure-portal"></a>tooimport hello Azure 入口網站的檔案從 runbook
您可以使用下列程序 tooimport 指令碼檔案到 Azure 自動化的 hello。  

> [!NOTE]
> 請注意，您可以只匯入.ps1 檔案至 PowerShell 工作流程 runbook 使用 hello 入口網站。
> 
> 

1. 在 hello Azure 入口網站，開啟您的自動化帳戶。
2. 從 hello 中樞，選取**Runbook** tooopen hello 的 runbook 的清單。
3. 按一下 hello**新增 runbook**  按鈕，然後**匯入**。
4. 按一下**Runbook 檔案**tooselect hello 檔案 tooimport
5. 如果 hello**名稱**欄位才會啟用，則您擁有 hello 選項 toochange 它。  hello runbook 名稱必須以字母開頭，而且可以有字母、 數字、 底線和連字號。
6. hello [runbook 類型](automation-runbook-types.md)會自動選取，但您可以變更 hello 類型後 hello 適用限制納入考量。 
7. hello 新的 runbook 會出現在 hello hello 自動化帳戶的 runbook 清單。
8. 您必須[發行 hello runbook](#publishing-a-runbook)才能執行它。

> [!NOTE]
> 您匯入圖形化 runbook 或圖形化的 PowerShell 工作流程 runbook 之後，您必須 hello 選項 tooconvert toohello 其他型別如果想。 您無法轉換 tootextual。
> 
> 

### <a name="tooimport-a-runbook-from-a-script-file-with-windows-powershell"></a>tooimport runbook 從使用 Windows PowerShell 指令碼檔案
您可以使用 hello[匯入 AzureRMAutomationRunbook](https://msdn.microsoft.com/library/mt603735.aspx) cmdlet tooimport 為草稿 PowerShell 工作流程 runbook 的指令碼檔案。 如果已經存在 hello runbook，hello 匯入將會失敗，除非您使用 hello *-Force*參數。 

hello，下列命令範例顯示如何 tooimport 指令碼檔案至 runbook。

    $automationAccountName =  "AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $scriptPath = "C:\Runbooks\Sample_TestRunbook.ps1"
    $RGName = "ResourceGroup"

    Import-AzureRMAutomationRunbook -Name $runbookName -Path $scriptPath `
    -ResourceGroupName $RGName -AutomationAccountName $automationAccountName `
    -Type PowerShellWorkflow 


## <a name="publishing-a-runbook"></a>發佈 Runbook
當您建立或匯入新的 Runbook 時，您必須發佈才能執行它。  自動化中的每個 Runbook 都有草稿和已發行的版本。 只有 hello 已發佈版本可用 toobe 執行，且 hello 草稿版本可供編輯。 hello 已發佈 」 版本不會受到任何變更 toohello 草稿版本。 當 hello 草稿版本應該成為可用時，您應發佈該 hello 草稿版本覆寫 hello 已發佈版本。

## <a name="toopublish-a-runbook-using-hello-azure-classic-portal"></a>toopublish 的 runbook 使用 hello Azure 傳統入口網站
1. Hello Azure 傳統入口網站中開啟 hello runbook。
2. 在 hello 囉 」 畫面頂端，按一下**作者**。
3. 在 hello 囉 」 畫面底部，按一下 **發行**然後**是**toohello 驗證訊息。

## <a name="toopublish-a-runbook-using-hello-azure-portal"></a>toopublish 的 runbook 使用 hello Azure 入口網站
1. 開啟 hello runbook 中的 hello Azure 入口網站。
2. 按一下 hello**編輯** 按鈕。
3. 按一下 hello**發行** 按鈕，然後**是**toohello 驗證訊息。

## <a name="toopublish-a-runbook-using-windows-powershell"></a>使用 Windows PowerShell runbook toopublish
您可以使用 hello[發行 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603705.aspx) cmdlet toopublish 使用 Windows PowerShell runbook。 hello 下列範例命令顯示如何 toopublish 範例 runbook。

    $automationAccountName =  AutomationAccount"
    $runbookName = "Sample_TestRunbook"
    $RGName = "ResourceGroup"

    Publish-AzureRmAutomationRunbook -AutomationAccountName $automationAccountName `
    -Name $runbookName -ResourceGroupName $RGName


## <a name="next-steps"></a>後續步驟
* 請參閱有關如何享有 hello Runbook 和 PowerShell 模組資源庫，toolearn [Azure 自動化 Runbook 和模組組件庫](automation-runbook-gallery.md)
* 進一步了解使用文字編輯器，編輯 PowerShell 和 PowerShell 工作流程 runbook toolearn 看到[編輯 Azure 自動化中的文字 runbook](automation-edit-textual-runbook.md)
* toolearn 進一步了解撰寫圖形化 runbook，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)

