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
# <a name="create-a-virtual-network-using-powershell"></a><span data-ttu-id="8558a-103">使用 PowerShell 建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="8558a-103">Create a virtual network using PowerShell</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="8558a-104">Azure 有兩個部署模型：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="8558a-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="8558a-105">Microsoft 建議您建立透過 hello Resource Manager 部署模型的資源。</span><span class="sxs-lookup"><span data-stu-id="8558a-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="8558a-106">深入了解 toolearn hello hello 兩個模型之間的差異讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="8558a-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>
 
<span data-ttu-id="8558a-107">本文說明如何透過 hello 資源管理員部署 VNet toocreate 模型使用 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="8558a-107">This article explains how toocreate a VNet through hello Resource Manager deployment model using PowerShell.</span></span> <span data-ttu-id="8558a-108">您也可以建立 VNet 資源管理員 」 透過使用其他工具，或從 hello 下列清單中選取不同的選項來建立 VNet 透過 hello 傳統部署模型：</span><span class="sxs-lookup"><span data-stu-id="8558a-108">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="8558a-109">入口網站</span><span class="sxs-lookup"><span data-stu-id="8558a-109">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="8558a-110">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8558a-110">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="8558a-111">CLI</span><span class="sxs-lookup"><span data-stu-id="8558a-111">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="8558a-112">範本</span><span class="sxs-lookup"><span data-stu-id="8558a-112">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="8558a-113">入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="8558a-113">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="8558a-114">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="8558a-114">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="8558a-115">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="8558a-115">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="8558a-116">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="8558a-116">Create a virtual network</span></span>

<span data-ttu-id="8558a-117">toocreate 虛擬網路使用 PowerShell，完成 hello 下列步驟：</span><span class="sxs-lookup"><span data-stu-id="8558a-117">toocreate a virtual network using PowerShell, complete hello following steps:</span></span>

1. <span data-ttu-id="8558a-118">安裝及設定 Azure PowerShell hello 中的 hello 步驟[如何 tooInstall 和設定 Azure PowerShell](/powershell/azure/overview)發行項。</span><span class="sxs-lookup"><span data-stu-id="8558a-118">Install and configure Azure PowerShell, by following hello steps in hello [How tooInstall and Configure Azure PowerShell](/powershell/azure/overview) article.</span></span>

2. <span data-ttu-id="8558a-119">如有必要，建立新的資源群組，如下所示。</span><span class="sxs-lookup"><span data-stu-id="8558a-119">If necessary, create a new resource group, as shown below.</span></span> <span data-ttu-id="8558a-120">在此案例中，會建立名為 *TestRG*的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8558a-120">For this scenario, create a resource group named *TestRG*.</span></span> <span data-ttu-id="8558a-121">如需資源群組的詳細資訊，請瀏覽 [Azure Resource Manager 概觀](../azure-resource-manager/resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8558a-121">For more information about resource groups, visit [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md).</span></span>

    ```powershell   
    New-AzureRmResourceGroup -Name TestRG -Location centralus
    ```

    <span data-ttu-id="8558a-122">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="8558a-122">Expected output:</span></span>

        ResourceGroupName : TestRG
        Location          : centralus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG    
3. <span data-ttu-id="8558a-123">建立新的 VNet，名為 *TestVNet*：</span><span class="sxs-lookup"><span data-stu-id="8558a-123">Create a new VNet named *TestVNet*:</span></span>

    ```powershell
    New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet `
    -AddressPrefix 192.168.0.0/16 -Location centralus
    ```

    <span data-ttu-id="8558a-124">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="8558a-124">Expected output:</span></span>

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
4. <span data-ttu-id="8558a-125">儲存在變數中的 hello 虛擬網路物件：</span><span class="sxs-lookup"><span data-stu-id="8558a-125">Store hello virtual network object in a variable:</span></span>

    ```powershell
    $vnet = Get-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet
    ```

   > [!TIP]
   > <span data-ttu-id="8558a-126">執行 `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus` 可以將步驟 3 和 4 結合在一起。</span><span class="sxs-lookup"><span data-stu-id="8558a-126">You can combine steps 3 and 4 by running `$vnet = New-AzureRmVirtualNetwork -ResourceGroupName TestRG -Name TestVNet -AddressPrefix 192.168.0.0/16 -Location centralus`.</span></span>
   > 

5. <span data-ttu-id="8558a-127">新增子網路 toohello VNet 變數：</span><span class="sxs-lookup"><span data-stu-id="8558a-127">Add a subnet toohello new VNet variable:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name FrontEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.1.0/24
    ```

    <span data-ttu-id="8558a-128">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="8558a-128">Expected output:</span></span>
   
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

6. <span data-ttu-id="8558a-129">重複上述步驟 5 想 toocreate 每個子網路。</span><span class="sxs-lookup"><span data-stu-id="8558a-129">Repeat step 5 above for each subnet you want toocreate.</span></span> <span data-ttu-id="8558a-130">hello 下列命令會建立 hello*後端*hello 案例中的子網路：</span><span class="sxs-lookup"><span data-stu-id="8558a-130">hello following command creates hello *BackEnd* subnet for hello scenario:</span></span>

    ```powershell
    Add-AzureRmVirtualNetworkSubnetConfig -Name BackEnd `
    -VirtualNetwork $vnet -AddressPrefix 192.168.2.0/24
    ```

7. <span data-ttu-id="8558a-131">雖然您建立子網路時，目前只存在於 hello 本機變數使用的 tooretrieve hello 您在上述的步驟 4 中建立的 VNet。</span><span class="sxs-lookup"><span data-stu-id="8558a-131">Although you create subnets, they currently only exist in hello local variable used tooretrieve hello VNet you create in step 4 above.</span></span> <span data-ttu-id="8558a-132">toosave hello 變更 tooAzure，執行下列命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="8558a-132">toosave hello changes tooAzure, run hello following command:</span></span>

    ```powershell
    Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
    ```
   
    <span data-ttu-id="8558a-133">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="8558a-133">Expected output:</span></span>
   
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

## <a name="next-steps"></a><span data-ttu-id="8558a-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8558a-134">Next steps</span></span>

<span data-ttu-id="8558a-135">深入了解如何 tooconnect:</span><span class="sxs-lookup"><span data-stu-id="8558a-135">Learn how tooconnect:</span></span>

- <span data-ttu-id="8558a-136">藉由讀取 hello 的虛擬機器 (VM) tooa 虛擬網路[建立 Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="8558a-136">A virtual machine (VM) tooa virtual network by reading hello [Create a Windows VM](../virtual-machines/virtual-machines-windows-ps-create.md) article.</span></span> <span data-ttu-id="8558a-137">而不是在 hello 步驟中的 hello 文件建立 VNet 和子網路，您可以選取的 VM 的現有 VNet 和子網路 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="8558a-137">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="8558a-138">藉由讀取 hello hello 虛擬網路的虛擬網路 tooother[連接 Vnet](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="8558a-138">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md) article.</span></span>
- <span data-ttu-id="8558a-139">使用站對站虛擬私人網路 (VPN) 或 ExpressRoute 電路 hello 虛擬網路 tooan 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="8558a-139">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="8558a-140">深入了解如何藉由讀取 hello [VNet tooan 在內部部署網路使用站對站 VPN 連線](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)和[連結 VNet tooan ExpressRoute 電路](../expressroute/expressroute-howto-linkvnet-arm.md)文件。</span><span class="sxs-lookup"><span data-stu-id="8558a-140">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-arm.md) articles.</span></span>
