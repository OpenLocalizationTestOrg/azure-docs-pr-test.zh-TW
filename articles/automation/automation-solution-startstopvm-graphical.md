---
title: "啟動和停止虛擬機器 - Graph | Microsoft Docs"
description: "Azure 自動化案例的 PowerShell 工作流程版本，包含可啟動和停止傳統虛擬機器的 Runbook。"
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
redirect_document_id: FALSE
ms.openlocfilehash: 338d5712239356e13cbf480d9655ca3ca499701d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="azure-automation-scenario---starting-and-stopping-virtual-machines"></a>Azure 自動化案例 - 啟動和停止虛擬機器
此 Azure 自動化案例包含可啟動和停止傳統虛擬機器的 Runbook。  此案例可用來做為下列任何用途：  

* 在您自己的環境中不修改而直接使用 Runbook。
* 修改 Runbook 來執行自訂的功能。  
* 在整個解決方案中從另一個 Runbook 呼叫 Runbook。
* 將 Runbook 當作教學課程來了解 Runbook 撰寫概念。

> [!div class="op_single_selector"]
> * [圖形化](automation-solution-startstopvm-graphical.md)
> * [PowerShell 工作流程](automation-solution-startstopvm-psworkflow.md)
>
>

這是此案例的圖形化 Runbook 版本。 也可以使用 [PowerShell 工作流程 Runbook](automation-solution-startstopvm-psworkflow.md)取得。

## <a name="getting-the-scenario"></a>取得案例
此案例包含兩個可以從下列連結下載的圖形化 Runbook。  請參閱此案例的 [PowerShell 工作流程版本](automation-solution-startstopvm-psworkflow.md) ，以取得 PowerShell 工作流程 Runbook 的連結。

| Runbook | 連結 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| StartAzureClassicVM |[啟動 Azure 傳統 VM 圖形化 Runbook](https://gallery.technet.microsoft.com/scriptcenter/Start-Azure-Classic-VM-c6067b3d) |圖形化 |啟動 Azure 訂用帳戶中的所有傳統虛擬機器，或具有特定服務名稱的所有虛擬機器。 |
| StopAzureClassicVM |[停止 Azure 傳統 VM 圖形化 Runbook](https://gallery.technet.microsoft.com/scriptcenter/Stop-Azure-Classic-VM-397819bd) |圖形化 |停止自動化帳戶中的所有虛擬機器，或具有特定服務名稱的所有虛擬機器。 |

## <a name="installing-and-configuring-the-scenario"></a>安裝和設定案例
### <a name="1-install-the-runbooks"></a>1.安裝 Runbook
下載 Runbook 之後，您可以使用 [圖形化 Runbook 程序](automation-graphical-authoring-intro.md#graphical-runbook-procedures)中的程序匯入它們。

### <a name="2-review-the-description-and-requirements"></a>2.檢閱描述和需求
Runbook 包含一個稱為 **讀我檔案** 的活動，其中含有描述和所需的資產。  您可以選取 [讀我檔案] 活動，然後選取 [工作流程指令碼] 參數，即可檢視這項資訊。  您也可以從這份文件取得相同的資訊。

### <a name="3-configure-assets"></a>3.設定資產
Runbook 需要下列資產，您必須建立這些資產並填入適當的值。  名稱是預設值。  您可以用不同的名稱來使用這些資產，但必須於啟動 Runbook 時，先在 [輸入參數](#using-the-runbooks) 中指定這些名稱。

| 資產類型 | 預設名稱 | 說明 |
|:--- |:--- |:--- |:--- |
| [認證](automation-credentials.md) |AzureCredential |包含帳戶的認證，此帳戶有權啟動和停止 Azure 訂用帳戶中的虛擬機器。 |
| [變數](automation-variables.md) |AzureSubscriptionId |包含 Azure 訂用帳戶的訂用帳戶識別碼。 |

## <a name="using-the-scenario"></a>使用案例
### <a name="parameters"></a>參數
每個 Runbook 都有下列 [輸入參數](automation-starting-a-runbook.md#runbook-parameters)。  您必須提供任何必要參數的值，另外可根據您的需求，選擇性地提供其他參數的值。

| 參數 | 類型 | 強制 | 說明 |
|:--- |:--- |:--- |:--- |
| ServiceName |string |否 |如果提供一個值，則會啟動或停止具有該服務名稱的所有虛擬機器。  如果不提供任何值，則會啟動或停止 Azure 訂用帳戶中的所有傳統虛擬機器。 |
| AzureSubscriptionIdAssetName |string |否 |包含 [變數資產](#installing-and-configuring-the-scenario) 的名稱，此資產含有 Azure 訂用帳戶的訂用帳戶識別碼。  如果不指定任何值，則會使用 *AzureSubscriptionId* 。 |
| AzureCredentialAssetName |string |否 |包含 [認證資產](#installing-and-configuring-the-scenario) 的名稱，此資產含有要使用的 Runbook 認證。  如果不指定任何值，則會使用 *AzureCredential* 。 |

### <a name="starting-the-runbooks"></a>啟動 Runbook
您可以使用 [在 Azure 自動化中啟動 Runbook](automation-starting-a-runbook.md) 中的任何方法，啟動此文章中的任一個 Runbook。

下列範例命令使用 Windows PowerShell 執行 **StartAzureClassicVM** ，以啟動服務名稱為 *MyVMService*的所有虛擬機器。

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "StartAzureClassicVM" –Parameters $params

### <a name="output"></a>輸出
Runbook 將為每部虛擬機器 [輸出訊息](automation-runbook-output-and-messages.md) ，指出是否已成功提交啟動或停止指令。  您可以在輸出中尋找特定的字串，以判斷每一個 Runbook 的結果。  下表列出可能的輸出字串。

| Runbook | 條件 | 訊息 |
|:--- |:--- |:--- |
| StartAzureClassicVM |虛擬機器已在執行中 |MyVM 已在執行中 |
| StartAzureClassicVM |成功提交虛擬機器的啟動要求 |MyVM 已啟動 |
| StartAzureClassicVM |虛擬機器的啟動要求失敗 |MyVM 無法啟動 |
| StopAzureClassicVM |虛擬機器已在執行中 |MyVM 已停止 |
| StopAzureClassicVM |成功提交虛擬機器的啟動要求 |MyVM 已啟動 |
| StopAzureClassicVM |虛擬機器的啟動要求失敗 |MyVM 無法啟動 |

下圖顯示在範例圖形化 Runbook 中使用 **StartAzureClassicVM** 作為 [子 Runbook](automation-child-runbooks.md) 。  這使用下表中的條件式連結。

| 連結 | 準則 |
|:--- |:--- |
| 成功連結 |$ActivityOutput['StartAzureClassicVM'] -like "\* has been started" |
| 錯誤連結 |$ActivityOutput['StartAzureClassicVM'] -notlike "\* has been started" |

![子 Runbook 範例](media/automation-solution-startstopvm/graphical-childrunbook-example.png)

## <a name="detailed-breakdown"></a>詳細分解圖
以下是此案例中所有 Runbook 的詳細分解圖。  您可以使用這項資訊來自訂 Runbook，或只是從中學習撰寫您自己的自動化案例。

### <a name="authentication"></a>驗證
![驗證](media/automation-solution-startstopvm/graphical-authentication.png)

Runbook 一開始的活動會先設定將用於 Runbook 其餘部分的[認證](automation-credentials.md)和 Azure 訂用帳戶。

前兩個活動 (**取得訂用帳戶 ID** 和**取得 Azure 認證**) 會擷取後續兩個活動所使用的[資產](#installing-the-runbook)。  這些活動可以直接指定資產，但需要資產名稱。  因為我們允許使用者在 [輸入參數](#using-the-runbooks)中指定這些名稱，我們需要這些活動，以根據輸入參數所指定的名稱來擷取資產。

**Add-AzureAccount** 設定將用於 Runbook 其餘部分的認證。  它從 **取得 Azure 認證** 中擷取的認證資產，必須有權啟動和停止 Azure 訂用帳戶中的虛擬機器。  所使用的訂用帳戶是透過 **Select-AzureSubscription** 來選取，其會使用來自**取得訂用帳戶 ID** 的訂用帳戶 ID。

### <a name="get-virtual-machines"></a>取得虛擬機器
![取得 VM](media/automation-solution-startstopvm/graphical-getvms.png)

Runbook 必須決定將會使用的虛擬機器，以及這些虛擬機器是否已啟動或停止 (取決於 Runbook)。   這兩個活動中，其中一個會擷取 VM。  **ServiceName** 輸入參數中有值， *ServiceName* 將會執行。  **ServiceName** 輸入參數中有值， *ServiceName* 將會執行。  每個活動之前的條件式連結會執行此邏輯。

這兩個活動都使用 **Get-AzureVM** Cmdlet。  **取得所有 VM** 會使用 **ListAllVMs** 參數集來傳回所有虛擬機器。  **取得服務中的 VM** 會使用 **GetVMByServiceAndVMName** 參數集，並提供 **ServiceName** 輸入參數作為 **ServiceName** 參數。  

### <a name="merge-vms"></a>合併 VM
![合併 VM](media/automation-solution-startstopvm/graphical-mergevms.png)

**合併 VM** 活動需要提供輸入給 **Start-AzureVM**，後者需要取得要啟動的 VM 的名稱和服務名稱。  該輸入可能來自**取得所有 VM** 或**取得服務中的 VM**，但 **Start-AzureVM** 只能指定一個活動作為輸入。   

此案例是建立**合併 VM** 來執行 **Write-Output** Cmdlet。  該 Cmdlet 的 **InputObject** 參數是結合先前兩個活動的輸入所形成的 PowerShell 運算式。  其中只有一個活動會執行，因此只會有一組輸出。  **Start-AzureVM** 可以使用該輸出作為輸入參數。

### <a name="startstop-virtual-machines"></a>啟動/停止虛擬機器
![啟動 VM](media/automation-solution-startstopvm/graphical-startvm.png) ![停止 VM](media/automation-solution-startstopvm/graphical-stopvm.png)

根據 Runkbook 而定，接下來的活動會使用 **Start-AzureVM** 或 **Stop-AzureVM**，嘗試啟動或停止 Runbook。  由於活動的前面都有管線連結，所以會對 **合併 VM**傳回的每個物件執行一次。  連結依條件而定，只有當虛擬機器的 *RunningState* 在 **Start-AzureVM** 中是 *Stopped*，而在 **Stop-AzureVM** 中是*Started* 時，活動才會執行。 如果不符合此條件，則會執行**通知已啟動**或**通知已停止**，以使用 **Write-Output** 傳送訊息。

### <a name="send-output"></a>傳送輸出
![通知啟動 VM](media/automation-solution-startstopvm/graphical-notifystart.png) ![通知停止 VM](media/automation-solution-startstopvm/graphical-notifystop.png)

Runbook 的最後一個步驟是傳送輸出，而不論是否成功提交每個虛擬機器的啟動或停止要求。 由於各自有一個 **Write-Output** 活動，我們根據條件式連結決定執行何者。  如果 *OperationStatus* 是 *Succeeded*，則會執行**通知 VM 已啟動**或**通知 VM 已停止**。  如果 *OperationStatus* 是任何其他值，會執行**通知無法啟動**或**通知無法停止**。

## <a name="next-steps"></a>後續步驟
* [Azure 自動化中的圖形化編寫](automation-graphical-authoring-intro.md)
* [Azure 自動化中的子 Runbook](automation-child-runbooks.md)
* [Azure 自動化中的 Runbook 輸出與訊息](automation-runbook-output-and-messages.md)
