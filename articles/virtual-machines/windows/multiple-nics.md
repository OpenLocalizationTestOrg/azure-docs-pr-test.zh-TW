---
title: "aaaCreate 和管理 Windows Azure 中的 Vm 使用多個 Nic |Microsoft 文件"
description: "深入了解如何 toocreate 和管理使用 Azure PowerShell 或資源管理員範本中有多個 Nic 附加的 tooit Windows VM。"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 9bff5b6d-79ac-476b-a68f-6f8754768413
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/05/2017
ms.author: iainfou
ms.openlocfilehash: c3c7d7569aca6f047238146d84b2ffccf05d4079
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-a-windows-virtual-machine-that-has-multiple-nics"></a>建立及管理具有多個 NIC 的 Windows 虛擬機器
在 Azure 中的虛擬機器 (Vm) 可以有多個虛擬網路介面卡 (Nic) 附加 toothem。 常見的案例是 toohave 前端和後端連線的不同子網路或網路專用 tooa 監視或備份解決方案。 這篇文章說明如何將 toocreate 具有多個 Nic VM 附加 tooit。 您也了解如何從現有的 VM tooadd 或移除 Nic。 不同的 [VM 大小](sizes.md) 支援不同數量的 NIC，因此可據以調整您的 VM。

如需詳細資訊，包括如何 toocreate 多個 Nic 內您自己的 PowerShell 指令碼，請參閱[部署多個 NIC Vm](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md)。

## <a name="prerequisites"></a>必要條件
請確定您擁有 hello[最新的 Azure PowerShell 版本安裝並設定](/powershell/azure/overview)。

在 hello 下列範例中，會取代您自己的值的範例參數名稱。 範例參數名稱包含 *myResourceGroup*、*myVnet* 和 *myVM*。


## <a name="create-a-vm-with-multiple-nics"></a>建立具有多個 NIC 的 VM
首先，建立資源群組。 hello 下列範例會建立名為的資源群組*myResourceGroup*在 hello *EastUs*位置：

```powershell
New-AzureRmResourceGroup -Name "myResourceGroup" -Location "EastUS"
```

### <a name="create-virtual-network-and-subnets"></a>建立虛擬網路和子網路
常見的案例是針對虛擬網路 toohave 兩個或多個子網路。 前端的流量，hello 其他後端流量可能會成為一個子網路。 tooconnect tooboth 子網路，然後您使用多個 Nic VM 上。

1. 使用 [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) 定義兩個虛擬網路子網路。 hello 下列範例會定義 hello 子網路的*mySubnetFrontEnd*和*mySubnetBackEnd*:

    ```powershell
    $mySubnetFrontEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetFrontEnd" `
        -AddressPrefix "192.168.1.0/24"
    $mySubnetBackEnd = New-AzureRmVirtualNetworkSubnetConfig -Name "mySubnetBackEnd" `
        -AddressPrefix "192.168.2.0/24"
    ```

2. 使用 [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) 建立虛擬網路和子網路。 hello 下列範例會建立虛擬網路，名為*myVnet*:

    ```powershell
    $myVnet = New-AzureRmVirtualNetwork -ResourceGroupName "myResourceGroup" `
        -Location "EastUs" `
        -Name "myVnet" `
        -AddressPrefix "192.168.0.0/16" `
        -Subnet $mySubnetFrontEnd,$mySubnetBackEnd
    ```


### <a name="create-multiple-nics"></a>建立多個 NIC
使用 [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) 建立兩個 NIC。 附加一個 NIC toohello 前端子網路和一個 NIC toohello 後端子。 hello 下列範例會建立名為的 Nic *myNic1*和*myNic2*:

```powershell
$frontEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetFrontEnd'}
$myNic1 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic1" `
    -Location "EastUs" `
    -SubnetId $frontEnd.Id

$backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}
$myNic2 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
    -Name "myNic2" `
    -Location "EastUs" `
    -SubnetId $backEnd.Id
```

通常您也會建立[網路安全性群組](../../virtual-network/virtual-networks-nsg.md)或[負載平衡器](../../load-balancer/load-balancer-overview.md)toohelp 管理，以及將流量分散到您的 Vm。 hello[更詳細的多個 NIC VM](../../virtual-network/virtual-network-deploy-multinic-arm-ps.md)文章將逐步引導您完成建立網路安全性群組並指派 Nic。

### <a name="create-hello-virtual-machine"></a>建立 hello 的虛擬機器
現在開始 toobuild VM 組態。 每個 VM 的大小，您可以加入 tooa VM 之 Nic 的 hello 總數的上限。 如需詳細資訊，請參閱 [Windows VM 大小](sizes.md)。

1. 設定您的 VM 認證 toohello`$cred`變數，如下所示：

    ```powershell
    $cred = Get-Credential
    ```

2. 使用 [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) 來定義您的 VM。 hello 下列範例會定義名為的 VM *myVM* ，並使用支援超過兩個 Nic VM 大小 (*Standard_DS3_v2*):

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName "myVM" -VMSize "Standard_DS3_v2"
    ```

3. 建立 VM 組態的 hello rest[組 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem)和[組 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage)。 hello 下列範例會建立 Windows Server 2016 VM:

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig `
        -Windows `
        -ComputerName "myVM" `
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig `
        -PublisherName "MicrosoftWindowsServer" `
        -Offer "WindowsServer" `
        -Skus "2016-Datacenter" `
        -Version "latest"
   ```

4. 附加您先前建立的 hello 兩個 Nic[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic1.Id -Primary
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $myNic2.Id
    ```

5. 最後，使用 [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) 建立 VM：

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName "myResourceGroup" -Location "EastUs"
    ```

## <a name="add-a-nic-tooan-existing-vm"></a>加入現有的 VM NIC tooan
加入現有的 VM 虛擬 NIC tooan，deallocate hello VM，tooadd hello 虛擬 NIC，然後啟動 hello VM。

1. 解除配置 hello 與 VM[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)。 hello 下列範例會取消配置 hello 名為 VM *myVM*中*myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. 取得 hello hello VM 之現有的組態與[Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm)。 hello 下列範例會取得名為 VM hello 資訊*myVM*中*myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. hello 下列範例會建立虛擬 NIC 與[新增 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface)名為*myNic3*太附加*mySubnetBackEnd*。 hello 虛擬 NIC，就會附加 toohello 名為 VM *myVM*中*myResourceGroup*與[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface):

    ```powershell
    # Get info for hello back end subnet
    $myVnet = Get-AzureRmVirtualNetwork -Name "myVnet" -ResourceGroupName "myResourceGroup"
    $backEnd = $myVnet.Subnets|?{$_.Name -eq 'mySubnetBackEnd'}

    # Create a virtual NIC
    $myNic3 = New-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" `
        -Name "myNic3" `
        -Location "EastUs" `
        -SubnetId $backEnd.Id

    # Get hello ID of hello new virtual NIC and add tooVM
    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "MyNic3").Id
    Add-AzureRmVMNetworkInterface -VM $vm -Id $nicId | Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```

    ### <a name="primary-virtual-nics"></a>主要虛擬 NIC
    其中一個 hello Nic 上的多個 NIC VM 需要 toobe 主要。 如果其中一個 hello 現有的虛擬 Nic 上 hello VM 已設定為主要，則可以略過此步驟。 hello 下列範例假設兩個虛擬 Nic 現在會出現在 VM 上，且您想 tooadd hello 第一個 NIC (`[0]`) 做為主要的 hello:
        
    ```powershell
    # List existing NICs on hello VM and find which one is primary
    $vm.NetworkProfile.NetworkInterfaces
    
    # Set NIC 0 toobe primary
    $vm.NetworkProfile.NetworkInterfaces[0].Primary = $true
    $vm.NetworkProfile.NetworkInterfaces[1].Primary = $false
    
    # Update hello VM state in Azure
    Update-AzureRmVM -VM $vm -ResourceGroupName "myResourceGroup"
    ```

4. 啟動 hello 與 VM[開始 AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -ResourceGroupName "myResourceGroup" -Name "myVM"
    ```

## <a name="remove-a-nic-from-an-existing-vm"></a>從現有的 VM 移除 NIC
tooremove 虛擬 NIC 從現有的 VM 解除配置 hello VM、 移除 hello 虛擬 NIC，然後開始 hello VM。

1. 解除配置 hello 與 VM[停止 AzureRmVM](/powershell/module/azurerm.compute/stop-azurermvm)。 hello 下列範例會取消配置 hello 名為 VM *myVM*中*myResourceGroup*:

    ```powershell
    Stop-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

2. 取得 hello hello VM 之現有的組態與[Get AzureRmVm](/powershell/module/azurerm.compute/get-azurermvm)。 hello 下列範例會取得名為 VM hello 資訊*myVM*中*myResourceGroup*:

    ```powershell
    $vm = Get-AzureRmVm -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```

3. 取得資訊 hello 與移除 NIC [Get AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface)。 hello 下列範例會取得資訊的相關*myNic3*:

    ```powershell
    # List existing NICs on hello VM if you need toodetermine NIC name
    $vm.NetworkProfile.NetworkInterfaces

    $nicId = (Get-AzureRmNetworkInterface -ResourceGroupName "myResourceGroup" -Name "myNic3").Id   
    ```

4. 移除 hello 與 NIC[移除 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/remove-azurermvmnetworkinterface)然後更新 hello 與 VM[更新 AzureRmVm](/powershell/module/azurerm.compute/update-azurermvm)。 hello 下列範例會移除*myNic3*取得的`$nicId`hello 前面步驟中：

    ```powershell
    Remove-AzureRmVMNetworkInterface -VM $vm -NetworkInterfaceIDs $nicId | `
        Update-AzureRmVm -ResourceGroupName "myResourceGroup"
    ```   

5. 啟動 hello 與 VM[開始 AzureRmVm](/powershell/module/azurerm.compute/start-azurermvm):

    ```powershell
    Start-AzureRmVM -Name "myVM" -ResourceGroupName "myResourceGroup"
    ```   

## <a name="create-multiple-nics-with-templates"></a>使用範本建立多個 NIC
Azure 資源管理員範本提供方式 toocreate 資源的多個執行個體在部署期間，例如建立多個 Nic。 資源管理員範本使用宣告式的 JSON 檔案 toodefine 環境。 如需詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)。 您可以使用*複製*執行個體 toocreate toospecify hello 數目：

```json
"copy": {
    "name": "multiplenics",
    "count": "[parameters('count')]"
}
```

如需詳細資訊，請參閱[使用 copy 建立多個執行個體](../../resource-group-create-multiple.md)。 

您也可以使用`copyIndex()`tooappend 數字的 tooa 資源名稱。 接著可以建立 myNic1、MyNic2 等等。 hello 下列程式碼顯示附加 hello 索引值的範例：

```json
"name": "[concat('myNic', copyIndex())]", 
```

您可以閱讀[使用 Resource Manager 範本建立多個 NIC](../../virtual-network/virtual-network-deploy-multinic-arm-template.md)的完整範例。

## <a name="next-steps"></a>後續步驟
檢閱[Windows VM 大小](sizes.md)當您嘗試 toocreate 具有多個 Nic VM。 請注意 toohello 最大數目的每個 VM 大小所支援的 Nic。 


