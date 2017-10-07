---
title: "從專用的磁碟在 Azure 中的 VM aaaCreate |Microsoft 文件"
description: "藉由附加專用的 unmanaged 的磁碟，hello Resource Manager 部署模型中建立新的 VM。"
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: c88f213b6629a6c1d6ff5845e76c2f7719672714
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-specialized-vhd-in-a-storage-account"></a>從儲存體帳戶中的特製化 VHD 建立 VM

藉由將專用的 unmanaged 的磁碟附加為 hello OS 磁碟使用 Powershell 建立新的 VM。 專用的磁碟是從現有的 VM 會維護 hello 使用者帳戶、 應用程式及其他狀態資料從您的原始 VM VHD 的複本。 

您有兩個選擇：
* [上傳 VHD](create-vm-specialized.md#option-1-upload-a-specialized-vhd)
* [複製現有的 Azure VM 的 VHD hello](create-vm-specialized.md#option-2-copy-an-existing-azure-vm)

## <a name="before-you-begin"></a>開始之前
如果您使用 PowerShell，請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。 執行 hello 下列命令 tooinstall 它。

```powershell
Install-Module AzureRM.Compute 
```
如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。


## <a name="option-1-upload-a-specialized-vhd"></a>選項 1：上傳特製化 VHD

您可以上傳的 hello 與內部部署虛擬化工具，像是從另一個雲端匯出 HYPER-V 或在 VM 建立從特製化的 VM 的 VHD。

### <a name="prepare-hello-vm"></a>準備 VM hello
您可以上傳使用內部部署 VM 建立的特製化 VHD，或上傳從另一個雲端匯出的 VHD。 特製化的 VHD 會維護 hello 使用者帳戶、 應用程式及其他狀態資料從您的原始 VM。 如果您想 toouse hello VHD 當做-是 toocreate 新的 VM，請完成下列步驟的 hello。 
  
  * [準備 Windows VHD tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 **不這麼做**一般化 hello VM 使用 Sysprep。
  * 移除任何客體的虛擬化工具和 hello VM （也就是 VMware 工具） 所安裝的代理程式。
  * 請確定 hello VM 是已設定的 toopull 其 IP 位址和 DNS 設定，透過 DHCP。 這可確保該 hello 伺服器會在啟動時，取得 hello VNet 內的 IP 位址。 


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
   
### <a name="upload-hello-vhd-tooyour-storage-account"></a>上傳 hello VHD tooyour 儲存體帳戶
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


## <a name="option-2-copy-hello-vhd-from-an-existing-azure-vm"></a>選項 2: Hello VHD 複製現有的 Azure VM

建立新的、 重複的 VM 時，您可以複製 VHD tooanother 儲存體帳戶 toouse。

### <a name="before-you-begin"></a>開始之前
請確定您︰

* 會有資訊 hello**來源和目的地儲存體帳戶**。 Hello 來源 VM，您需要 toohave hello 儲存體帳戶和容器名稱。 通常，是 hello 容器名稱**vhd**。 您也需要 toohave 目的地儲存體帳戶。 如果您還沒有其中一個，您可以建立一個使用任一個 hello 入口網站 (**更服務**> 儲存體帳戶 > 加入) 或使用 hello[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet。 
* 已下載並安裝 hello [AzCopy 工具](../../storage/common/storage-use-azcopy.md)。 

### <a name="deallocate-hello-vm"></a>Hello VM 解除配置
解除配置 VM，這可釋 hello VHD toobe 複製 hello。 

* **入口網站**︰ 按一下 [虛擬機器]  >  [myVM] > [停止]
* **Powershell**： 使用[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm) toostop （解除配置） hello 名為 VM **myVM**資源群組中**myResourceGroup**。

```powershell
Stop-AzureRmVM -ResourceGroupName myResourceGroup -Name myVM
```

hello**狀態**hello VM 在 hello Azure 入口網站變更從**已停止**太**已停止 （取消配置）**。

### <a name="get-hello-storage-account-urls"></a>取得 hello 儲存體帳戶 Url
您需要 hello hello 來源和目的地儲存體帳戶的 Url。 hello Url 如下： `https://<storageaccount>.blob.core.windows.net/<containerName>/`。 如果您已經知道 hello 儲存體帳戶和容器名稱，您可以只取代之間 hello 方括號 toocreate hello 資訊 URL。 

您可以使用 hello Azure 入口網站或 Azure Powershell tooget hello URL:

* **入口網站**： 按一下 hello  **>** 如**更多服務** > **儲存體帳戶** >  *儲存體帳戶* > **Blob**和原始程式 VHD 檔可能是 hello **vhd**容器。 按一下**屬性**hello 容器和複製 hello 文字標示為**URL**。 您將需要這兩個 hello 來源和目的地容器的 hello Url。 
* **Powershell**： 使用[Get AzureRmVM](/powershell/module/azurerm.compute/get-azurermvm)名為 VM 的 tooget hello 資訊**myVM** hello 資源群組中**myResourceGroup**。 在 hello 結果，請查看 hello**儲存體設定檔**hello 區段**Vhd Uri**。 hello 的 hello Uri 的第一個部分是 hello URL toohello 容器和 hello 最後一個部分是 hello hello VM 的 OS VHD 名稱。

```powershell
Get-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
``` 

## <a name="get-hello-storage-access-keys"></a>取得 hello 儲存體存取金鑰
尋找 hello hello 便捷鍵的來源和目的地儲存體帳戶。 如需存取金鑰的詳細資訊，請參閱 [關於 Azure 儲存體帳戶](../../storage/common/storage-create-storage-account.md)。

* **入口網站**︰按一下 [更多服務]  > [儲存體帳戶]  > [儲存體帳戶] > [存取金鑰]。 複製 hello 機碼標示為**key1**。
* **Powershell**： 使用[Get AzureRmStorageAccountKey](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) tooget hello hello 儲存體帳戶的儲存體金鑰**mystorageaccount** hello 資源群組中**myResourceGroup**。 複製 hello 機碼標示為**key1**。

```powershell
Get-AzureRmStorageAccountKey -Name mystorageaccount -ResourceGroupName myResourceGroup
```

### <a name="copy-hello-vhd"></a>複製 hello VHD
您可以使用 AzCopy 在儲存體帳戶之間複製檔案。 Hello 目的地容器，如果 hello 指定的容器不存在，它就會為您建立。 

toouse AzCopy，開啟命令提示字元在本機電腦上，並瀏覽 toohello AzCopy 安裝所在的資料夾。 它將會類似太*C:\Program Files (x86) \Microsoft SDKs\Azure\AzCopy*。 

toocopy hello 的所有檔案的容器內，使用 hello **/S**切換。 這可以是使用的 toocopy hello 作業系統 VHD 和所有 hello 資料磁碟，如果它們是在 hello 相同的容器。 這個範例會示範如何 toocopy hello 的所有檔案在 hello 容器**mysourcecontainer**儲存體帳戶中**mysourcestorageaccount** toohello 容器**mydestinationcontainer**在 hello **mydestinationstorageaccount**儲存體帳戶。 以您自己取代 hello hello 儲存體帳戶和容器的名稱。 使用您自己的金鑰取代 `<sourceStorageAccountKey1>` 和 `<destinationStorageAccountKey1>`。

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
    /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
    /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> /S
```

如果您只想 toocopy 容器中的特定 VHD 與多個檔案，您也可以指定使用 hello /Pattern 交換器 hello 檔案名稱。 在此範例中，只有 hello 檔名為**myFileName.vhd**會被複製。

```
AzCopy /Source:https://mysourcestorageaccount.blob.core.windows.net/mysourcecontainer `
  /Dest:https://mydestinationatorageaccount.blob.core.windows.net/mydestinationcontainer `
  /SourceKey:<sourceStorageAccountKey1> /DestKey:<destinationStorageAccountKey1> `
  /Pattern:myFileName.vhd
```


完成時，您將收到如下的訊息：

```
Finished 2 of total 2 file(s).
[2016/10/07 17:37:41] Transfer summary:
-----------------
Total files transferred: 2
Transfer successfully:   2
Transfer skipped:        0
Transfer failed:         0
Elapsed time:            00.00:13:07
```

### <a name="troubleshooting"></a>疑難排解
* 當您使用 AZCopy，如果您看到 hello 錯誤 「 伺服器無法 tooauthenticate hello 要求 」 時，請確定 hello hello 授權標頭值格式正確並包含 hello 簽章。 如果您使用索引鍵 2 或 hello 次要儲存體金鑰，請嘗試使用 hello 主要或第 1 個儲存體金鑰。

## <a name="create-hello-new-vm"></a>建立 hello 新的 VM 

您需要 toocreate 網路功能與其他 VM 資源 toobe hello 使用新的 VM。

### <a name="create-hello-subnet-and-vnet"></a>建立 hello 子網路和 vNet

建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。

1. 建立 hello 子網路。 這個範例會建立名為的子網路**mySubNet**，hello 資源群組中**myResourceGroup**，並設定太 hello 子網路位址首碼**10.0.0.0/24**。
   
    ```powershell
    $rgName = "myResourceGroup"
    $subnetName = "mySubNet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. 建立 hello vNet。 此範例中設定 hello 虛擬網路名稱 toobe **myVnetName**，太 hello 位置**美國西部**，太 hello hello 虛擬網路的位址前置詞和**10.0.0.0/16**。 
   
    ```powershell
    $location = "West US"
    $vnetName = "myVnetName"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

### <a name="create-a-public-ip-address-and-nic"></a>建立公用 IP 位址和 NIC
tooenable 與 hello hello 虛擬網路中的虛擬機器的通訊，您需要[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)和網路介面。

1. 建立 hello 公用 IP。 在此範例中，hello 公用 IP 位址名稱設定太**myIP**。
   
    ```powershell
    $ipName = "myIP"
    $pip = New-AzureRmPublicIpAddress -Name $ipName -ResourceGroupName $rgName -Location $location `
        -AllocationMethod Dynamic
    ```       
2. 建立 hello nic。 在此範例中，hello NIC 設定名稱太**myNicName**。
   
    ```powershell
    $nicName = "myNicName"
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
    -Location $location -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id
    ```

### <a name="create-hello-network-security-group-and-an-rdp-rule"></a>建立網路安全性群組 hello 和 RDP 規則
toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 安全性規則，允許連接埠 3389 RDP 存取權。 Hello VHD 已建立新的 VM，從現有的 hello 特製化，因為 VM hello VM 建立您之後可以使用現有的帳戶從有權限 toolog 上使用 RDP 的 hello 來源虛擬機器。
此範例中設定 hello NSG 名稱太**myNsg**和 hello RDP 規則名稱太**myRdpRule**。

```powershell
$nsgName = "myNsg"

$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name myRdpRule -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389
$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
    
```

如需有關端點和 NSG 規則的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

### <a name="set-hello-vm-name-and-size"></a>設定 hello VM 名稱和大小

此範例中設定 hello VM 名稱太"myVM 」 和 hello VM 大小太"Standard_A2"。
```powershell
$vmName = "myVM"
$vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize "Standard_A2"
```

### <a name="add-hello-nic"></a>新增 hello NIC
    
```powershell
$vm = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id
```
    
    
### <a name="configure-hello-os-disk"></a>設定 hello OS 磁碟

1. 設定您上傳或複製的 VHD hello URI。 在此範例中，hello VHD 檔案命名為**myOsDisk.vhd**保留在儲存體帳戶中**myStorageAccount**中名為的容器**myContainer**。

    ```powershell
    $osDiskUri = "https://myStorageAccount.blob.core.windows.net/myContainer/myOsDisk.vhd"
    ```
2. 新增 hello 作業系統磁碟。 在此範例中，建立 hello 作業系統磁碟時，hello 詞彙"osDisk"會是 appened toohello VM 名稱 toocreate hello 作業系統磁碟名稱。 此範例也會指定此 windows VHD 應該附加的 toohello 為 hello OS 磁碟的 VM。
    
    ```powershell
    $osDiskName = $vmName + "osDisk"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name $osDiskName -VhdUri $osDiskUri -CreateOption attach -Windows
    ```

選擇性： 如果您有資料磁碟的需要 toobe 附加 toohello VM、 使用的資料 Vhd hello Url 新增 hello 資料磁碟和 hello 適當的邏輯單元編號 (Lun)。

```powershell
$dataDiskName = $vmName + "dataDisk"
$vm = Add-AzureRmVMDataDisk -VM $vm -Name $dataDiskName -VhdUri $dataDiskUri -Lun 1 -CreateOption attach
```

使用時的儲存體帳戶，hello 資料及作業系統磁碟 Url 看起來像這樣： `https://StorageAccountName.blob.core.windows.net/BlobContainerName/DiskName.vhd`。 您可以在 hello 入口網站上找到此來瀏覽 toohello 目標儲存體容器，按一下 hello 作業系統或資料已複製的 VHD，然後複製 hello URL hello 內容。


### <a name="complete-hello-vm"></a>完成 hello VM 

建立 hello 使用我們剛才建立的 hello 組態的 VM。

```powershell
#Create hello new VM
New-AzureRmVM -ResourceGroupName $rgName -Location $location -VM $vm
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
$vmList = Get-AzureRmVM -ResourceGroupName $rgName
$vmList.Name
```

## <a name="next-steps"></a>後續步驟
在 tooyour 的新虛擬機器，而在 hello 瀏覽 toohello VM toosign[入口網站](https://portal.azure.com)，按一下**連接**，並開啟 hello 遠端桌面 RDP 檔案。 Tooyour 新虛擬機器中使用原始的虛擬機器 toosign hello 帳戶認證。 如需詳細資訊，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md)。

