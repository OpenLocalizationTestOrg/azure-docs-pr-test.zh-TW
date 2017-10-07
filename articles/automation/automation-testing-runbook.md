---
title: "Azure 自動化中 runbook aaaTesting |Microsoft 文件"
description: "在 Azure 自動化中發佈 runbook 之前，您可以如預期般運作的 tooensure 對它進行測試。  本文說明如何 tootest runbook 並檢視其輸出。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 7f7db785-52c0-4613-aa12-b02fd32a5182
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/12/2016
ms.author: magoedte;bwren
ms.openlocfilehash: 8c531f702699d586f8215d4c171cb0ecf94732b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="testing-a-runbook-in-azure-automation"></a>在 Azure 自動化中測試 Runbook
當您測試 runbook 時，hello[草稿版本](automation-creating-importing-runbook.md#publishing-a-runbook)執行並且完成之後，它會執行任何動作。 沒有工作歷程記錄會建立，但 hello[輸出](automation-runbook-output-and-messages.md#output-stream)和[警告和錯誤](automation-runbook-output-and-messages.md#message-streams)資料流會顯示在 hello 測試輸出窗格。 訊息 toohello [Verbose Stream](automation-runbook-output-and-messages.md#message-streams)才會顯示在輸出窗格 hello hello [$VerbosePreference 變數](automation-runbook-output-and-messages.md#preference-variables)tooContinue 設定。

即使執行 hello 草稿版本時，hello runbook 仍然會正常執行 hello 工作流程，並針對執行任何動作資源 hello 環境中。 因此，您只能在非生產資源中測試 Runbook。

hello 程序 tootest 每個[的 runbook 類型](automation-runbook-types.md)hello 相同，而且會在測試 hello 文字編輯器與 hello hello Azure 入口網站中的圖形化編輯器之間沒有差異。  

## <a name="tootest-a-runbook-in-hello-azure-portal"></a>tootest hello Azure 入口網站中 runbook
您可以使用任何[runbook 類型](automation-runbook-types.md)hello Azure 入口網站中。

1. 在任一 hello hello runbook 開啟 hello 草稿版本[文字編輯器](automation-edit-textual-runbook.md)或[圖形化編輯器](automation-graphical-authoring-intro.md)。
2. 按一下 hello**測試**按鈕 tooopen hello 測試刀鋒視窗。
3. 如果 hello runbook 有參數，則會列出中，您可以在其中提供用於 hello 測試值 toobe hello 左窗格中。
4. 如果您想 toorun hello 測試上[Hybrid Runbook Worker](automation-hybrid-runbook-worker.md)，然後變更**回合設定**太**Hybrid Worker**和選取 hello hello 目標群組名稱。  否則，請保留預設 hello **Azure** toorun hello 測試 hello 雲端中的。
5. 按一下 hello**啟動**按鈕 toostart hello 測試。
6. 如果 hello runbook [PowerShell 工作流程](automation-runbook-types.md#powershell-workflow-runbooks)或[圖形](automation-runbook-types.md#graphical-runbooks)，則您可以停止或暫停它時測試 hello 輸出窗格 下的 hello 按鈕。 當您暫停 hello runbook 時，它先完成 hello 目前活動再暫停。 Hello runbook 暫停後，您可以將它停止或重新啟動它。
7. 檢查 hello hello [輸出] 窗格中的 hello runbook 的輸出。

## <a name="next-steps"></a>後續步驟
* 如何 toocreate 或匯入 runbook，請參閱的 toolearn[建立或匯入在 Azure 自動化 runbook](automation-creating-importing-runbook.md)
* toolearn 詳細資料圖形化撰寫，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md)
* tooget 開始使用 PowerShell 工作流程 runbook，請參閱[我的第一個 PowerShell 工作流程 runbook](automation-first-runbook-textual.md)
* toolearn 進一步了解設定 runboks tooreturn 狀態訊息和錯誤，包括建議的做法，請參閱[Runbook 輸出和在 Azure 自動化中的訊息](automation-runbook-output-and-messages.md)

