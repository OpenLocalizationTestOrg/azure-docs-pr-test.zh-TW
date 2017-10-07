---
title: "在 Azure 自動化中的 aaaVariable 資產 |Microsoft 文件"
description: "變數資產是屬於可用 tooall runbook 在 Azure 自動化 DSC 設定的值。  這篇文章說明 hello 詳細資料的變數以及與它們的 toowork 文字及圖形化撰寫。"
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: b880c15f-46f5-4881-8e98-e034cc5a66ec
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/09/2017
ms.author: magoedte;bwren
ms.openlocfilehash: f9daa49fc1dc883ffb218a9adf26e36df1d6bb27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="variable-assets-in-azure-automation"></a>Azure 自動化中的變數資產

變數資產是屬於可用 tooall runbook 以及自動化帳戶中的 DSC 設定的值。 他們可以建立、 修改，並將擷取從 hello Azure 入口網站中，Windows PowerShell，從 runbook 或 DSC 設定。 自動化變數適用於下列案例的 hello:

- 在多個 Runbook 或 DSC 設定之間共用值。

- Hello 從多個工作之間共用一個值相同的 runbook 或 DSC 設定。

- 從 hello 入口網站或從 hello 所使用的 runbook 或 DSC 設定，例如一組常用設定項目特定清單類似的 VM 名稱、 特定的資源群組、 AD 網域名稱、 等的 Windows PowerShell 命令列管理值。  

自動化變數會保存，以便繼續使用 toobe 即使 hello runbook 或 DSC 設定失敗。  這麼做也可以設定一個 runbook，然後由另一個，或由 hello 值 toobe 相同的 runbook 或 DSC 組態 hello 執行的下一次。

建立變數時，您可以指定將其加密儲存。  變數加密後，會安全地儲存在 Azure 自動化中，而且無法擷取其值，從 hello [Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)隨附於 hello Azure PowerShell 模組的 cmdlet。  hello，可以擷取加密的值的唯一方式是從 hello **Get-automationvariable**活動在 runbook 或 DSC 設定。

> [!NOTE]
> Azure 自動化中的安全資產包括認證、憑證、連接和加密的變數。 這些資產都會經過加密並儲存在 hello 使用產生的唯一索引鍵，每個自動化帳戶的 Azure 自動化中。 這個索引鍵是由主要憑證加密，並且儲存在 Azure 自動化中。 之前儲存安全資產，hello 自動化帳戶的 hello 金鑰會解密使用 hello 主要憑證，並接著使用 tooencrypt hello 資產。

## <a name="variable-types"></a>變數型別

當您建立變數以 hello Azure 入口網站時，您必須指定 hello 下拉式清單中的資料類型，所以 hello 入口網站可以顯示 hello 適當的控制項輸入 hello 變數值。 hello 變數不是受限制的 toothis 資料類型，不過您必須設定使用 Windows PowerShell，如果您想 toospecify hello 變數不同類型的值。 如果您指定**未定義**，hello hello 變數值會設定得則**$null**，而且您必須將以 hello hello 值[Set-azureautomationvariable](http://msdn.microsoft.com/library/dn913767.aspx) cmdlet 或**Set-automationvariable**活動。  您無法建立或變更複雜變數類型 hello 入口網站中的 hello 值，但是您可以提供使用 Windows PowerShell 的任何類型的值。 複雜型別會傳回為 [PSCustomObject](http://msdn.microsoft.com/library/system.management.automation.pscustomobject.aspx)。

您可以藉由建立陣列或雜湊表，並將它儲存 toohello 變數來儲存多個值 tooa 單一變數。

hello 下面是可用在自動化中的變數類型的清單：

* String
* Integer
* DateTime
* Boolean
* Null

## <a name="cmdlets-and-workflow-activities"></a>Cmdlet 和工作流程活動

hello 下表中的 hello cmdlet 會使用的 toocreate 和管理使用 Windows PowerShell 的自動化變數。 這些 cmdlet 隨附 hello [Azure PowerShell 模組](../powershell-install-configure.md)可用於自動化 runbook 和 DSC 設定。

|Cmdlet|說明|
|:---|:---|
|[Get-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)|擷取現有變數的 hello 值。|
|[New-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx)|建立新的變數並設定其值。|
|[Remove-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt619354.aspx)|移除現有的變數。|
|[Set-AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603601.aspx)|設定現有變數的 hello 值。|

在 hello 下表中的 hello 工作流程活動是使用的 tooaccess runbook 中的自動化變數。 它們只可用於 runbook 或 DSC 設定，而且不要 hello Azure PowerShell 模組的一部分。

|工作流程活動|說明|
|:---|:---|
|Get-AutomationVariable|擷取現有變數的 hello 值。|
|Set-AutomationVariable|設定現有變數的 hello 值。|

> [!NOTE] 
> 您應該避免使用中的變數 hello – Name 參數**Get-automationvariable**在 runbook 或 DSC 設定，因為這可以使得探索 runbook 或 DSC 設定和自動化之間的相依性在設計階段的變數。

## <a name="creating-a-new-automation-variable"></a>建立新自動化變數

### <a name="toocreate-a-new-variable-with-hello-azure-portal"></a>toocreate hello Azure 入口網站的新變數

1. 從您的自動化帳戶，按一下 hello**資產**磚，然後在 hello**資產**刀鋒視窗中，選取**變數**。
2. 在 hello**變數**磚中，選取**加入變數**。
3. 完成上 hello 的 hello 選項**新變數**刀鋒視窗，然後按一下**建立**儲存 hello 新變數。

### <a name="toocreate-a-new-variable-with-windows-powershell"></a>toocreate 使用 Windows PowerShell 的新變數

hello[新增 AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603613.aspx) cmdlet 會建立新的變數，並設定其初始值。 您可以擷取 hello 值使用[Get AzureRmAutomationVariable](https://msdn.microsoft.com/library/mt603849.aspx)。 如果 hello 值是簡單類型，則會傳回該相同的類型。 如果它是複雜型別，則會傳回 **PSCustomObject** 。

hello 下列範例命令顯示如何 toocreate 類型之變數的字串，然後傳回其值。

    New-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" 
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable' `
    –Encrypted $false –Value 'My String'
    $string = (Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name 'MyStringVariable').Value

hello 下列範例命令顯示如何 toocreate 複雜變數類型與然後傳回其屬性。 在此情況下，會使用來自 **Get-AzureRmVm** 的虛擬機器物件。

    $vm = Get-AzureRmVm -ResourceGroupName "ResourceGroup01" –Name "VM01"
    New-AzureRmAutomationVariable –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable" –Encrypted $false –Value $vm
    
    $vmValue = (Get-AzureRmAutomationVariable -ResourceGroupName "ResourceGroup01" `
    –AutomationAccountName "MyAutomationAccount" –Name "MyComplexVariable").Value
    $vmName = $vmValue.Name
    $vmIpAddress = $vmValue.IpAddress



## <a name="using-a-variable-in-a-runbook-or-dsc-configuration"></a>在 Runbook 或 DSC 設定中使用變數

使用 hello **Set-automationvariable**活動 tooset hello 自動化中的變數值的 runbook 或 DSC 設定和 hello **Get-automationvariable** tooretrieve 它。  您不應該使用 hello **Set-azureautomationvariable**或**Get-azureautomationvariable** runbook 或 DSC 設定，因為它們都不如 hello 工作流程活動中的 cmdlet。  您也無法擷取安全的變數與 hello 值**Get-azureautomationvariable**。  hello 只方式 toocreate 從 runbook 中的新變數，或在 DSC 設定為 toouse hello [New-azureautomationvariable](http://msdn.microsoft.com/library/dn913771.aspx) cmdlet。


### <a name="textual-runbook-samples"></a>文字式 Runbook 範例

#### <a name="setting-and-retrieving-a-simple-value-from-a-variable"></a>從變數設定和擷取簡單的值

hello 下列範例命令顯示如何 tooset 及擷取文字的 runbook 中的變數。 在此範例中，假設已經建立名稱為 *NumberOfIterations* 和 *NumberOfRunnings* 的整數類型變數，以及名稱為 *SampleMessage* 字串類型變數。

    $NumberOfIterations = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfIterations'
    $NumberOfRunnings = Get-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" -Name 'NumberOfRunnings'
    $SampleMessage = Get-AutomationVariable -Name 'SampleMessage'
    
    Write-Output "Runbook has been run $NumberOfRunnings times."
    
    for ($i = 1; $i -le $NumberOfIterations; $i++) {
       Write-Output "$i`: $SampleMessage"
    }
    Set-AzureRmAutomationVariable -ResourceGroupName "ResouceGroup01" –AutomationAccountName "MyAutomationAccount" –Name NumberOfRunnings –Value ($NumberOfRunnings += 1)

#### <a name="setting-and-retrieving-a-complex-object-in-a-variable"></a>設定和擷取變數中的複雜物件

hello 以下範例程式碼將示範如何 tooupdate 文字 runbook 中的複雜值的變數。 在此範例中，Azure 虛擬機器會擷取與**Get-azurevm**和儲存的 tooan 現有的自動化變數。  如 [變數型別](#variable-types)中所述，這會儲存為 PSCustomObject。

    $vm = Get-AzureVM -ServiceName "MyVM" -Name "MyVM"
    Set-AutomationVariable -Name "MyComplexVariable" -Value $vm


在下列程式碼的 hello，hello 值會擷取從 hello 變數和已使用 toostart hello 虛擬機器。

    $vmObject = Get-AutomationVariable -Name "MyComplexVariable"
    if ($vmObject.PowerState -eq 'Stopped') {
       Start-AzureVM -ServiceName $vmObject.ServiceName -Name $vmObject.Name
    }


#### <a name="setting-and-retrieving-a-collection-in-a-variable"></a>設定和擷取變數中的集合

hello 以下範例程式碼將示範如何 toouse 文字 runbook 中的複雜值集合的變數。 在此範例中，使用擷取多個 Azure 虛擬機器**Get-azurevm**和儲存的 tooan 現有的自動化變數。  如 [變數型別](#variable-types)中所述，這會儲存為 PSCustomObject 的集合。

    $vms = Get-AzureVM | Where -FilterScript {$_.Name -match "my"}     
    Set-AutomationVariable -Name 'MyComplexVariable' -Value $vms

在下列程式碼的 hello，hello 集合擷取自 hello 變數，且使用 toostart 每部虛擬機器。

    $vmValues = Get-AutomationVariable -Name "MyComplexVariable"
    ForEach ($vmValue in $vmValues)
    {
       if ($vmValue.PowerState -eq 'Stopped') {
          Start-AzureVM -ServiceName $vmValue.ServiceName -Name $vmValue.Name
       }
    }


### <a name="graphical-runbook-samples"></a>圖形化 Runbook 範例

在圖形化 runbook，您會新增 hello **Get-automationvariable**或**Set-automationvariable** hello hello 圖形編輯器的程式庫 窗格中的 hello 變數上按一下滑鼠右鍵，然後選取 hello您想要的活動。

![加入變數 toocanvas](media/automation-variables/runbook-variable-add-canvas.png)

#### <a name="setting-values-in-a-variable"></a>變數中的設定值
hello 下圖顯示範例活動 tooupdate 簡單的值的變數在圖形化 runbook。 在此範例中，單一 Azure 虛擬機器會擷取與**Get AzureRmVM**和 hello 電腦名稱會儲存 tooan 現有的自動化變數類型為字串。  無論是否 hello[連結是管線或順序](automation-graphical-authoring-intro.md#links-and-workflow)因為我們只預期有單一物件 hello 輸出中。

![設定簡單變數](media/automation-variables/runbook-set-simple-variable.png)

## <a name="next-steps"></a>後續步驟

* toolearn 進一步了解一起連接活動，在圖形化撰寫，請參閱[中圖形化撰寫連結](automation-graphical-authoring-intro.md#links-and-workflow)
* tooget 開始使用圖形化 runbook，請參閱[我的第一個圖形化 runbook](automation-first-runbook-graphical.md) 

