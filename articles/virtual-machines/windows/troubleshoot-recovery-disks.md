---
title: "Windows 疑難排解 VM 使用 Azure PowerShell aaaUse |Microsoft 文件"
description: "了解如何 tootroubleshoot Windows VM 在 Azure 中藉由來發出連接 hello OS 磁碟 tooa 復原 VM 使用 Azure PowerShell"
services: virtual-machines-windows
documentationCenter: 
authors: genlin
manager: timlt
editor: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/26/2017
ms.author: genli
ms.openlocfilehash: 7a6a76f64824fe5d06dc4286cb1d87ab8bb794e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-windows-vm-by-attaching-hello-os-disk-tooa-recovery-vm-using-azure-powershell"></a>疑難排解 Windows VM，藉由附加 hello OS 磁碟 tooa 復原 VM 使用 Azure PowerShell
如果 Windows 虛擬機器 (VM) 在 Azure 中會發生開機或磁碟錯誤，您可能需要 tooperform 疑難排解 hello 虛擬硬碟上本身的步驟。 常見範例是防止 hello VM 可以 tooboot 成功失敗的應用程式更新。 此發行項詳細資料時，如何 toouse Azure PowerShell tooconnect 您的虛擬硬碟 tooanother Windows VM toofix 任何錯誤，然後重新建立原始 VM。


## <a name="recovery-process-overview"></a>復原程序概觀
hello 疑難排解程序如下所示：

1. 刪除 hello VM 遇到問題，保留 hello 虛擬硬碟。
2. 附加和掛接 hello Windows VM 的虛擬硬碟 tooanother 供疑難排解之用。
3. 連接 toohello 疑難排解 VM。 編輯檔案，或在 hello 原始虛擬硬碟上執行任何工具 toofix 問題。
4. 取消掛接並卸離 hello 虛擬硬碟從 hello 疑難排解 VM。
5. 使用建立 VM hello 原始虛擬硬碟。

請確定您有[hello 最新 Azure PowerShell](/powershell/azure/overview)安裝並登入 tooyour 訂用帳戶：

```powershell
Login-AzureRMAccount
```

在 hello 下列範例中，會取代您自己的值的參數名稱。 範例參數名稱包含 `myResourceGroup`、`mystorageaccount` 和 `myVM`。


## <a name="determine-boot-issues"></a>判斷開機問題
您可以在 Azure 中檢視您的 VM 的螢幕擷取畫面 toohelp 開機問題進行疑難排解。 這個螢幕擷取畫面可以協助您找出 VM 失敗 tooboot 的原因。 hello 下列範例會取得 hello 螢幕擷取畫面來自 hello 名為 Windows VM `myVM` hello 資源群組中名為`myResourceGroup`:

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup `
    -Name myVM -Windows -LocalPath C:\Users\ops\
```

檢閱 hello 螢幕擷取畫面 toodetermine hello VM 失敗 tooboot 的原因。 請注意任何特定的錯誤訊息或提供的錯誤代碼。


## <a name="view-existing-virtual-hard-disk-details"></a>檢視現有的虛擬硬碟詳細資料
您可以將附加您的虛擬硬碟 tooanother VM 之前，您會需要 tooidentify hello hello 虛擬硬碟 (VHD) 名稱。

hello 下列範例會取得名為 VM hello 資訊`myVM`hello 資源群組中名為`myResourceGroup`:

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

尋找`Vhd URI`內 hello `StorageProfile` hello 輸出中的 hello 上述命令 > 一節。 hello 下列截斷的範例輸出顯示 hello`Vhd URI`朝向 hello hello 程式碼區塊的結尾：

```powershell
RequestId                     : 8a134642-2f01-4e08-bb12-d89b5b81a0a0
StatusCode                    : OK
ResourceGroupName             : myResourceGroup
Id                            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM
Name                          : myVM
Type                          : Microsoft.Compute/virtualMachines
...
StorageProfile                :
  ImageReference              :
    Publisher                 : MicrosoftWindowsServer
    Offer                     : WindowsServer
    Sku                       : 2016-Datacenter
    Version                   : latest
  OsDisk                      :
    OsType                    : Windows
    Name                      : myVM
    Vhd                       :
      Uri                     : https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd
    Caching                   : ReadWrite
    CreateOption              : FromImage
```


## <a name="delete-existing-vm"></a>刪除現有的 VM
虛擬硬碟和 VM 在 Azure 中是兩個不同的資源。 虛擬硬碟是存放 hello 作業系統本身、 應用程式和組態的位置。 hello VM 本身是定義 hello 大小或位置，並參考資源，例如虛擬硬碟或虛擬網路介面卡 (NIC) 的只是中繼資料。 每個虛擬硬碟已連接時，指派租用 tooa VM。 雖然可以附加和卸離 hello VM 正在執行時，即使資料磁碟，除非刪除 hello VM 資源無法中斷 hello 作業系統磁碟。 hello 租用會繼續 tooassociate hello OS 磁碟 vm，即使該 VM 是處於已停止和取消配置狀態。

hello 第一個步驟 toorecover VM 是 toodelete hello VM 資源本身。 刪除 hello VM 離開您的儲存體帳戶中的 hello 虛擬硬碟。 刪除 VM hello 之後, 您附加 hello 虛擬硬碟 tooanother VM tootroubleshoot，並解決 hello 錯誤。

下列範例刪除 hello hello 名為 VM`myVM`從名為 hello 資源群組`myResourceGroup`:

```powershell
Remove-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
```

請等到完成刪除附加 hello 虛擬硬碟 tooanother VM 之前 hello VM。 hello 租用 hello 虛擬硬碟關聯 hello VM 需要 toobe 附加 hello 虛擬硬碟 tooanother VM 之前釋出。


## <a name="attach-existing-virtual-hard-disk-tooanother-vm"></a>附加現有的虛擬硬碟 tooanother VM
如 hello 接下來的幾個步驟，您可以使用另一個 VM 供疑難排解之用。 附加 hello 疑難排解 VM toobrowse 現有虛擬硬碟 toothis 並編輯 hello 磁碟的內容。 此程序可讓您 toocorrect 任何組態錯誤或檢閱其他應用程式或系統記錄檔，例如。 選擇或建立另一個 VM toouse 供疑難排解之用。

當您附加 hello 現有虛擬硬碟時，指定在 hello 上述中取得的 hello URL toohello 磁碟`Get-AzureRmVM`命令。 hello 下列範例會附加疑難排解名為 VM 的現有虛擬硬碟 toohello `myVMRecovery` hello 資源群組中名為`myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
Add-AzureRmVMDataDisk -VM $myVM -CreateOption "Attach" -Name "DataDisk" -DiskSizeInGB $null `
    -VhdUri "https://mystorageaccount.blob.core.windows.net/vhds/myVM.vhd"
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

> [!NOTE]
> 新增磁碟需要 toospecify hello hello 磁碟大小。 因為我們連接現有的磁碟，hello`-DiskSizeInGB`指定為`$null`。 此值可確保正確連接 hello 資料磁碟，而且沒有 hello 需要 toodetermine hello 資料磁碟大小，則為 true。


## <a name="mount-hello-attached-data-disk"></a>掛接 hello 連接的資料磁碟

1. RDP tooyour 疑難排解 VM 使用 hello 適當的認證。 hello 下列範例會下載 hello hello 名為 VM 的 RDP 連線檔案`myVMRecovery`hello 資源群組中名為`myResourceGroup`，並將它下載太`C:\Users\ops\Documents`"

    ```powershell
    Get-AzureRMRemoteDesktopFile -ResourceGroupName "myResourceGroup" -Name "myVMRecovery" `
        -LocalPath "C:\Users\ops\Documents\myVMRecovery.rdp"
    ```

2. 自動偵測並附加 hello 資料磁碟。 檢視連接的磁碟區 toodetermine hello 的磁碟機代號 hello 清單如下所示：

    ```powershell
    Get-Disk
    ```

    下列範例輸出的 hello 可讓您顯示 hello 虛擬硬碟連接磁碟**2**。 (您也可以使用`Get-Volume`tooview hello 磁碟機代號):

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Online       127 GB MBR
    ```

## <a name="fix-issues-on-original-virtual-hard-disk"></a>修正原始虛擬硬碟的問題
與 hello 現有虛擬硬碟掛接，您現在可以執行任何維護和疑難排解步驟，視需要。 一旦解決 hello 問題之後，繼續進行步驟 hello。


## <a name="unmount-and-detach-original-virtual-hard-disk"></a>卸載並中斷連結原始虛擬硬碟
一旦解決的錯誤，您會卸載，並中斷您疑難排解的 VM 中的 hello 現有虛擬硬碟。 您無法使用虛擬硬碟與任何其他 VM，直到釋放附加 hello 疑難排解 VM 的虛擬硬碟 toohello hello 租用。

1. 從您的 RDP 工作階段內卸載 hello 資料磁碟上您將復原 VM。 您需要從 hello hello 磁碟編號先前`Get-Disk`cmdlet。 然後，使用`Set-Disk`tooset hello 磁碟為離線狀態：

    ```powershell
    Set-Disk -Number 2 -IsOffline $True
    ```

    確認 hello 磁碟現在已設定為離線使用`Get-Disk`一次。 hello 下列範例輸出顯示 hello 磁碟現在已設定為離線：

    ```powershell
    Number   Friendly Name   Serial Number   HealthStatus   OperationalStatus   Total Size   Partition
                                                                                             Style
    ------   -------------   -------------   ------------   -----------------   ----------   ----------
    0        Virtual HD                                     Healthy             Online       127 GB MBR
    1        Virtual HD                                     Healthy             Online       50 GB MBR
    2        Msft Virtu...                                  Healthy             Offline      127 GB MBR
    ```

2. 結束您的 RDP 工作階段。 從您的 Azure PowerShell 工作階段移除 hello 疑難排解 VM 中的 hello 虛擬硬碟。

    ```powershell
    $myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMRecovery"
    Remove-AzureRmVMDataDisk -VM $myVM -Name "DataDisk"
    Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
    ```


## <a name="create-vm-from-original-hard-disk"></a>從原始硬碟建立 VM
toocreate 原始虛擬硬碟，從 VM 使用[此 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd-existing-vnet)。 hello 實際的 JSON 範本位於 hello 下列連結：

- https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json

hello 範本會將 VM 部署到現有的虛擬網路，使用從 hello hello VHD URL 稍早的命令。 hello 下列範例會將部署 hello 範本 toohello 資源群組名稱`myResourceGroup`:

```powershell
New-AzureRmResourceGroupDeployment -Name myDeployment -ResourceGroupName myResourceGroup `
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vm-specialized-vhd-existing-vnet/azuredeploy.json
```

回應 hello 提示 hello 範本，例如 VM 名稱、 OS 類型與 VM 大小。 hello `osDiskVhdUri` hello 如先前附加時會使用 hello 疑難排解 VM 現有虛擬硬碟 toohello 相同。


## <a name="re-enable-boot-diagnostics"></a>重新啟用開機診斷

當您從 hello 現有虛擬硬碟建立 VM 時，開機診斷可能不會自動啟用。 hello 下列範例會啟用 hello hello 名為 VM 上的診斷延伸模組`myVMDeployed`hello 資源群組中名為`myResourceGroup`:

```powershell
$myVM = Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVMDeployed"
Set-AzureRmVMBootDiagnostics -ResourceGroupName myResourceGroup -VM $myVM -enable
Update-AzureRmVM -ResourceGroup "myResourceGroup" -VM $myVM
```

## <a name="next-steps"></a>後續步驟
如果您有連接 tooyour VM 的問題，請參閱[疑難排解 RDP 連線 tooan Azure VM](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 如果存取 VM 上執行的應用程式時發生問題，請參閱[針對 Windows VM 上的應用程式連線問題進行疑難排解](troubleshoot-app-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

如需使用 Resource Manager 的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。
