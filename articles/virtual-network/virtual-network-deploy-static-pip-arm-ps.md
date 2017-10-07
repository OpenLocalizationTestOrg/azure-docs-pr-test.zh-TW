---
title: "aaaCreate VM 使用靜態公用 IP 位址-Azure PowerShell |Microsoft 文件"
description: "了解如何 toocreate VM 的靜態公用 IP 位址使用 PowerShell。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ad975ab9-d69f-45c1-9e45-0d3f0f51e87e
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0d2b88319cb114b8616f60dbee41e8fdc6d8b1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-powershell"></a><span data-ttu-id="0e3d4-103">使用 PowerShell 建立具有靜態公用 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="0e3d4-103">Create a VM with a static public IP address using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="0e3d4-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="0e3d4-104">Azure portal</span></span>](virtual-network-deploy-static-pip-arm-portal.md)
> * [<span data-ttu-id="0e3d4-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e3d4-105">PowerShell</span></span>](virtual-network-deploy-static-pip-arm-ps.md)
> * [<span data-ttu-id="0e3d4-106">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="0e3d4-106">Azure CLI</span></span>](virtual-network-deploy-static-pip-arm-cli.md)
> * [<span data-ttu-id="0e3d4-107">範本</span><span class="sxs-lookup"><span data-stu-id="0e3d4-107">Template</span></span>](virtual-network-deploy-static-pip-arm-template.md)
> * [<span data-ttu-id="0e3d4-108">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="0e3d4-108">PowerShell (Classic)</span></span>](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> <span data-ttu-id="0e3d4-109">Azure 建立和處理資源的部署模型有二種：[Resource Manager 和傳統](../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-109">Azure has two different deployment models for creating and working with resources:  [Resource Manager and classic](../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="0e3d4-110">本文說明如何使用 hello Resource Manager 部署模型，Microsoft 建議您針對大部分新的部署，而不是 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-110">This article covers using hello Resource Manager deployment model, which Microsoft recommends for most new deployments instead of hello classic deployment model.</span></span>

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="step-1---start-your-script"></a><span data-ttu-id="0e3d4-111">步驟 1：啟動指令碼</span><span class="sxs-lookup"><span data-stu-id="0e3d4-111">Step 1 - Start your script</span></span>
<span data-ttu-id="0e3d4-112">您可以下載用 hello 完整 PowerShell 指令碼[這裡](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1)。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-112">You can download hello full PowerShell script used [here](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/virtual-network-deploy-static-pip-arm-ps.ps1).</span></span> <span data-ttu-id="0e3d4-113">請遵循下列 toochange hello 指令碼 toowork 您環境中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-113">Follow hello steps below toochange hello script toowork in your environment.</span></span>

<span data-ttu-id="0e3d4-114">變更 hello 值 hello 變數的下列根據 hello 值要 toouse 為您的部署。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-114">Change hello values of hello variables below based on hello values you want toouse for your deployment.</span></span> <span data-ttu-id="0e3d4-115">遵循本文章中所使用的值對應 toohello 案例 hello:</span><span class="sxs-lookup"><span data-stu-id="0e3d4-115">hello following values map toohello scenario used in this article:</span></span>

```powershell
# Set variables resource group
$rgName                = "IaaSStory"
$location              = "West US"

# Set variables for VNet
$vnetName              = "WTestVNet"
$vnetPrefix            = "192.168.0.0/16"
$subnetName            = "FrontEnd"
$subnetPrefix          = "192.168.1.0/24"

# Set variables for storage
$stdStorageAccountName = "iaasstorystorage"

# Set variables for VM
$vmSize                = "Standard_A1"
$diskSize              = 127
$publisher             = "MicrosoftWindowsServer"
$offer                 = "WindowsServer"
$sku                   = "2012-R2-Datacenter"
$version               = "latest"
$vmName                = "WEB1"
$osDiskName            = "osdisk"
$nicName               = "NICWEB1"
$privateIPAddress      = "192.168.1.101"
$pipName               = "PIPWEB1"
$dnsName               = "iaasstoryws1"
```

## <a name="step-2---create-hello-necessary-resources-for-your-vm"></a><span data-ttu-id="0e3d4-116">步驟 2-建立 hello vm 所需的資源</span><span class="sxs-lookup"><span data-stu-id="0e3d4-116">Step 2 - Create hello necessary resources for your VM</span></span>
<span data-ttu-id="0e3d4-117">建立 VM 之前, 您需要的資源群組、 VNet、 公用 IP 和 NIC toobe hello VM 所使用。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-117">Before creating a VM, you need a resource group, VNet, public IP, and NIC toobe used by hello VM.</span></span>

1. <span data-ttu-id="0e3d4-118">建立新的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-118">Create a new resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name $rgName -Location $location
    ```

2. <span data-ttu-id="0e3d4-119">建立 hello VNet 和子網路。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-119">Create hello VNet and subnet.</span></span>

    ```powershell
    $vnet = New-AzureRmVirtualNetwork -ResourceGroupName $rgName -Name $vnetName `
        -AddressPrefix $vnetPrefix -Location $location

    Add-AzureRmVirtualNetworkSubnetConfig -Name $subnetName `
        -VirtualNetwork $vnet -AddressPrefix $subnetPrefix

    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```

3. <span data-ttu-id="0e3d4-120">建立 hello 公用 IP 資源。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-120">Create hello public IP resource.</span></span> 

    ```powershell
    $pip = New-AzureRmPublicIpAddress -Name $pipName -ResourceGroupName $rgName `
        -AllocationMethod Static -DomainNameLabel $dnsName -Location $location
    ```

4. <span data-ttu-id="0e3d4-121">建立 hello 與 hello 公用 IP 建立上述的子網路中的 hello VM hello 網路介面 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-121">Create hello network interface (NIC) for hello VM in hello subnet created above, with hello public IP.</span></span> <span data-ttu-id="0e3d4-122">請注意 hello 從 Azure 擷取 hello VNet 的第一個 cmdlet，這是因為必要`Set-AzureRmVirtualNetwork`已執行的 toochange hello 現有 VNet。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-122">Notice hello first cmdlet retrieving hello VNet from Azure, this is necessary since a `Set-AzureRmVirtualNetwork` was executed toochange hello existing VNet.</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -Name $vnetName -ResourceGroupName $rgName
    $subnet = Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name $subnetName
    $nic = New-AzureRmNetworkInterface -Name $nicName -ResourceGroupName $rgName `
        -Subnet $subnet -Location $location -PrivateIpAddress $privateIPAddress `
        -PublicIpAddress $pip
    ```

5. <span data-ttu-id="0e3d4-123">建立儲存體帳戶 toohost hello VM OS 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-123">Create a storage account toohost hello VM OS drive.</span></span>

    ```powershell
    $stdStorageAccount = New-AzureRmStorageAccount -Name $stdStorageAccountName `
    -ResourceGroupName $rgName -Type Standard_LRS -Location $location
    ```

## <a name="step-3---create-hello-vm"></a><span data-ttu-id="0e3d4-124">步驟 3-建立 hello VM</span><span class="sxs-lookup"><span data-stu-id="0e3d4-124">Step 3 - Create hello VM</span></span>
<span data-ttu-id="0e3d4-125">現在所有必要的資源已準備就緒，您可以建立新的 VM。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-125">Now that all necessary resources are in place, you can create a new VM.</span></span>

1. <span data-ttu-id="0e3d4-126">建立 hello hello VM 組態物件。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-126">Create hello configuration object for hello VM.</span></span>

    ```powershell
    $vmConfig = New-AzureRmVMConfig -VMName $vmName -VMSize $vmSize
    ```

2. <span data-ttu-id="0e3d4-127">取得 hello VM 本機系統管理員帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-127">Get credentials for hello VM local administrator account.</span></span>

    ```powershell
    $cred = Get-Credential -Message "Type hello name and password for hello local administrator account."
    ```

3. <span data-ttu-id="0e3d4-128">建立 VM 設定物件。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-128">Create a VM configuration object.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMOperatingSystem -VM $vmConfig -Windows -ComputerName $vmName `
        -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    ```

4. <span data-ttu-id="0e3d4-129">設定 hello hello VM 的作業系統映像。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-129">Set hello operating system image for hello VM.</span></span>

    ```powershell
    $vmConfig = Set-AzureRmVMSourceImage -VM $vmConfig -PublisherName $publisher `
        -Offer $offer -Skus $sku -Version $version
    ```

5. <span data-ttu-id="0e3d4-130">設定 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-130">Configure hello OS disk.</span></span>

    ```powershell
    $osVhdUri = $stdStorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $osDiskName + ".vhd"
    $vmConfig = Set-AzureRmVMOSDisk -VM $vmConfig -Name $osDiskName -VhdUri $osVhdUri -CreateOption fromImage
    ```

6. <span data-ttu-id="0e3d4-131">新增 hello NIC toohello VM。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-131">Add hello NIC toohello VM.</span></span>

    ```powershell
    $vmConfig = Add-AzureRmVMNetworkInterface -VM $vmConfig -Id $nic.Id -Primary
    ```

7. <span data-ttu-id="0e3d4-132">建立 hello VM。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-132">Create hello VM.</span></span>

    ```powershell
    New-AzureRmVM -VM $vmConfig -ResourceGroupName $rgName -Location $location
    ```

8. <span data-ttu-id="0e3d4-133">儲存 hello 指令碼檔案。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-133">Save hello script file.</span></span>

## <a name="step-4---run-hello-script"></a><span data-ttu-id="0e3d4-134">步驟 4-執行 hello 指令碼</span><span class="sxs-lookup"><span data-stu-id="0e3d4-134">Step 4 - Run hello script</span></span>
<span data-ttu-id="0e3d4-135">在進行任何必要的變更，並了解 hello 指令碼之後顯示上方，執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-135">After making any necessary changes, and understanding hello script show above, run hello script.</span></span> 

1. <span data-ttu-id="0e3d4-136">從 PowerShell 主控台或 PowerShell ISE 中，執行上述的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="0e3d4-136">From a PowerShell console, or PowerShell ISE, run hello script above.</span></span>
2. <span data-ttu-id="0e3d4-137">幾分鐘後應該顯示 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="0e3d4-137">hello following output should be displayed after a few minutes:</span></span>
   
        ResourceGroupName : IaaSStory
        Location          : westus
        ProvisioningState : Succeeded
        Tags              : 
        ResourceId        : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {}
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "AddressPrefix": "192.168.1.0/24"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : W/"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
        Id                : /subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        AddressSpace      : Microsoft.Azure.Commands.Network.Models.PSAddressSpace
        DhcpOptions       : Microsoft.Azure.Commands.Network.Models.PSDhcpOptions
        Subnets           : {FrontEnd}
        ProvisioningState : Succeeded
        AddressSpaceText  : {
                              "AddressPrefixes": [
                                "192.168.0.0/16"
                              ]
                            }
        DhcpOptionsText   : {
                              "DnsServers": []
                            }
        SubnetsText       : [
                              {
                                "Name": "FrontEnd",
                                "Etag": [Id],
                                "Id": "/subscriptions/[Subscription ID]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet/subnets/FrontEnd",
                                "AddressPrefix": "192.168.1.0/24",
                                "IpConfigurations": [],
                                "ProvisioningState": "Succeeded"
                              }
                            ]
        ResourceGroupName : IaaSStory
        Location          : westus
        ResourceGuid      : [Id]
        Tag               : {}
        TagsTable         : 
        Name              : WTestVNet
        Etag              : [Id]
        Id                : /subscriptions/[Subscription Id]/resourceGroups/IaaSStory/providers/Microsoft.Network/virtualNetworks/WTestVNet
   
        TrackingOperationId : [Id]
        RequestId           : [Id]
        Status              : Succeeded
        StatusCode          : OK
        Output              : 
        StartTime           : [Subscription Id]
        EndTime             : [Subscription Id]
        Error               : 
        ErrorText           : 

