---
title: "aaaStarting 並停止虛擬機器-圖形 |Microsoft 文件"
description: "Azure 自動化案例，包括 runbook toostart 和停止傳統的虛擬機器的 PowerShell 工作流程版本。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 62d93170-ca3d-42ef-ac1d-6d50b61ac87d
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 5add8d8cf35ea2e89a570744755ac7db0a6feb07
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Azure 自動化案例 - 啟動和停止虛擬機器
此 Azure 自動化案例中包括 runbook toostart 和停止傳統虛擬機器。  您可以使用此案例中的 hello 下列任何一項：  

* 使用您自己的環境中的 hello runbook，而不需修改。
* 修改 hello runbook tooperform 自訂功能。  
* 從做為整體解決方案的一部分的另一個 runbook 呼叫 hello runbook。
* 使用 hello runbook 撰寫概念的教學課程 toolearn runbook。

> [!div class="op_single_selector"]
> * [圖形化](automation-solution-startstopvm-graphical.md)
> * [PowerShell 工作流程](automation-solution-startstopvm-psworkflow.md)
>
>

這是此案例的 hello 圖形化 runbook 版本。 也可以使用 [PowerShell 工作流程 Runbook](automation-solution-startstopvm-psworkflow.md)取得。

## <a name="getting-hello-scenario"></a>取得 hello 案例
此案例包含兩個您可以從下載的兩個圖形化 runbook hello 下列連結。  請參閱 hello [PowerShell 工作流程版本](automation-solution-startstopvm-psworkflow.md)此案例的連結 toohello PowerShell 工作流程 runbook。

| Runbook | 連結 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[啟動 Azure 傳統 VM 圖形化 Runbook](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |圖形化 |啟動 Azure 訂用帳戶中的所有傳統虛擬機器，或具有特定服務名稱的所有虛擬機器。 |
| StopAzureClassicVM |[停止 Azure 傳統 VM 圖形化 Runbook](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |圖形化 |停止自動化帳戶中的所有虛擬機器，或具有特定服務名稱的所有虛擬機器。 |

## <a name="installing-and-configuring-hello-scenario"></a>安裝和設定 hello 案例
### <a name="1-install-hello-runbooks"></a>1.安裝 hello runbook
下載之後 hello runbook，您可以匯入使用中的 hello 程序[圖形化 runbook 程序](automation-graphical-authoring-intro.md#graphical-runbook-procedures)。

### <a name="2-review-hello-description-and-requirements"></a>2.檢閱 hello 描述和需求
hello runbook 包含的活動**讀我**描述以及必要的資產。  您可以檢視這項資訊藉由選取 hello**讀我**活動，然後 hello**工作流程指令碼**參數。  您也可以取得 hello 在此文件的相同資訊。

### <a name="3-configure-assets"></a>3.設定資產
hello runbook 需要 hello 下列的資產，您必須建立並填入適當的值。  hello 名稱是預設值。  您可以使用資產有不同的名稱，如果您指定這些名稱在 hello[輸入參數](#using-the-runbooks)hello runbook 啟動時。

| 資產類型 | 預設名稱 | 說明 |
|:--- |:--- |:--- |:--- |
| [認證](automation-credentials.md) |AzureCredential |包含在 hello Azure 訂用帳戶中具有授權 toostart 並停止虛擬機器帳戶的認證。 |
| [Variable](automation-variables.md) |AzureSubscriptionId |包含您的 Azure 訂閱 hello 訂用帳戶 ID。 |

## <a name="using-hello-scenario"></a>使用 hello 案例
### <a name="parameters"></a>參數
hello 每個 runbook 有 hello 下列[輸入參數](automation-starting-a-runbook.md#runbook-parameters)。  您必須提供任何必要參數的值，另外可根據您的需求，選擇性地提供其他參數的值。

| 參數 | 類型 | 強制 | 說明 |
|:--- |:--- |:--- |:--- |
| ServiceName |string |否 |如果提供一個值，則會啟動或停止具有該服務名稱的所有虛擬機器。  如果未不提供任何值，然後 hello Azure 訂用帳戶中的所有傳統虛擬機器啟動或停止。 |
| AzureSubscriptionIdAssetName |string |否 |包含 hello hello 名稱[變數資產](#installing-and-configuring-the-scenario)，其中包含您的 Azure 訂閱 hello 訂用帳戶 ID。  如果不指定任何值，則會使用 *AzureSubscriptionId* 。 |
| AzureCredentialAssetName |string |否 |包含 hello hello 名稱[認證資產](#installing-and-configuring-the-scenario)包含 hello runbook toouse hello 認證。  如果不指定任何值，則會使用 *AzureCredential* 。 |

### <a name="starting-hello-runbooks"></a>啟動 hello runbook
您可以使用任何一種方法在 hello [Azure 自動化中啟動 runbook](automation-starting-a-runbook.md) toostart 是本文章中的 hello runbook。

hello 下列範例命令會使用 Windows PowerShell toorun **StartAzureClassicVM** toostart hello 服務名稱的所有虛擬機器*MyVMService*。

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>輸出
hello runbook 將[輸出訊息](automation-runbook-output-and-messages.md)指出每個虛擬機器是否 hello 開始或已成功提交停止指令。  您可以尋找每個 runbook hello 輸出 toodetermine hello 結果中的特定字串。  hello 下表列出 hello 可能的輸出字串。

| Runbook | 條件 | 訊息 |
|:--- |:--- |:--- |
| StartAzureClassicVM |虛擬機器已在執行中 |MyVM 已在執行中 |
| StartAzureClassicVM |成功提交虛擬機器的啟動要求 |MyVM 已啟動 |
| StartAzureClassicVM |虛擬機器的啟動要求失敗 |失敗的 MyVM toostart |
| StopAzureClassicVM |虛擬機器已在執行中 |MyVM 已停止 |
| StopAzureClassicVM |成功提交虛擬機器的啟動要求 |MyVM 已啟動 |
| StopAzureClassicVM |虛擬機器的啟動要求失敗 |失敗的 MyVM toostart |

以下是使用 hello 的映像**StartAzureClassicVM**為[子系 runbook](automation-child-runbooks.md)範例圖形化 runbook 中。  這會在下表中的 hello 使用 hello 條件式連結。

| 連結 | 準則 |
|:--- |:--- |
| 成功連結 |$ActivityOutput['StartAzureClassicVM'] -like "\* has been started" |
| 錯誤連結 |$ActivityOutput['StartAzureClassicVM'] -notlike "\* has been started" |

![子 Runbook 範例](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>詳細分解圖
以下是在此案例中的 hello runbook 的詳細的細目。  您可以使用這項資訊 tooeither 自訂 hello runbook 或只是 toolearn 從中來撰寫您自己的自動化案例。

### <a name="authentication"></a>驗證
![驗證](media/automation-solution-startstopvm/graphical-authentication.png)

hello runbook 活動 tooset hello 以開始[認證](automation-credentials.md)和 Azure 訂用帳戶將用於 hello runbook hello 其餘部分。

hello 前兩個活動，**取得訂用帳戶 Id**和**取得 Azure 認證**，擷取 hello[資產](#installing-the-runbook)hello 下面兩個活動所使用的。  這些活動可以直接指定 hello 資產，但他們需要 hello 資產名稱。  因為我們允許 hello 使用者 toospecify 這些名稱在 hello[輸入參數](#using-the-runbooks)，我們需要這些活動 tooretrieve hello 資產的輸入參數所指定的名稱。

**Add-azureaccount**集 hello hello runbook hello 其餘部分將使用的認證。  它會從擷取的 hello 認證資產**取得 Azure 認證**hello Azure 訂用帳戶中必須存取 toostart 並停止虛擬機器。  hello 訂用帳戶會選取**Select-azuresubscription**使用 hello 訂用帳戶 Id 從**取得訂用帳戶 Id**。

### <a name="get-virtual-machines"></a>取得虛擬機器
![取得 VM](media/automation-solution-startstopvm/graphical-getvms.png)

hello runbook 需要的虛擬機器就會使用的 toodetermine 和它們已經是否處於啟動或停止 （取決於 hello runbook)。   其中兩個活動會擷取 hello Vm。  **取得服務中的 Vm**會執行 hello *ServiceName* hello runbook 的輸入的參數包含的值。  **取得所有 Vm**會執行 hello *ServiceName* hello runbook 的輸入的參數不包含值。  此邏輯的執行方式 hello 上述每個活動的條件式連結。

這兩個活動使用 hello **Get-azurevm** cmdlet。  **取得所有 Vm**使用 hello **ListAllVMs**參數設定 tooreturn 所有虛擬機器。  **取得服務中的 Vm**使用 hello **GetVMByServiceAndVMName**參數設定，並提供 hello **ServiceName**輸入的參數的 hello **ServiceName**參數。  

### <a name="merge-vms"></a>合併 VM
![合併 VM](media/automation-solution-startstopvm/graphical-mergevms.png)

hello**合併 Vm**活動是輸入過長的必要的 tooprovide**Start-azurevm**哪些需要 hello 名稱和 hello vm toostart 的服務名稱。  該輸入可能來自**取得所有 VM** 或**取得服務中的 VM**，但 **Start-AzureVM** 只能指定一個活動作為輸入。   

hello 案例是 toocreate**合併 Vm**執行 hello **Write-output** cmdlet。  hello **InputObject**該 cmdlet 的參數是結合 hello 輸入 hello 前兩個活動的 PowerShell 運算式。  其中只有一個活動會執行，因此只會有一組輸出。  **Start-AzureVM** 可以使用該輸出作為輸入參數。

### <a name="startstop-virtual-machines"></a>啟動/停止虛擬機器
![啟動 VM](media/automation-solution-startstopvm/graphical-startvm.png) ![停止 VM](media/automation-solution-startstopvm/graphical-stopvm.png)

根據 hello runbook、 hello 下一個活動嘗試 toostart 或停止 hello runbook 使用**Start-azurevm**或**Stop-azurevm**。  Hello 活動已加上管線連結，因為它會執行一次所傳回的每個物件**合併 Vm**。  hello 連結是條件式以便 hello 活動才會執行 hello *RunningState* hello 的虛擬機器是*已停止*如**Start-azurevm**和*啟動*如**Stop-azurevm**。 如果這不符合條件，然後**通知已經啟動**或**通知已經停止**執行 toosend 訊息使用**Write-output**。

### <a name="send-output"></a>傳送輸出
![通知啟動 VM](media/automation-solution-startstopvm/graphical-notifystart.png) ![通知停止 VM](media/automation-solution-startstopvm/graphical-notifystop.png)

hello hello runbook 中的最後一個步驟是 toosend 輸出是否 hello 開始或已成功提交停止要求每個虛擬機器。 沒有個別**Write-output**針對每個，活動，我們判斷哪一個 toorun 使用條件式連結。  如果 *OperationStatus* 是 *Succeeded*，則會執行**通知 VM 已啟動**或**通知 VM 已停止**。  如果*OperationStatus*是任何其他值，則**通知失敗 tooStart**或**通知失敗 tooStop**執行。

## <a name="next-steps"></a>後續步驟
* [Azure 自動化中的圖形化編寫](automation-graphical-authoring-intro.md)
* [Azure 自動化中的子 Runbook](automation-child-runbooks.md)
* [Azure 自動化中的 Runbook 輸出與訊息](automation-runbook-output-and-messages.md)
