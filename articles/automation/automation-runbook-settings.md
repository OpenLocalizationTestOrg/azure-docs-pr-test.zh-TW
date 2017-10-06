---
title: "aaaRunbook 設定 |Microsoft 文件"
description: "描述 Azure 自動化中 runbook 的 hello 組態設定以及如何 toochange 它們兩者都使用 hello Azure 管理入口網站和 Windows PowerShell。"
services: automation
documentationcenter: 
author: mgoedtel
manager: stevenka
editor: tysonn
ms.assetid: a726f20c-a952-48b8-88ee-36d76aa3ac61
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/11/2016
ms.author: bwren
ms.openlocfilehash: 6f0ef09c148355a351464424c22c33df9300f0dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="runbook-settings"></a>Runbook 設定
在 Azure 自動化中的每個 runbook 都有多項設定可協助它 toobe 識別和 toochange 其登入行為。 這些設定下面會描述如何在程序之後 toomodify 它們。

## <a name="settings"></a>設定
### <a name="name-and-description"></a>名稱和描述
一旦建立後，您無法變更 hello runbook 名稱。 hello 描述是選擇性的而且可以是 too512 字元組成。

### <a name="tags"></a>標記
Tag 可讓您 tooassign 不同的字和片語 toohelp 識別 runbook。 例如，當您提交 runbook toohello [PowerShell 資源庫](https://www.powershellgallery.com/)，您可以指定特定的標籤 tooidentify 所屬的類別目錄 hello runbook 應該會列在。 您可以為 Runbook 指定多個標記，使用逗號分隔。

### <a name="logging"></a>記錄
根據預設，詳細資訊和進度記錄不會寫入 toojob 歷程記錄。 您可以變更特定 runbook toolog hello 設定這些記錄。 如需有關這些記錄的詳細資訊，請參閱 [Runbook 輸出和訊息](automation-runbook-output-and-messages.md)。

## <a name="changing-runbook-settings"></a>變更 Runbook 設定

### <a name="changing-runbook-settings-with-hello-azure-portal"></a>使用 hello Azure 入口網站變更 runbook 設定
您可以變更 hello Azure 入口網站中 runbook 的設定從 hello**設定**hello runbook 刀鋒視窗。

1. 在 hello Azure 入口網站，選取 **自動化**，然後按一下 hello 自動化帳戶名稱。
2. 選取 hello **Runbook**  索引標籤。
3. 按一下 runbook 的 hello 名稱，而且您有向的 toohello hello runbook 的設定 刀鋒視窗。 從這裡，您可以指定或修改標記、 hello runbook 描述、 設定記錄和追蹤設定，並存取支援工具 toohelp 解決問題。     

### <a name="changing-runbook-settings-with-windows-powershell"></a>使用 Windows PowerShell 變更 Runbook 設定
您可以使用 hello[組 AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603786.aspx) cmdlet toochange hello runbook 的設定。 如果您想 toospecify 多個標記，您可以提供陣列或單一字串以逗號分隔值 toohello Tags 參數。 您可以取得 hello 目前標記以 hello [Get AzureRmAutomationRunbook](https://msdn.microsoft.com/library/mt603728.aspx)。

hello，下列命令範例顯示如何 tooset hello runbook 內容。 這個範例會將三個標記 toohello 現有的標記，並指定應記錄詳細記錄。

    $automationAccountName = "MyAutomationAccount"
    $runbookName = "Sample-TestRunbook"
    $tags = (Get-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName).Tags
    $tags += "Tag1,Tag2,Tag3"
    Set-AzureRmAutomationRunbook -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName $automationAccountName –Name $runbookName –LogVerbose $true –Tags $tags

## <a name="next-steps"></a>後續步驟
* 如何 toocreate 並擷取輸出和錯誤訊息從 runbook，請參閱的 toolearn [Runbook 輸出和訊息](automation-runbook-output-and-messages.md) 
* 如何查看 tooadd 已經由開發 hello community 或其他來源或 toocreate 您自己的 runbook 的 runbook toounderstand[建立或匯入 Runbook](automation-creating-importing-runbook.md) 

