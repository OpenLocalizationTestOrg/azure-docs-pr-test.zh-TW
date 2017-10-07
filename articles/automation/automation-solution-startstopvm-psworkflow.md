---
title: "Azure 自動化的 PowerShell 工作流程的 aaaStarting 和停止虛擬機器 |Microsoft 文件"
description: "Azure 自動化案例，包括 runbook toostart 和停止傳統的虛擬機器的圖形化版本。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: d380bd43-d45d-45af-a5b2-78e7f66263c3
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/06/2016
ms.author: magoedte;bwren
redirect_url: https://docs.microsoft.com/azure/automation/automation-solution-vm-management
redirect_document_id: False
ms.openlocfilehash: 273631c7fc5ddb989b3bbdc82b470ac3af6ee482
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

這是 hello 這種情況的 PowerShell 工作流程 runbook 版本。 也可以使用 [圖形化 Runbook](automation-solution-startstopvm-graphical.md)取得。

## <a name="getting-hello-scenario"></a>取得 hello 案例
此案例包含兩個您可以從下列連結查看 hello 的 PowerShell 工作流程 runbook。  請參閱 hello[圖形化版本](automation-solution-startstopvm-graphical.md)此案例的連結 toohello 圖形化 runbook。

| Runbook | 連結 | 類型 | 說明 |
|:--- |:--- |:--- |:--- |
| Start-AzureVMs |[啟動 Azure 傳統 VM](https://gallery.technet.microsoft.com/Start-Azure-Classic-VMs-86ef746b) |PowerShell 工作流程 |啟動 Azure 訂用帳戶中的所有傳統虛擬機器，或具有特定服務名稱的所有虛擬機器。 |
| Stop-AzureVMs |[停止 Azure 傳統 VM](https://gallery.technet.microsoft.com/Stop-Azure-Classic-VMs-7a4ae43e) |PowerShell 工作流程 |停止自動化帳戶中的所有虛擬機器，或具有特定服務名稱的所有虛擬機器。 |

## <a name="installing-and-configuring-hello-scenario"></a>安裝和設定 hello 案例
### <a name="1-install-hello-runbooks"></a>1.安裝 hello runbook
下載之後 hello runbook，您可以匯入使用中的 hello 程序[匯入 Runbook](http://msdn.microsoft.com/library/dn643637.aspx#ImportRunbook)。

### <a name="2-review-hello-description-and-requirements"></a>2.檢閱 hello 描述和需求
hello runbook 包含加上註解的說明文字，其中包含描述以及必要的資產。  您也可以取得 hello 在此文件的相同資訊。

### <a name="3-configure-assets"></a>3.設定資產
hello runbook 需要 hello 下列的資產，您必須建立並填入適當的值。

| 資產類型 | 資產名稱 | 說明 |
|:--- |:--- |:--- |:--- |
| 認證 |AzureCredential |包含在 hello Azure 訂用帳戶中具有授權 toostart 並停止虛擬機器帳戶的認證。  或者，您可以指定其他認證資產中 hello**認證**hello 參數**Add-azureaccount**活動。 |
| 變數 |AzureSubscriptionId |包含您的 Azure 訂閱 hello 訂用帳戶 ID。 |

## <a name="using-hello-scenario"></a>使用 hello 案例
### <a name="parameters"></a>參數
hello runbook 每個有下列參數的 hello。  您必須提供任何必要參數的值，另外可根據您的需求，選擇性地提供其他參數的值。

| 參數 | 類型 | 強制 | 說明 |
|:--- |:--- |:--- |:--- |
| ServiceName |string |否 |如果提供一個值，則會啟動或停止具有該服務名稱的所有虛擬機器。  如果未不提供任何值，然後 hello Azure 訂用帳戶中的所有傳統虛擬機器啟動或停止。 |
| AzureSubscriptionIdAssetName |string |否 |包含 hello hello 名稱[變數資產](#installing-and-configuring-the-scenario)，其中包含您的 Azure 訂閱 hello 訂用帳戶 ID。  如果不指定任何值，則會使用 *AzureSubscriptionId* 。 |
| AzureCredentialAssetName |string |否 |包含 hello hello 名稱[認證資產](#installing-and-configuring-the-scenario)包含 hello runbook toouse hello 認證。  如果不指定任何值，則會使用 *AzureCredential* 。 |

### <a name="starting-hello-runbooks"></a>啟動 hello runbook
您可以使用任何一種方法在 hello [Azure 自動化中啟動 runbook](automation-starting-a-runbook.md) toostart 任一 hello runbook 在這個案例中。

hello 下列範例命令會使用 Windows PowerShell toorun **StartAzureVMs** toostart hello 服務名稱的所有虛擬機器*MyVMService*。

    $params = @{"ServiceName"="MyVMService"}
    Start-AzureAutomationRunbook –AutomationAccountName "MyAutomationAccount" –Name "Start-AzureVMs" –Parameters $params

### <a name="output"></a>輸出
hello runbook 將[輸出訊息](automation-runbook-output-and-messages.md)指出每個虛擬機器是否 hello 開始或已成功提交停止指令。  您可以尋找每個 runbook hello 輸出 toodetermine hello 結果中的特定字串。  hello 下表列出 hello 可能的輸出字串。

| Runbook | 條件 | 訊息 |
|:--- |:--- |:--- |
| Start-AzureVMs |虛擬機器已在執行中 |MyVM 已在執行中 |
| Start-AzureVMs |成功提交虛擬機器的啟動要求 |MyVM 已啟動 |
| Start-AzureVMs |虛擬機器的啟動要求失敗 |失敗的 MyVM toostart |
| Stop-AzureVMs |虛擬機器已停止 |MyVM 已停止 |
| Stop-AzureVMs |成功提交虛擬機器的停止要求 |MyVM 已停止 |
| Stop-AzureVMs |虛擬機器的停止要求失敗 |失敗的 MyVM toostop |

例如，runbook 中的下列程式碼片段的 hello 會嘗試 toostart hello 服務名稱的所有虛擬機器*MyServiceName*。  如果任何 hello 啟動要求失敗，則可以採取錯誤動作。

    $results = Start-AzureVMs -ServiceName "MyServiceName"
    foreach ($result in $results) {
        if ($result -like "* has been started" ) {
            # Action tootake in case of success.
        }
        else {
            # Action tootake in case of error.
        }
    }


## <a name="detailed-breakdown"></a>詳細分解圖
以下是在此案例中的 hello runbook 的詳細的細目。  您可以使用這項資訊 tooeither 自訂 hello runbook 或只是 toolearn 從中來撰寫您自己的自動化案例。

### <a name="parameters"></a>參數
    param (
        [Parameter(Mandatory=$false)]
        [String]  $AzureCredentialAssetName = 'AzureCredential',

        [Parameter(Mandatory=$false)]
        [String] $AzureSubscriptionIdAssetName = 'AzureSubscriptionId',

        [Parameter(Mandatory=$false)]
        [String] $ServiceName
    )

hello 啟動工作流程藉由取得 hello 值 hello[輸入參數](#using-the-scenario)。  如果沒有提供 hello 資產名稱則會使用預設名稱。

### <a name="output"></a>輸出
    # Returns strings with status messages
    [OutputType([String])]

這一行會宣告 hello runbook 的 hello 輸出會是一個字串。  這不是必要，但會作為使用 hello runbook 時的最佳作法[子系 runbook](automation-child-runbooks.md) ，以便在父 runbook 知道 hello 輸出輸入 tooexpect。

### <a name="authentication"></a>驗證
    # Connect tooAzure and select hello subscription toowork against
    $Cred = Get-AutomationPSCredential -Name $AzureCredentialAssetName
    $null = Add-AzureAccount -Credential $Cred -ErrorAction Stop
    $SubId = Get-AutomationVariable -Name $AzureSubscriptionIdAssetName
    $null = Select-AzureSubscription -SubscriptionId $SubId -ErrorAction Stop

接下來幾行 hello 設定 hello[認證](automation-credentials.md)和 Azure 訂用帳戶將用於 hello runbook hello 其餘部分。
第一次使用**Get-automationpscredential** tooget hello 資產 hello Azure 訂用帳戶保留 hello 認證以存取 toostart 並停止虛擬機器。 **Add-azureaccount**接著會使用此資產 tooset hello 認證。  hello 輸出會指派 tooa 虛設變數，使它不包含在 hello runbook 輸出。  

hello 與 hello 訂用帳戶 ID 擷取與變數的資產**Get-automationvariable**和 hello 訂用帳戶與設定**Select-azuresubscription**。

### <a name="get-vms"></a>取得 VM
    # If there is a specific cloud service, then get all VMs in hello service,
    # otherwise get all VMs in hello subscription.
    if ($ServiceName)
    {
        $VMs = Get-AzureVM -ServiceName $ServiceName
    }
    else
    {
        $VMs = Get-AzureVM
    }

**Get-azurevm**是使用的 tooretrieve hello hello runbook 將會使用的虛擬機器。  如果提供的值在 hello **ServiceName**輸入會擷取與該服務名稱的變數，則只 hello 虛擬機器。  如果 **ServiceName** 是空的，則會擷取所有虛擬機器。

### <a name="startstop-virtual-machines-and-send-output"></a>啟動/停止虛擬機器和傳送輸出
    # Start each of hello stopped VMs
    foreach ($VM in $VMs)
    {
        if ($VM.PowerState -eq "Started")
        {
            # hello VM is already started, so send notice
            Write-Output ($VM.InstanceName + " is already running")
        }
        else
        {
            # hello VM needs toobe started
            $StartRtn = Start-AzureVM -Name $VM.Name -ServiceName $VM.ServiceName -ErrorAction Continue

            if ($StartRtn.OperationStatus -ne 'Succeeded')
            {
                # hello VM failed toostart, so send notice
                Write-Output ($VM.InstanceName + " failed toostart")
            }
            else
            {
                # hello VM started, so send notice
                Write-Output ($VM.InstanceName + " has been started")
            }
        }
    }

接下來幾行 hello 逐步執行每個虛擬機器。  第一次 hello **PowerState** hello 的虛擬機器時，已檢查的 toosee 已經是執行中還是已停止，相依於 hello runbook。  如果已經在 hello 目標狀態，然後會傳送一則訊息，toooutput，且 hello runbook 結尾。  如果沒有，然後**Start-azurevm**或**Stop-azurevm** hello 要求預存的 tooa 變數 hello 結果的使用的 tooattempt toostart 或停止 hello 虛擬機器。  訊息會接著傳送 toooutput 指定是否已成功提交 hello 要求 toostart 或停止。

## <a name="next-steps"></a>後續步驟
* toolearn 進一步了解使用子 runbook，請參閱[Azure 自動化中的子 runbook](automation-child-runbooks.md)
* 深入了解 toolearn 輸出內執行 runbook 及記錄 toohelp 訊息進行疑難排解，請參閱[Runbook 輸出和在 Azure 自動化中的訊息](automation-runbook-output-and-messages.md)

