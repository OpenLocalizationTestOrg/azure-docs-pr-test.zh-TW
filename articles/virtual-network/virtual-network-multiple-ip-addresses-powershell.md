---
title: "Azure 虛擬機器-PowerShell aaaMultiple IP 位址 |Microsoft 文件"
description: "了解如何 tooassign 多個 IP 位址使用 PowerShell tooa 虛擬機器 |資源管理員。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c44ea62f-7e54-4e3b-81ef-0b132111f1f8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/24/2017
ms.author: jdial;annahar
ms.openlocfilehash: df54c4386ce13521e660a3e7208c8c1ab1459bc2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a><span data-ttu-id="ec65b-103">使用 PowerShell toovirtual 機器指派多個 IP 位址</span><span class="sxs-lookup"><span data-stu-id="ec65b-103">Assign multiple IP addresses toovirtual machines using PowerShell</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

<span data-ttu-id="ec65b-104">本文說明如何透過 hello Azure Resource Manager 部署的虛擬機器 (VM) toocreate 模型使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="ec65b-104">This article explains how toocreate a virtual machine (VM) through hello Azure Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="ec65b-105">Tooresources 透過 hello 傳統部署模型所建立，無法指派多個 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ec65b-105">Multiple IP addresses cannot be assigned tooresources created through hello classic deployment model.</span></span> <span data-ttu-id="ec65b-106">深入了解 Azure 的部署模型，讀取 hello toolearn[了解部署模型](../resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ec65b-106">toolearn more about Azure deployment models, read hello [Understand deployment models](../resource-manager-deployment-model.md) article.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <span data-ttu-id="ec65b-107"><a name = "create"></a>建立有多個 IP 位址的 VM</span><span class="sxs-lookup"><span data-stu-id="ec65b-107"><a name = "create"></a>Create a VM with multiple IP addresses</span></span>

<span data-ttu-id="ec65b-108">hello 遵循的步驟說明如何 toocreate 範例 VM 具有多個 IP 位址，hello 案例中所述。</span><span class="sxs-lookup"><span data-stu-id="ec65b-108">hello steps that follow explain how toocreate an example VM with multiple IP addresses, as described in hello scenario.</span></span> <span data-ttu-id="ec65b-109">請依據您的實作需求來變更變數值。</span><span class="sxs-lookup"><span data-stu-id="ec65b-109">Change variable values as required for your implementation.</span></span>

1. <span data-ttu-id="ec65b-110">開啟 PowerShell 命令提示字元，然後完成 hello 剩餘單一 PowerShell 工作階段中的這一節的步驟。</span><span class="sxs-lookup"><span data-stu-id="ec65b-110">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="ec65b-111">如果您還沒有 PowerShell 安裝和設定，完成 hello 步驟 hello[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。</span><span class="sxs-lookup"><span data-stu-id="ec65b-111">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="ec65b-112">登入 tooyour 帳戶以 hello`login-azurermaccount`命令。</span><span class="sxs-lookup"><span data-stu-id="ec65b-112">Login tooyour account with hello `login-azurermaccount` command.</span></span>
3. <span data-ttu-id="ec65b-113">使用您選擇的名稱和位置來取代 *myResourceGroup* 和 *westus*。</span><span class="sxs-lookup"><span data-stu-id="ec65b-113">Replace *myResourceGroup* and *westus* with a name and location of your choosing.</span></span> <span data-ttu-id="ec65b-114">建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="ec65b-114">Create a resource group.</span></span> <span data-ttu-id="ec65b-115">資源群組是在其中部署與管理 Azure 資源的邏輯容器。</span><span class="sxs-lookup"><span data-stu-id="ec65b-115">A resource group is a logical container into which Azure resources are deployed and managed.</span></span>

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. <span data-ttu-id="ec65b-116">在 hello 中建立虛擬網路 (VNet) 和子網路與 hello 資源群組相同的位置：</span><span class="sxs-lookup"><span data-stu-id="ec65b-116">Create a virtual network (VNet) and subnet in hello same location as hello resource group:</span></span>

    ```powershell
    
    # Create a subnet configuration
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
    -Name MySubnet `
    -AddressPrefix 10.0.0.0/24

    # Create a virtual network
    $VNet = New-AzureRmVirtualNetwork `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyVNet `
    -AddressPrefix 10.0.0.0/16 `
    -Subnet $subnetConfig

    # Get hello subnet object
    $Subnet = Get-AzureRmVirtualNetworkSubnetConfig -Name $SubnetConfig.Name -VirtualNetwork $VNet
    ```

5. <span data-ttu-id="ec65b-117">建立網路安全性群組 (NSG) 和規則。</span><span class="sxs-lookup"><span data-stu-id="ec65b-117">Create a network security group (NSG) and a rule.</span></span> <span data-ttu-id="ec65b-118">hello NSG 保護 hello VM 使用輸入和輸出規則。</span><span class="sxs-lookup"><span data-stu-id="ec65b-118">hello NSG secures hello VM using inbound and outbound rules.</span></span> <span data-ttu-id="ec65b-119">在此情況下，會建立連接埠 3389 的輸入規則，以允許連入的遠端桌面連線。</span><span class="sxs-lookup"><span data-stu-id="ec65b-119">In this case, an inbound rule is created for port 3389, which allows incoming remote desktop connections.</span></span>

    ```powershell
    
    # Create an inbound network security group rule for port 3389

    $NSGRule = New-AzureRmNetworkSecurityRuleConfig `
    -Name MyNsgRuleRDP `
    -Protocol Tcp `
    -Direction Inbound `
    -Priority 1000 `
    -SourceAddressPrefix * `
    -SourcePortRange * `
    -DestinationAddressPrefix * `
    -DestinationPortRange 3389 -Access Allow
    
    # Create a network security group
    $NSG = New-AzureRmNetworkSecurityGroup `
    -ResourceGroupName $RgName `
    -Location $Location `
    -Name MyNetworkSecurityGroup `
    -SecurityRules $NSGRule
    ```

6. <span data-ttu-id="ec65b-120">定義 hello NIC hello 主要 IP 設定</span><span class="sxs-lookup"><span data-stu-id="ec65b-120">Define hello primary IP configuration for hello NIC.</span></span> <span data-ttu-id="ec65b-121">在您建立，如果您沒有使用先前定義的 hello 值 hello 子網路中變更 10.0.0.4 tooa 有效位址。</span><span class="sxs-lookup"><span data-stu-id="ec65b-121">Change 10.0.0.4 tooa valid address in hello subnet you created, if you didn't use hello value defined previously.</span></span> <span data-ttu-id="ec65b-122">指派靜態 IP 位址之前，建議您先確認該位址尚未處於使用中。</span><span class="sxs-lookup"><span data-stu-id="ec65b-122">Before assigning a static IP address, it's recommended that you first confirm it's not already in use.</span></span> <span data-ttu-id="ec65b-123">輸入 hello 命令`Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`。</span><span class="sxs-lookup"><span data-stu-id="ec65b-123">Enter hello command `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`.</span></span> <span data-ttu-id="ec65b-124">Hello 如果 hello 位址，則輸出傳回*True*。</span><span class="sxs-lookup"><span data-stu-id="ec65b-124">If hello address is available, hello output returns *True*.</span></span> <span data-ttu-id="ec65b-125">如果沒有的話，hello 輸出傳回*False*以及一份可用的位址。</span><span class="sxs-lookup"><span data-stu-id="ec65b-125">If it's not available, hello output returns *False* and a list of addresses that are available.</span></span> 

    <span data-ttu-id="ec65b-126">在下列命令，hello **hello 唯一 DNS 名稱 toouse 以取代 < 取代為與-您的唯一名稱 >。**</span><span class="sxs-lookup"><span data-stu-id="ec65b-126">In hello following commands, **Replace <replace-with-your-unique-name> with hello unique DNS name toouse.**</span></span> <span data-ttu-id="ec65b-127">跨 Azure 區域內的所有公用 IP 位址，hello 名稱必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="ec65b-127">hello name must be unique across all public IP addresses within an Azure region.</span></span> <span data-ttu-id="ec65b-128">這是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="ec65b-128">This is an optional parameter.</span></span> <span data-ttu-id="ec65b-129">如果您只想 tooconnect toohello VM 可以移除它使用 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ec65b-129">It can be removed if you only want tooconnect toohello VM using hello public IP address.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP1 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP1" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -DomainNameLabel <replace-with-your-unique-name> `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName1 = "IPConfig-1"
    $IpConfig1     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName1 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.4 `
    -PublicIpAddress $PublicIP1 `
    -Primary
    ```

    <span data-ttu-id="ec65b-130">當您指派多個 IP 組態 tooa NIC 時，一個組態時，必須可指派為 hello *-主要*。</span><span class="sxs-lookup"><span data-stu-id="ec65b-130">When you assign multiple IP configurations tooa NIC, one configuration must be assigned as hello *-Primary*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ec65b-131">公用 IP 位址需要少許費用。</span><span class="sxs-lookup"><span data-stu-id="ec65b-131">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="ec65b-132">進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。</span><span class="sxs-lookup"><span data-stu-id="ec65b-132">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="ec65b-133">沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。</span><span class="sxs-lookup"><span data-stu-id="ec65b-133">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="ec65b-134">深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。</span><span class="sxs-lookup"><span data-stu-id="ec65b-134">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>

7. <span data-ttu-id="ec65b-135">定義 hello 次要 IP 設定的 hello nic。</span><span class="sxs-lookup"><span data-stu-id="ec65b-135">Define hello secondary IP configurations for hello NIC.</span></span> <span data-ttu-id="ec65b-136">您可以視需要新增或移除組態。</span><span class="sxs-lookup"><span data-stu-id="ec65b-136">You can add or remove configurations as necessary.</span></span> <span data-ttu-id="ec65b-137">每個 IP 組態都必須有一個指派的私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ec65b-137">Each IP configuration must have a private IP address assigned.</span></span> <span data-ttu-id="ec65b-138">每個組態可以視需要有一個指派的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ec65b-138">Each configuration can optionally have one public IP address assigned.</span></span>

    ```powershell
    
    # Create a public IP address
    $PublicIP2 = New-AzureRmPublicIpAddress `
    -Name "MyPublicIP2" `
    -ResourceGroupName $RgName `
    -Location $Location `
    -AllocationMethod Static
        
    #Create an IP configuration with a static private IP address and assign hello public IP ddress tooit
    $IpConfigName2 = "IPConfig-2"
    $IpConfig2     = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IpConfigName2 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.5 `
    -PublicIpAddress $PublicIP2
        
    $IpConfigName3 = "IpConfig-3"
    $IpConfig3 = New-AzureRmNetworkInterfaceIpConfig `
    -Name $IPConfigName3 `
    -Subnet $Subnet `
    -PrivateIpAddress 10.0.0.6
    ```

8. <span data-ttu-id="ec65b-139">建立 hello NIC，並將三個 IP 組態 tooit hello:</span><span class="sxs-lookup"><span data-stu-id="ec65b-139">Create hello NIC and associate hello three IP configurations tooit:</span></span>

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    ><span data-ttu-id="ec65b-140">雖然所有組態都指派 tooone NIC 本文中的，您可以指派多個 IP 組態 tooevery 附加 NIC toohello VM。</span><span class="sxs-lookup"><span data-stu-id="ec65b-140">Though all configurations are assigned tooone NIC in this article, you can assign multiple IP configurations tooevery NIC attached toohello VM.</span></span> <span data-ttu-id="ec65b-141">toolearn toocreate 具有多個 Nic，VM 的讀取方式 hello[建立具有多個 Nic VM](virtual-network-deploy-multinic-arm-ps.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="ec65b-141">toolearn how toocreate a VM with multiple NICs, read hello [Create a VM with multiple NICs](virtual-network-deploy-multinic-arm-ps.md) article.</span></span>

9. <span data-ttu-id="ec65b-142">輸入下列命令的 hello 建立 hello VM:</span><span class="sxs-lookup"><span data-stu-id="ec65b-142">Create hello VM by entering hello following commands:</span></span>

    ```powershell
    
    # Define a credential object. When you run these commands, you're prompted tooenter a sername and password for hello VM you're reating.
    $cred = Get-Credential
    
    # Create a virtual machine configuration
    $VmConfig = New-AzureRmVMConfig `
    -VMName MyVM `
    -VMSize Standard_DS1_v2 | `
    Set-AzureRmVMOperatingSystem -Windows `
    -ComputerName MyVM `
    -Credential $cred | `
    Set-AzureRmVMSourceImage `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest | `
    Add-AzureRmVMNetworkInterface `
    -Id $NIC.Id
    
    # Create hello VM
    New-AzureRmVM `
    -ResourceGroupName $RgName `
    -Location $Location `
    -VM $VmConfig
    ```

10. <span data-ttu-id="ec65b-143">新增 hello 私人 IP 位址 toohello VM 作業系統 hello hello 作業系統的步驟，以[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。</span><span class="sxs-lookup"><span data-stu-id="ec65b-143">Add hello private IP addresses toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="ec65b-144">請勿將 hello 公用 IP 位址 toohello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="ec65b-144">Do not add hello public IP addresses toohello operating system.</span></span>

## <span data-ttu-id="ec65b-145"><a name="add"></a>新增 IP 位址 tooa VM</span><span class="sxs-lookup"><span data-stu-id="ec65b-145"><a name="add"></a>Add IP addresses tooa VM</span></span>

<span data-ttu-id="ec65b-146">您可以藉由完成 hello 遵照的步驟，新增私人和公用 IP 位址 tooa NIC。</span><span class="sxs-lookup"><span data-stu-id="ec65b-146">You can add private and public IP addresses tooa NIC by completing hello steps that follow.</span></span> <span data-ttu-id="ec65b-147">hello hello 下列各節中的範例假設您已經有含 hello 三 hello 中所述的 IP 組態的 VM[案例](#Scenario)在此文件，但它不需要您執行。</span><span class="sxs-lookup"><span data-stu-id="ec65b-147">hello examples in hello following sections assume that you already have a VM with hello three IP configurations described in hello [scenario](#Scenario) in this article, but it's not required that you do.</span></span>

1. <span data-ttu-id="ec65b-148">開啟 PowerShell 命令提示字元，然後完成 hello 剩餘單一 PowerShell 工作階段中的這一節的步驟。</span><span class="sxs-lookup"><span data-stu-id="ec65b-148">Open a PowerShell command prompt and complete hello remaining steps in this section within a single PowerShell session.</span></span> <span data-ttu-id="ec65b-149">如果您還沒有 PowerShell 安裝和設定，完成 hello 步驟 hello[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。</span><span class="sxs-lookup"><span data-stu-id="ec65b-149">If you don't already have PowerShell installed and configured, complete hello steps in hello [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) article.</span></span>
2. <span data-ttu-id="ec65b-150">變更 hello 「 值 」 的 hello $Variables toohello 名稱的 hello 想 tooadd IP 位址 tooand hello 資源群組及位置 hello 中存在的 NIC 的 NIC 之後：</span><span class="sxs-lookup"><span data-stu-id="ec65b-150">Change hello "values" of hello following $Variables toohello name of hello NIC you want tooadd IP address tooand hello resource group and location hello NIC exists in:</span></span>

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    <span data-ttu-id="ec65b-151">如果您不知道 hello NIC 想 toochange hello 名稱，輸入下列命令，hello，然後變更 hello hello 先前的變數值：</span><span class="sxs-lookup"><span data-stu-id="ec65b-151">If you don't know hello name of hello NIC you want toochange, enter hello following commands, then change hello values of hello previous variables:</span></span>

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. <span data-ttu-id="ec65b-152">建立變數，並將它設定 toohello 現有 NIC 的輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="ec65b-152">Create a variable and set it toohello existing NIC by typing hello following command:</span></span>

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. <span data-ttu-id="ec65b-153">在 hello 下列命令，變更*MyVNet*和*MySubnet* toohello hello VNet 和子網路 hello NIC 連接到名稱。</span><span class="sxs-lookup"><span data-stu-id="ec65b-153">In hello following commands, change *MyVNet* and *MySubnet* toohello names of hello VNet and subnet hello NIC is connected to.</span></span> <span data-ttu-id="ec65b-154">輸入 hello 命令 tooretrieve hello VNet 和子網路物件 hello NIC 連線到：</span><span class="sxs-lookup"><span data-stu-id="ec65b-154">Enter hello commands tooretrieve hello VNet and subnet objects hello NIC is connected to:</span></span>

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    <span data-ttu-id="ec65b-155">如果您不知道 hello VNet 或子網路名稱 hello NIC 連線到，請輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec65b-155">If you don't know hello VNet or subnet name hello NIC is connected to, enter hello following command:</span></span>
    ```powershell
    $MyNIC.IpConfigurations
    ```
    <span data-ttu-id="ec65b-156">Hello 輸出中尋找文字類似 toohello 下列範例輸出：</span><span class="sxs-lookup"><span data-stu-id="ec65b-156">In hello output, look for text similar toohello following example output:</span></span>
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    <span data-ttu-id="ec65b-157">在此輸出中， *MyVnet*為 hello VNet 和*MySubnet*為 hello 子網路 hello NIC 連線到。</span><span class="sxs-lookup"><span data-stu-id="ec65b-157">In this output, *MyVnet* is hello VNet and *MySubnet* is hello subnet hello NIC is connected to.</span></span>

5. <span data-ttu-id="ec65b-158">完成下列各節，您的需求為基礎的 hello 的其中一個 hello 步驟：</span><span class="sxs-lookup"><span data-stu-id="ec65b-158">Complete hello steps in one of hello following sections, based on your requirements:</span></span>

    <span data-ttu-id="ec65b-159">**新增私人 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="ec65b-159">**Add a private IP address**</span></span>

    <span data-ttu-id="ec65b-160">tooadd 私用 IP 位址 tooa NIC，您必須建立 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="ec65b-160">tooadd a private IP address tooa NIC, you must create an IP configuration.</span></span> <span data-ttu-id="ec65b-161">hello 下列命令會建立一個設定靜態 IP 位址 10.0.0.7。</span><span class="sxs-lookup"><span data-stu-id="ec65b-161">hello following command creates a configuration with a static IP address of 10.0.0.7.</span></span> <span data-ttu-id="ec65b-162">在指定的靜態 IP 位址時，它必須是未使用的 hello 子網路位址。</span><span class="sxs-lookup"><span data-stu-id="ec65b-162">When specifying a static IP address, it must be an unused address for hello subnet.</span></span> <span data-ttu-id="ec65b-163">我們建議您先測試並使用輸入 hello hello 位址 tooensure`Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet`命令。</span><span class="sxs-lookup"><span data-stu-id="ec65b-163">It's recommended that you first test hello address tooensure it's available by entering hello `Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet` command.</span></span> <span data-ttu-id="ec65b-164">Hello 如果 hello IP 位址，則輸出傳回*True*。</span><span class="sxs-lookup"><span data-stu-id="ec65b-164">If hello IP address is available, hello output returns *True*.</span></span> <span data-ttu-id="ec65b-165">如果沒有的話，hello 輸出傳回*False*，以及一份可用的位址。</span><span class="sxs-lookup"><span data-stu-id="ec65b-165">If it's not available, hello output returns *False*, and a list of addresses that are available.</span></span>

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    <span data-ttu-id="ec65b-166">使用唯一組態名稱和私人 IP 位址 (適用於具有靜態 IP 位址的組態)，視需要建立最多的組態。</span><span class="sxs-lookup"><span data-stu-id="ec65b-166">Create as many configurations as you require, using unique configuration names and private IP addresses (for configurations with static IP addresses).</span></span>

    <span data-ttu-id="ec65b-167">完成您的作業系統中 hello hello 步驟新增 hello 私用 IP 位址 toohello VM 作業系統[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。</span><span class="sxs-lookup"><span data-stu-id="ec65b-167">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span>

    <span data-ttu-id="ec65b-168">**新增公用 IP 位址**</span><span class="sxs-lookup"><span data-stu-id="ec65b-168">**Add a public IP address**</span></span>

    <span data-ttu-id="ec65b-169">公用 IP 位址是由新的 IP 設定或現有的 IP 組態關聯公用 IP 位址資源 tooeither 加入。</span><span class="sxs-lookup"><span data-stu-id="ec65b-169">A public IP address is added by associating a public IP address resource tooeither a new IP configuration or an existing IP configuration.</span></span> <span data-ttu-id="ec65b-170">視需要完成 hello hello 以下各節，其中的步驟。</span><span class="sxs-lookup"><span data-stu-id="ec65b-170">Complete hello steps in one of hello sections that follow, as you require.</span></span>

    > [!NOTE]
    > <span data-ttu-id="ec65b-171">公用 IP 位址需要少許費用。</span><span class="sxs-lookup"><span data-stu-id="ec65b-171">Public IP addresses have a nominal fee.</span></span> <span data-ttu-id="ec65b-172">進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。</span><span class="sxs-lookup"><span data-stu-id="ec65b-172">toolearn more about IP address pricing, read hello [IP address pricing](https://azure.microsoft.com/pricing/details/ip-addresses) page.</span></span> <span data-ttu-id="ec65b-173">沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。</span><span class="sxs-lookup"><span data-stu-id="ec65b-173">There is a limit toohello number of public IP addresses that can be used in a subscription.</span></span> <span data-ttu-id="ec65b-174">深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。</span><span class="sxs-lookup"><span data-stu-id="ec65b-174">toolearn more about hello limits, read hello [Azure limits](../azure-subscription-service-limits.md#networking-limits) article.</span></span>
    >

    - <span data-ttu-id="ec65b-175">**關聯的 hello 公用 IP 位址資源 tooa 新的 IP 設定**</span><span class="sxs-lookup"><span data-stu-id="ec65b-175">**Associate hello public IP address resource tooa new IP configuration**</span></span>
    
        <span data-ttu-id="ec65b-176">每當您在新的 IP 組態中新增公用 IP 位址時，也必須新增私人 IP 位址，因為所有的 IP 組態都必須有一個私人 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="ec65b-176">Whenever you add a public IP address in a new IP configuration, you must also add a private IP address, because all IP configurations must have a private IP address.</span></span> <span data-ttu-id="ec65b-177">您可以新增現有的公用 IP 位址資源，或建立一個新的資源。</span><span class="sxs-lookup"><span data-stu-id="ec65b-177">You can either add an existing public IP address resource, or create a new one.</span></span> <span data-ttu-id="ec65b-178">toocreate 一個新輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="ec65b-178">toocreate a new one, enter hello following command:</span></span>
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        <span data-ttu-id="ec65b-179">新的 IP 設定，以靜態私人 IP 位址和相關聯的 hello toocreate *myPublicIp3*公用 IP 位址資源，請輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec65b-179">toocreate a new IP configuration with a static private IP address and hello associated *myPublicIp3* public IP address resource, enter hello following command:</span></span>

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - <span data-ttu-id="ec65b-180">**關聯的 hello 公用 IP 位址資源 tooan 現有 IP 組態**</span><span class="sxs-lookup"><span data-stu-id="ec65b-180">**Associate hello public IP address resource tooan existing IP configuration**</span></span>

        <span data-ttu-id="ec65b-181">公用 IP 位址資源只能是關聯的 tooan 還沒有相關聯的 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="ec65b-181">A public IP address resource can only be associated tooan IP configuration that doesn't already have one associated.</span></span> <span data-ttu-id="ec65b-182">您可以判斷 IP 組態是否有相關聯的公用 IP 位址，輸入下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec65b-182">You can determine whether an IP configuration has an associated public IP address by entering hello following command:</span></span>

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        <span data-ttu-id="ec65b-183">您會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="ec65b-183">You see output similar toohello following:</span></span>

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        <span data-ttu-id="ec65b-184">因為 hello **PublicIpAddress**資料行*IpConfig 3*是空白的沒有公用 IP 位址資源是 tooit 目前相關聯。</span><span class="sxs-lookup"><span data-stu-id="ec65b-184">Since hello **PublicIpAddress** column for *IpConfig-3* is blank, no public IP address resource is currently associated tooit.</span></span> <span data-ttu-id="ec65b-185">您可以新增現有公用 IP 位址資源 tooIpConfig-3，或輸入下列其中一個命令 toocreate hello:</span><span class="sxs-lookup"><span data-stu-id="ec65b-185">You can add an existing public IP address resource tooIpConfig-3, or enter hello following command toocreate one:</span></span>

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        <span data-ttu-id="ec65b-186">輸入下列命令 tooassociate hello 公用 IP 位址資源 toohello 現有 IP 設定名為 hello *IpConfig 3*:</span><span class="sxs-lookup"><span data-stu-id="ec65b-186">Enter hello following command tooassociate hello public IP address resource toohello existing IP configuration named *IpConfig-3*:</span></span>
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. <span data-ttu-id="ec65b-187">輸入下列命令的 hello 設定 hello NIC 與 hello 新的 IP 設定：</span><span class="sxs-lookup"><span data-stu-id="ec65b-187">Set hello NIC with hello new IP configuration by entering hello following command:</span></span>

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. <span data-ttu-id="ec65b-188">檢視 hello 私人 IP 位址和 hello 公用 IP 位址資源指派的 toohello NIC 輸入 hello 下列命令：</span><span class="sxs-lookup"><span data-stu-id="ec65b-188">View hello private IP addresses and hello public IP address resources assigned toohello NIC by entering hello following command:</span></span>

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. <span data-ttu-id="ec65b-189">完成您的作業系統中 hello hello 步驟新增 hello 私用 IP 位址 toohello VM 作業系統[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。</span><span class="sxs-lookup"><span data-stu-id="ec65b-189">Add hello private IP address toohello VM operating system by completing hello steps for your operating system in hello [Add IP addresses tooa VM operating system](#os-config) section of this article.</span></span> <span data-ttu-id="ec65b-190">請勿將 hello 公用 IP 位址 toohello 作業系統。</span><span class="sxs-lookup"><span data-stu-id="ec65b-190">Do not add hello public IP address toohello operating system.</span></span>

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
