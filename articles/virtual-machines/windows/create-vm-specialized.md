---
title: "在 Azure 中的特定 VHD 從 Windows VM aaaCreate |Microsoft 文件"
description: "建立新的 Windows VM，藉由將特定的受管理的磁碟附加為 hello hello 資源管理員部署模型中使用的作業系統磁碟。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 3b7d3cd5-e3d7-4041-a2a7-0290447458ea
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: cynthn
ms.openlocfilehash: c72c6f4fb650e2664e87cf38ec9be62f0b2209fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-vm-from-a-specialized-disk"></a>從特製化磁碟建立 Windows VM

藉由將特定的受管理的磁碟附加為 hello OS 磁碟使用 Powershell 建立新的 VM。 專用的磁碟是從現有的 VM 會維護 hello 使用者帳戶、 應用程式及其他狀態資料從您的原始 VM 的虛擬硬碟 (VHD) 的複本。 

當您使用特殊的 VHD toocreate 新的 VM 時，新的 VM 會保留 hello 電腦名稱的 hello hello 原始 VM。 系統也會保留其他電腦特定資訊，在某些情況下，此重複資訊可能會造成問題。 複製 VM 時，請留意您的應用程式會依賴哪些類型的電腦特定資訊。

您有兩個選擇：
* [上傳 VHD](#option-1-upload-a-specialized-vhd)
* [複製現有的 Azure VM](#option-2-copy-an-existing-azure-vm)

本主題說明如何 toouse 管理的磁碟。 如果您的舊版部署需要使用儲存體帳戶，請參閱[從儲存體帳戶中的特殊化 VHD 建立 VM](sa-create-vm-specialized.md)

## <a name="before-you-begin"></a>開始之前
如果您使用 PowerShell，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。 

```powershell
Install-Module AzureRM.Compute -RequiredVersion 2.6.0
```
如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。


## <a name="option-1-upload-a-specialized-vhd"></a>選項 1：上傳特製化 VHD

您可以上傳的 hello 與內部部署虛擬化工具，像是從另一個雲端匯出 HYPER-V 或在 VM 建立從特製化的 VM 的 VHD。

### <a name="prepare-hello-vm"></a>準備 VM hello
如果您想 toouse hello VHD 當做-是 toocreate 新的 VM，請完成下列步驟的 hello。 
  
  * [準備 Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 **不這麼做**一般化 hello VM 使用 Sysprep。
  * 移除任何客體的虛擬化工具和 hello VM （例如 VMware 工具） 所安裝的代理程式。
  * 請確定 hello VM 是已設定的 toopull 其 IP 位址和 DNS 設定，透過 DHCP。 這可確保該 hello 伺服器會在啟動時，取得 hello VNet 內的 IP 位址。 


### <a name="get-hello-storage-account"></a>取得 hello 儲存體帳戶
您需要儲存體帳戶中 Azure toostore hello 上傳 VHD。 您可以使用現有的儲存體帳戶或建立新帳戶。 

tooshow hello 可用儲存體帳戶，請輸入：

```powershell
Get-AzureRmStorageAccount
```

如果您想 toouse 現有的儲存體帳戶，請繼續 toohello[上載 hello VHD](#upload-the-vhd-to-your-storage-account) > 一節。

如果您需要 toocreate 儲存體帳戶，請遵循下列步驟：

1. 您需要 hello hello 儲存體帳戶建立所在的 hello 資源群組名稱。 toofind 出您的訂用帳戶中，而型別中的所有 hello 資源群組：
   
    ```powershell
    Get-AzureRmResourceGroup
    ```

    資源群組命名為的 toocreate *myResourceGroup*在 hello*美國西部*區域中，輸入：

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "West US"
    ```

2. 建立名為儲存體帳戶*mystorageaccount*使用 hello 此資源群組中[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "West US" `
        -SkuName "Standard_LRS" -Kind "Storage"
    ```

### <a name="upload-hello-vhd-tooyour-storage-account"></a>上傳 hello VHD tooyour 儲存體帳戶 
使用 hello[新增 AzureRmVhd](/powershell/module/azurerm.compute/add-azurermvhd) cmdlet tooupload hello VHD tooa 容器儲存體帳戶中的。 此範例中上傳 hello 檔案*myVHD.vhd*從`"C:\Users\Public\Documents\Virtual hard disks\"`tooa 儲存體帳戶*mystorageaccount*在 hello *myResourceGroup*資源群組。 hello 檔案會儲存在名為 「 hello 容器*mycontainer* hello 新的檔案名稱將會*myUploadedVHD.vhd*。

```powershell
$resourceGroupName = "myResourceGroup"
$urlOfUploadedVhd = "https://mystorageaccount.blob.core.windows.net/mycontainer/myUploadedVHD.vhd"
Add-AzureRmVhd -ResourceGroupName $resourceGroupName -Destination $urlOfUploadedVhd `
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

根據您的網路連線和 hello VHD 檔案的大小，此命令可能需要一些時間 toocomplete

### <a name="create-a-managed-disk-from-hello-vhd"></a>從 hello VHD 建立受管理的磁碟

從 hello 建立受管理的磁碟在儲存體帳戶中使用特製化 VHD[新增 AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)。 這個範例會使用**myOSDisk1** hello 磁碟名稱 中，將 hello 磁碟*StandardLRS*存放裝置，並使用*https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd*為 hello hello 來源 VHD URI。

建立新的資源群組 hello 新的 VM。

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

建立從 hello hello 新作業系統磁碟上傳 VHD。 

```powershell
$sourceUri = https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd)
$osDiskName = 'myOsDisk'
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig -AccountType StandardLRS  -Location $location -CreateOption Import `
    -SourceUri $sourceUri) `
    -ResourceGroupName $destinationResourceGroup
```

## <a name="option-2-copy-an-existing-azure-vm"></a>選項 2：複製現有的 Azure VM

您可以建立一份使用受磁碟 hello VM 的快照，然後使用該快照集 toocreate 新受管理的磁碟和新的 VM 的 VM。


### <a name="take-a-snapshot-of-hello-os-disk"></a>取得 hello 作業系統磁碟的快照

您可以製作整個 VM (包括所有磁碟) 或僅只單一磁碟的快照集。 hello 下列步驟說明如何 tootake 只 hello OS 磁碟 VM 使用的快照集 hello[新增 AzureRmSnapshot](/powershell/module/azurerm.compute/new-azurermsnapshot) cmdlet。 

設定部分參數。 

 ```powershell
$resourceGroupName = 'myResourceGroup' 
$vmName = 'myVM'
$location = 'westus' 
$snapshotName = 'mySnapshot'  
```

收到 hello VM 物件。

```powershell
$vm = Get-AzureRmVM -Name $vmName -ResourceGroupName $resourceGroupName
```
收到 hello 作業系統磁碟名稱。

 ```powershell
$disk = Get-AzureRmDisk -ResourceGroupName $resourceGroupName -DiskName $vm.StorageProfile.OsDisk.Name
```

建立 hello 快照集設定。 

 ```powershell
$snapshotConfig =  New-AzureRmSnapshotConfig -SourceUri $disk.Id -OsType Windows -CreateOption Copy -Location $location 
```

取得 hello 快照集。

```powershell
$snapShot = New-AzureRmSnapshot -Snapshot $snapshotConfig -SnapshotName $snapshotName -ResourceGroupName $resourceGroupName
```


如果您計劃 toouse hello 快照 toocreate 需要 toobe 高執行 VM 時，使用 hello 參數`-AccountType Premium_LRS`hello 新增 AzureRmSnapshot 命令。 hello 參數建立 hello 快照集，使它儲存為 Premium 管理磁碟。 進階受控磁碟的價格高於「標準」受控磁碟。 因此務必真的需要付費才能使用 hello 參數。

### <a name="create-a-new-disk-from-hello-snapshot"></a>從 hello 快照集建立新的磁碟

建立受管理的磁碟，從快照集使用的 hello[新增 AzureRMDisk](/powershell/module/azurerm.compute/new-azurermdisk)。 這個範例會使用*myOSDisk* hello 磁碟名稱。

建立新的資源群組 hello 新的 VM。

```powershell
$destinationResourceGroup = 'myDestinationResourceGroup'
New-AzureRmResourceGroup -Location $location -Name $destinationResourceGroup
```

設定 hello 作業系統磁碟名稱。 

```powershell
$osDiskName = 'myOsDisk'
```

建立 hello 受管理的磁碟。

```powershell
$osDisk = New-AzureRmDisk -DiskName $osDiskName -Disk `
    (New-AzureRmDiskConfig  -Location $location -CreateOption Copy `
    -SourceResourceId $snapshot.Id) `
    -ResourceGroupName $destinationResourceGroup
```


## <a name="create-hello-new-vm"></a>建立 hello 新的 VM 

網路功能與 hello 所使用的其他 VM 資源 toobe 建立新的 VM。

### <a name="create-hello-subnet-and-vnet"></a>建立 hello 子網路和 vNet

建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。

建立 hello 子網路。 這個範例會建立名為的子網路**mySubNet**，hello 資源群組中**myDestinationResourceGroup**，並設定太 hello 子網路位址首碼**10.0.0.0/24**。
   
```powershell
$subnetName = 'mySubNet'
$singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
```

建立 hello vNet。 此範例中設定 hello 虛擬網路名稱 toobe **myVnetName**，太 hello 位置**美國西部**，太 hello hello 虛擬網路的位址前置詞和**10.0.0.0/16**。 
   
```powershell
$vnetName = "myVnetName"
$vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $destinationResourceGroup -Location $location `
    -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
```    


### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>建立網路安全性群組 hello 和 RDP 規則
toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 允許連接埠 3389 RDP 存取權的安全性規則。 因為 hello 的 hello 從現有特製化的 VM 建立新的 VM 的 VHD，您可以使用帳戶 hello 來源虛擬機器從 rdp。

此範例中設定 hello NSG 名稱太**myNsg**和 hello RDP 規則名稱太**myRdpRule**。

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $destinationResourceGroup -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

如需有關端點和 NSG 規則的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

### <a name="create-a-public-ip-address-and-nic"></a>建立公用 IP 位址和 NIC
tooenable 與 hello hello 虛擬網路中的虛擬機器的通訊，您需要[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)和網路介面。

建立 hello 公用 IP。 在此範例中，hello 公用 IP 位址名稱設定太**myIP**。
   
```powershell
$ipName = "myIP"
$pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $destinationResourceGroup -Location $location `
   -AllocationMethod Dynamic
```       

建立 hello nic。 在此範例中，hello NIC 設定名稱太**myNicName**。
   
```powershell
$nicName = "myNicName"
$nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $destinationResourceGroup `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id -NetworkSecurityGroupId $nsg.Id
```



### <a name="set-hello-vm-name-and-size"></a>設定 hello VM 名稱和大小

此範例中設定 hello VM 名稱太*myVM*和 hello VM 大小太*Standard_A2*。

```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>新增 hello NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    

### <a name="add-hello-os-disk"></a>新增 hello OS 磁碟 

Hello OS 磁碟 toohello 設定使用新增[組 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk)。 此範例會設定 hello hello 磁碟大小太*128 GB*附加 hello 受管理的磁碟和*Windows*作業系統磁碟。
 
```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -ManagedDiskId $osDisk.Id -StorageAccountType StandardLRS `
    -DiskSizeInGB 128 -CreateOption Attach -Windows
```

### <a name="complete-hello-vm"></a>完成 hello VM 

建立 hello VM 使用[新增 AzureRMVM](/powershell/module/azurerm.compute/new-azurermvm)hello 剛才所建立的組態。

```powershell
New-AzureRmVM -ResourceGroupName $destinationResourceGroup -Location $location -VM $vm
```

如果此命令成功，您會看到如下的輸出︰

```powershell
RequestId IsSuccessStatusCode StatusCode ReasonPhrase
--------- ------------------- ---------- ------------
                         True         OK OK   

```

### <a name="verify-that-hello-vm-was-created"></a>請確認 VM 已建立該 hello
您應該會看到 hello 新建立的 VM 在 hello [Azure 入口網站](https://portal.azure.com)下**瀏覽** > **虛擬機器**，或使用下列 PowerShell hello命令：

```powershell
$vmList = Get-AzureRmVM -ResourceGroupName $destinationResourceGroup
$vmList.Name
```

## <a name="next-steps"></a>後續步驟
在 tooyour 的新虛擬機器，而在 hello 瀏覽 toohello VM toosign[入口網站](https://portal.azure.com)，按一下**連接**，並開啟 hello 遠端桌面 RDP 檔案。 Tooyour 新虛擬機器中使用原始的虛擬機器 toosign hello 帳戶認證。 如需詳細資訊，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md)。

