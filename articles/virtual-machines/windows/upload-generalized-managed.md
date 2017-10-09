---
title: "受管理的 Azure VM 從內部一般化的 VHD aaaCreate |Microsoft 文件"
description: "上傳一般化的 VHD tooAzure，並用它 toocreate hello Resource Manager 部署模型中的新 Vm。"
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
ms.date: 05/19/2017
ms.author: cynthn
ms.openlocfilehash: 2fd0c0eec922e6ca8af4e712c1bceb1f9466105c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-generalized-vhd-and-use-it-toocreate-new-vms-in-azure"></a>一般化的 VHD 上傳，並用它 toocreate Azure 中的新 Vm

本主題會引導您逐步使用 PowerShell tooupload 一般化 VM tooAzure 的 VHD 從 hello VHD 建立映像，從該映像建立新的 VM。 您可以上傳從內部部署虛擬化工具或另一個雲端匯出的 VHD。 使用[管理磁碟](managed-disks-overview.md)hello 新的 VM 可簡化 hello VM 管理和 hello VM 放置於可用性集合時提供更佳的可用性。 

如果您想 toouse 範例指令碼，請參閱[範例指令碼 tooupload VHD tooAzure 並建立新的 VM](../scripts/virtual-machines-windows-powershell-upload-generalized-script.md)

## <a name="before-you-begin"></a>開始之前

- 上傳任何 VHD tooAzure 之前, 您應該遵循[準備 Windows VHD 或 VHDX tooupload tooAzure](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
- 檢閱[hello 移轉計劃 tooManaged 磁碟](on-prem-to-azure.md#plan-for-the-migration-to-managed-disks)太開始移轉之前[管理磁碟](managed-disks-overview.md)。
- 請確定您擁有 hello hello AzureRM.Compute PowerShell 模組最新版本。 執行 hello 下列命令 tooinstall 它。

    ```powershell
    Install-Module AzureRM.Compute -RequiredVersion 2.6.0
    ```
    如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。


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



## <a name="log-in-tooazure"></a>登入 tooAzure
如果您還沒有 PowerShell 1.4 版或更新版本安裝，讀取[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)。

1. 開啟 Azure PowerShell，然後登入 tooyour Azure 帳戶。 快顯視窗中開啟您 tooenter 以您的 Azure 帳戶的認證。
   
    ```powershell
    Login-AzureRmAccount
    ```
2. 取得可用的訂閱 hello 訂用帳戶 Id。
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. 設定使用 hello 訂用帳戶識別碼 hello 正確訂用帳戶 取代 *<subscriptionID>*  hello 識別碼 hello 包含正確的訂用帳戶。
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="get-hello-storage-account"></a>取得 hello 儲存體帳戶
您需要 Azure toostore hello 上傳 VM 映像的儲存體帳戶。 您可以使用現有的儲存體帳戶或建立新帳戶。 

如果您將使用 hello VHD toocreate 受管理磁碟 vm，hello 儲存體帳戶位置必須是相同的 hello 位置，其中您要建立 hello VM。

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

    資源群組命名為的 toocreate **myResourceGroup**在 hello**美國東部**區域中，輸入：

    ```powershell
    New-AzureRmResourceGroup -Name myResourceGroup -Location "East US"
    ```

2. 建立名為儲存體帳戶**mystorageaccount**使用 hello 此資源群組中[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet:
   
    ```powershell
    New-AzureRmStorageAccount -ResourceGroupName myResourceGroup -Name mystorageaccount -Location "East US"`
        -SkuName "Standard_LRS" -Kind "Storage"
    ```
   
    -SkuName 的有效值包括：
   
   * **Standard_LRS** - 本地備援儲存體。 
   * **Standard_ZRS** - 區域備援儲存體。
   * **Standard_GRS** - 異地備援儲存體。 
   * **Standard_RAGRS** - 讀取權限異地備援儲存體。 
   * **Premium_LRS** - 進階本地備援儲存體。 

## <a name="upload-hello-vhd-tooyour-storage-account"></a>上傳 hello VHD tooyour 儲存體帳戶

使用 hello[新增 AzureRmVhd](https://msdn.microsoft.com/library/mt603554.aspx) cmdlet tooupload hello VHD tooa 容器儲存體帳戶中的。 此範例中上傳 hello 檔案*myVHD.vhd*從*"C:\Users\Public\Documents\Virtual 硬碟\"* tooa 儲存體帳戶*mystorageaccount*在 hello *myResourceGroup*資源群組。 hello 檔案會放入名為 「 hello 容器*mycontainer* hello 新的檔案名稱將會*myUploadedVHD.vhd*。

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

根據您的網路連線和 hello VHD 檔案的大小，此命令可能需要一些時間 toocomplete

儲存 hello**目的地 URI**路徑 toouse 稍後如果您正在 toocreate 受管理的磁碟，或使用 hello 的新 VM 上傳 VHD。

### <a name="other-options-for-uploading-a-vhd"></a>上傳 VHD 的其他選項
 
 
您也可以上傳 VHD tooyour 儲存體帳戶使用 hello 下列其中一種：

- [AzCopy](http://aka.ms/downloadazcopy)
- [Azure 儲存體複製 Blob API](https://msdn.microsoft.com/library/azure/dd894037.aspx)
- [Azure 儲存體總管上傳 Blob](https://azurestorageexplorer.codeplex.com/)
- [儲存體匯入/匯出服務 REST API 參考](https://msdn.microsoft.com/library/dn529096.aspx)
-   如果預估的上傳時間長度超過 7 天，我們建議使用匯入/匯出服務。 您可以使用[DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate hello 時間資料的大小和傳輸的單位。 
    可以匯入/匯出用 toocopy tooa 標準儲存體帳戶。 您必須從標準儲存體 toopremium 儲存體帳戶，使用 AzCopy 這類工具 toocopy。


## <a name="create-a-managed-image-from-hello-uploaded-vhd"></a>建立受管理 hello 從映像上傳 VHD 

使用一般化 OS VHD 建立受控映像。 Hello 值取代為您自己的資訊。


1.  首先，設定 hello 一般參數：

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    $vmSize = "Standard_DS1_v2"
    $location = "East US" 
    $imageName = "yourImageName"
    ```

4.  建立 hello 使用一般化的 OS VHD 的映像。

    ```powershell
    $imageConfig = New-AzureRmImageConfig -Location $location
    $imageConfig = Set-AzureRmImageOsDisk -Image $imageConfig -OsType Windows -OsState Generalized -BlobUri $urlOfUploadedImageVhd
    $image = New-AzureRmImage -ImageName $imageName -ResourceGroupName $rgName -Image $imageConfig
    ```

## <a name="create-a-virtual-network"></a>建立虛擬網路
建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。

1. 建立 hello 子網路。 這個範例會建立名為的子網路*mySubnet* hello 位址前置詞與*10.0.0.0/24*。  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. 建立 hello 虛擬網路。 這個範例會建立虛擬網路，名為*myVnet* hello 位址前置詞與*10.0.0.0/16*。  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>建立公用 IP 位址和網路介面

tooenable 與 hello hello 虛擬網路中的虛擬機器的通訊，您需要[公用 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)和網路介面。

1. 建立公用 IP 位址。 此範例會建立名為 *myPip* 的公用 IP 位址。 
   
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

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>建立網路安全性群組 hello 和 RDP 規則

toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 網路安全性規則 (NSG)，允許連接埠 3389 RDP 存取權。 

此範例會建立名為 *myNsg* 的 NSG，其包含的規則 *myRdpRule* 可允許透過連接埠 3389 的 RDP 流量。 如需 Nsg 的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

```powershell
$nsgName = "myNsg"
$ruleName = "myRdpRule"
$rdpRule = New-AzureRmNetworkSecurityRuleConfig -Name $ruleName -Description "Allow RDP" `
    -Access Allow -Protocol Tcp -Direction Inbound -Priority 110 `
    -SourceAddressPrefix Internet -SourcePortRange * `
    -DestinationAddressPrefix * -DestinationPortRange 3389

$nsg = New-AzureRmNetworkSecurityGroup -ResourceGroupName $rgName -Location $location `
    -Name $nsgName -SecurityRules $rdpRule
```


## <a name="create-a-variable-for-hello-virtual-network"></a>針對 hello 虛擬網路建立的變數

建立 hello 完成虛擬網路的變數。 

```powershell
$vnet = Get-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName

```

## <a name="get-hello-credentials-for-hello-vm"></a>取得 hello VM hello 認證

hello 下列 cmdlet 會開啟的視窗，您就會在輸入新的使用者名稱和密碼 toouse hello 的本機 administrator 帳戶從遠端存取 hello VM。 

```powershell
$cred = Get-Credential
```

## <a name="add-hello-vm-name-and-size-toohello-vm-configuration"></a>加入 hello VM 名稱和大小 toohello VM 組態。

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>集 hello VM 映像 hello 的來源映像為新的 VM

設定使用受管理的 hello VM 映像的 hello 識別碼 hello 來源映像。

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>設定 hello 作業系統設定以及新增 hello nic。

輸入 hello 儲存類型 （PremiumLRS 或 StandardLRS） 和 hello hello 作業系統磁碟大小。 此範例會設定 hello 帳戶類型太*PremiumLRS*，太 hello 磁碟大小*128 GB*和磁碟快取太*ReadWrite*。

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>建立 hello VM

建立新的 VM 使用 hello 組態儲存在 hello hello **$vm**變數。

```powershell
New-AzureRmVM -VM $vm -ResourceGroupName $rgName -Location $location
```

## <a name="verify-that-hello-vm-was-created"></a>請確認 VM 已建立該 hello
完成時，您應該會看到新建立的 VM 中 hello hello [Azure 入口網站](https://portal.azure.com)下**瀏覽** > **虛擬機器**，或使用 hello 下列PowerShell 命令：

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>後續步驟

在 tooyour 的新虛擬機器，而在 hello 瀏覽 toohello VM toosign[入口網站](https://portal.azure.com)，按一下**連接**，並開啟 hello 遠端桌面 RDP 檔案。 Tooyour 新虛擬機器中使用原始的虛擬機器 toosign hello 帳戶認證。 如需詳細資訊，請參閱[如何 tooconnect 和登入 tooan Azure 虛擬機器執行 Windows](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 

