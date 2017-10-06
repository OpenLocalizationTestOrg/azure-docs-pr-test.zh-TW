---
title: "使用 aaaControl 路由和虛擬裝置 hello Azure CLI 2.0 |Microsoft 文件"
description: "了解如何使用 toocontrol 路由和虛擬裝置 hello Azure CLI 2.0。"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.assetid: 5452a0b8-21a6-4699-8d6a-e2d8faf32c25
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/12/2017
ms.author: jdial
ms.openlocfilehash: 79b908848932a4365dab1b7497b6a0dbf44bbaf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-user-defined-routes-udr-using-hello-azure-cli-20"></a><span data-ttu-id="b06b0-103">建立使用者定義的路由 (UDR) 使用 hello Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b06b0-103">Create User-Defined Routes (UDR) using hello Azure CLI 2.0</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="b06b0-104">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b06b0-104">PowerShell</span></span>](virtual-network-create-udr-arm-ps.md)
> * [<span data-ttu-id="b06b0-105">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b06b0-105">Azure CLI</span></span>](virtual-network-create-udr-arm-cli.md)
> * [<span data-ttu-id="b06b0-106">範本</span><span class="sxs-lookup"><span data-stu-id="b06b0-106">Template</span></span>](virtual-network-create-udr-arm-template.md)
> * [<span data-ttu-id="b06b0-107">PowerShell (傳統部署)</span><span class="sxs-lookup"><span data-stu-id="b06b0-107">PowerShell (Classic deployment)</span></span>](virtual-network-create-udr-classic-ps.md)
> * [<span data-ttu-id="b06b0-108">CLI (傳統部署)</span><span class="sxs-lookup"><span data-stu-id="b06b0-108">CLI (Classic deployment)</span></span>](virtual-network-create-udr-classic-cli.md)

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="b06b0-109">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="b06b0-109">CLI versions toocomplete hello task</span></span> 

<span data-ttu-id="b06b0-110">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="b06b0-110">You can complete hello task using one of hello following CLI versions:</span></span> 

- <span data-ttu-id="b06b0-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – 我們 CLI hello 傳統和資源管理部署模型</span><span class="sxs-lookup"><span data-stu-id="b06b0-111">[Azure CLI 1.0](virtual-network-create-udr-arm-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span> 
- <span data-ttu-id="b06b0-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) -hello 資源管理部署模型 （即本文） 我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="b06b0-112">[Azure CLI 2.0](#Create-the-UDR-for-the-front-end-subnet) - our next generation CLI for hello resource management deployment model (this article)</span></span>

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

[!INCLUDE [virtual-network-create-udr-intro-include.md](../../includes/virtual-network-create-udr-intro-include.md)]

[!INCLUDE [virtual-network-create-udr-scenario-include.md](../../includes/virtual-network-create-udr-scenario-include.md)]

<span data-ttu-id="b06b0-113">下列的 hello 範例 Azure CLI 命令預期已經根據上述的 hello 案例建立簡單的環境。</span><span class="sxs-lookup"><span data-stu-id="b06b0-113">hello sample Azure CLI commands below expect a simple environment already created based on hello scenario above.</span></span> <span data-ttu-id="b06b0-114">如果您想 toorun hello 命令，因為它們會顯示在此文件，第一次建立 hello 測試環境部署[此範本](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before)，按一下 **部署 tooAzure**，取代 hello 預設參數值如果有必要，並遵循中的 hello 指示 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="b06b0-114">If you want toorun hello commands as they are displayed in this document, first build hello test environment by deploying [this template](http://github.com/telmosampaio/azure-templates/tree/master/IaaS-NSG-UDR-Before), click **Deploy tooAzure**, replace hello default parameter values if necessary, and follow hello instructions in hello portal.</span></span>


## <a name="create-hello-udr-for-hello-front-end-subnet"></a><span data-ttu-id="b06b0-115">建立 hello UDR hello 前端子網路</span><span class="sxs-lookup"><span data-stu-id="b06b0-115">Create hello UDR for hello front-end subnet</span></span>
<span data-ttu-id="b06b0-116">toocreate hello 路由表和路由所需的 hello 前端子網路，根據 hello 案例以上版本，請遵循下列 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="b06b0-116">toocreate hello route table and route needed for hello front end subnet based on hello scenario above, follow hello steps below.</span></span>

1. <span data-ttu-id="b06b0-117">建立 hello 前端子網路路由表以 hello [az 網路路由表建立](/cli/azure/network/route-table#create)命令：</span><span class="sxs-lookup"><span data-stu-id="b06b0-117">Create a route table for hello front-end subnet with hello [az network route-table create](/cli/azure/network/route-table#create) command:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --location centralus \
    --name UDR-FrontEnd
    ```

    <span data-ttu-id="b06b0-118">輸出：</span><span class="sxs-lookup"><span data-stu-id="b06b0-118">Output:</span></span>

    ```json
    {
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
    "location": "centralus",
    "name": "UDR-FrontEnd",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "routes": [],
    "subnets": null,
    "tags": null,
    "type": "Microsoft.Network/routeTables"
    }
    ```

2. <span data-ttu-id="b06b0-119">建立路由傳送所有流量 toohello 後端子 (192.168.2.0/24) toohello **FW1** VM (已將 192.168.0.4) 使用 hello [az 網路路由表路由建立](/cli/azure/network/route-table/route#create)命令：</span><span class="sxs-lookup"><span data-stu-id="b06b0-119">Create a route that sends all traffic destined toohello back-end subnet (192.168.2.0/24) toohello **FW1** VM (192.168.0.4) using hello [az network route-table route create](/cli/azure/network/route-table/route#create) command:</span></span>

    ```azurecli 
    az network route-table route create \
    --resource-group testrg \
    --name RouteToBackEnd \
    --route-table-name UDR-FrontEnd \
    --address-prefix 192.168.2.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

    <span data-ttu-id="b06b0-120">輸出：</span><span class="sxs-lookup"><span data-stu-id="b06b0-120">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd/routes/RouteToBackEnd",
    "name": "RouteToBackEnd",
    "nextHopIpAddress": "192.168.0.4",
    "nextHopType": "VirtualAppliance",
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg"
    }
    ```
    <span data-ttu-id="b06b0-121">參數：</span><span class="sxs-lookup"><span data-stu-id="b06b0-121">Parameters:</span></span>

    * <span data-ttu-id="b06b0-122">**--route-table-name**。</span><span class="sxs-lookup"><span data-stu-id="b06b0-122">**--route-table-name**.</span></span> <span data-ttu-id="b06b0-123">將會加入 hello 路由 hello 路由表的名稱。</span><span class="sxs-lookup"><span data-stu-id="b06b0-123">Name of hello route table where hello route will be added.</span></span> <span data-ttu-id="b06b0-124">在本文案例中為 *UDR-FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="b06b0-124">For our scenario, *UDR-FrontEnd*.</span></span>
    * <span data-ttu-id="b06b0-125">**--address-prefix**。</span><span class="sxs-lookup"><span data-stu-id="b06b0-125">**--address-prefix**.</span></span> <span data-ttu-id="b06b0-126">Hello 封包會指向其中的子網路的位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="b06b0-126">Address prefix for hello subnet where packets are destined to.</span></span> <span data-ttu-id="b06b0-127">在本文案例中為 *192.168.2.0/24*。</span><span class="sxs-lookup"><span data-stu-id="b06b0-127">For our scenario, *192.168.2.0/24*.</span></span>
    * <span data-ttu-id="b06b0-128">**--next-hop-type**。</span><span class="sxs-lookup"><span data-stu-id="b06b0-128">**--next-hop-type**.</span></span> <span data-ttu-id="b06b0-129">將傳送流量的目標物件類型。</span><span class="sxs-lookup"><span data-stu-id="b06b0-129">Type of object traffic will be sent to.</span></span> <span data-ttu-id="b06b0-130">可能的值為 VirtualAppliance、VirtualNetworkGateway、VNETLocal、Internet 或 None。</span><span class="sxs-lookup"><span data-stu-id="b06b0-130">Possible values are *VirtualAppliance*, *VirtualNetworkGateway*, *VNETLocal*, *Internet*, or *None*.</span></span>
    * <span data-ttu-id="b06b0-131">**--next-hop-ip-address**。</span><span class="sxs-lookup"><span data-stu-id="b06b0-131">**--next-hop-ip-address**.</span></span> <span data-ttu-id="b06b0-132">下個躍點的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b06b0-132">IP address for next hop.</span></span> <span data-ttu-id="b06b0-133">在本文案例中為 *192.168.0.4*。</span><span class="sxs-lookup"><span data-stu-id="b06b0-133">For our scenario, *192.168.0.4*.</span></span>

3. <span data-ttu-id="b06b0-134">執行 hello [az 網路 vnet 子網路更新](/cli/azure/network/vnet/subnet#update)命令 tooassociate hello 路由表上面建立以 hello**前端**子網路：</span><span class="sxs-lookup"><span data-stu-id="b06b0-134">Run hello [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) command tooassociate hello route table created above with hello **FrontEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name FrontEnd \
    --route-table UDR-FrontEnd
    ```

    <span data-ttu-id="b06b0-135">輸出：</span><span class="sxs-lookup"><span data-stu-id="b06b0-135">Output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.1.0/24",
    "etag": "W/\"<guid>\"",
    "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/virtualNetworks/testvnet/subnets/FrontEnd",
    "ipConfigurations": null,
    "name": "FrontEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "testrg",
    "resourceNavigationLinks": null,
    "routeTable": {
        "etag": null,
        "id": "/subscriptions/<guid>/resourceGroups/testrg/providers/Microsoft.Network/routeTables/UDR-FrontEnd",
        "location": null,
        "name": null,
        "provisioningState": null,
        "resourceGroup": "testrg",
        "routes": null,
        "subnets": null,
        "tags": null,
        "type": null
        }
    }
    ```

    <span data-ttu-id="b06b0-136">參數：</span><span class="sxs-lookup"><span data-stu-id="b06b0-136">Parameters:</span></span>
    
    * <span data-ttu-id="b06b0-137">**--vnet-name**。</span><span class="sxs-lookup"><span data-stu-id="b06b0-137">**--vnet-name**.</span></span> <span data-ttu-id="b06b0-138">Hello hello 子網路所在的 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="b06b0-138">Name of hello VNet where hello subnet is located.</span></span> <span data-ttu-id="b06b0-139">在本文案例中為 *TestVNet*。</span><span class="sxs-lookup"><span data-stu-id="b06b0-139">For our scenario, *TestVNet*.</span></span>

## <a name="create-hello-udr-for-hello-back-end-subnet"></a><span data-ttu-id="b06b0-140">建立 hello UDR hello 後端子網路</span><span class="sxs-lookup"><span data-stu-id="b06b0-140">Create hello UDR for hello back-end subnet</span></span>

<span data-ttu-id="b06b0-141">toocreate hello 路由表和路由所需的 hello 後端子根據上述步驟的完整 hello hello 案例：</span><span class="sxs-lookup"><span data-stu-id="b06b0-141">toocreate hello route table and route needed for hello back-end subnet based on hello scenario above, complete hello following steps:</span></span>

1. <span data-ttu-id="b06b0-142">執行下列命令 toocreate hello hello 後端子網路路由表：</span><span class="sxs-lookup"><span data-stu-id="b06b0-142">Run hello following command toocreate a route table for hello back-end subnet:</span></span>

    ```azurecli
    az network route-table create \
    --resource-group testrg \
    --name UDR-BackEnd \
    --location centralus
    ```

2. <span data-ttu-id="b06b0-143">執行下列命令 toocreate hello 路由表 toosend 中路由 hello 所有流量 toohello 前端的子網路 (192.168.1.0/24) toohello **FW1** VM (已將 192.168.0.4):</span><span class="sxs-lookup"><span data-stu-id="b06b0-143">Run hello following command toocreate a route in hello route table toosend all traffic destined toohello front-end subnet (192.168.1.0/24) toohello **FW1** VM (192.168.0.4):</span></span>

    ```azurecli
    az network route-table route create \
    --resource-group testrg \
    --name RouteToFrontEnd \
    --route-table-name UDR-BackEnd \
    --address-prefix 192.168.1.0/24 \
    --next-hop-type VirtualAppliance \
    --next-hop-ip-address 192.168.0.4
    ```

3. <span data-ttu-id="b06b0-144">執行 hello 下列命令以 hello tooassociate hello 路由表**後端**子網路：</span><span class="sxs-lookup"><span data-stu-id="b06b0-144">Run hello following command tooassociate hello route table with hello **BackEnd** subnet:</span></span>

    ```azurecli
    az network vnet subnet update \
    --resource-group testrg \
    --vnet-name testvnet \
    --name BackEnd \
    --route-table UDR-BackEnd
    ```

## <a name="enable-ip-forwarding-on-fw1"></a><span data-ttu-id="b06b0-145">啟用 FW1 上的 IP 轉送</span><span class="sxs-lookup"><span data-stu-id="b06b0-145">Enable IP forwarding on FW1</span></span>

<span data-ttu-id="b06b0-146">tooenable 在 hello NIC 所使用的 IP 轉送**FW1**，完成下列步驟 hello:</span><span class="sxs-lookup"><span data-stu-id="b06b0-146">tooenable IP forwarding in hello NIC used by **FW1**, complete hello following steps:</span></span>

1. <span data-ttu-id="b06b0-147">執行 hello [az 網路 nic 顯示](/cli/azure/network/nic#show)命令搭配 JMESPATH 篩選 toodisplay hello 目前**啟用 ip 轉送**值**啟用 IP 轉送**。</span><span class="sxs-lookup"><span data-stu-id="b06b0-147">Run hello [az network nic show](/cli/azure/network/nic#show) command with a JMESPATH filter toodisplay hello current **enable-ip-forwarding** value for **Enable IP forwarding**.</span></span> <span data-ttu-id="b06b0-148">才應該設定太*false*。</span><span class="sxs-lookup"><span data-stu-id="b06b0-148">It should be set too*false*.</span></span>

    ```azurecli
    az network nic show \
    --resource-group testrg \
    --nname nicfw1 \
    --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="b06b0-149">輸出：</span><span class="sxs-lookup"><span data-stu-id="b06b0-149">Output:</span></span>

        false

2. <span data-ttu-id="b06b0-150">執行下列命令 tooenable IP 轉送的 hello:</span><span class="sxs-lookup"><span data-stu-id="b06b0-150">Run hello following command tooenable IP forwarding:</span></span>

    ```azurecli
    az network nic update \
    --resource-group testrg \
    --name nicfw1 \
    --ip-forwarding true
    ```

    <span data-ttu-id="b06b0-151">您可以檢查 hello 輸出資料流處理的 toohello 主控台中，或只重新測試特定的 hello **enableIpForwarding**值：</span><span class="sxs-lookup"><span data-stu-id="b06b0-151">You can examine hello output streamed toohello console, or just retest for hello specific **enableIpForwarding** value:</span></span>

    ```azurecli
    az network nic show -g testrg -n nicfw1 --query 'enableIpForwarding' -o tsv
    ```

    <span data-ttu-id="b06b0-152">輸出：</span><span class="sxs-lookup"><span data-stu-id="b06b0-152">Output:</span></span>

        true

    <span data-ttu-id="b06b0-153">參數：</span><span class="sxs-lookup"><span data-stu-id="b06b0-153">Parameters:</span></span>

    <span data-ttu-id="b06b0-154">**--ip-forwarding**：*true* 或 *false*。</span><span class="sxs-lookup"><span data-stu-id="b06b0-154">**--ip-forwarding**: *true* or *false*.</span></span>

