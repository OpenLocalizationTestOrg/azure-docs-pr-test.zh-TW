---
title: "從受管理的 VM 映像，在 Azure 中的 VM aaaCreate |Microsoft 文件"
description: "從通用 managed VM 映像在 hello Resource Manager 部署模型中使用 Azure PowerShell 中建立 Windows 虛擬機器。"
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
ms.date: 05/22/2017
ms.author: cynthn
ms.openlocfilehash: 5036ef1533c144a9a328e94599b359e0166f337d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-from-a-managed-image"></a>從 Managed 映像建立 VM

您可以在 Azure 中從受控 VM 映像建立多個 VM。 受管理的 VM 映像包含 hello 資訊必要 toocreate VM，包括 hello OS 和資料磁碟。 hello hello 映像，包括 hello OS 磁碟和任何資料磁碟所組成，會儲存成受管理的磁碟的 Vhd。 


## <a name="prerequisites"></a>必要條件

您必須已經 toohave[建立受管理的 VM 映像](capture-image-resource.md)toouse 建立 hello 新的 VM。 

請確定您已擁有 hello hello AzureRM.Compute 和 AzureRM.Network PowerShell 模組最新版本。 開啟以系統管理員的 PowerShell 命令提示字元，然後執行下列命令 tooinstall hello 它們。

```powershell
Install-Module AzureRM.Compute,AzureRM.Network
```
如需詳細資訊，請參閱 [Azure PowerShell 版本控制](/powershell/azure/overview)。



## <a name="collect-information-about-hello-image"></a>收集 hello 映像的相關資訊

首先我們需要 toogather hello 映像相關資訊的基本資訊，並針對 hello 映像建立的變數。 這個範例會使用名為受管理的 VM 映像**myImage**也就是在 hello **myResourceGroup** hello 中的資源群組**中央美國西部**位置。 

```powershell
$rgName = "myResourceGroup"
$location = "West Central US"
$imageName = "myImage"
$image = Get-AzureRMImage -ImageName $imageName -ResourceGroupName $rgName
```

## <a name="create-a-virtual-network"></a>建立虛擬網路
建立 hello vNet 和子網路的 hello[虛擬網路](../../virtual-network/virtual-networks-overview.md)。

1. 建立 hello 子網路。 這個範例會建立名為的子網路**mySubnet** hello 位址前置詞與**10.0.0.0/24**。  
   
    ```powershell
    $subnetName = "mySubnet"
    $singleSubnet = New-AzureRmVirtualNetworkSubnetConfig -Name $subnetName -AddressPrefix 10.0.0.0/24
    ```
2. 建立 hello 虛擬網路。 這個範例會建立虛擬網路，名為**myVnet** hello 位址前置詞與**10.0.0.0/16**。  
   
    ```powershell
    $vnetName = "myVnet"
    $vnet = New-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName -Location $location `
        -AddressPrefix 10.0.0.0/16 -Subnet $singleSubnet
    ```    

## <a name="create-a-public-ip-address-and-network-interface"></a>建立公用 IP 位址和網路介面

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

## <a name="create-hello-network-security-group-and-an-rdp-rule"></a>建立網路安全性群組 hello 和 RDP 規則

toobe 無法 toolog tooyour 中的使用 RDP 的 VM，您需要 toohave 網路安全性規則 (NSG)，允許連接埠 3389 RDP 存取權。 

此範例會建立名為 **myNsg** 的 NSG，其包含的規則 **myRdpRule** 可允許透過連接埠 3389 的 RDP 流量。 如需 Nsg 的詳細資訊，請參閱[使用 PowerShell 在 Azure 中開啟連接埠 tooa VM](nsg-quickstart-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

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

## <a name="set-variables-for-hello-vm-name-computer-name-and-hello-size-of-hello-vm"></a>Hello VM 設定的變數名稱，電腦名稱，而且 hello hello VM 的大小

1. 建立 hello VM 名稱與電腦名稱的變數。 此範例會設定為 hello VM 名稱**myVM**和 hello 電腦名稱與**myComputer**。

    ```powershell
    $vmName = "myVM"
    $computerName = "myComputer"
    ```
2. 設定 hello hello 虛擬機器大小。 這個範例會建立 **Standard_DS1_v2** 大小的 VM。 請參閱 hello [VM 大小](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-sizes/)文件的詳細資訊。

    ```powershell
    $vmSize = "Standard_DS1_v2"
    ```

3. 加入 hello VM 名稱和大小 toohello VM 組態。

```powershell
$vm = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
```

## <a name="set-hello-vm-image-as-source-image-for-hello-new-vm"></a>集 hello VM 映像 hello 的來源映像為新的 VM

設定使用受管理的 hello VM 映像的 hello 識別碼 hello 來源映像。

```powershell
$vm = Set-AzureRmVMSourceImage -VM $vm -Id $image.Id
```

## <a name="set-hello-os-configuration-and-add-hello-nic"></a>設定 hello 作業系統設定以及新增 hello nic。

輸入 hello 儲存類型 （PremiumLRS 或 StandardLRS） 和 hello hello 作業系統磁碟大小。 此範例會設定 hello 帳戶類型太**PremiumLRS**，太 hello 磁碟大小**128 GB**和磁碟快取太**ReadWrite**。

```powershell
$vm = Set-AzureRmVMOSDisk -VM $vm  -StorageAccountType PremiumLRS -DiskSizeInGB 128 `
-CreateOption FromImage -Caching ReadWrite

$vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName $computerName `
-Credential $cred -ProvisionVMAgent -EnableAutoUpdate

$vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
```

## <a name="create-hello-vm"></a>建立 hello VM

建立新的 Vm 使用 hello 組態，我們已建立及儲存在 hello 的 hello **$vm**變數。

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
toomanage 新的虛擬機器使用 Azure PowerShell，請參閱[建立及管理 Windows Vm hello Azure PowerShell 模組](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

