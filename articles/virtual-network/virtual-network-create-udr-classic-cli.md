---
title: "在 Azure 虛擬網路的 CLI-傳統路由 aaaControl |Microsoft 文件"
description: "了解如何使用 Vnet 中的路由 toocontrol hello hello 傳統部署模型中的 Azure CLI"
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
ms.openlocfilehash: 07dde573f1a605bf280156c261d51e213ede0cdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="control-routing-and-use-virtual-appliances-classic-using-hello-azure-cli"></a><span data-ttu-id="b4c0a-103">控制路由和使用 （傳統） 的虛擬應用程式使用 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4c0a-103">Control routing and use virtual appliances (classic) using hello Azure CLI</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b4c0a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b4c0a-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="b4c0a-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b4c0a-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="b4c0a-106">範本</span><span class="sxs-lookup"><span data-stu-id="b4c0a-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="b4c0a-107">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="b4c0a-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="b4c0a-108">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="b4c0a-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="b4c0a-109">本文涵蓋 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-109">This article covers hello classic deployment model.</span></span> <span data-ttu-id="b4c0a-110">您也可以[控制路由，並在 hello Resource Manager 部署模型中使用虛擬應用裝置](virtual-network-create-udr-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-110">You can also [control routing and use virtual appliances in hello Resource Manager deployment model](virtual-network-create-udr-arm-cli.md).</span></span>

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="b4c0a-111">下列的 hello 範例 Azure CLI 命令預期已經根據上述的 hello 案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-111">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="b4c0a-112">如果您想 toorun hello 命令，因為它們會顯示在此文件，建立所示的 hello 環境[建立 VNet （傳統） 使用 Azure CLI hello](virtual-networks-create-vnet-classic-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-112">If you want toorun hello commands as they are displayed in this document, create hello environment shown in [create a VNet (classic) using hello Azure CLI](virtual-networks-create-vnet-classic-cli.md).</span></span>

[!INCLUDE [azure-cli-prerequisites-include.md](../../includes/azure-cli-prerequisites-include.md)]

## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="b4c0a-113">建立 hello UDR hello 前端子網路</span><span class="sxs-lookup"><span data-stu-id="b4c0a-113">Create hello UDR for hello front end subnet</span></span>
<span data-ttu-id="b4c0a-114">toocreate hello 路由表和路由所需的 hello 前端子網路，根據 hello 案例以上版本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-114">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="b4c0a-115">執行下列命令 tooswitch tooclassic 模式 hello:</span><span class="sxs-lookup"><span data-stu-id="b4c0a-115">Run hello following command tooswitch tooclassic mode:</span></span>

    ```azurecli
    azure config mode asm
    ```

    <span data-ttu-id="b4c0a-116">輸出：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-116">Output:</span></span>

        info:    New mode is asm

2. <span data-ttu-id="b4c0a-117">執行下列命令 toocreate hello hello 前端子網路路由表：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-117">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="b4c0a-118">輸出：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-118">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Creating route table "UDR-FrontEnd"
        info:    Getting route table "UDR-FrontEnd"
        data:    Name                            : UDR-FrontEnd
        data:    Location                        : West US
        info:    network route-table create command OK
   
    <span data-ttu-id="b4c0a-119">參數：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-119">Parameters:</span></span>
   
   * <span data-ttu-id="b4c0a-120">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-120">**-l (or --location)**.</span></span> <span data-ttu-id="b4c0a-121">Hello 新的 NSG 建立所在的 azure 區域。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-121">Azure region where hello new NSG will be created.</span></span> <span data-ttu-id="b4c0a-122">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-122">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="b4c0a-123">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-123">**-n (or --name)**.</span></span> <span data-ttu-id="b4c0a-124">名稱 hello 新的 NSG。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-124">Name for hello new NSG.</span></span> <span data-ttu-id="b4c0a-125">在本文案例中為 *NSG-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-125">For our scenario, *NSG-FrontEnd*.</span></span>
3. <span data-ttu-id="b4c0a-126">執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 後端子 (192.168.2.0/24) toohello **FW1** VM (已將 192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="b4c0a-126">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

    <span data-ttu-id="b4c0a-127">輸出：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-127">Output:</span></span>
   
        info:    Executing command network route-table route set
        info:    Getting route table "UDR-FrontEnd"
        info:    Setting route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    network route-table route set command OK
   
    <span data-ttu-id="b4c0a-128">參數：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-128">Parameters:</span></span>
   
   * <span data-ttu-id="b4c0a-129">**-r (或 --route-table-name)**。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-129">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="b4c0a-130">將會加入 hello 路由 hello 路由表的名稱。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-130">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="b4c0a-131">在本文案例中為 *UDR-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-131">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="b4c0a-132">**-a (或 --address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-132">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="b4c0a-133">Hello 封包會指向其中的子網路的位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-133">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="b4c0a-134">在本文案例中為 *192.168.2.0/24*。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-134">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="b4c0a-135">**-t (或 --next-hop-type)**。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-135">**-t (or --next-hop-type)**.</span></span> <span data-ttu-id="b4c0a-136">將傳送流量的目標物件類型。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-136">Type of object traffic will be sent to.</span></span> <span data-ttu-id="b4c0a-137">可能的值為 VirtualAppliance、VirtualNetworkGateway、VNETLocal、Internet 或 None。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-137">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="b4c0a-138">**-p (或 --next-hop-ip-address)**。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-138">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="b4c0a-139">下個躍點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-139">IP address for next hop.</span></span> <span data-ttu-id="b4c0a-140">在本文案例中為 *192.168.0.4*。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-140">For our scenario, *192.168.0.4*.</span></span>
4. <span data-ttu-id="b4c0a-141">Hello 執行的下列命令建立以 hello tooassociate hello 路由表**前端**子網路：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-141">Run hello following command tooassociate hello route table created with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="b4c0a-142">輸出：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-142">Output:</span></span>
   
        info:    Executing command network vnet subnet route-table add
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up network configuration
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        info:    Associating route table "UDR-FrontEnd" and subnet "FrontEnd"
        info:    Looking up network gateway route tables in virtual network "TestVNet" subnet "FrontEnd"
        data:    Route table name                : UDR-FrontEnd
        data:      Location                      : West US
        data:      Routes:
        info:    network vnet subnet route-table add command OK    
   
    <span data-ttu-id="b4c0a-143">參數：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-143">Parameters:</span></span>
   
   * <span data-ttu-id="b4c0a-144">**-t (或 --vnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-144">**-t (or --vnet-name)**.</span></span> <span data-ttu-id="b4c0a-145">Hello hello 子網路所在的 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-145">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="b4c0a-146">在本文案例中為 *TestVNet*。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-146">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="b4c0a-147">**-n (或 --subnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-147">**-n (or --subnet-name**.</span></span> <span data-ttu-id="b4c0a-148">將加入 hello 子網路 hello 路由表名稱。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-148">Name of hello subnet hello route table will be added to.</span></span> <span data-ttu-id="b4c0a-149">在本文案例中為 *FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="b4c0a-149">For our scenario, *FrontEnd*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="b4c0a-150">建立 hello UDR hello 後端子網路</span><span class="sxs-lookup"><span data-stu-id="b4c0a-150">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="b4c0a-151">toocreate hello 路由表和路由所需的 hello 後端子根據 hello 案例中，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="b4c0a-151">toocreate hello route table and route needed for hello back-end subnet based on hello scenario, complete hello following steps:</span></span>

1. <span data-ttu-id="b4c0a-152">執行下列命令 toocreate hello hello 後端子網路路由表：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-152">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -n UDR-BackEnd -l uswest
    ```

2. <span data-ttu-id="b4c0a-153">執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 前端的子網路 (192.168.1.0/24) toohello **FW1** VM (已將 192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="b4c0a-153">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route set -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -t VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="b4c0a-154">執行 hello 下列命令以 hello tooassociate hello 路由表**後端**子網路：</span><span class="sxs-lookup"><span data-stu-id="b4c0a-154">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet route-table add -t TestVNet -n BackEnd -r UDR-BackEnd
    ```

