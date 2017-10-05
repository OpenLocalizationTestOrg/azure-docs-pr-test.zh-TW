---
title: "建立虛擬網路 - Azure CLI 2.0 | Microsoft Docs"
description: "了解如何使用 Azure CLI 2.0 建立虛擬網路。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 75966bcc-0056-4667-8482-6f08ca38e77a
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c7d7b3543f488aedff1ea2c68a2b497e0ca744af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-network-using-the-azure-cli-20"></a><span data-ttu-id="65661-103">使用 Azure CLI 2.0 建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="65661-103">Create a virtual network using the Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="65661-104">Azure 有兩個部署模型：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="65661-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="65661-105">Microsoft 建議透過 Resource Manager 部署模型建立資源。</span><span class="sxs-lookup"><span data-stu-id="65661-105">Microsoft recommends creating resources through the Resource Manager deployment model.</span></span> <span data-ttu-id="65661-106">若要深入了解兩個模型的差異，請閱讀[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="65661-106">To learn more about the differences between the two models, read the [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="65661-107">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="65661-107">CLI versions to complete the task</span></span>
<span data-ttu-id="65661-108">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="65661-108">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="65661-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – 適用於傳統和資源管理部署模型的 CLI</span><span class="sxs-lookup"><span data-stu-id="65661-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for the classic and resource management deployment models</span></span>
- <span data-ttu-id="65661-110">[Azure CLI 2.0](#create-a-virtual-network) - 適用於資源管理部署模型的新一代 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="65661-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for the resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="65661-111">您也可以使用其他工具透過 Resource Manager 建立 VNet，或從下列清單中選取不同選項以透過傳統部署模型建立 VNet︰</span><span class="sxs-lookup"><span data-stu-id="65661-111">You can also create a VNet through Resource Manager using other tools or create a VNet through the classic deployment model by selecting a different option from the following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="65661-112">入口網站</span><span class="sxs-lookup"><span data-stu-id="65661-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="65661-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="65661-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="65661-114">CLI</span><span class="sxs-lookup"><span data-stu-id="65661-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="65661-115">範本</span><span class="sxs-lookup"><span data-stu-id="65661-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="65661-116">入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="65661-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="65661-117">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="65661-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="65661-118">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="65661-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="65661-119">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="65661-119">Create a virtual network</span></span>

<span data-ttu-id="65661-120">若要使用 Azure CLI 2.0 來建立虛擬網路，請完成下列步驟︰</span><span class="sxs-lookup"><span data-stu-id="65661-120">To create a virtual network using the Azure CLI 2.0, complete the following steps:</span></span>

1. <span data-ttu-id="65661-121">安裝及設定最新的 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並使用 [az login](/cli/azure/#login) 來登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="65661-121">Install and configure the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in to an Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="65661-122">使用 [az group create](/cli/azure/group#create) 命令搭配 `--name` 和 `--location` 引數來為您的 VNet 建立資源群組：</span><span class="sxs-lookup"><span data-stu-id="65661-122">Create a resource group for your VNet using the [az group create](/cli/azure/group#create) command with the `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="65661-123">建立 VNet 和子網路：</span><span class="sxs-lookup"><span data-stu-id="65661-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="65661-124">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="65661-124">Expected output:</span></span>
    
    ```json
    {
        "newVNet": {
            "addressSpace": {
            "addressPrefixes": [
            "192.168.0.0/16"
            ]
            },
            "dhcpOptions": {
            "dnsServers": []
            },
            "provisioningState": "Succeeded",
            "resourceGuid": "<guid>",
            "subnets": [
            {
                "etag": "W/\"<guid>\"",
                "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/FrontEnd",
                "name": "FrontEnd",
                "properties": {
                "addressPrefix": "192.168.1.0/24",
                "provisioningState": "Succeeded"
                },
                "resourceGroup": "TestRG"
            }
            ]
            }
    }
    ```

    <span data-ttu-id="65661-125">使用的參數：</span><span class="sxs-lookup"><span data-stu-id="65661-125">Parameters used:</span></span>

    - <span data-ttu-id="65661-126">`--name TestVNet`：要建立的 VNet 名稱。</span><span class="sxs-lookup"><span data-stu-id="65661-126">`--name TestVNet`: Name of the VNet to be created.</span></span>
    - <span data-ttu-id="65661-127">`--resource-group TestRG`：控制資源的資源群組名稱。</span><span class="sxs-lookup"><span data-stu-id="65661-127">`--resource-group TestRG`: # The resource group name that controls the resource.</span></span> 
    - <span data-ttu-id="65661-128">`--location centralus`：要在其中進行部署的位置。</span><span class="sxs-lookup"><span data-stu-id="65661-128">`--location centralus`: The location into which to deploy.</span></span>
    - <span data-ttu-id="65661-129">`--address-prefix 192.168.0.0/16`：位址首碼和區塊。</span><span class="sxs-lookup"><span data-stu-id="65661-129">`--address-prefix 192.168.0.0/16`: The address prefix and block.</span></span>  
    - <span data-ttu-id="65661-130">`--subnet-name FrontEnd`：子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="65661-130">`--subnet-name FrontEnd`: The name of the subnet.</span></span>
    - <span data-ttu-id="65661-131">`--subnet-prefix 192.168.1.0/24`：位址首碼和區塊。</span><span class="sxs-lookup"><span data-stu-id="65661-131">`--subnet-prefix 192.168.1.0/24`: The address prefix and block.</span></span>

    <span data-ttu-id="65661-132">若要列出要在下一個命令中使用的基本資訊，您可以使用[查詢篩選](/cli/azure/query-az-cli2)來查詢 VNet：</span><span class="sxs-lookup"><span data-stu-id="65661-132">To list the basic information to use in the next command, you can query the VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="65661-133">這會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="65661-133">Which produces the following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="65661-134">建立子網路：</span><span class="sxs-lookup"><span data-stu-id="65661-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="65661-135">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="65661-135">Expected output:</span></span>

    ```json
    {
    "addressPrefix": "192.168.2.0/24",
    "etag": "W/\"<guid> \"",
    "id": "/subscriptions/<guid>/resourceGroups/TestRG/providers/Microsoft.Network/virtualNetworks/TestVNet/subnets/BackEnd",
    "ipConfigurations": null,
    "name": "BackEnd",
    "networkSecurityGroup": null,
    "provisioningState": "Succeeded",
    "resourceGroup": "TestRG",
    "resourceNavigationLinks": null,
    "routeTable": null
    }
    ```

    <span data-ttu-id="65661-136">使用的參數：</span><span class="sxs-lookup"><span data-stu-id="65661-136">Parameters used:</span></span>

    - <span data-ttu-id="65661-137">`--address-prefix 192.168.2.0/24`：子網路 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="65661-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="65661-138">`--name BackEnd`：新子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="65661-138">`--name BackEnd`: Name of the new subnet.</span></span>
    - <span data-ttu-id="65661-139">`--resource-group TestRG`：資源群組。</span><span class="sxs-lookup"><span data-stu-id="65661-139">`--resource-group TestRG`: The resource group.</span></span>
    - <span data-ttu-id="65661-140">`--vnet-name TestVNet`：上層 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="65661-140">`--vnet-name TestVNet`: The name of the owning VNet.</span></span>

5. <span data-ttu-id="65661-141">查詢新 VNet 的屬性：</span><span class="sxs-lookup"><span data-stu-id="65661-141">Query the properties of the new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="65661-142">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="65661-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="65661-143">查詢子網路的屬性：</span><span class="sxs-lookup"><span data-stu-id="65661-143">Query the properties of the subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="65661-144">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="65661-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="65661-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="65661-145">Next steps</span></span>

<span data-ttu-id="65661-146">了解如何連接︰</span><span class="sxs-lookup"><span data-stu-id="65661-146">Learn how to connect:</span></span>

- <span data-ttu-id="65661-147">虛擬機器 (VM) 至虛擬網路；請閱讀[建立 Linux VM](../virtual-machines/linux/quick-create-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="65661-147">A virtual machine (VM) to a virtual network by reading the [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="65661-148">但不是如文章中的步驟建立 VNet 和子網路，而是選取現有的 VNet 和子網路來連接 VM。</span><span class="sxs-lookup"><span data-stu-id="65661-148">Instead of creating a VNet and subnet in the steps of the articles, you can select an existing VNet and subnet to connect a VM to.</span></span>
- <span data-ttu-id="65661-149">虛擬網路至其他虛擬網路；請閱讀[連接 VNet](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="65661-149">The virtual network to other virtual networks by reading the [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="65661-150">虛擬網路至內部部署網路；使用網站對網站虛擬私人網路 (VPN) 或 ExpressRoute 線路。</span><span class="sxs-lookup"><span data-stu-id="65661-150">The virtual network to an on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="65661-151">如需了解做法，請閱讀[使用站台對站台 VPN 將 VNet 連接到內部部署網路](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)和[將 VNet 連結至 ExpressRoute 線路](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="65661-151">Learn how by reading the [Connect a VNet to an on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet to an ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>