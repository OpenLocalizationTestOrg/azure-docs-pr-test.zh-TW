---
title: "aaaAvailability 適用於 Windows Vm 在 Azure 中設定教學課程 |Microsoft 文件"
description: "深入了解 hello 可用性集的 Windows Azure 中的 Vm。"
documentationcenter: 
services: virtual-machines-windows
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
ms.date: 05/08/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 853775c5f126dd815c1933f9d71d2274a75ea661
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>如何 toouse 可用性設定組

在本教學課程中，您將學習如何 tooincrease hello 可用性和可靠性的虛擬機器上使用此功能的 Azure 方案的呼叫可用性設定組。 可用性設定組，請確定您在 Azure 上部署的 Vm 會分散到多個隔離的硬體叢集該 hello。 如此一來，可確保如果在 Azure 中的硬體或軟體失敗，會影響您的 Vm 子組可用且正常運作，從您的客戶使用它的 hello 觀點來看，將會保留您的整體解決方案。 

在本教學課程中，您將了解如何：

> [!div class="checklist"]
> * 建立可用性設定組
> * 在可用性設定組中建立 VM
> * 檢查可用的 VM 大小

本教學課程需要 hello Azure PowerShell 模組版本 3.6 版或更新版本。 執行` Get-Module -ListAvailable AzureRM`toofind hello 版本。 如果您需要 tooupgrade，請參閱[安裝 Azure PowerShell 模組](/powershell/azure/install-azurerm-ps)。

## <a name="availability-set-overview"></a>可用性設定組概觀

可用性設定組中您在其中放置 hello VM 資源時，都是彼此隔離的 Azure 資料中心內部署的 Azure tooensure 是一種邏輯群組功能，您可以使用。 Azure 可確保該 hello 您放置多個實體伺服器上執行可用性設定組內的 Vm、 計算機架、 儲存體單位及網路交換器。 這樣可以確保在 hello 事件中的硬體或 Azure 軟體失敗，會影響 Vm 的子集，整體應用程式將保持為設定並繼續 toobe 可用 tooyour 客戶。 使用可用性設定組時，重要的功能 tooleverage 想 toobuild 可靠的雲端解決方案。

請想想典型的 VM 架構解決方案，在此解決方案中，您可能有 4 個前端 Web 伺服器，並使用 2 個後端 VM 來裝載資料庫。 有了 Azure，您會想 toodefine 兩個可用性設定組才能部署您的 Vm: hello"web"層和一個可用性設定 hello 「 資料庫 」 層的一個可用性設定組。 當您建立新的 VM，您可以接著指定 hello 可用性設定組參數 toohello az vm 建立命令，以及 Azure 會自動確保該 hello hello 可用中所建立的 Vm 組會隔離跨多個實體硬體資源。 這表示如果 hello 實體硬體上執行您的 Web 伺服器或資料庫伺服器 Vm 的其中一個發生問題，您知道該 hello 網頁伺服器及資料庫 Vm 的其他執行個體將會繼續執行正常因為它們是在不同硬體上。

當您想在 Azure 中的 toodeploy 可靠 VM 基礎解決方案時，您應該一律使用可用性設定組。

## <a name="create-an-availability-set"></a>建立可用性設定組

您可以使用 [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset) 建立可用性設定組。 在此範例中，我們設定兩個 hello 的更新和容錯網域數目在*2* hello 可用性名為*myAvailabilitySet*在 hello *myResourceGroupAvailability*資源群組。

建立資源群組。

```powershell
New-AzureRmResourceGroup -Name myResourceGroupAvailability -Location EastUS
```


```powershell
New-AzureRmAvailabilitySet `
   -Location EastUS `
   -Name myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability `
   -Managed `
   -PlatformFaultDomainCount 2 `
   -PlatformUpdateDomainCount 2
```

## <a name="create-vms-inside-an-availability-set"></a>建立位於可用性設定組內的 VM

Vm 需要 toobe hello 可用性集 toomake 確定正確分散 hello 硬體內建立。 您無法加入現有 VM tooan 可用性設定組建立之後。 

分割的位置中的 hello 硬體 toomultiple 更新網域和故障網域。 **更新網域**是一組的 Vm 和可以重新啟動在 hello 的基礎實體硬體相同的時間。 中的 Vm hello 相同**容錯網域**共用通用的儲存體，以及通用電源來源和網路交換器。 

當您使用建立 VM 組態使用[新增 AzureRMVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig)指定 hello 可用性設定組使用 hello`-AvailabilitySetId`參數 toospecify hello 識別碼 hello 可用性設定組。

建立具有 2 個 Vm[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) hello 可用性設定。

```powershell
$availabilitySet = Get-AzureRmAvailabilitySet `
    -ResourceGroupName myResourceGroupAvailability `
    -Name myAvailabilitySet

$cred = Get-Credential -Message "Enter a username and password for hello virtual machine."

$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name mySubnet `
    -AddressPrefix 192.168.1.0/24
$vnet = New-AzureRmVirtualNetwork `
    -ResourceGroupName myResourceGroupAvailability `
    -Location EastUS `
    -Name MYvNET `
    -AddressPrefix 192.168.0.0/16 `
    -Subnet $subnetConfig

for ($i=1; $i -le 2; $i++)
{
   $pip = New-AzureRmPublicIpAddress `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name "mypublicdns$(Get-Random)" `
        -AllocationMethod Static `
        -IdleTimeoutInMinutes 4

   $nsgRuleRDP = New-AzureRmNetworkSecurityRuleConfig `
        -Name myNetworkSecurityGroupRuleRDP$i `
        -Protocol Tcp `
        -Direction Inbound `
        -Priority 1000 `
        -SourceAddressPrefix * `
        -SourcePortRange * `
        -DestinationAddressPrefix * `
        -DestinationPortRange 3389 `
        -Access Allow

   $nsg = New-AzureRmNetworkSecurityGroup `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -Name myNetworkSecurityGroup$i `
        -SecurityRules $nsgRuleRDP

   $nic = New-AzureRmNetworkInterface `
        -Name myNic$i `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -SubnetId $vnet.Subnets[0].Id `
        -PublicIpAddressId $pip.Id `
        -NetworkSecurityGroupId $nsg.Id

   # Here is where we specify hello availability set
   $vm = New-AzureRmVMConfig `
        -VMName myVM$i `
        -VMSize Standard_D1 `
        -AvailabilitySetId $availabilitySet.Id

   $vm = Set-AzureRmVMOperatingSystem `
        -VM $vm `
        -Windows -ComputerName myVM$i `   
        -Credential $cred `
        -ProvisionVMAgent `
        -EnableAutoUpdate
   $vm = Set-AzureRmVMSourceImage `
        -VM $vm `
        -PublisherName MicrosoftWindowsServer `
        -Offer WindowsServer `
        -Skus 2016-Datacenter `
        -Version latest
   $vm = Set-AzureRmVMOSDisk `
        -VM $vm `
        -Name myOsDisk$i `
        -DiskSizeInGB 128 `
        -CreateOption FromImage `
        -Caching ReadWrite
   $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
   New-AzureRmVM `
        -ResourceGroupName myResourceGroupAvailability `
        -Location EastUS `
        -VM $vm
}

```

它會採用幾分鐘的時間 toocreate 並設定這兩個 Vm。 完成時，您必須 2 的虛擬機器分散於 hello 基礎硬體。 

## <a name="check-for-available-vm-sizes"></a>檢查可用的 VM 大小 

您可以加入更多的 Vm toohello 可用性設定組更新版本中，但您需要一個 tooknow hello 硬體上可用哪些 VM 大小。 使用[Get AzureRMVMSize](/powershell/module/azurerm.compute/get-azurermvmsize) toolist hello 硬體上的 hello 可用大小叢集以 hello 可用性設定組。

```powershell
Get-AzureRmVMSize `
   -AvailabilitySetName myAvailabilitySet `
   -ResourceGroupName myResourceGroupAvailability  
```

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 建立可用性設定組
> * 在可用性設定組中建立 VM
> * 檢查可用的 VM 大小

前進 toohello 下一個教學課程的 toolearn 有關虛擬機器規模集。

> [!div class="nextstepaction"]
> [建立 VM 擴展集](tutorial-create-vmss.md)


