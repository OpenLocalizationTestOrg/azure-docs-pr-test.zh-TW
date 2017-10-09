---
title: "在 Azure 虛擬網路的 PowerShell-傳統路由 aaaControl |Microsoft 文件"
description: "深入了解如何使用 PowerShell 的 Vnet 中的路由，toocontrol |傳統"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: d8d07c16-cbe5-4536-acd6-870269346fe3
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.openlocfilehash: 36edf263fb434d5fb13310d4324da20e57f016a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a>透過 PowerShell 控制路由和使用虛擬應用裝置 (傳統) 

> [!div class="op_single_selector"]
> * [PowerShell](virtual-network-create-udr-arm-ps.md)
> * [Azure CLI](virtual-network-create-udr-arm-cli.md)
> * [範本](virtual-network-create-udr-arm-template.md)
> * [PowerShell (傳統)](virtual-network-create-udr-classic-ps.md)
> * [CLI (傳統)](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> 您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand: Azure 資源管理員] 和 [傳統。 在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-resource-manager/resource-manager-deployment-model.md) 。 您可以檢視不同的工具 hello 文件選取上方的這篇文章 hello 選項。 本文涵蓋 hello 傳統部署模型。
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

hello 範例 Azure PowerShell，下列命令會預期簡單的環境中已建立根據上面的 hello 案例。 如果您想 toorun hello 命令，因為它們會顯示在此文件，建立所示的 hello 環境[建立 VNet （傳統） 使用 PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md)。

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a>建立 hello UDR hello 前端子網路
toocreate hello 路由表和路由所需的 hello 前端子網路，根據 hello 案例以上版本，請遵循下列 hello 步驟。

1. 執行下列命令 toocreate hello hello 前端子網路路由表：

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. 執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 後端子 (192.168.2.0/24) toohello **FW1** VM (已將 192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. 執行 hello 下列命令以 hello tooassociate hello 路由表**前端**子網路：

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a>建立 hello UDR hello 後端子網路
toocreate hello 路由表和路由所需的 hello 後結束 hello 案例為基礎的子網路，請完成下列步驟的 hello:

1. 執行下列命令 toocreate hello hello 後端子網路路由表：

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. 執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 前端的子網路 (192.168.1.0/24) toohello **FW1** VM (已將 192.168.0.4):

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. 執行 hello 下列命令以 hello tooassociate hello 路由表**後端**子網路：

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a>啟用 hello FW1 VM 上的 IP 轉送

在 hello FW1 VM，完成下列步驟的 hello tooenable IP 轉送：

1. 執行下列命令 toocheck hello 的 IP 轉送狀態的 hello:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. Hello 執行的下列命令 tooenable IP 轉送 hello *FW1* VM:

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
