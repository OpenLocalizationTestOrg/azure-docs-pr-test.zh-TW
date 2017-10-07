---
title: "虛擬網路-Azure CLI 2.0 aaaCreate |Microsoft 文件"
description: "了解如何使用虛擬網路的 toocreate hello Azure CLI 2.0。"
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
ms.openlocfilehash: e79b7fe780fc81f4866f810d830824e43a5a43b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli-20"></a><span data-ttu-id="1483c-103">建立虛擬網路使用 Azure CLI 2.0 hello</span><span class="sxs-lookup"><span data-stu-id="1483c-103">Create a virtual network using hello Azure CLI 2.0</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="1483c-104">Azure 有兩個部署模型：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="1483c-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="1483c-105">Microsoft 建議您建立透過 hello Resource Manager 部署模型的資源。</span><span class="sxs-lookup"><span data-stu-id="1483c-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="1483c-106">深入了解 toolearn hello hello 兩個模型之間的差異讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="1483c-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="1483c-107">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="1483c-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="1483c-108">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="1483c-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="1483c-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – 我們 CLI hello 傳統和資源管理部署模型</span><span class="sxs-lookup"><span data-stu-id="1483c-109">[Azure CLI 1.0](virtual-networks-create-vnet-cli-nodejs.md) – our CLI for hello classic and resource management deployment models</span></span>
- <span data-ttu-id="1483c-110">[Azure CLI 2.0](#create-a-virtual-network) -hello 資源管理部署模型 （即本文） 我們下一個層代 CLI'</span><span class="sxs-lookup"><span data-stu-id="1483c-110">[Azure CLI 2.0](#create-a-virtual-network) - our next generation CLI for hello resource management deployment model (this article)\`</span></span>
 
    <span data-ttu-id="1483c-111">您也可以建立 VNet 資源管理員 」 透過使用其他工具，或從 hello 下列清單中選取不同的選項來建立 VNet 透過 hello 傳統部署模型：</span><span class="sxs-lookup"><span data-stu-id="1483c-111">You can also create a VNet through Resource Manager using other tools or create a VNet through hello classic deployment model by selecting a different option from hello following list:</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="1483c-112">入口網站</span><span class="sxs-lookup"><span data-stu-id="1483c-112">Portal</span></span>](virtual-networks-create-vnet-arm-pportal.md)
> * [<span data-ttu-id="1483c-113">PowerShell</span><span class="sxs-lookup"><span data-stu-id="1483c-113">PowerShell</span></span>](virtual-networks-create-vnet-arm-ps.md)
> * [<span data-ttu-id="1483c-114">CLI</span><span class="sxs-lookup"><span data-stu-id="1483c-114">CLI</span></span>](virtual-networks-create-vnet-arm-cli.md)
> * [<span data-ttu-id="1483c-115">範本</span><span class="sxs-lookup"><span data-stu-id="1483c-115">Template</span></span>](virtual-networks-create-vnet-arm-template-click.md)
> * [<span data-ttu-id="1483c-116">入口網站 (傳統)</span><span class="sxs-lookup"><span data-stu-id="1483c-116">Portal (Classic)</span></span>](virtual-networks-create-vnet-classic-pportal.md)
> * [<span data-ttu-id="1483c-117">PowerShell (傳統)</span><span class="sxs-lookup"><span data-stu-id="1483c-117">PowerShell (Classic)</span></span>](virtual-networks-create-vnet-classic-netcfg-ps.md)
> * [<span data-ttu-id="1483c-118">CLI (傳統)</span><span class="sxs-lookup"><span data-stu-id="1483c-118">CLI (Classic)</span></span>](virtual-networks-create-vnet-classic-cli.md)

[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]


## <a name="create-a-virtual-network"></a><span data-ttu-id="1483c-119">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="1483c-119">Create a virtual network</span></span>

<span data-ttu-id="1483c-120">虛擬網路使用 toocreate hello Azure CLI 2.0 中，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="1483c-120">toocreate a virtual network using hello Azure CLI 2.0, complete hello following steps:</span></span>

1. <span data-ttu-id="1483c-121">安裝及最新設定 hello [Azure CLI 2.0](/cli/azure/install-az-cli2) tooan Azure 帳戶使用登入和[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="1483c-121">Install and configure hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) and log in tooan Azure account using [az login](/cli/azure/#login).</span></span>

2. <span data-ttu-id="1483c-122">建立資源群組的 VNet 使用 hello [az 群組建立](/cli/azure/group#create)命令與 hello`--name`和`--location`引數：</span><span class="sxs-lookup"><span data-stu-id="1483c-122">Create a resource group for your VNet using hello [az group create](/cli/azure/group#create) command with hello `--name` and `--location` arguments:</span></span>

    ```azurecli
    az group create --name TestRG --location centralus
    ```

3. <span data-ttu-id="1483c-123">建立 VNet 和子網路：</span><span class="sxs-lookup"><span data-stu-id="1483c-123">Create a VNet and a subnet:</span></span>

    ```azurecli
    az network vnet create \
    --name TestVNet \
    --resource-group TestRG \
    --location centralus \
    --address-prefix 192.168.0.0/16 \
    --subnet-name FrontEnd \
    --subnet-prefix 192.168.1.0/24
    ```

    <span data-ttu-id="1483c-124">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="1483c-124">Expected output:</span></span>
    
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

    <span data-ttu-id="1483c-125">使用的參數：</span><span class="sxs-lookup"><span data-stu-id="1483c-125">Parameters used:</span></span>

    - <span data-ttu-id="1483c-126">`--name TestVNet`： 建立 hello VNet toobe 名稱。</span><span class="sxs-lookup"><span data-stu-id="1483c-126">`--name TestVNet`: Name of hello VNet toobe created.</span></span>
    - <span data-ttu-id="1483c-127">`--resource-group TestRG`: # hello 資源群組名稱控制 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="1483c-127">`--resource-group TestRG`: # hello resource group name that controls hello resource.</span></span> 
    - <span data-ttu-id="1483c-128">`--location centralus`: hello 哪些 toodeploy 位置。</span><span class="sxs-lookup"><span data-stu-id="1483c-128">`--location centralus`: hello location into which toodeploy.</span></span>
    - <span data-ttu-id="1483c-129">`--address-prefix 192.168.0.0/16`: hello 位址前置詞和區塊。</span><span class="sxs-lookup"><span data-stu-id="1483c-129">`--address-prefix 192.168.0.0/16`: hello address prefix and block.</span></span>  
    - <span data-ttu-id="1483c-130">`--subnet-name FrontEnd`: hello hello 子網路名稱。</span><span class="sxs-lookup"><span data-stu-id="1483c-130">`--subnet-name FrontEnd`: hello name of hello subnet.</span></span>
    - <span data-ttu-id="1483c-131">`--subnet-prefix 192.168.1.0/24`: hello 位址前置詞和區塊。</span><span class="sxs-lookup"><span data-stu-id="1483c-131">`--subnet-prefix 192.168.1.0/24`: hello address prefix and block.</span></span>

    <span data-ttu-id="1483c-132">在 hello toolist hello 的基本資訊 toouse 接下來命令時，您可以查詢 hello VNet 使用[查詢篩選器](/cli/azure/query-az-cli2):</span><span class="sxs-lookup"><span data-stu-id="1483c-132">toolist hello basic information toouse in hello next command, you can query hello VNet using a [query filter](/cli/azure/query-az-cli2):</span></span>

    ```azurecli
    az network vnet list --query '[?name==`TestVNet`].{Where:location,Name:name,Group:resourceGroup}' -o table
    ```

    <span data-ttu-id="1483c-133">這會產生下列輸出的 hello:</span><span class="sxs-lookup"><span data-stu-id="1483c-133">Which produces hello following output:</span></span>

        Where      Name      Group

        centralus  TestVNet  TestRG

4. <span data-ttu-id="1483c-134">建立子網路：</span><span class="sxs-lookup"><span data-stu-id="1483c-134">Create a subnet:</span></span>

    ```azurecli
    az network vnet subnet create \
    --address-prefix 192.168.2.0/24 \
    --name BackEnd \
    --resource-group TestRG \
    --vnet-name TestVNet
    ```

    <span data-ttu-id="1483c-135">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="1483c-135">Expected output:</span></span>

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

    <span data-ttu-id="1483c-136">使用的參數：</span><span class="sxs-lookup"><span data-stu-id="1483c-136">Parameters used:</span></span>

    - <span data-ttu-id="1483c-137">`--address-prefix 192.168.2.0/24`：子網路 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="1483c-137">`--address-prefix 192.168.2.0/24`: Subnet CIDR block.</span></span>
    - <span data-ttu-id="1483c-138">`--name BackEnd`: Hello 新的子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="1483c-138">`--name BackEnd`: Name of hello new subnet.</span></span>
    - <span data-ttu-id="1483c-139">`--resource-group TestRG`: hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="1483c-139">`--resource-group TestRG`: hello resource group.</span></span>
    - <span data-ttu-id="1483c-140">`--vnet-name TestVNet`: hello hello 擁有 VNet 名稱。</span><span class="sxs-lookup"><span data-stu-id="1483c-140">`--vnet-name TestVNet`: hello name of hello owning VNet.</span></span>

5. <span data-ttu-id="1483c-141">查詢 hello 屬性的 hello 新的 VNet:</span><span class="sxs-lookup"><span data-stu-id="1483c-141">Query hello properties of hello new VNet:</span></span>

    ```azurecli
    az network vnet show \
    -g TestRG \
    -n TestVNet \
    --query '{Name:name,Where:location,Group:resourceGroup,Status:provisioningState,SubnetCount:subnets | length(@)}' \
    -o table
    ```

    <span data-ttu-id="1483c-142">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="1483c-142">Expected output:</span></span>

        Name      Where      Group    Status       SubnetCount

        TestVNet  centralus  TestRG   Succeeded              2

6. <span data-ttu-id="1483c-143">查詢 hello 子網路的 hello 的屬性：</span><span class="sxs-lookup"><span data-stu-id="1483c-143">Query hello properties of hello subnets:</span></span>

    ```azurecli
    az network vnet subnet list \
    -g TestRG \
    --vnet-name testvnet \
    --query '[].{Name:name,CIDR:addressPrefix,Status:provisioningState}' \
    -o table
    ```

    <span data-ttu-id="1483c-144">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="1483c-144">Expected output:</span></span>

        Name      CIDR            Status

        FrontEnd  192.168.1.0/24  Succeeded
        BackEnd   192.168.2.0/24  Succeeded

## <a name="next-steps"></a><span data-ttu-id="1483c-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1483c-145">Next steps</span></span>

<span data-ttu-id="1483c-146">深入了解如何 tooconnect:</span><span class="sxs-lookup"><span data-stu-id="1483c-146">Learn how tooconnect:</span></span>

- <span data-ttu-id="1483c-147">藉由讀取 hello 的虛擬機器 (VM) tooa 虛擬網路[建立 Linux VM](../virtual-machines/linux/quick-create-cli.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="1483c-147">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="1483c-148">而不是在 hello 步驟中的 hello 文件建立 VNet 和子網路，您可以選取的 VM 的現有 VNet 和子網路 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="1483c-148">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="1483c-149">藉由讀取 hello hello 虛擬網路的虛擬網路 tooother[連接 Vnet](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="1483c-149">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="1483c-150">使用站對站虛擬私人網路 (VPN) 或 ExpressRoute 電路 hello 虛擬網路 tooan 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="1483c-150">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="1483c-151">深入了解如何藉由讀取 hello [VNet tooan 在內部部署網路使用站對站 VPN 連線](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)和[連結 VNet tooan ExpressRoute 電路](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="1483c-151">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
