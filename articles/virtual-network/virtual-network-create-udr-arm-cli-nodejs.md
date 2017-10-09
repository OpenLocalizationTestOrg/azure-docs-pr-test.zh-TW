---
title: "使用 aaaControl 路由和虛擬裝置 hello Azure CLI 1.0 |Microsoft 文件"
description: "了解如何使用 toocontrol 路由和虛擬裝置 hello Azure CLI 1.0。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/18/2017
ms.author: jdial
ms.openlocfilehash: 1c8a552d949521fa554880c00405e65fa47a8162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-10"></a><span data-ttu-id="eefb7-103">建立使用者定義的路由 (UDR) 使用 hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="eefb7-103">Create User-Defined Routes (UDR) using hello Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="eefb7-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="eefb7-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="eefb7-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="eefb7-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="eefb7-106">範本</span><span class="sxs-lookup"><span data-stu-id="eefb7-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="eefb7-107">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="eefb7-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="eefb7-108">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="eefb7-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="eefb7-109">建立自訂路由和使用 Azure CLI hello 的虛擬應用裝置。</span><span class="sxs-lookup"><span data-stu-id="eefb7-109">Create custom routing and virtual appliances using hello Azure CLI.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="eefb7-110">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="eefb7-110">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="eefb7-111">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="eefb7-111">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="eefb7-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="eefb7-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="eefb7-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="eefb7-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="eefb7-114">下列的 hello 範例 Azure CLI 命令預期已經根據上述的 hello 案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="eefb7-114">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="eefb7-115">如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before)，按一下 **部署 tooAzure**，取代 hello 預設參數值如果有必要，並遵循中的 hello 指示 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="eefb7-115">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="eefb7-116">建立 hello UDR hello 前端子網路</span><span class="sxs-lookup"><span data-stu-id="eefb7-116">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="eefb7-117">toocreate hello 路由表和路由所需的 hello 前端子網路，根據 hello 案例以上版本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="eefb7-117">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="eefb7-118">執行下列命令 toocreate hello hello 前端子網路路由表：</span><span class="sxs-lookup"><span data-stu-id="eefb7-118">Run hello following command toocreate a route table for hello front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="eefb7-119">輸出：</span><span class="sxs-lookup"><span data-stu-id="eefb7-119">Output:</span></span>
   
        info:    Executing command network route-table create
        info:    Looking up route table "UDR-FrontEnd"
        info:    Creating route table "UDR-FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    Name                            : UDR-FrontEnd
        data:    Type                            : Microsoft.Network/routeTables
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        info:    network route-table create command OK
   
    <span data-ttu-id="eefb7-120">參數：</span><span class="sxs-lookup"><span data-stu-id="eefb7-120">Parameters:</span></span>
   
   * <span data-ttu-id="eefb7-121">**-g (or --resource-group)**。</span><span class="sxs-lookup"><span data-stu-id="eefb7-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="eefb7-122">將會建立 hello UDR hello 資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="eefb7-122">Name of hello resource group where hello UDR will be created.</span></span> <span data-ttu-id="eefb7-123">在本文案例中為 *TestRG*。</span><span class="sxs-lookup"><span data-stu-id="eefb7-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="eefb7-124">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="eefb7-124">**-l (or --location)**.</span></span> <span data-ttu-id="eefb7-125">Hello 新 UDR 建立所在的 azure 區域。</span><span class="sxs-lookup"><span data-stu-id="eefb7-125">Azure region where hello new UDR will be created.</span></span> <span data-ttu-id="eefb7-126">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="eefb7-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="eefb7-127">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="eefb7-127">**-n (or --name)**.</span></span> <span data-ttu-id="eefb7-128">名稱 hello 新 UDR。</span><span class="sxs-lookup"><span data-stu-id="eefb7-128">Name for hello new UDR.</span></span> <span data-ttu-id="eefb7-129">在本文案例中為 *UDR-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="eefb7-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="eefb7-130">執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 後端子 (192.168.2.0/24) toohello **FW1** VM (已將 192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="eefb7-130">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="eefb7-131">輸出：</span><span class="sxs-lookup"><span data-stu-id="eefb7-131">Output:</span></span>
   
        info:    Executing command network route-table route create
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        info:    Creating route "RouteToBackEnd" in a route table "UDR-FrontEnd"
        info:    Looking up route "RouteToBackEnd" in route table "UDR-FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd/routes/RouteToBackEnd
        data:    Name                            : RouteToBackEnd
        data:    Provisioning state              : Succeeded
        data:    Next hop type                   : VirtualAppliance
        data:    Next hop IP address             : 192.168.0.4
        data:    Address prefix                  : 192.168.2.0/24
        info:    network route-table route create command OK
   
    <span data-ttu-id="eefb7-132">參數：</span><span class="sxs-lookup"><span data-stu-id="eefb7-132">Parameters:</span></span>
   
   * <span data-ttu-id="eefb7-133">**-r (或 --route-table-name)**。</span><span class="sxs-lookup"><span data-stu-id="eefb7-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="eefb7-134">將會加入 hello 路由 hello 路由表的名稱。</span><span class="sxs-lookup"><span data-stu-id="eefb7-134">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="eefb7-135">在本文案例中為 *UDR-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="eefb7-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="eefb7-136">**-a (或 --address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="eefb7-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="eefb7-137">Hello 封包會指向其中的子網路的位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="eefb7-137">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="eefb7-138">在本文案例中為 *192.168.2.0/24*。</span><span class="sxs-lookup"><span data-stu-id="eefb7-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="eefb7-139">**-y (或 --next-hop-type)**。</span><span class="sxs-lookup"><span data-stu-id="eefb7-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="eefb7-140">將傳送流量的目標物件類型。</span><span class="sxs-lookup"><span data-stu-id="eefb7-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="eefb7-141">可能的值為 VirtualAppliance、VirtualNetworkGateway、VNETLocal、Internet 或 None。</span><span class="sxs-lookup"><span data-stu-id="eefb7-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="eefb7-142">**-p (或 --next-hop-ip-address)**。</span><span class="sxs-lookup"><span data-stu-id="eefb7-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="eefb7-143">下個躍點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="eefb7-143">IP address for next hop.</span></span> <span data-ttu-id="eefb7-144">在本文案例中為 *192.168.0.4*。</span><span class="sxs-lookup"><span data-stu-id="eefb7-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="eefb7-145">Hello 執行的下列命令以 hello 上面所建立的 tooassociate hello 路由表**前端**子網路：</span><span class="sxs-lookup"><span data-stu-id="eefb7-145">Run hello following command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="eefb7-146">輸出：</span><span class="sxs-lookup"><span data-stu-id="eefb7-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up hello subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up hello subnet "FrontEnd"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/FrontEnd
        data:    Type                            : Microsoft.Network/virtualNetworks/subnets
        data:    ProvisioningState               : Succeeded
        data:    Name                            : FrontEnd
        data:    Address prefix                  : 192.168.1.0/24
        data:    Network security group          : [object Object]
        data:    Route Table                     : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        routeTables/UDR-FrontEnd
        data:    IP configurations:
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB1/ipConf
        igurations/ipconfig1
        data:      /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/networkInterfaces/NICWEB2/ipConf
        igurations/ipconfig1
        data:    
        info:    network vnet subnet set command OK
   
    <span data-ttu-id="eefb7-147">參數：</span><span class="sxs-lookup"><span data-stu-id="eefb7-147">Parameters:</span></span>
   
   * <span data-ttu-id="eefb7-148">**-e (或 --vnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="eefb7-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="eefb7-149">Hello hello 子網路所在的 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="eefb7-149">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="eefb7-150">在本文案例中為 *TestVNet*。</span><span class="sxs-lookup"><span data-stu-id="eefb7-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="eefb7-151">建立 hello UDR hello 後端子網路</span><span class="sxs-lookup"><span data-stu-id="eefb7-151">Create hello UDR for hello back-end subnet</span></span>
<span data-ttu-id="eefb7-152">toocreate hello 路由表和路由所需的 hello 後端子根據上述步驟的完整 hello hello 案例：</span><span class="sxs-lookup"><span data-stu-id="eefb7-152">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="eefb7-153">執行下列命令 toocreate hello hello 後端子網路路由表：</span><span class="sxs-lookup"><span data-stu-id="eefb7-153">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="eefb7-154">執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 前端的子網路 (192.168.1.0/24) toohello **FW1** VM (已將 192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="eefb7-154">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="eefb7-155">執行 hello 下列命令以 hello tooassociate hello 路由表**後端**子網路：</span><span class="sxs-lookup"><span data-stu-id="eefb7-155">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="eefb7-156">啟用 FW1 上的 IP 轉送</span><span class="sxs-lookup"><span data-stu-id="eefb7-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="eefb7-157">tooenable 在 hello NIC 所使用的 IP 轉送**FW1**，完成下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="eefb7-157">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="eefb7-158">執行之後，請注意 hello 值 hello 命令**啟用 IP 轉送**。</span><span class="sxs-lookup"><span data-stu-id="eefb7-158">Run hello command that follows and notice hello value for **Enable IP forwarding**.</span></span> <span data-ttu-id="eefb7-159">才應該設定太*false*。</span><span class="sxs-lookup"><span data-stu-id="eefb7-159">It should be set too*false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="eefb7-160">輸出：</span><span class="sxs-lookup"><span data-stu-id="eefb7-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : false
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic show command OK
2. <span data-ttu-id="eefb7-161">執行下列命令 tooenable IP 轉送的 hello:</span><span class="sxs-lookup"><span data-stu-id="eefb7-161">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="eefb7-162">輸出：</span><span class="sxs-lookup"><span data-stu-id="eefb7-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up hello network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up hello network interface "NICFW1"
        data:    Id                              : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        networkInterfaces/NICFW1
        data:    Name                            : NICFW1
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : westus
        data:    Provisioning state              : Succeeded
        data:    MAC address                     : 00-0D-3A-30-95-B3
        data:    Enable IP forwarding            : true
        data:    Tags                            : displayName=NetworkInterfaces - DMZ
        data:    Virtual machine                 : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Compute/
        virtualMachines/FW1
        data:    IP configurations:
        data:      Name                          : ipconfig1
        data:      Provisioning state            : Succeeded
        data:      Public IP address             : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        publicIPAddresses/PIPFW1
        data:      Private IP address            : 192.168.0.4
        data:      Private IP Allocation Method  : Static
        data:      Subnet                        : /subscriptions/[Subscription Id]/resourceGroups/TestRG/providers/Microsoft.Network/
        virtualNetworks/TestVNet/subnets/DMZ
        data:    
        info:    network nic set command OK
   
    <span data-ttu-id="eefb7-163">參數：</span><span class="sxs-lookup"><span data-stu-id="eefb7-163">Parameters:</span></span>
   
   * <span data-ttu-id="eefb7-164">**-f (或 --enable-ip-forwarding)**。</span><span class="sxs-lookup"><span data-stu-id="eefb7-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="eefb7-165">*true* 或 *false*。</span><span class="sxs-lookup"><span data-stu-id="eefb7-165">*true* or *false*.</span></span>

