---
title: "aaaUpload 一般化 VHD toocreate 在 Azure 中的多個 Vm |Microsoft 文件"
description: "上傳一般化的 VHD tooan Azure 儲存體帳戶 toocreate Windows VM toouse 與 hello 資源管理員部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: cynthn
ms.openlocfilehash: aa1af2a0acf81685e62853de71afa51e819cb696
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-tooazure-toocreate-a-new-vm"></a>上傳一般化的 VHD tooAzure toocreate 新的 VM

本主題涵蓋上載一般化 unmanaged 的磁碟 tooa 儲存體帳戶，然後再建立新的 VM 使用上傳的 hello 磁碟。 一般化 VHD 映像已使用 Sysprep 移除您所有的個人帳戶資訊。 

如果您想 toocreate 將 VM 從儲存體帳戶中的特定 VHD，請參閱[從特定的 VHD 建立 VM](sa-create-vm-specialized.md)。

本主題將說明如何使用儲存體帳戶，但我們建議客戶改用移動 toousing 受管理的磁碟。 如需 tooprepare 上, 傳內容，以及建立新的 VM 使用的完整逐步解說會管理磁碟，請參閱 <<c0> [ 建立新的 VM 從一般化的 VHD 上傳 tooAzure 使用受管理磁碟](upload-generalized-managed.md)。



## <a name="prepare-hello-vm"></a>準備 VM hello

一般化 VHD - 已使用 Sysprep 移除您所有的個人帳戶資訊。 如果您想 toouse hello 做為映像 toocreate VHD 中的新 Vm，您應該：
  
  * [準備 Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md)。 
  * 一般化 hello 使用 Sysprep 的虛擬機器

### <a name="generalize-a-windows-virtual-machine-using-sysprep"></a>使用 Sysprep 將 Windows 虛擬機器一般化
這個區段會顯示如何 toogeneralize 用作映像的 Windows 虛擬機器。 Sysprep 會移除所有您個人的帳戶資訊，以及其他項目，並準備作為映像的 hello 機器 toobe。 如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。

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
6. Sysprep 完成時，它會關閉 hello 虛擬機器。 

> [!IMPORTANT]
> 不要重新啟動 hello VM，直到您完成上傳的 hello VHD tooAzure 或從 hello VM 建立映像。 如果 hello VM 不小心取得重新啟動，執行 Sysprep toogeneralize 再試一次。
> 
> 


## <a name="upload-hello-vhd"></a>上傳 VHD hello

上傳 hello VHD tooan Azure 儲存體帳戶。

### <a name="log-in-tooazure"></a>登入 tooAzure
如果您還沒有 PowerShell 1.4 版或更新版本安裝，讀取[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

1. 開啟 Azure PowerShell，然後登入 tooyour Azure 帳戶。 快顯視窗中開啟您 tooenter 以您的 Azure 帳戶的認證。
   
    ```powershell
    Login-AzureRmAccount
    ```
2. 取得可用的訂閱 hello 訂用帳戶 Id。
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. 設定使用 hello 訂用帳戶識別碼 hello 正確訂用帳戶 取代`<subscriptionID>`hello 識別碼 hello 包含正確的訂用帳戶。
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

### <a name="get-hello-storage-account"></a>取得 hello 儲存體帳戶
您需要 Azure toostore hello 上傳 VM 映像的儲存體帳戶。 您可以使用現有的儲存體帳戶或建立新帳戶。 

tooshow hello 可用儲存體帳戶，請輸入：

```powershell
Get-AzureRmStorageAccount
```

如果您想 toouse 現有的儲存體帳戶，請繼續 toohello [hello VM 映像上載](#upload-the-vm-vhd-to-your-storage-account)> 一節。

如果您需要 toocreate 儲存體帳戶，請遵循下列步驟：

1. 您需要 hello hello 儲存體帳戶建立所在的 hello 資源群組名稱。 toofind 出您的訂用帳戶中，而型別中的所有 hello 資源群組：
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    資源群組命名為的 toocreate **myResourceGroup**在 hello**美國西部**區域中，輸入：

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. 建立名為儲存體帳戶**mystorageaccount**使用 hello 此資源群組中[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
 
### <a name="start-hello-upload"></a>開始 hello 上傳 

使用 hello[新增 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello 影像 tooa 容器儲存體帳戶中的。 此範例中上傳 hello 檔案**myVHD.vhd**從`"C:\Users\Public\Documents\Virtual hard disks\"`tooa 儲存體帳戶**mystorageaccount**在 hello **myResourceGroup**資源群組。 hello 檔案會放入名為 「 hello 容器**mycontainer** hello 新的檔案名稱將會**myUploadedVHD.vhd**。

```powershell
$rgName = "myResourceGroup"
$urlOfUploadedImageVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $rgName -Destination $urlOfUploadedImageVhd `
    -LocalFilePath "C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd"
```


如果成功的話，您會收到的回應，看起來類似 toothis:

```powershell
MD5 hash is being calculated for hello file C:\Users\Public\Documents\Virtual hard disks\myVHD.vhd.
MD5 hash calculation is completed.
Elapsed time for hello operation: 00:03:35
Creating new page blob of size 53687091712...
Elapsed time for upload: 01:12:49

LocalFilePath           DestinationUri
-------------           --------------
C:\Users\Public\Doc...  https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd
```

根據您的網路連線和 hello VHD 檔案的大小，此命令可能需要一些時間 toocomplete。


## <a name="create-a-new-vm"></a>建立新的 VM 

您可以現在使用 hello 上傳 VHD toocreate 新的 VM。 

### <a name="set-hello-uri-of-hello-vhd"></a>設定 hello hello VHD URI

如 hello VHD toouse hello URI 的格式 hello: https://**mystorageaccount**.blob.core.windows.net/**mycontainer**/**MyVhdName**.vhd。 在此範例中的 hello VHD 名為**myVHD** hello 儲存體帳戶中是**mystorageaccount** hello 容器中**mycontainer**。

```powershell
$imageURI = "https://mystorageaccount.blob.core.windows.net/mycontainer/myVhd.vhd"
```


### <a name="create-a-virtual-network"></a>建立虛擬網路
建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。

1. 建立 hello 子網路。 hello 下列範例會建立名為的子網路**mySubnet** hello 資源群組中**myResourceGroup** hello 位址前置詞與**10.0.0.0/24**。  
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. 建立 hello 虛擬網路。 hello 下列範例會建立虛擬網路，名為**myVnet**在 hello**美國西部**hello 位址前置詞的位置**10.0.0.0/16**。  
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-network-interface"></a>建立公用 IP 位址和網路介面
tooenable 與 hello hello 虛擬網路中的虛擬機器的通訊，您需要[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)和網路介面。

1. 建立公用 IP 位址。 此範例會建立名為 **myPip** 的公用 IP 位址。 
   
    ```powershell
    $ipName = "myPip"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. 建立 hello nic。 此範例會建立名為 **myNic** 的 NIC。 
   
    ```powershell
    $nicName = "myNic"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName -Location $location `
        -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>建立網路安全性群組 hello 和 RDP 規則
toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 允許連接埠 3389 RDP 存取權的安全性規則。 

此範例會建立名為 **myNsg** 的 NSG，其包含的規則 **myRdpRule** 可允許透過連接埠 3389 的 RDP 流量。 如需 Nsg 的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


### <a name="create-a-variable-for-hello-virtual-network"></a>針對 hello 虛擬網路建立的變數
建立 hello 完成虛擬網路的變數。 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName
```

### <a name="create-hello-vm"></a>建立 hello VM
hello 下列 PowerShell 指令碼會示範如何 hello 虛擬機器設定和使用 hello tooset 上傳 VM 映像為 hello hello 新安裝的來源。



```powershell
# Enter a new user name and password toouse as hello local administrator account 
    # for remotely accessing hello VM.
    $cred = Get-Credential

    # Name of hello storage account where hello VHD is located. This example sets hello 
    # storage account name as "myStorageAccount"
    $storageAccName = "myStorageAccount"

    # Name of hello virtual machine. This example sets hello VM name as "myVM".
    $vmName = "myVM"

    # Size of hello virtual machine. This example creates "Standard_D2_v2" sized VM. 
    # See hello VM sizes documentation for more information: 
    # https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/
    $vmSize = "Standard_D2_v2"

    # Computer name for hello VM. This examples sets hello computer name as "myComputer".
    $computerName = "myComputer"

    # Name of hello disk that holds hello OS. This example sets hello 
    # OS disk name as "myOsDisk"
    $osDiskName = "myOsDisk"

    # Assign a SKU name. This example sets hello SKU name as "Standard_LRS"
    # Valid values for -SkuName are: Standard_LRS - locally redundant storage, Standard_ZRS - zone redundant
    # storage, Standard_GRS - geo redundant storage, Standard_RAGRS - read access geo redundant storage,
    # Premium_LRS - premium locally redundant storage. 
    $skuName = "Standard_LRS"

    # Get hello storage account where hello uploaded image is stored
    $storageAcc = Get-AzureRmStorageAccount -ResourceGroupName $rgName -AccountName $storageAccName

    # Set hello VM name and size
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize

    #Set hello Windows operating system configuration and add hello NIC
    $vm = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $computerName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id

    # Create hello OS disk URI
    $osDiskUri = '{0}vhds/{1}-{2}.vhd' `
        -f $storageAcc.PrimaryEndpoints.Blob.ToString(), $vmName.ToLower(), $osDiskName

    # Configure hello OS disk toobe created from hello existing VHD image (-CreateOption fromImage).
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri `
        -CreateOption fromImage -SourceImageUri $imageURI -Windows

    # Create hello new VM
    New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
```

## <a name="verify-that-hello-vm-was-created"></a>請確認 VM 已建立該 hello
完成時，您應該會看到新建立的 VM 中 hello hello [Azure 入口網站](https://portal.azure.com)下**瀏覽** > **虛擬機器**，或使用 hello 下列PowerShell 命令：

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>後續步驟
toomanage 新的虛擬機器使用 Azure PowerShell，請參閱[使用 Azure 資源管理員和 PowerShell 管理虛擬機器](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。


