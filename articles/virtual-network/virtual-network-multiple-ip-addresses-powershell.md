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
# <a name="assign-multiple-ip-addresses-toovirtual-machines-using-powershell"></a>使用 PowerShell toovirtual 機器指派多個 IP 位址

[!INCLUDE [virtual-network-multiple-ip-addresses-intro.md](../../includes/virtual-network-multiple-ip-addresses-intro.md)]

本文說明如何透過 hello Azure Resource Manager 部署的虛擬機器 (VM) toocreate 模型使用 PowerShell。 Tooresources 透過 hello 傳統部署模型所建立，無法指派多個 IP 位址。 深入了解 Azure 的部署模型，讀取 hello toolearn[了解部署模型](../resource-manager-deployment-model.md)發行項。

[!INCLUDE [virtual-network-multiple-ip-addresses-template-scenario.md](../../includes/virtual-network-multiple-ip-addresses-scenario.md)]

## <a name = "create"></a>建立有多個 IP 位址的 VM

hello 遵循的步驟說明如何 toocreate 範例 VM 具有多個 IP 位址，hello 案例中所述。 請依據您的實作需求來變更變數值。

1. 開啟 PowerShell 命令提示字元，然後完成 hello 剩餘單一 PowerShell 工作階段中的這一節的步驟。 如果您還沒有 PowerShell 安裝和設定，完成 hello 步驟 hello[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。
2. 登入 tooyour 帳戶以 hello`login-azurermaccount`命令。
3. 使用您選擇的名稱和位置來取代 *myResourceGroup* 和 *westus*。 建立資源群組。 資源群組是在其中部署與管理 Azure 資源的邏輯容器。

    ```powershell
    $RgName   = "MyResourceGroup"
    $Location = "westus"

    New-AzureRmResourceGroup `
    -Name $RgName `
    -Location $Location
    ```

4. 在 hello 中建立虛擬網路 (VNet) 和子網路與 hello 資源群組相同的位置：

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

5. 建立網路安全性群組 (NSG) 和規則。 hello NSG 保護 hello VM 使用輸入和輸出規則。 在此情況下，會建立連接埠 3389 的輸入規則，以允許連入的遠端桌面連線。

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

6. 定義 hello NIC hello 主要 IP 設定 在您建立，如果您沒有使用先前定義的 hello 值 hello 子網路中變更 10.0.0.4 tooa 有效位址。 指派靜態 IP 位址之前，建議您先確認該位址尚未處於使用中。 輸入 hello 命令`Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.4 -VirtualNetwork $VNet`。 Hello 如果 hello 位址，則輸出傳回*True*。 如果沒有的話，hello 輸出傳回*False*以及一份可用的位址。 

    在下列命令，hello **hello 唯一 DNS 名稱 toouse 以取代 < 取代為與-您的唯一名稱 >。** 跨 Azure 區域內的所有公用 IP 位址，hello 名稱必須是唯一的。 這是選擇性參數。 如果您只想 tooconnect toohello VM 可以移除它使用 hello 公用 IP 位址。

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

    當您指派多個 IP 組態 tooa NIC 時，一個組態時，必須可指派為 hello *-主要*。

    > [!NOTE]
    > 公用 IP 位址需要少許費用。 進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。 沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。 深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。

7. 定義 hello 次要 IP 設定的 hello nic。 您可以視需要新增或移除組態。 每個 IP 組態都必須有一個指派的私人 IP 位址。 每個組態可以視需要有一個指派的公用 IP 位址。

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

8. 建立 hello NIC，並將三個 IP 組態 tooit hello:

    ```powershell
    
    $NIC = New-AzureRmNetworkInterface `
    -Name MyNIC `
    -ResourceGroupName $RgName `
    -Location $Location `
    -NetworkSecurityGroupId $NSG.Id `
    -IpConfiguration $IpConfig1,$IpConfig2,$IpConfig3
    ```

    >[!NOTE]
    >雖然所有組態都指派 tooone NIC 本文中的，您可以指派多個 IP 組態 tooevery 附加 NIC toohello VM。 toolearn toocreate 具有多個 Nic，VM 的讀取方式 hello[建立具有多個 Nic VM](virtual-network-deploy-multinic-arm-ps.md)發行項。

9. 輸入下列命令的 hello 建立 hello VM:

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

10. 新增 hello 私人 IP 位址 toohello VM 作業系統 hello hello 作業系統的步驟，以[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。 請勿將 hello 公用 IP 位址 toohello 作業系統。

## <a name="add"></a>新增 IP 位址 tooa VM

您可以藉由完成 hello 遵照的步驟，新增私人和公用 IP 位址 tooa NIC。 hello hello 下列各節中的範例假設您已經有含 hello 三 hello 中所述的 IP 組態的 VM[案例](#Scenario)在此文件，但它不需要您執行。

1. 開啟 PowerShell 命令提示字元，然後完成 hello 剩餘單一 PowerShell 工作階段中的這一節的步驟。 如果您還沒有 PowerShell 安裝和設定，完成 hello 步驟 hello[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。
2. 變更 hello 「 值 」 的 hello $Variables toohello 名稱的 hello 想 tooadd IP 位址 tooand hello 資源群組及位置 hello 中存在的 NIC 的 NIC 之後：

    ```powershell
    $NicName  = "MyNIC"
    $RgName   = "MyResourceGroup"
    $Location = "westus"
    ```

    如果您不知道 hello NIC 想 toochange hello 名稱，輸入下列命令，hello，然後變更 hello hello 先前的變數值：

    ```powershell
    Get-AzureRmNetworkInterface | Format-Table Name, ResourceGroupName, Location
    ```
3. 建立變數，並將它設定 toohello 現有 NIC 的輸入 hello 下列命令：

    ```powershell
    $MyNIC = Get-AzureRmNetworkInterface -Name $NicName -ResourceGroupName $RgName
    ```
4. 在 hello 下列命令，變更*MyVNet*和*MySubnet* toohello hello VNet 和子網路 hello NIC 連接到名稱。 輸入 hello 命令 tooretrieve hello VNet 和子網路物件 hello NIC 連線到：

    ```powershell
    $MyVNet = Get-AzureRMVirtualnetwork -Name MyVNet -ResourceGroupName $RgName
    $Subnet = $MyVnet.Subnets | Where-Object { $_.Name -eq "MySubnet" }
    ```
    如果您不知道 hello VNet 或子網路名稱 hello NIC 連線到，請輸入下列命令的 hello:
    ```powershell
    $MyNIC.IpConfigurations
    ```
    Hello 輸出中尋找文字類似 toohello 下列範例輸出：
    
    ```
    "Id": "/subscriptions/[Id]/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/MyVNet/subnets/MySubnet"
    ```
    在此輸出中， *MyVnet*為 hello VNet 和*MySubnet*為 hello 子網路 hello NIC 連線到。

5. 完成下列各節，您的需求為基礎的 hello 的其中一個 hello 步驟：

    **新增私人 IP 位址**

    tooadd 私用 IP 位址 tooa NIC，您必須建立 IP 組態。 hello 下列命令會建立一個設定靜態 IP 位址 10.0.0.7。 在指定的靜態 IP 位址時，它必須是未使用的 hello 子網路位址。 我們建議您先測試並使用輸入 hello hello 位址 tooensure`Test-AzureRmPrivateIPAddressAvailability -IPAddress 10.0.0.7 -VirtualNetwork $myVnet`命令。 Hello 如果 hello IP 位址，則輸出傳回*True*。 如果沒有的話，hello 輸出傳回*False*，以及一份可用的位址。

    ```powershell
    Add-AzureRmNetworkInterfaceIpConfig -Name IPConfig-4 -NetworkInterface `
    $MyNIC -Subnet $Subnet -PrivateIpAddress 10.0.0.7
    ```
    使用唯一組態名稱和私人 IP 位址 (適用於具有靜態 IP 位址的組態)，視需要建立最多的組態。

    完成您的作業系統中 hello hello 步驟新增 hello 私用 IP 位址 toohello VM 作業系統[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。

    **新增公用 IP 位址**

    公用 IP 位址是由新的 IP 設定或現有的 IP 組態關聯公用 IP 位址資源 tooeither 加入。 視需要完成 hello hello 以下各節，其中的步驟。

    > [!NOTE]
    > 公用 IP 位址需要少許費用。 進一步瞭解 IP 位址定價，toolearn 讀取 hello [IP 位址定價](https://azure.microsoft.com/pricing/details/ip-addresses)頁面。 沒有可用的訂用帳戶中的公用 IP 位址限制 toohello 數目。 深入了解 hello 限制、 讀取 hello toolearn [Azure 限制](../azure-subscription-service-limits.md#networking-limits)發行項。
    >

    - **關聯的 hello 公用 IP 位址資源 tooa 新的 IP 設定**
    
        每當您在新的 IP 組態中新增公用 IP 位址時，也必須新增私人 IP 位址，因為所有的 IP 組態都必須有一個私人 IP 位址。 您可以新增現有的公用 IP 位址資源，或建立一個新的資源。 toocreate 一個新輸入 hello 下列命令：
    
        ```powershell
        $myPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "myPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location `
        -AllocationMethod Static
        ```

        新的 IP 設定，以靜態私人 IP 位址和相關聯的 hello toocreate *myPublicIp3*公用 IP 位址資源，請輸入下列命令的 hello:

        ```powershell
        Add-AzureRmNetworkInterfaceIpConfig `
        -Name IPConfig-4 `
        -NetworkInterface $myNIC `
        -Subnet $Subnet `
        -PrivateIpAddress 10.0.0.7 `
        -PublicIpAddress $myPublicIp3
        ```

    - **關聯的 hello 公用 IP 位址資源 tooan 現有 IP 組態**

        公用 IP 位址資源只能是關聯的 tooan 還沒有相關聯的 IP 組態。 您可以判斷 IP 組態是否有相關聯的公用 IP 位址，輸入下列命令的 hello:

        ```powershell
        $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
        ```

        您會看到類似 toohello 下列輸出：

        ```     
        Name       PrivateIpAddress PublicIpAddress                                           Primary
        
        IPConfig-1 10.0.0.4         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress    True
        IPConfig-2 10.0.0.5         Microsoft.Azure.Commands.Network.Models.PSPublicIpAddress   False
        IpConfig-3 10.0.0.6                                                                     False
        ```

        因為 hello **PublicIpAddress**資料行*IpConfig 3*是空白的沒有公用 IP 位址資源是 tooit 目前相關聯。 您可以新增現有公用 IP 位址資源 tooIpConfig-3，或輸入下列其中一個命令 toocreate hello:

        ```powershell
        $MyPublicIp3 = New-AzureRmPublicIpAddress `
        -Name "MyPublicIp3" `
        -ResourceGroupName $RgName `
        -Location $Location -AllocationMethod Static
        ```

        輸入下列命令 tooassociate hello 公用 IP 位址資源 toohello 現有 IP 設定名為 hello *IpConfig 3*:
    
        ```powershell
        Set-AzureRmNetworkInterfaceIpConfig `
        -Name IpConfig-3 `
        -NetworkInterface $mynic `
        -Subnet $Subnet `
        -PublicIpAddress $myPublicIp3
        ```

6. 輸入下列命令的 hello 設定 hello NIC 與 hello 新的 IP 設定：

    ```powershell
    Set-AzureRmNetworkInterface -NetworkInterface $MyNIC
    ```

7. 檢視 hello 私人 IP 位址和 hello 公用 IP 位址資源指派的 toohello NIC 輸入 hello 下列命令：

    ```powershell   
    $MyNIC.IpConfigurations | Format-Table Name, PrivateIPAddress, PublicIPAddress, Primary
    ```
8. 完成您的作業系統中 hello hello 步驟新增 hello 私用 IP 位址 toohello VM 作業系統[新增 IP 位址 tooa VM 作業系統](#os-config)本文一節。 請勿將 hello 公用 IP 位址 toohello 作業系統。

[!INCLUDE [virtual-network-multiple-ip-addresses-os-config.md](../../includes/virtual-network-multiple-ip-addresses-os-config.md)]
