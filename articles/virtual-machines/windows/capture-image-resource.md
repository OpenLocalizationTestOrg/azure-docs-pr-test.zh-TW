---
title: "在 Azure 中對 managed 影像 aaaCreate |Microsoft 文件"
description: "在 Azure 中建立一般化 VM 或 VHD 的受控映像。 映像可以是使用的 toocreate 使用受管理的磁碟的多個 Vm。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: cynthn
ms.openlocfilehash: d8cd6c2ce8c5d704de2c845abced85139944d682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-image-of-a-generalized-vm-in-azure"></a>在 Azure 中建立一般化 VM 的受控映像

您可以從在儲存體帳戶中儲存為受控磁碟或非受控磁碟的一般化 VM，建立受控映像資源。 hello 映像可以，則是使用的 toocreate 多個 Vm。 


## <a name="generalize-hello-windows-vm-using-sysprep"></a>一般化 hello Windows VM 使用 Sysprep

Sysprep 會移除所有您個人的帳戶資訊，以及其他項目，並準備作為映像的 hello 機器 toobe。 如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。

請確定 hello hello 機器上執行的伺服器角色支援 sysprep。 如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> 如果您第一次上傳您的 VHD tooAzure hello 之前執行 Sysprep，請確定您有[備妥您的 VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)執行 Sysprep 之前。 
> 
> 

1. 登入 toohello Windows 虛擬機器。
2. 系統管理員身分開啟 hello 命令提示字元視窗。 變更 hello 目錄太**%windir%\system32\sysprep**，然後執行`sysprep.exe`。
3. 在 hello**系統準備工具**對話方塊中，選取**進入系統的全新體驗 (OOBE)**，並確定該 hello**一般化**選取核取方塊。
4. 在 [關機選項] 中選取 [關機]。
5. 按一下 [確定] 。
   
    ![啟動 Sysprep](./media/upload-generalized-managed/sysprepgeneral.png)
6. Sysprep 完成時，它會關閉 hello 虛擬機器。 無法重新啟動 hello VM。


## <a name="create-a-managed-image-in-hello-portal"></a>Hello 入口網站中建立的受管理的映像 

1. 開啟 hello[入口網站](https://portal.azure.com)。
2. 按一下 hello 加號 toocreate 新的資源。
3. 在 hello 篩選搜尋中，輸入**映像**。
4. 選取**映像**hello 結果中。
5. 在 hello**映像**刀鋒視窗中，按一下 **建立**。
6. 在**名稱**，輸入 hello 映像的名稱。
7. 如果您有多個訂閱，選取 hello 之一從 hello**訂用帳戶**下拉式清單。
7. 在**資源群組**選取**建立新**和輸入的名稱，或選取**從現有**從 hello 下拉式清單中選取資源群組 toouse。
8. 在**位置**，選擇您的資源群組的 hello 位置。
9. 在**OS 類型**選取的作業系統，Windows 或 Linux 的 hello 類型。
11. 在**儲存體 blob**，按一下 **瀏覽**toolook 您 Azure 儲存體中的 hello VHD。
12. 在 [帳戶類型] 中選擇 Standard_LRS 或 Premium_LRS。 標準使用硬碟機，而進階使用固態磁碟機。 兩者都使用本機備援的儲存體。
13. 在**磁碟快取**選取 hello 適當的磁碟快取選項。 hello 選項**無**，**唯讀**和**可讀取 \ 寫入**。
14. 選用： 您也可以加入現有的資料磁碟 toohello 映像即可**+ 新增資料磁碟**。  
15. 完成選取之後，請按一下 [建立]。
16. 建立 hello 映像之後，您會看到它做為**映像**hello hello 資源群組中選擇清單中的資源。



## <a name="create-a-managed-image-of-a-vm-using-powershell"></a>使用 Powershell 建立 VM 的受控映像

建立映像，直接從 hello VM 可確保該 hello 映像包括所有的 hello 與 hello VM，包括 hello OS 磁碟和任何資料磁碟相關聯的磁碟。


在開始之前，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。 執行 hello 下列命令 tooinstall 它。

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。


1. 建立一些變數。

    ```powershell
    $vmName = "myVM"
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $imageName = "myImage"
    ```
2. 請確定已解除配置 VM 的 hello。

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. 設定得 hello hello 虛擬機器狀態**一般**。 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized
    ```
    
4. 取得 hello 虛擬機器。 

    ```powershell
    $vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $rgName
    ```

5. 建立 hello 映像設定。

    ```powershell
    $image = New-AzureRmImageConfig -Location $location -SourceVirtualMachineId $vm.ID 
    ```
6. 建立 hello 映像。

    ```powershell
    New-AzureRmImage -Image $image -ImageName $imageName -ResourceGroupName $rgName
    ``` 



## <a name="create-a-managed-image-of-a-vhd-in-powershell"></a>在 PowerShell 中建立 VHD 的受控映像

使用一般化 OS VHD 建立受控映像。


1.  首先，設定 hello 一般參數：

    ```powershell
    $rgName = "myResourceGroupName"
    $vmName = "myVM"
    $location = "West Central US" 
    $imageName = "yourImageName"
    $osVhdUri = "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd"
    ```
2. Step\deallocate hello VM。

    ```powershell
    Stop-AzureRmVM -ResourceGroupName $rgName -Name $vmName -Force
    ```
    
3. 將標示為一般化 VM hello。

    ```powershell
    Set-AzureRmVm -ResourceGroupName $rgName -Name $vmName -Generalized 
    ```
4.  建立 hello 使用一般化的 OS VHD 的映像。

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $osVhdUri
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```


## <a name="create-a-managed-image-from-a-snapshot-using-powershell"></a>使用 Powershell 從快照集建立受控映像

您也可以從 hello VHD 從一般化 VM 的快照集建立的受管理的映像。

    
1. 建立一些變數。 

    ```powershell
    $rgName = "myResourceGroup"
    $location = "EastUS"
    $snapshotName = "mySnapshot"
    $imageName = "myImage"
    ```

2. 收到 hello 快照集。

   ```powershell
   $snapshot = Get-AzureRmSnapshot -ResourceGroupName $rgName -SnapshotName $snapshotName
   ```
   
3. 建立 hello 映像設定。

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsState Generalized -OsType Windows -SnapshotId $snapshot.Id
    ```
4. 建立 hello 映像。

    ```powershell
    New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ``` 
    

## <a name="next-steps"></a>後續步驟
- 現在您可以[從 hello 一般化受管理的映像建立 VM](create-vm-generalized-managed.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。    

