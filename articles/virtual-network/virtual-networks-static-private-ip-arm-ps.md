---
title: "適用於 Vm 的 Azure PowerShell aaaConfigure 私人 IP 位址 |Microsoft 文件"
description: "了解如何 tooconfigure 私人 IP 位址的虛擬機器使用 PowerShell。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: d5f18929-15e3-40a2-9ee3-8188bc248ed8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4a3eb67de583e08208fcab40de1c2a8a9b65618c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="d365b-103">使用 PowerShell 設定虛擬機器的私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d365b-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="d365b-104">Azure 有兩個部署模型：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="d365b-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="d365b-105">Microsoft 建議您建立透過 hello Resource Manager 部署模型的資源。</span><span class="sxs-lookup"><span data-stu-id="d365b-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="d365b-106">深入了解 toolearn hello hello 兩個模型之間的差異讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="d365b-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="d365b-107">本文涵蓋 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="d365b-107">This article covers hello Resource Manager deployment model.</span></span> <span data-ttu-id="d365b-108">您也可以[管理 hello 傳統部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="d365b-108">You can also [manage static private IP address in hello classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="d365b-109">hello 範例 PowerShell 預期簡單的環境中已經建立下列命令會根據上面的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="d365b-109">hello sample PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="d365b-110">如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境中所述[建立 vnet](virtual-networks-create-vnet-arm-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="d365b-110">If you want toorun hello commands as they are displayed in this document, first build hello test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="d365b-111">建立具有靜態私人 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="d365b-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="d365b-112">名為的 VM toocreate *DNS01*在 hello*前端*名為 VNet 的子網路*TestVNet*以靜態私人 ip 位址的*192.168.1.101*，請遵循下列步驟執行 hello:</span><span class="sxs-lookup"><span data-stu-id="d365b-112">toocreate a VM named *DNS01* in hello *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow hello steps below:</span></span>

1. <span data-ttu-id="d365b-113">設定 hello 儲存體帳戶、 位置、 資源群組，以及使用認證 toobe 的變數。</span><span class="sxs-lookup"><span data-stu-id="d365b-113">Set variables for hello storage account, location, resource group, and credentials toobe used.</span></span> <span data-ttu-id="d365b-114">Hello VM，您將需要 tooenter 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d365b-114">You will need tooenter a user name and password for hello VM.</span></span> <span data-ttu-id="d365b-115">hello 儲存體帳戶和資源群組必須已經存在。</span><span class="sxs-lookup"><span data-stu-id="d365b-115">hello storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type hello name and password of hello local administrator account."
    ```

2. <span data-ttu-id="d365b-116">擷取 hello 虛擬網路和子網路要 toocreate hello VM 中。</span><span class="sxs-lookup"><span data-stu-id="d365b-116">Retrieve hello virtual network and subnet you want toocreate hello VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="d365b-117">如有必要，建立公用 IP 位址 tooaccess hello VM 從 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="d365b-117">If necessary, create a public IP address tooaccess hello VM from hello Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="d365b-118">建立使用 hello 靜態私人 IP 位址要 tooassign toohello VM NIC。</span><span class="sxs-lookup"><span data-stu-id="d365b-118">Create a NIC using hello static private IP address you want tooassign toohello VM.</span></span> <span data-ttu-id="d365b-119">請確定 hello IP 是您要加入的 hello 子網路範圍內 hello VM。</span><span class="sxs-lookup"><span data-stu-id="d365b-119">Make sure hello IP is from hello subnet range you are adding hello VM to.</span></span> <span data-ttu-id="d365b-120">這是這個發行項，其中您設定私用 IP toobe hello 靜態 hello 主要步驟。</span><span class="sxs-lookup"><span data-stu-id="d365b-120">This is hello main step for this article, where you set hello private IP toobe static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="d365b-121">建立的 hello 使用 hello NIC VM 上面所建立。</span><span class="sxs-lookup"><span data-stu-id="d365b-121">Create hello VM using hello NIC created above.</span></span>

    ```powershell
    $vm = New-AzureRmVMConfig -VMName DNS01 -VMSize "Standard_A1"
    $vm = Set-AzureRmVMOperatingSystem -VM $vm -Windows -ComputerName DNS01 `
    -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm = Set-AzureRmVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri = $storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/WindowsVMosDisk.vhd"
    $vm = Set-AzureRmVMOSDisk -VM $vm -Name "windowsvmosdisk" -VhdUri $osDiskUri `
    -CreateOption fromImage
    New-AzureRmVM -ResourceGroupName $rgName -Location $locName -VM $vm 
    ```

    <span data-ttu-id="d365b-122">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d365b-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="d365b-123">擷取網路介面的靜態私人 IP 位址資訊</span><span class="sxs-lookup"><span data-stu-id="d365b-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="d365b-124">tooview hello 靜態私人 IP 位址建立 VM 與 hello 指令碼，請執行下列 PowerShell 命令的 hello hello 資訊，並觀察 hello 值*PrivateIpAddress*和*將 PrivateIpAllocationMethod*:</span><span class="sxs-lookup"><span data-stu-id="d365b-124">tooview hello static private IP address information for hello VM created with hello script above, run hello following PowerShell command and observe hello values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="d365b-125">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d365b-125">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/DNS01"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Static",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="d365b-126">從網路介面移除靜態私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="d365b-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="d365b-127">tooremove hello 靜態私人 IP 位址執行下列 PowerShell 命令的 hello 上方的 hello 指令碼中加入 toohello VM:</span><span class="sxs-lookup"><span data-stu-id="d365b-127">tooremove hello static private IP address added toohello VM in hello script above, run hello following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="d365b-128">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="d365b-128">Expected output:</span></span>

    Name                 : TestNIC
    ResourceGroupName    : TestRG
    Location             : centralus
    Id                   : /subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC
    Etag                 : W/"[Id]"
    ProvisioningState    : Succeeded
    Tags                 : 
    VirtualMachine       : {
                             "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/WindowsVM"
                           }
    IpConfigurations     : [
                             {
                               "Name": "ipconfig1",
                               "Etag": "W/\"[Id]\"",
                               "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/TestNIC/ipConfigurations/ipconfig1",
                               "PrivateIpAddress": "192.168.1.101",
                               "PrivateIpAllocationMethod": "Dynamic",
                               "Subnet": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd"
                               },
                               "PublicIpAddress": {
                                 "Id": "/subscriptions/[Id]/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP"
                               },
                               "LoadBalancerBackendAddressPools": [],
                               "LoadBalancerInboundNatRules": [],
                               "ProvisioningState": "Succeeded"
                             }
                           ]
    DnsSettings          : {
                             "DnsServers": [],
                             "AppliedDnsServers": [],
                             "InternalDnsNameLabel": null,
                             "InternalFqdn": null
                           }
    EnableIPForwarding   : False
    NetworkSecurityGroup : null
    Primary              : True

## <a name="add-a-static-private-ip-address-tooa-network-interface"></a><span data-ttu-id="d365b-129">新增靜態私人 IP 位址 tooa 網路介面</span><span class="sxs-lookup"><span data-stu-id="d365b-129">Add a static private IP address tooa network interface</span></span>
<span data-ttu-id="d365b-130">tooadd 靜態私人 IP 位址 toohello VM 建立使用 hello 指令碼，請執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d365b-130">tooadd a static private IP address toohello VM created using hello script above, run hello following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-hello-allocation-method-for-a-private-ip-address-assigned-tooa-network-interface"></a><span data-ttu-id="d365b-131">變更指派 tooa 網路介面的私用 IP 位址的 hello 配置方法</span><span class="sxs-lookup"><span data-stu-id="d365b-131">Change hello allocation method for a private IP address assigned tooa network interface</span></span>

<span data-ttu-id="d365b-132">私人 IP 位址會指派 tooa NIC 與 hello 靜態或動態配置方法。</span><span class="sxs-lookup"><span data-stu-id="d365b-132">A private IP address is assigned tooa NIC with hello static or dynamic allocation method.</span></span> <span data-ttu-id="d365b-133">開始之前 hello 在 VM 停止 （取消配置） 的狀態之後，可以變更的動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d365b-133">Dynamic IP addresses can change after starting a VM that was previously in hello stopped (deallocated) state.</span></span> <span data-ttu-id="d365b-134">這可能會造成問題，如果 hello VM 裝載的服務需要 hello 相同的 IP 位址，即使之後重新啟動時從已停止 （取消配置） 狀態。</span><span class="sxs-lookup"><span data-stu-id="d365b-134">This can potentially cause issues if hello VM is hosting a service that requires hello same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="d365b-135">刪除 hello VM 之前，仍會保留靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="d365b-135">Static IP addresses are retained until hello VM is deleted.</span></span> <span data-ttu-id="d365b-136">IP 位址，執行下列指令碼，從動態 toostatic 變更 hello 配置方法的 hello toochange hello 分派方法。</span><span class="sxs-lookup"><span data-stu-id="d365b-136">toochange hello allocation method of an IP address, run hello following script, which changes hello allocation method from dynamic toostatic.</span></span> <span data-ttu-id="d365b-137">如果靜態 hello hello 目前私人 IP 位址配置方法，請變更*靜態*太*動態*之前執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="d365b-137">If hello allocation method for hello current private IP address is static, change *Static* too*Dynamic* before executing hello script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "hello allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for hello IP address" $IP"." -NoNewline
```

<span data-ttu-id="d365b-138">如果您不知道 hello NIC hello 名稱，您可以檢視資源群組內的 Nic 清單，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="d365b-138">If you don't know hello name of hello NIC, you can view a list of NICs within a resource group by entering hello following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="d365b-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d365b-139">Next steps</span></span>
* <span data-ttu-id="d365b-140">深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="d365b-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d365b-141">深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="d365b-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="d365b-142">請參閱 hello[保留 IP REST Api](https://msdn.microsoft.com/library/azure/dn722420.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d365b-142">Consult hello [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

