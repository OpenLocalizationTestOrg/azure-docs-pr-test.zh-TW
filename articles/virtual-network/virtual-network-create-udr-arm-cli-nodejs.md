---
title: "使用 Azure CLI 1.0 控制路由和虛擬應用裝置 | Microsoft Docs"
description: "了解如何使用 Azure CLI 1.0 控制路由和虛擬應用裝置。"
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
ms.openlocfilehash: 5f21bc7a4fcd9507ea9d6b2b752a2328a7b834f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-user-defined-routes-udr-using-the-azure-cli-10"></a><span data-ttu-id="9446a-103">使用 Azure CLI 1.0 建立使用者定義的路由 (UDR)</span><span class="sxs-lookup"><span data-stu-id="9446a-103">Create User-Defined Routes (UDR) using the Azure CLI 1.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="9446a-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="9446a-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="9446a-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9446a-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="9446a-106">範本</span><span class="sxs-lookup"><span data-stu-id="9446a-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="9446a-107">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="9446a-107">PowerShell (Classic)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="9446a-108">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="9446a-108">CLI (Classic)</span></span>](virtual-network-create-udr-classic-cli.md)

<span data-ttu-id="9446a-109">使用 Azure CLI 建立自訂路由和虛擬應用裝置。</span><span class="sxs-lookup"><span data-stu-id="9446a-109">Create custom routing and virtual appliances using the Azure CLI.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="9446a-110">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="9446a-110">CLI versions to complete the task</span></span> 

<span data-ttu-id="9446a-111">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="9446a-111">You can complete the task using one of the following CLI versions:</span></span> 

- <span data-ttu-id="9446a-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="9446a-112">[Azure CLI 1.0](#Create-the-UDR-for-the-front-end-subnet) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9446a-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="9446a-113">[Azure CLI 2.0](virtual-network-create-udr-arm-cli.md) - our next generation CLI for the resource management deployment model</span></span> 


[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="9446a-114">以下的範例 Azure CLI 命令是假設您已根據上述案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="9446a-114">The sample Azure CLI commands below expect a simple environment already created based on the scenario above.</span></span> <span data-ttu-id="9446a-115">如果您想要以本文件顯示的方式執行命令，請先依照下列方式建置測試環境：部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before)，按一下 [部署至 Azure]，視情況取代預設參數值，然後遵循入口網站中的指示。</span><span class="sxs-lookup"><span data-stu-id="9446a-115">If you want to run the commands as they are displayed in this document, first build the test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy to Azure**, replace the default parameter values if necessary, and follow the instructions in the portal.</span></span>


## <a name="create-the-udr-for-the-front-end-subnet"></a><span data-ttu-id="9446a-116">建立前端子網路的 UDR</span><span class="sxs-lookup"><span data-stu-id="9446a-116">Create the UDR for the front-end subnet</span></span>
<span data-ttu-id="9446a-117">若要根據上述案例建立前端子網路所需的路由表和路由，請依照下列步驟執行。</span><span class="sxs-lookup"><span data-stu-id="9446a-117">To create the route table and route needed for the front end subnet based on the scenario above, follow the steps below.</span></span>

1. <span data-ttu-id="9446a-118">執行下列命令，建立前端子網路的路由表：</span><span class="sxs-lookup"><span data-stu-id="9446a-118">Run the following command to create a route table for the front-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-FrontEnd -l uswest
    ```
   
    <span data-ttu-id="9446a-119">輸出：</span><span class="sxs-lookup"><span data-stu-id="9446a-119">Output:</span></span>
   
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
   
    <span data-ttu-id="9446a-120">參數：</span><span class="sxs-lookup"><span data-stu-id="9446a-120">Parameters:</span></span>
   
   * <span data-ttu-id="9446a-121">**-g (or --resource-group)**。</span><span class="sxs-lookup"><span data-stu-id="9446a-121">**-g (or --resource-group)**.</span></span> <span data-ttu-id="9446a-122">將會在當中建立 UDR 之資源群組的名稱。</span><span class="sxs-lookup"><span data-stu-id="9446a-122">Name of the resource group where the UDR will be created.</span></span> <span data-ttu-id="9446a-123">在本文案例中為 *TestRG*。</span><span class="sxs-lookup"><span data-stu-id="9446a-123">For our scenario, *TestRG*.</span></span>
   * <span data-ttu-id="9446a-124">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="9446a-124">**-l (or --location)**.</span></span> <span data-ttu-id="9446a-125">將要建立新 UDR 的 Azure 區域。</span><span class="sxs-lookup"><span data-stu-id="9446a-125">Azure region where the new UDR will be created.</span></span> <span data-ttu-id="9446a-126">在本文案例中為 *westus*。</span><span class="sxs-lookup"><span data-stu-id="9446a-126">For our scenario, *westus*.</span></span>
   * <span data-ttu-id="9446a-127">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="9446a-127">**-n (or --name)**.</span></span> <span data-ttu-id="9446a-128">新 UDR 的名稱。</span><span class="sxs-lookup"><span data-stu-id="9446a-128">Name for the new UDR.</span></span> <span data-ttu-id="9446a-129">在本文案例中為 *UDR-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="9446a-129">For our scenario, *UDR-FrontEnd*.</span></span>
2. <span data-ttu-id="9446a-130">執行下列命令，在上方建立的路由表中建立路由，將目的地為後端子網路 (192.168.2.0/24) 的所有流量傳送到 **FW1** VM (192.168.0.4)：</span><span class="sxs-lookup"><span data-stu-id="9446a-130">Run the following command to create a route in the route table to send all traffic destined to the back-end subnet (192.168.2.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-FrontEnd -n RouteToBackEnd -a 192.168.2.0/24 -y VirtualAppliance -p 192.168.0.4
    ```
   
    <span data-ttu-id="9446a-131">輸出：</span><span class="sxs-lookup"><span data-stu-id="9446a-131">Output:</span></span>
   
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
   
    <span data-ttu-id="9446a-132">參數：</span><span class="sxs-lookup"><span data-stu-id="9446a-132">Parameters:</span></span>
   
   * <span data-ttu-id="9446a-133">**-r (或 --route-table-name)**。</span><span class="sxs-lookup"><span data-stu-id="9446a-133">**-r (or --route-table-name)**.</span></span> <span data-ttu-id="9446a-134">將會加入路由的路由表的名稱。</span><span class="sxs-lookup"><span data-stu-id="9446a-134">Name of the route table where the route will be added.</span></span> <span data-ttu-id="9446a-135">在本文案例中為 *UDR-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="9446a-135">For our scenario, *UDR-FrontEnd*.</span></span>
   * <span data-ttu-id="9446a-136">**-a (或 --address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="9446a-136">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="9446a-137">封包所指向位置的子網路的位址首碼。</span><span class="sxs-lookup"><span data-stu-id="9446a-137">Address prefix for the subnet where packets are destined to.</span></span> <span data-ttu-id="9446a-138">在本文案例中為 *192.168.2.0/24*。</span><span class="sxs-lookup"><span data-stu-id="9446a-138">For our scenario, *192.168.2.0/24*.</span></span>
   * <span data-ttu-id="9446a-139">**-y (或 --next-hop-type)**。</span><span class="sxs-lookup"><span data-stu-id="9446a-139">**-y (or --next-hop-type)**.</span></span> <span data-ttu-id="9446a-140">將傳送流量的目標物件類型。</span><span class="sxs-lookup"><span data-stu-id="9446a-140">Type of object traffic will be sent to.</span></span> <span data-ttu-id="9446a-141">可能的值為 VirtualAppliance、VirtualNetworkGateway、VNETLocal、Internet 或 None。</span><span class="sxs-lookup"><span data-stu-id="9446a-141">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
   * <span data-ttu-id="9446a-142">**-p (或 --next-hop-ip-address)**。</span><span class="sxs-lookup"><span data-stu-id="9446a-142">**-p (or --next-hop-ip-address**).</span></span> <span data-ttu-id="9446a-143">下個躍點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9446a-143">IP address for next hop.</span></span> <span data-ttu-id="9446a-144">在本文案例中為 *192.168.0.4*。</span><span class="sxs-lookup"><span data-stu-id="9446a-144">For our scenario, *192.168.0.4*.</span></span>
3. <span data-ttu-id="9446a-145">執行下列命令，將上方建立的路由表關聯至 **FrontEnd** 子網路：</span><span class="sxs-lookup"><span data-stu-id="9446a-145">Run the following command to associate the route table created above with the **FrontEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n FrontEnd -r UDR-FrontEnd
    ```
   
    <span data-ttu-id="9446a-146">輸出：</span><span class="sxs-lookup"><span data-stu-id="9446a-146">Output:</span></span>
   
        info:    Executing command network vnet subnet set
        info:    Looking up the subnet "FrontEnd"
        info:    Looking up route table "UDR-FrontEnd"
        info:    Setting subnet "FrontEnd"
        info:    Looking up the subnet "FrontEnd"
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
   
    <span data-ttu-id="9446a-147">參數：</span><span class="sxs-lookup"><span data-stu-id="9446a-147">Parameters:</span></span>
   
   * <span data-ttu-id="9446a-148">**-e (或 --vnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="9446a-148">**-e (or --vnet-name)**.</span></span> <span data-ttu-id="9446a-149">子網路所在的 VNet 名稱。</span><span class="sxs-lookup"><span data-stu-id="9446a-149">Name of the VNet where the subnet is located.</span></span> <span data-ttu-id="9446a-150">在本文案例中為 *TestVNet*。</span><span class="sxs-lookup"><span data-stu-id="9446a-150">For our scenario, *TestVNet*.</span></span>

## <a name="create-the-udr-for-the-back-end-subnet"></a><span data-ttu-id="9446a-151">建立後端子網路的 UDR</span><span class="sxs-lookup"><span data-stu-id="9446a-151">Create the UDR for the back-end subnet</span></span>
<span data-ttu-id="9446a-152">若要根據上述案例建立後端子網路所需的路由表和路徑，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9446a-152">To create the route table and route needed for the back-end subnet based on the scenario above, complete the following steps:</span></span>

1. <span data-ttu-id="9446a-153">執行下列命令，建立後端子網路的路由表：</span><span class="sxs-lookup"><span data-stu-id="9446a-153">Run the following command to create a route table for the back-end subnet:</span></span>

    ```azurecli
    azure network route-table create -g TestRG -n UDR-BackEnd -l westus
    ```

2. <span data-ttu-id="9446a-154">執行下列命令，在上方建立的路由表中建立路由，將目的地為前端子網路 (192.168.1.0/24) 的所有流量傳送到 **FW1** VM (192.168.0.4)：</span><span class="sxs-lookup"><span data-stu-id="9446a-154">Run the following command to create a route in the route table to send all traffic destined to the front-end subnet (192.168.1.0/24) to the **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    azure network route-table route create -g TestRG -r UDR-BackEnd -n RouteToFrontEnd -a 192.168.1.0/24 -y VirtualAppliance -p 192.168.0.4
    ```

3. <span data-ttu-id="9446a-155">執行下列命令，建立與 **BackEnd** 子網路關聯的路由表：</span><span class="sxs-lookup"><span data-stu-id="9446a-155">Run the following command to associate the route table with the **BackEnd** subnet:</span></span>

    ```azurecli
    azure network vnet subnet set -g TestRG -e TestVNet -n BackEnd -r UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="9446a-156">啟用 FW1 上的 IP 轉送</span><span class="sxs-lookup"><span data-stu-id="9446a-156">Enable IP forwarding on FW1</span></span>
<span data-ttu-id="9446a-157">若要啟用 **FW1**所使用之 NIC 中的 IP 轉送，完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="9446a-157">To enable IP forwarding in the NIC used by **FW1**, complete the following steps:</span></span>

1. <span data-ttu-id="9446a-158">執行以下的命令，並注意 [啟用 IP 轉送] 的值。</span><span class="sxs-lookup"><span data-stu-id="9446a-158">Run the command that follows and notice the value for **Enable IP forwarding**.</span></span> <span data-ttu-id="9446a-159">應該設定為 *false*。</span><span class="sxs-lookup"><span data-stu-id="9446a-159">It should be set to *false*.</span></span>

    ```azurecli
    azure network nic show -g TestRG -n NICFW1
    ```

    <span data-ttu-id="9446a-160">輸出：</span><span class="sxs-lookup"><span data-stu-id="9446a-160">Output:</span></span>
   
        info:    Executing command network nic show
        info:    Looking up the network interface "NICFW1"
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
2. <span data-ttu-id="9446a-161">執行下列命令以啟用 IP 轉送：</span><span class="sxs-lookup"><span data-stu-id="9446a-161">Run the following command to enable IP forwarding:</span></span>

    ```azurecli
    azure network nic set -g TestRG -n NICFW1 -f true
    ```
   
    <span data-ttu-id="9446a-162">輸出：</span><span class="sxs-lookup"><span data-stu-id="9446a-162">Output:</span></span>
   
        info:    Executing command network nic set
        info:    Looking up the network interface "NICFW1"
        info:    Updating network interface "NICFW1"
        info:    Looking up the network interface "NICFW1"
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
   
    <span data-ttu-id="9446a-163">參數：</span><span class="sxs-lookup"><span data-stu-id="9446a-163">Parameters:</span></span>
   
   * <span data-ttu-id="9446a-164">**-f (或 --enable-ip-forwarding)**。</span><span class="sxs-lookup"><span data-stu-id="9446a-164">**-f (or --enable-ip-forwarding)**.</span></span> <span data-ttu-id="9446a-165">*true* 或 *false*。</span><span class="sxs-lookup"><span data-stu-id="9446a-165">*true* or *false*.</span></span>

