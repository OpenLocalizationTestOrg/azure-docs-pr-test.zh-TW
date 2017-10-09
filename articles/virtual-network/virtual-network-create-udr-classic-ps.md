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
# <a name="control-routing-and-use-virtual-appliances-classic-using-powershell"></a><span data-ttu-id="78d02-103">透過 PowerShell 控制路由和使用虛擬應用裝置 (傳統) </span><span class="sxs-lookup"><span data-stu-id="78d02-103">Control routing and use virtual appliances (classic) using PowerShell</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="78d02-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="78d02-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="78d02-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="78d02-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="78d02-106">範本</span><span class="sxs-lookup"><span data-stu-id="78d02-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="78d02-107">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="78d02-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="78d02-108">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="78d02-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

> [!IMPORTANT]
> <span data-ttu-id="78d02-109">您可以使用 Azure 資源之前，它是 Azure 目前有兩種部署模型的重要 toounderstand: Azure 資源管理員] 和 [傳統。</span><span class="sxs-lookup"><span data-stu-id="78d02-109">Before you work with Azure resources, it's important toounderstand that Azure currently has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="78d02-110">在使用任何 Azure 資源之前，請先確認您了解 [部署模型和工具](../azure-resource-manager/resource-manager-deployment-model.md) 。</span><span class="sxs-lookup"><span data-stu-id="78d02-110">Make sure you understand [deployment models and tools](../azure-resource-manager/resource-manager-deployment-model.md) before you work with any Azure resource.</span></span> <span data-ttu-id="78d02-111">您可以檢視不同的工具 hello 文件選取上方的這篇文章 hello 選項。</span><span class="sxs-lookup"><span data-stu-id="78d02-111">You can view hello documentation for different tools by selecting an option at hello top of this article.</span></span> <span data-ttu-id="78d02-112">本文涵蓋 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="78d02-112">This article covers hello classic deployment model.</span></span>
> 

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="78d02-113">hello 範例 Azure PowerShell，下列命令會預期簡單的環境中已建立根據上面的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="78d02-113">hello sample Azure PowerShell commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="78d02-114">如果您想 toorun hello 命令，因為它們會顯示在此文件，建立所示的 hello 環境[建立 VNet （傳統） 使用 PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md)。</span><span class="sxs-lookup"><span data-stu-id="78d02-114">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using PowerShell](virtual-networks-create-vnet-classic-netcfg-ps.md).</span></span>

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="78d02-115">建立 hello UDR hello 前端子網路</span><span class="sxs-lookup"><span data-stu-id="78d02-115">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="78d02-116">toocreate hello 路由表和路由所需的 hello 前端子網路，根據 hello 案例以上版本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="78d02-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="78d02-117">執行下列命令 toocreate hello hello 前端子網路路由表：</span><span class="sxs-lookup"><span data-stu-id="78d02-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-FrontEnd -Location uswest `
    -Label "Route table for front end subnet"
    ```

2. <span data-ttu-id="78d02-118">執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 後端子 (192.168.2.0/24) toohello **FW1** VM (已將 192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="78d02-118">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-FrontEnd `
    |Set-AzureRoute -RouteName RouteToBackEnd -AddressPrefix 192.168.2.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="78d02-119">執行 hello 下列命令以 hello tooassociate hello 路由表**前端**子網路：</span><span class="sxs-lookup"><span data-stu-id="78d02-119">Run hello following command tooassociate hello route table with hello **FrontEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName FrontEnd `
    -RouteTableName UDR-FrontEnd
    ```

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="78d02-120">建立 hello UDR hello 後端子網路</span><span class="sxs-lookup"><span data-stu-id="78d02-120">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="78d02-121">toocreate hello 路由表和路由所需的 hello 後結束 hello 案例為基礎的子網路，請完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="78d02-121">toocreate hello route table and route needed for hello back end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="78d02-122">執行下列命令 toocreate hello hello 後端子網路路由表：</span><span class="sxs-lookup"><span data-stu-id="78d02-122">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```powershell
    New-AzureRouteTable -Name UDR-BackEnd `
    -Location uswest `
    -Label "Route table for back end subnet"
    ```

2. <span data-ttu-id="78d02-123">執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 前端的子網路 (192.168.1.0/24) toohello **FW1** VM (已將 192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="78d02-123">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```powershell
    Get-AzureRouteTable UDR-BackEnd
    | Set-AzureRoute `
    -RouteName RouteToFrontEnd `
    -AddressPrefix 192.168.1.0/24 `
    -NextHopType VirtualAppliance `
    -NextHopIpAddress 192.168.0.4
    ```

3. <span data-ttu-id="78d02-124">執行 hello 下列命令以 hello tooassociate hello 路由表**後端**子網路：</span><span class="sxs-lookup"><span data-stu-id="78d02-124">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```powershell
    Set-AzureSubnetRouteTable -VirtualNetworkName TestVNet `
    -SubnetName BackEnd `
    -RouteTableName UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-hello-fw1-vm"></a><span data-ttu-id="78d02-125">啟用 hello FW1 VM 上的 IP 轉送</span><span class="sxs-lookup"><span data-stu-id="78d02-125">Enable IP forwarding on hello FW1 VM</span></span>

<span data-ttu-id="78d02-126">在 hello FW1 VM，完成下列步驟的 hello tooenable IP 轉送：</span><span class="sxs-lookup"><span data-stu-id="78d02-126">tooenable IP forwarding in hello FW1 VM, complete hello following steps:</span></span>

1. <span data-ttu-id="78d02-127">執行下列命令 toocheck hello 的 IP 轉送狀態的 hello:</span><span class="sxs-lookup"><span data-stu-id="78d02-127">Run hello following command toocheck hello status of IP forwarding:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Get-AzureIPForwarding
    ```

2. <span data-ttu-id="78d02-128">Hello 執行的下列命令 tooenable IP 轉送 hello *FW1* VM:</span><span class="sxs-lookup"><span data-stu-id="78d02-128">Run hello following command tooenable IP forwarding for hello *FW1* VM:</span></span>

    ```powershell
    Get-AzureVM -Name FW1 -ServiceName TestRGFW `
    | Set-AzureIPForwarding -Enable
    ```
