---
title: "虛擬網路的 Azure PowerShell aaaCreate |Microsoft 文件"
description: "了解如何 toocreate 的虛擬網路，使用 PowerShell。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a31f4f12-54ee-4339-b968-1a8097ca77d3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8d6e395a77f71de9f94b6304b05450e46b47544f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-powershell"></a>使用 PowerShell 建立虛擬網路

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

Azure 有兩個部署模型：Azure Resource Manager 和傳統。 Microsoft 建議您建立透過 hello Resource Manager 部署模型的資源。 深入了解 toolearn hello hello 兩個模型之間的差異讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)發行項。
 
本文說明如何透過 hello 資源管理員部署 VNet toocreate 模型使用 PowerShell。 您也可以建立 VNet 資源管理員 」 透過使用其他工具，或從 hello 下列清單中選取不同的選項來建立 VNet 透過 hello 傳統部署模型：

> [!div class="op_single_selector"]
> * [入口網站](virtual-networks-create-vnet-arm-pportal.md)
> * [PowerShell](virtual-networks-create-vnet-arm-ps.md)
> * [CLI](virtual-networks-create-vnet-arm-cli.md)
> * [範本](virtual-networks-create-vnet-arm-template-click.md)
> * [入口網站 (傳統)](virtual-networks-create-vnet-classic-pportal.md)
> * [PowerShell (傳統)](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [CLI (傳統)](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a>建立虛擬網路

toocreate 虛擬網路使用 PowerShell，完成 hello 下列步驟：

1. 安裝及設定 Azure PowerShell hello 中的 hello 步驟[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。

2. 如有必要，建立新的資源群組，如下所示。 在此案例中，會建立名為 *TestRG*的資源群組。 如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    預期的輸出：

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. 建立新的 VNet，名為 *TestVNet*：

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    預期的輸出：

        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                   : W/"[Id]"
        ProvisioningState          : Succeeded
        Tags                       : 
        AddressSpace               : {
                                   "AddressPrefixes": [
                                     "192.168.0.0/16"
                                   ]
                                  }
        DhcpOptions                : {}
        Subnets                    : []
        VirtualNetworkPeerings     : []
4. 儲存在變數中的 hello 虛擬網路物件：

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > 執行 `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus` 可以將步驟 3 和 4 結合在一起。
   > 

5. 新增子網路 toohello VNet 變數：

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    預期的輸出：
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {}
        Subnets             : [
                                  {
                                    "Name": "FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24"
                                  }
                                ]
        VirtualNetworkPeerings     : []

6. 重複上述步驟 5 想 toocreate 每個子網路。 hello 下列命令會建立 hello*後端*hello 案例中的子網路：

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. 雖然您建立子網路時，目前只存在於 hello 本機變數使用的 tooretrieve hello 您在上述的步驟 4 中建立的 VNet。 toosave hello 變更 tooAzure，執行下列命令的 hello:

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    預期的輸出：
   
        Name                  : TestVNet
        ResourceGroupName     : TestRG
        Location              : centralus
        Id                    : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet
        Etag                  : W/"[Id]"
        ProvisioningState     : Succeeded
        Tags                  :
        AddressSpace          : {
                                  "AddressPrefixes": [
                                    "192.168.0.0/16"
                                  ]
                                }
        DhcpOptions           : {
                                  "DnsServers": []
                                }
        Subnets               : [
                                  {
                                    "Name": "FrontEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                                    "AddressPrefix": "192.168.1.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  },
                                  {
                                    "Name": "BackEnd",
                                    "Etag": "W/\"[Id]\"",
                                    "Id": "/subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
                                    "AddressPrefix": "192.168.2.0/24",
                                    "IpConfigurations": [],
                                    "ProvisioningState": "Succeeded"
                                  }
                                ]
        VirtualNetworkPeerings : []

## <a name="next-steps"></a>後續步驟

深入了解如何 tooconnect:

- 藉由讀取 hello 的虛擬機器 (VM) tooa 虛擬網路[建立 Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md)發行項。 而不是在 hello 步驟中的 hello 文件建立 VNet 和子網路，您可以選取的 VM 的現有 VNet 和子網路 tooconnect。
- 藉由讀取 hello hello 虛擬網路的虛擬網路 tooother[連接 Vnet](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)發行項。
- 使用站對站虛擬私人網路 (VPN) 或 ExpressRoute 電路 hello 虛擬網路 tooan 在內部部署網路。 深入了解如何藉由讀取 hello [VNet tooan 在內部部署網路使用站對站 VPN 連線](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)和[連結 VNet tooan ExpressRoute 電路](../expressroute/expressroute-howto-linkvnet-arm.md)文件。
