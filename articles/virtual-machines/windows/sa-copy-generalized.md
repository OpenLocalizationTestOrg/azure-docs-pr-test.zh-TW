---
title: "未受管理的 Azure 中的一般化 VM 映像 aaaCreate |Microsoft 文件"
description: "在 Azure 中建立通用的 Windows VM toouse toocreate unmanaged 映的像 VM 的多個複本。"
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
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: b8a044d20313efa6dd9b9757e61154f922134476
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-unmanaged-vm-image-from-an-azure-vm"></a>Toocreate 未受管理的 VM 從 Azure VM 的映像

本文章涵蓋使用儲存體帳戶的內容。 建議您使用受控磁碟和受管理的映像，不要使用儲存體帳戶。 如需詳細資訊，請參閱[在 Azure 中擷取一般化 VM 的受管理映像](capture-image-resource.md)。

本文章將示範如何 toouse Azure PowerShell toocreate 使用儲存體帳戶的一般化 Azure VM 的映像。 另一個 VM 時，可以使用 hello 映像 toocreate。 hello 映像包括 hello OS 磁碟和 hello 附加的 toohello 虛擬機器之資料磁碟。 hello 映像不含 hello 虛擬網路資源，因此當您建立時，需要這些資源 tooset hello 新的 VM。 

## <a name="prerequisites"></a>必要條件
您需要 toohave Azure PowerShell 版本 1.0.x 或較新的安裝。 如果您尚未安裝 PowerShell，請參閱[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)如需安裝步驟。

## <a name="generalize-hello-vm"></a>一般化 VM hello 
這個區段會顯示如何 toogeneralize 用作映像的 Windows 虛擬機器。 將 VM 一般化移除所有您個人的帳戶資訊，以及其他項目，並準備 hello 機器 toobe 做為映像。 如需 Sysprep 的詳細資訊，請參閱[如何 tooUse Sysprep： 簡介](http://technet.microsoft.com/library/bb457073.aspx)。

請確定 hello hello 機器上執行的伺服器角色支援 sysprep。 如需詳細資訊，請參閱 [Sysprep Support for Server Roles (伺服器角色的 Sysprep 支援)](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

> [!IMPORTANT]
> 如果您要上傳您的 VHD tooAzure hello 第一次，請確定您有[備妥您的 VM](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)執行 Sysprep 之前。 
> 
> 

您也可以普及使用 Linux VM `sudo waagent -deprovision+user` ，然後使用 PowerShell toocapture hello VM。 如需使用 hello CLI toocapture VM 的資訊，請參閱[toogeneralize 和 Linux 虛擬機器使用的擷取 hello Azure CLI ](../linux/capture-image.md)。


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

## <a name="log-in-tooazure-powershell"></a>登入 tooAzure PowerShell
1. 開啟 Azure PowerShell，然後登入 tooyour Azure 帳戶。
   
    ```powershell
    Login-AzureRmAccount
    ```
   
    快顯視窗中開啟您 tooenter 以您的 Azure 帳戶的認證。
2. 取得可用的訂閱 hello 訂用帳戶 Id。
   
    ```powershell
    Get-AzureRmSubscription
    ```
3. 設定使用 hello 訂用帳戶識別碼 hello 正確訂用帳戶
   
    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<subscriptionID>"
    ```

## <a name="deallocate-hello-vm-and-set-hello-state-toogeneralized"></a>解除配置 hello VM 並設定 hello 狀態 toogeneralized
1. 解除配置 hello VM 資源。
   
    ```powershell
    Stop-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName>
    ```
   
    hello*狀態*hello VM 在 hello Azure 入口網站變更從**已停止**太**已停止 （取消配置）**。
2. 設定得 hello hello 虛擬機器狀態**一般**。 
   
    ```powershell
    Set-AzureRmVm -ResourceGroupName <resourceGroup> -Name <vmName> -Generalized
    ```
3. 檢查 hello hello VM 狀態。 hello **OSState/一般化**區段中針對 hello VM 應有 hello **DisplayStatus**設定得**一般化 VM**。  
   
    ```powershell
    $vm = Get-AzureRmVM -ResourceGroupName <resourceGroup> -Name <vmName> -Status
    $vm.Statuses
    ```

## <a name="create-hello-image"></a>建立 hello 映像

使用這個命令的 hello 目的地儲存體容器中建立未受管理的虛擬機器映像。 hello 映像中建立 hello 相同 hello 原始虛擬機器的儲存體帳戶。 hello`-Path`參數將儲存 hello 來源 VM tooyour 本機電腦的 hello JSON 範本的複本。 hello`-DestinationContainerName`參數就是您希望 toohold 影像 hello 容器 hello 名稱。 如果 hello 容器不存在，它會為您建立。
   
```powershell
Save-AzureRmVMImage -ResourceGroupName <resourceGroupName> -Name <vmName> `
    -DestinationContainerName <destinationContainerName> -VHDNamePrefix <templateNamePrefix> `
    -Path <C:\local\Filepath\Filename.json>
```
   
您可以取得映像的 hello URL 從 hello JSON 檔案的範本。 移 toohello**資源** > **storageProfile** > **osDisk** > **映像** > **uri**映像的區段 hello 完整路徑。 hello hello 影像 URL 看起來像： `https://<storageAccountName>.blob.core.windows.net/system/Microsoft.Compute/Images/<imagesContainer>/<templatePrefix-osDisk>.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd`。
   
您也可以驗證在 hello 入口網站中的 hello URI。 hello 映像會複製的 tooa 容器名稱**系統**儲存體帳戶中。 

## <a name="create-a-vm-from-hello-image"></a>從 hello 映像建立 VM

現在您可以建立一個或多個 Vm 從 hello unmanaged 映像。

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
hello 下列 PowerShell 完成 hello 虛擬機器組態，並使用未受管理的映像為 hello 來源 hello 全新安裝。

</br>

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

### <a name="verify-that-hello-vm-was-created"></a>請確認 VM 已建立該 hello
完成時，您應該會看到新建立的 VM 中 hello hello [Azure 入口網站](https://portal.azure.com)下**瀏覽** > **虛擬機器**，或使用 hello 下列PowerShell 命令：

```powershell
    $vmList = Get-AzureRmVM -ResourceGroupName $rgName
    $vmList.Name
```

## <a name="next-steps"></a>後續步驟
toomanage 新的虛擬機器使用 Azure PowerShell，請參閱[使用 Azure 資源管理員和 PowerShell 管理虛擬機器](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。


