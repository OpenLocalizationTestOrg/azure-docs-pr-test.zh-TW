---
title: "設定 VM 的私人 IP 位址 - Azure PowerShell | Microsoft Docs"
description: "了解如何使用 PowerShell 設定虛擬機器的私人 IP 位址。"
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
ms.openlocfilehash: 2810190897c44c944912ef3325b1f40479aa3078
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-powershell"></a><span data-ttu-id="cc3f9-103">使用 PowerShell 設定虛擬機器的私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="cc3f9-103">Configure private IP addresses for a virtual machine using PowerShell</span></span>

[!INCLUDE [virtual-networks-static-private-ip-selectors-arm-include](../../includes/virtual-networks-static-private-ip-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

<span data-ttu-id="cc3f9-104">Azure 有兩個部署模型：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="cc3f9-105">Microsoft 建議透過 Resource Manager 部署模型建立資源。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="cc3f9-106">若要深入了解兩個模型的差異，請閱讀[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span> <span data-ttu-id="cc3f9-107">本文涵蓋之內容包括資源管理員部署模型。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-107">This article covers the Resource Manager deployment model.</span></span> <span data-ttu-id="cc3f9-108">您也可以 [管理傳統部署模型中的靜態私人 IP 位址](virtual-networks-static-private-ip-classic-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-108">You can also [manage static private IP address in the classic deployment model](virtual-networks-static-private-ip-classic-ps.md).</span></span>

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

<span data-ttu-id="cc3f9-109">以下的範例 PowerShell 命令會預期已根據上述案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-109">The sample PowerShell commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="cc3f9-110">如果您想要執行如本文件中所顯示的命令，請先建置 [建立 vnet](virtual-networks-create-vnet-arm-ps.md)中所說明的測試環境。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-110">If you want to run the commands as they are displayed in this document, first build the test environment described in [create a vnet](virtual-networks-create-vnet-arm-ps.md).</span></span>

## <a name="create-a-vm-with-a-static-private-ip-address"></a><span data-ttu-id="cc3f9-111">建立具有靜態私人 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="cc3f9-111">Create a VM with a static private IP address</span></span>
<span data-ttu-id="cc3f9-112">若要在名為 TestVNet 之 VNet 的FrontEnd子網路中建立名為 DNS01 且其靜態私人 IP 為 192.168.1.101 的 VM，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="cc3f9-112">To create a VM named *DNS01* in the *FrontEnd* subnet of a VNet named *TestVNet* with a static private IP of *192.168.1.101*, follow the steps below:</span></span>

1. <span data-ttu-id="cc3f9-113">針對儲存體帳戶、位置、 資源群組和要使用的認證設定變數。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-113">Set variables for the storage account, location, resource group, and credentials to be used.</span></span> <span data-ttu-id="cc3f9-114">您必須輸入 VM 的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-114">You will need to enter a user name and password for the VM.</span></span> <span data-ttu-id="cc3f9-115">儲存體帳戶和資源群組必須已經存在。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-115">The storage account and resource group must already exist.</span></span>

    ```powershell
    $stName  = "vnetstorage"
    $locName = "Central US"
    $rgName  = "TestRG"
    $cred    = Get-Credential -Message "Type the name and password of the local administrator account."
    ```

2. <span data-ttu-id="cc3f9-116">擷取虛擬網路以及您想要在其中建立 VM 的子網路。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-116">Retrieve the virtual network and subnet you want to create the VM in.</span></span>

    ```powershell
    $vnet   = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    $subnet = $vnet.Subnets[0].Id
    ```

3. <span data-ttu-id="cc3f9-117">必要時，請建立公用 IP 位址從網際網路存取 VM。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-117">If necessary, create a public IP address to access the VM from the Internet.</span></span>

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name TestPIP -ResourceGroupName $rgName `
    -Location $locName -AllocationMethod Dynamic
    ```

4. <span data-ttu-id="cc3f9-118">使用您想要指派給 VM 的靜態私人 IP 位址建立 NIC。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-118">Create a NIC using the static private IP address you want to assign to the VM.</span></span> <span data-ttu-id="cc3f9-119">請確定該 IP 來自您要新增 VM 的子網路範圍。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-119">Make sure the IP is from the subnet range you are adding the VM to.</span></span> <span data-ttu-id="cc3f9-120">這是本文中將私人 IP 設定為靜態的主要步驟。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-120">This is the main step for this article, where you set the private IP to be static.</span></span>

    ```powershell
    $nic = New-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName $rgName `
    -Location $locName -SubnetId $vnet.Subnets[0].Id -PublicIpAddressId $pip.Id `
    -PrivateIpAddress 192.168.1.101
    ```

5. <span data-ttu-id="cc3f9-121">使用上述建立的 NIC 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-121">Create the VM using the NIC created above.</span></span>

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

    <span data-ttu-id="cc3f9-122">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="cc3f9-122">Expected output:</span></span>
    
        EndTime             : [Date and time]
        Error               : 
        Output              : 
        StartTime           : [Date and time]
        Status              : Succeeded
        TrackingOperationId : [Id]
        RequestId           : [Id]
        StatusCode          : OK 

## <a name="retrieve-static-private-ip-address-information-for-a-network-interface"></a><span data-ttu-id="cc3f9-123">擷取網路介面的靜態私人 IP 位址資訊</span><span class="sxs-lookup"><span data-stu-id="cc3f9-123">Retrieve static private IP address information for a network interface</span></span>
<span data-ttu-id="cc3f9-124">如果要檢視使用上述指令碼所建立之 VM 的靜態私人 IP 位址資訊，請執行下列 PowerShell 命令並查看 *PrivateIpAddress* 和 *PrivateIpAllocationMethod* 的值：</span><span class="sxs-lookup"><span data-stu-id="cc3f9-124">To view the static private IP address information for the VM created with the script above, run the following PowerShell command and observe the values for *PrivateIpAddress* and *PrivateIpAllocationMethod*:</span></span>

```powershell
Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
```

<span data-ttu-id="cc3f9-125">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="cc3f9-125">Expected output:</span></span>

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

## <a name="remove-a-static-private-ip-address-from-a-network-interface"></a><span data-ttu-id="cc3f9-126">從網路介面移除靜態私人 IP 位址</span><span class="sxs-lookup"><span data-stu-id="cc3f9-126">Remove a static private IP address from a network interface</span></span>
<span data-ttu-id="cc3f9-127">若要移除上述指令碼中新增至 VM 的靜態私人 IP 位址，請執行下列 PowerShell 命令：</span><span class="sxs-lookup"><span data-stu-id="cc3f9-127">To remove the static private IP address added to the VM in the script above, run the following PowerShell commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Dynamic"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="cc3f9-128">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="cc3f9-128">Expected output:</span></span>

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

## <a name="add-a-static-private-ip-address-to-a-network-interface"></a><span data-ttu-id="cc3f9-129">將靜態私人 IP 位址新增至網路介面</span><span class="sxs-lookup"><span data-stu-id="cc3f9-129">Add a static private IP address to a network interface</span></span>
<span data-ttu-id="cc3f9-130">若要將靜態私人 IP 位址新增至使用上述指令碼建立之 VM，請執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="cc3f9-130">To add a static private IP address to the VM created using the script above, run the following commands:</span></span>

```powershell
$nic=Get-AzureRmNetworkInterface -Name TestNIC -ResourceGroupName TestRG
$nic.IpConfigurations[0].PrivateIpAllocationMethod = "Static"
$nic.IpConfigurations[0].PrivateIpAddress = "192.168.1.101"
Set-AzureRmNetworkInterface -NetworkInterface $nic
```
## <a name="change-the-allocation-method-for-a-private-ip-address-assigned-to-a-network-interface"></a><span data-ttu-id="cc3f9-131">針對指派至網路介面的私人 IP 位址變更配置方法</span><span class="sxs-lookup"><span data-stu-id="cc3f9-131">Change the allocation method for a private IP address assigned to a network interface</span></span>

<span data-ttu-id="cc3f9-132">私人 IP 位址是透過靜態或動態配置方法指派至 NIC。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-132">A private IP address is assigned to a NIC with the static or dynamic allocation method.</span></span> <span data-ttu-id="cc3f9-133">啟動原先處於已停止 (已解除配置) 狀態的 VM 之後，動態 IP 位址可能變更。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-133">Dynamic IP addresses can change after starting a VM that was previously in the stopped (deallocated) state.</span></span> <span data-ttu-id="cc3f9-134">即使 VM 從已停止 (已解除配置) 狀態重新啟動之後，如果 VM 裝載的服務需要相同的 IP 位址，這可能會造成問題。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-134">This can potentially cause issues if the VM is hosting a service that requires the same IP address, even after restarts from a stopped (deallocated) state.</span></span> <span data-ttu-id="cc3f9-135">靜態 IP 位址會一直保留，直到刪除 VM 為止。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-135">Static IP addresses are retained until the VM is deleted.</span></span> <span data-ttu-id="cc3f9-136">若要變更 IP 位址的配置方法，請執行下列指令碼，將配置方法從動態變更為靜態。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-136">To change the allocation method of an IP address, run the following script, which changes the allocation method from dynamic to static.</span></span> <span data-ttu-id="cc3f9-137">如果目前私人 IP 位址的配置方法是靜態，請先將 *Static* 變更為 *Dynamic*，再執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-137">If the allocation method for the current private IP address is static, change *Static* to *Dynamic* before executing the script.</span></span>

```powershell
$RG = "TestRG"
$NIC_name = "testnic1"

$nic = Get-AzureRmNetworkInterface -ResourceGroupName $RG -Name $NIC_name
$nic.IpConfigurations[0].PrivateIpAllocationMethod = 'Static'
Set-AzureRmNetworkInterface -NetworkInterface $nic 
$IP = $nic.IpConfigurations[0].PrivateIpAddress

Write-Host "The allocation method is now set to"$nic.IpConfigurations[0].PrivateIpAllocationMethod"for the IP address" $IP"." -NoNewline
```

<span data-ttu-id="cc3f9-138">如果您不知道的 NIC 的名稱，您可以輸入下列命令，檢視資源群組內的 NIC 清單︰</span><span class="sxs-lookup"><span data-stu-id="cc3f9-138">If you don't know the name of the NIC, you can view a list of NICs within a resource group by entering the following command:</span></span>

```powershell
Get-AzureRmNetworkInterface -ResourceGroupName $RG | Where-Object {$_.ProvisioningState -eq 'Succeeded'} 
```

## <a name="next-steps"></a><span data-ttu-id="cc3f9-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc3f9-139">Next steps</span></span>
* <span data-ttu-id="cc3f9-140">深入了解 [保留的公用 IP](virtual-networks-reserved-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-140">Learn about [reserved public IP](virtual-networks-reserved-public-ip.md) addresses.</span></span>
* <span data-ttu-id="cc3f9-141">深入了解 [執行個體層級公用 IP (ILPIP)](virtual-networks-instance-level-public-ip.md) 位址。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-141">Learn about [instance-level public IP (ILPIP)](virtual-networks-instance-level-public-ip.md) addresses.</span></span>
* <span data-ttu-id="cc3f9-142">請參閱 [保留 IP REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cc3f9-142">Consult the [Reserved IP REST APIs](https://msdn.microsoft.com/library/azure/dn722420.aspx).</span></span>

