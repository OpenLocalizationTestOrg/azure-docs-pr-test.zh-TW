---
title: "在 Azure 自動化的圖形化 runbook 中處理 aaaError |Microsoft 文件"
description: "本文說明如何 tooimplement 錯誤處理邏輯，在 Azure 自動化的圖形化 runbook。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 12/26/2016
ms.author: magoedte
ms.openlocfilehash: b9ff01361d2ebd9c0174b074a7a290b1cc2fd1c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="error-handling-in-azure-automation-graphical-runbooks"></a>Azure 自動化之圖形化 Runbook 中的錯誤處理

索引鍵的 runbook 設計主體 tooconsider 發現不同 runbook 可能會遇到的問題。 這些問題包括成功、預期的錯誤狀態，以及非預期的錯誤情況。

Runbook 應該包含錯誤處理。 toovalidate hello 活動的輸出，或處理的錯誤與圖形化 runbook，您可以使用 Windows PowerShell 程式碼活動、 hello 輸出連結的 hello 活動上定義的條件式邏輯或套用另一種方法。          

通常，如果沒有與 runbook 活動，就會發生非終止錯誤，遵循任何活動處理不論 hello 錯誤。 hello 錯誤可能 toogenerate 例外狀況，但 hello 下一個活動仍允許 toorun。 這是 PowerShell 是設計的 toohandle 錯誤 hello 方法。    

終止或非終止 hello PowerShell 發生的錯誤可以在執行期間的類型。 hello 終止和非終止錯誤之間的差異如下所示：

* **終止錯誤**： 完全中止 hello 命令 （或執行指令碼） 的執行期間發生嚴重錯誤。 範例包括不存在的 Cmdlet、防止 Cmdlet 執行的語法錯誤，或其他嚴重錯誤。

* **非終止錯誤**： 可讓執行 toocontinue 儘管 hello 失敗的非嚴重錯誤。 範例包括操作錯誤，例如找不到檔案錯誤和權限問題。

Azure 自動化的圖形化 runbook 已改善了 hello 功能 tooinclude 錯誤處理。 您現在可以將例外狀況變成非終止錯誤，並建立活動之間的錯誤連結。 此程序可讓 runbook 作者 toocatch 錯誤，並管理實現或非預期的條件。  

## <a name="when-toouse-error-handling"></a>當 toouse 錯誤處理

重要的活動會擲回錯誤或例外狀況時，它是重要 tooprevent hello 下一個活動處理和 toohandle hello 錯誤從 runbook 中的適當地。 當 Runbook 支援商務或服務營運流程時，這點格外重要。

每個活動可能會產生錯誤，hello runbook 作者可以加入錯誤連結指向 tooany 其他活動。  hello 目的地活動可以是任何類型，包括程式碼活動叫用 cmdlet 中叫用另一個 runbook，並以此類推。

此外，hello 目的地活動也可以連出連結。 這些連結可以是一般連結或錯誤連結。 這表示 hello runbook 作者可以實作複雜的錯誤處理邏輯，就可以做到 tooa 沒有程式碼活動。 hello 建議的作法是 toocreate 專用的錯誤處理 runbook 一般功能，但不是強制性。 不是 PowerShell 程式碼活動中的錯誤處理邏輯 hello 僅 選項。  

比方說，請思考嘗試 toostart runbook 的 VM，並在其上安裝應用程式。 如果 hello VM 並未正確啟動，它會執行兩個動作：

1. 傳送關於這個問題的通知。
2. 改為啟動另一個會自動佈建新 VM 的 Runbook。

其中一種解決方案是 toohave 指向 tooan 活動處理步驟一錯誤連結。 例如，您就可以連接 hello **Write-warning** cmdlet tooan 活動的第二個，步驟，例如 hello**開始 AzureRmAutomationRunbook** cmdlet。

您也無法將這兩種活動放在個別錯誤處理 runbook 和先前建議下列 hello 指引來一般化許多 runbook 中使用這個的行為。 然後再呼叫此錯誤處理 runbook，可以建構自訂訊息 hello 原始 runbook、 hello 資料，然後將它傳遞為參數 toohello 錯誤處理 runbook。

## <a name="how-toouse-error-handling"></a>如何 toouse 錯誤處理

每個活動均有組態設定可將例外狀況變成非終止錯誤。 此設定預設為停用狀態。 我們建議您啟用這項設定在您想要 toohandle 錯誤的任何活動。  

您會藉由啟用這項設定，以確保在 hello 活動的終止和非終止錯誤會當做非終止錯誤，處理，而且可以處理與錯誤連結。  

設定此設定之後, 您可以建立處理 hello 錯誤的活動。 活動就會產生任何錯誤，然後 hello 傳出錯誤連結會遵循，和 hello 標準連結則不會，即使 hello 活動都會產生以及規則的輸出。<br><br> ![自動化 Runbook 的錯誤連結範例](media/automation-runbook-graphical-error-handling/error-link-example.png)

在下列範例的 hello，runbook 會擷取包含 hello 的虛擬機器的電腦名稱的變數。 接著，它會嘗試 toostart hello 虛擬機器與 hello 下一個活動。<br><br> ![自動化 Runbook 的錯誤處理範例](media/automation-runbook-graphical-error-handling/runbook-example-error-handling.png)<br><br>      

hello **Get-automationvariable**活動和**開始 AzureRmVm**會設定的 tooconvert 例外狀況 tooerrors。  如果有問題 hello 變數或起始 hello VM，則會產生錯誤。<br><br> ![自動化 Runbook 的錯誤處理活動設定](media/automation-runbook-graphical-error-handling/activity-blade-convertexception-option.png)

錯誤連結會從單一這些活動 tooa 流向**錯誤管理**活動 （程式碼活動）。 此活動設定簡單的 PowerShell 運算式使用 hello*擲回*處理，以及與關鍵字 toostop *$Error.Exception.Message* tooget hello 訊息，描述 hello目前的例外狀況。<br><br> ![自動化 Runbook 的錯誤處理程式碼範例](media/automation-runbook-graphical-error-handling/runbook-example-error-handling-code.png)


## <a name="next-steps"></a>後續步驟

* toolearn 深入了解連結和連結類型，在圖形化 runbook，請參閱[Azure 自動化中的圖形化撰寫](automation-graphical-authoring-intro.md#links-and-workflow)。

* 深入了解 runbook 執行時，如何 toomonitor runbook 作業和其他技術的詳細資訊，請參閱 toolearn[追蹤 runbook 工作](automation-runbook-execution.md)。
