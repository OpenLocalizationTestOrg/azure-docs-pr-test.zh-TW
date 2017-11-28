---
title: "控制 Azure 虛擬網路中的路由 - CLI - 傳統 | Microsoft Docs"
description: "了解如何在傳統部署模型中使用 Azure CLI 來控制 VNet 中的路由"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-service-management
ms.assetid: ca2b4638-8777-4d30-b972-eb790a7c804f
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 8fcb98723e7e872c932908e3456dc8680deb0901
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-the-azure-cli"></a><span data-ttu-id="4ebea-103">使用 Azure CLI 控制路由和使用虛擬應用裝置 (傳統)</span><span class="sxs-lookup"><span data-stu-id="4ebea-103">Control routing and use virtual appliances (classic) using the Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="4ebea-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ebea-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="4ebea-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="4ebea-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="4ebea-106">範本</span><span class="sxs-lookup"><span data-stu-id="4ebea-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="4ebea-107">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="4ebea-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="4ebea-108">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="4ebea-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="4ebea-109">本文涵蓋之內容包括傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="4ebea-109">This article covers the classic deployment model.</span></span> <span data-ttu-id="4ebea-110">您也可以 [在資源管理員部署模型中控制路由和使用虛擬應用裝置](virtual-network-create-udr-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="4ebea-110">You can also [control routing and use virtual appliances in the Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="4ebea-111">以下的範例 Azure CLI 命令是假設您已根據上述案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="4ebea-111">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="4ebea-112">如果您想要執行如本文件中所示的命令，請建立 [使用 Azure CLI 建立 VNet (傳統)](virtual-networks-create-vnet-classic-cli.md)中所示的環境。</span><span class="sxs-lookup"><span data-stu-id="4ebea-112">If you want to run the commands as they are displayed in this document, create the environment shown in [create a VNet (classic) using the Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="4ebea-113">建立前端子網路的 UDR</span><span class="sxs-lookup"><span data-stu-id="4ebea-113">Create the UDR for the front end subnet</span></span>
<span data-ttu-id="4ebea-114">若要根據上述案例建立前端子網路所需的路由表和路由，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="4ebea-114">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="4ebea-115">執行下列命令切換至傳統模式：</span><span class="sxs-lookup"><span data-stu-id="4ebea-115">Run the following command to switch to classic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="4ebea-116">輸出：</span><span class="sxs-lookup"><span data-stu-id="4ebea-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="4ebea-117">執行下列命令，建立前端子網路的路由表：</span><span class="sxs-lookup"><span data-stu-id="4ebea-117">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="4ebea-118">輸出：</span><span class="sxs-lookup"><span data-stu-id="4ebea-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="4ebea-119">參數：</span><span class="sxs-lookup"><span data-stu-id="4ebea-119">Parameters:</span></span>
   
   * <span data-ttu-id="4ebea-120">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="4ebea-120">**-l (or --location)**.</span></span> <span data-ttu-id="4ebea-121">將要建立新 NSG 的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="4ebea-121">Azure region where the new NSG will be created.</span></span> <span data-ttu-id="4ebea-122">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="4ebea-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="4ebea-123">**-n (或 --name)**。</span><span class="sxs-lookup"><span data-stu-id="4ebea-123">**-n (or --name)**.</span></span> <span data-ttu-id="4ebea-124">新 NSG 的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ebea-124">Name for the new NSG.</span></span> <span data-ttu-id="4ebea-125">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="4ebea-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="4ebea-126">執行下列命令，在上方建立的路由表中建立路由，將目的地為後端子網路 (192.168.2.0/24) 的所有流量傳送到 **FW1** VM (192.168.0.4)：</span><span class="sxs-lookup"><span data-stu-id="4ebea-126">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="4ebea-127">輸出：</span><span class="sxs-lookup"><span data-stu-id="4ebea-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="4ebea-128">參數：</span><span class="sxs-lookup"><span data-stu-id="4ebea-128">Parameters:</span></span>
   
   * <span data-ttu-id="4ebea-129">**-r (或 --route-table-name)**。</span><span class="sxs-lookup"><span data-stu-id="4ebea-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="4ebea-130">將會加入路由的路由表的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ebea-130">Name of the route table where the route will be added.</span></span> <span data-ttu-id="4ebea-131">在本文案例中為 *UDR-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="4ebea-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="4ebea-132">**-a (或 --address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="4ebea-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="4ebea-133">封包所指向位置的子網路的位址首碼。</span><span class="sxs-lookup"><span data-stu-id="4ebea-133">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="4ebea-134">在本文案例中為 *192.168.2.0/24*。</span><span class="sxs-lookup"><span data-stu-id="4ebea-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="4ebea-135">**-t (或 --next-hop-type)**。</span><span class="sxs-lookup"><span data-stu-id="4ebea-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="4ebea-136">將傳送流量的目標物件類型。</span><span class="sxs-lookup"><span data-stu-id="4ebea-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="4ebea-137">可能的值為 VirtualAppliance、VirtualNetworkGateway、VNETLocal、Internet 或 None。</span><span class="sxs-lookup"><span data-stu-id="4ebea-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="4ebea-138">**-p (或 --next-hop-ip-address)**。</span><span class="sxs-lookup"><span data-stu-id="4ebea-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="4ebea-139">下個躍點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="4ebea-139">IP address for next hop.</span></span> <span data-ttu-id="4ebea-140">在本文案例中為 *192.168.0.4*。</span><span class="sxs-lookup"><span data-stu-id="4ebea-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="4ebea-141">執行下列命令，將建立的路由表關聯至 **FrontEnd** 子網路：</span><span class="sxs-lookup"><span data-stu-id="4ebea-141">Run the following command to associate the route table created with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="4ebea-142">輸出：</span><span class="sxs-lookup"><span data-stu-id="4ebea-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="4ebea-143">參數：</span><span class="sxs-lookup"><span data-stu-id="4ebea-143">Parameters:</span></span>
   
   * <span data-ttu-id="4ebea-144">**-t (或 --vnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="4ebea-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="4ebea-145">子網路所在的 VNet 名稱。</span><span class="sxs-lookup"><span data-stu-id="4ebea-145">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="4ebea-146">在本文案例中為 *TestVNet*。</span><span class="sxs-lookup"><span data-stu-id="4ebea-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="4ebea-147">**-n (或 --subnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="4ebea-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="4ebea-148">路由表將加入的子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ebea-148">Name of the subnet the route table will be added to.</span></span> <span data-ttu-id="4ebea-149">在本文案例中為 *FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="4ebea-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="4ebea-150">建立後端子網路的 UDR</span><span class="sxs-lookup"><span data-stu-id="4ebea-150">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="4ebea-151">若要根據案例建立後端子網路所需的路由表和路徑，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4ebea-151">To create the route table and route needed for the back-end subnet based on the scenario, complete the following steps:</span></span>

1. <span data-ttu-id="4ebea-152">執行下列命令，建立後端子網路的路由表：</span><span class="sxs-lookup"><span data-stu-id="4ebea-152">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="4ebea-153">執行下列命令，在上方建立的路由表中建立路由，將目的地為前端子網路 (192.168.1.0/24) 的所有流量傳送到 **FW1** VM (192.168.0.4)：</span><span class="sxs-lookup"><span data-stu-id="4ebea-153">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="4ebea-154">執行下列命令，建立與 **BackEnd** 子網路關聯的路由表：</span><span class="sxs-lookup"><span data-stu-id="4ebea-154">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

