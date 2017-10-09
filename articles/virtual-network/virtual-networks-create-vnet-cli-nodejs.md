---
title: "虛擬網路使用 aaaCreate hello Azure CLI 1.0 |Microsoft 文件"
description: "了解如何使用虛擬網路的 toocreate hello Azure CLI 1.0 |資源管理員。"
services: virtual-network
documentationcenter: 
author: jimdial
manager: carmonm
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: jdial
ms.openlocfilehash: f48a8b23a5994164b71c9b51ee8a6810d17f9392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-network-using-hello-azure-cli"></a><span data-ttu-id="6ff07-103">建立虛擬網路使用 Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="6ff07-103">Create a virtual network using hello Azure CLI</span></span>

[!INCLUDE [virtual-networks-create-vnet-intro](../../includes/virtual-networks-create-vnet-intro-include.md)]

<span data-ttu-id="6ff07-104">Azure 有兩個部署模型：Azure Resource Manager 和傳統。</span><span class="sxs-lookup"><span data-stu-id="6ff07-104">Azure has two deployment models: Azure Resource Manager and classic.</span></span> <span data-ttu-id="6ff07-105">Microsoft 建議您建立透過 hello Resource Manager 部署模型的資源。</span><span class="sxs-lookup"><span data-stu-id="6ff07-105">Microsoft recommends creating resources through hello Resource Manager deployment model.</span></span> <span data-ttu-id="6ff07-106">深入了解 toolearn hello hello 兩個模型之間的差異讀取 hello[了解 Azure 部署模型](../azure-resource-manager/resource-manager-deployment-model.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="6ff07-106">toolearn more about hello differences between hello two models, read hello [Understand Azure deployment models](../azure-resource-manager/resource-manager-deployment-model.md) article.</span></span>

## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="6ff07-107">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="6ff07-107">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="6ff07-108">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="6ff07-108">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="6ff07-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="6ff07-109">[Azure CLI 2.0](virtual-networks-create-vnet-arm-cli.md) - our next generation CLI for hello resource management deployment model</span></span>
- <span data-ttu-id="6ff07-110">[Azure CLI 1.0](#create-a-virtual-network) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="6ff07-110">[Azure CLI 1.0](#create-a-virtual-network) – our CLI for hello classic and resource management deployment models (this article)</span></span>

 
[!INCLUDE [virtual-networks-create-vnet-scenario-include](../../includes/virtual-networks-create-vnet-scenario-include.md)]

## <a name="create-a-virtual-network"></a><span data-ttu-id="6ff07-111">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="6ff07-111">Create a virtual network</span></span>

<span data-ttu-id="6ff07-112">虛擬網路使用 toocreate hello Azure CLI，完成下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="6ff07-112">toocreate a virtual network using hello Azure CLI, complete hello following steps:</span></span>

1. <span data-ttu-id="6ff07-113">在安裝和設定步驟的下列 hello Azure CLI hello hello[安裝及設定 hello Azure CLI](../cli-install-nodejs.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="6ff07-113">Install and configure hello Azure CLI by following hello steps in hello [Install and Configure hello Azure CLI](../cli-install-nodejs.md) article.</span></span>

2. <span data-ttu-id="6ff07-114">建立 VNet 和子網路：</span><span class="sxs-lookup"><span data-stu-id="6ff07-114">Create a VNet and a subnet:</span></span>

    ```azurecli
    azure network vnet create --vnet TestVNet -e 192.168.0.0 -i 16 -n FrontEnd -p 192.168.1.0 -r 24 -l "Central US"
    ```

    <span data-ttu-id="6ff07-115">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ff07-115">Expected output:</span></span>
   
            info:    Executing command network vnet create
            + Looking up network configuration
            + Looking up locations
            + Setting network configuration
            info:    network vnet create command OK

    <span data-ttu-id="6ff07-116">使用的參數：</span><span class="sxs-lookup"><span data-stu-id="6ff07-116">Parameters used:</span></span>

   * <span data-ttu-id="6ff07-117">**--vnet**。</span><span class="sxs-lookup"><span data-stu-id="6ff07-117">**--vnet**.</span></span> <span data-ttu-id="6ff07-118">建立 hello VNet toobe 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ff07-118">Name of hello VNet toobe created.</span></span> <span data-ttu-id="6ff07-119">在本文案例中為 *TestVNet*</span><span class="sxs-lookup"><span data-stu-id="6ff07-119">For our scenario, *TestVNet*</span></span>
   * <span data-ttu-id="6ff07-120">**-e (或 --address-space)**。</span><span class="sxs-lookup"><span data-stu-id="6ff07-120">**-e (or --address-space)**.</span></span> <span data-ttu-id="6ff07-121">VNet 位址空間。</span><span class="sxs-lookup"><span data-stu-id="6ff07-121">VNet address space.</span></span> <span data-ttu-id="6ff07-122">在本文案例中為 *192.168.0.0*</span><span class="sxs-lookup"><span data-stu-id="6ff07-122">For our scenario, *192.168.0.0*</span></span>
   * <span data-ttu-id="6ff07-123">**-i (或 -cidr)**。</span><span class="sxs-lookup"><span data-stu-id="6ff07-123">**-i (or -cidr)**.</span></span> <span data-ttu-id="6ff07-124">CIDR 格式的網路遮罩。</span><span class="sxs-lookup"><span data-stu-id="6ff07-124">Network mask in CIDR format.</span></span> <span data-ttu-id="6ff07-125">在本文案例中為 *16*。</span><span class="sxs-lookup"><span data-stu-id="6ff07-125">For our scenario, *16*.</span></span>
   * <span data-ttu-id="6ff07-126">**-n (或 --subnet-name**)。</span><span class="sxs-lookup"><span data-stu-id="6ff07-126">**-n (or --subnet-name**).</span></span> <span data-ttu-id="6ff07-127">Hello 第一個子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ff07-127">Name of hello first subnet.</span></span> <span data-ttu-id="6ff07-128">在本文案例中為 *FrontEnd*。</span><span class="sxs-lookup"><span data-stu-id="6ff07-128">For our scenario, *FrontEnd*.</span></span>
   * <span data-ttu-id="6ff07-129">**-p (或 --subnet-start-ip)**。</span><span class="sxs-lookup"><span data-stu-id="6ff07-129">**-p (or --subnet-start-ip)**.</span></span> <span data-ttu-id="6ff07-130">子網路的起始 IP 位址或子網路位址空間。</span><span class="sxs-lookup"><span data-stu-id="6ff07-130">Starting IP address for subnet, or subnet address space.</span></span> <span data-ttu-id="6ff07-131">在本文案例中為 *192.168.1.0*。</span><span class="sxs-lookup"><span data-stu-id="6ff07-131">For our scenario, *192.168.1.0*.</span></span>
   * <span data-ttu-id="6ff07-132">**-r (或 --subnet-cidr)**。</span><span class="sxs-lookup"><span data-stu-id="6ff07-132">**-r (or --subnet-cidr)**.</span></span> <span data-ttu-id="6ff07-133">CIDR 格式的子網路網路遮罩。</span><span class="sxs-lookup"><span data-stu-id="6ff07-133">Network mask in CIDR format for subnet.</span></span> <span data-ttu-id="6ff07-134">在本文案例中為 *24*。</span><span class="sxs-lookup"><span data-stu-id="6ff07-134">For our scenario, *24*.</span></span>
   * <span data-ttu-id="6ff07-135">**-l (或 --location)**。</span><span class="sxs-lookup"><span data-stu-id="6ff07-135">**-l (or --location)**.</span></span> <span data-ttu-id="6ff07-136">Hello VNet 建立所在的 azure 區域。</span><span class="sxs-lookup"><span data-stu-id="6ff07-136">Azure region where hello VNet is created.</span></span> <span data-ttu-id="6ff07-137">在本文案例中為「美國中部」 。</span><span class="sxs-lookup"><span data-stu-id="6ff07-137">For our scenario, *Central US*.</span></span>

3. <span data-ttu-id="6ff07-138">建立子網路：</span><span class="sxs-lookup"><span data-stu-id="6ff07-138">Create a subnet:</span></span>

    ```azurecli
    azure network vnet subnet create -t TestVNet -n BackEnd -a 192.168.2.0/24
    ```
   
    <span data-ttu-id="6ff07-139">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ff07-139">Expected output:</span></span>

            info:    Executing command network vnet subnet create
            + Looking up network configuration
            + Creating subnet "BackEnd"
            + Setting network configuration
            + Looking up hello subnet "BackEnd"
            + Looking up network configuration
            data:    Name                            : BackEnd
            data:    Address prefix                  : 192.168.2.0/24
            info:    network vnet subnet create command OK

    <span data-ttu-id="6ff07-140">使用的參數：</span><span class="sxs-lookup"><span data-stu-id="6ff07-140">Parameters used:</span></span>

   * <span data-ttu-id="6ff07-141">**-t (或 --vnet-name)**。</span><span class="sxs-lookup"><span data-stu-id="6ff07-141">**-t (or --vnet-name**.</span></span> <span data-ttu-id="6ff07-142">Hello hello 子網路將會建立的 VNet 的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ff07-142">Name of hello VNet where hello subnet will be created.</span></span> <span data-ttu-id="6ff07-143">在本文案例中為 *TestVNet*。</span><span class="sxs-lookup"><span data-stu-id="6ff07-143">For our scenario, *TestVNet*.</span></span>
   * <span data-ttu-id="6ff07-144">**-n (or --name)**。</span><span class="sxs-lookup"><span data-stu-id="6ff07-144">**-n (or --name)**.</span></span> <span data-ttu-id="6ff07-145">Hello 新的子網路的名稱。</span><span class="sxs-lookup"><span data-stu-id="6ff07-145">Name of hello new subnet.</span></span> <span data-ttu-id="6ff07-146">在本文案例中為 *BackEnd*。</span><span class="sxs-lookup"><span data-stu-id="6ff07-146">For our scenario, *BackEnd*.</span></span>
   * <span data-ttu-id="6ff07-147">**-a (或 --address-prefix)**。</span><span class="sxs-lookup"><span data-stu-id="6ff07-147">**-a (or --address-prefix)**.</span></span> <span data-ttu-id="6ff07-148">子網路 CIDR 區塊。</span><span class="sxs-lookup"><span data-stu-id="6ff07-148">Subnet CIDR block.</span></span> <span data-ttu-id="6ff07-149">在本文案例中為 *192.168.2.0/24*。</span><span class="sxs-lookup"><span data-stu-id="6ff07-149">Four our scenario, *192.168.2.0/24*.</span></span>
   
4. <span data-ttu-id="6ff07-150">tooview hello 屬性 hello 新的 VNet:</span><span class="sxs-lookup"><span data-stu-id="6ff07-150">tooview hello properties of hello new VNet:</span></span>

    ```azurecli
    azure network vnet show
    ```
   
    <span data-ttu-id="6ff07-151">預期的輸出：</span><span class="sxs-lookup"><span data-stu-id="6ff07-151">Expected output:</span></span>
   
            info:    Executing command network vnet show
            Virtual network name: TestVNet
            + Looking up hello virtual network sites
            data:    Name                            : TestVNet
            data:    Location                        : Central US
            data:    State                           : Created
            data:    Address space                   : 192.168.0.0/16
            data:    Subnets:
            data:      Name                          : FrontEnd
            data:      Address prefix                : 192.168.1.0/24
            data:
            data:      Name                          : BackEnd
            data:      Address prefix                : 192.168.2.0/24
            data:
            info:    network vnet show command OK

## <a name="next-steps"></a><span data-ttu-id="6ff07-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ff07-152">Next steps</span></span>

<span data-ttu-id="6ff07-153">深入了解如何 tooconnect:</span><span class="sxs-lookup"><span data-stu-id="6ff07-153">Learn how tooconnect:</span></span>

- <span data-ttu-id="6ff07-154">藉由讀取 hello 的虛擬機器 (VM) tooa 虛擬網路[建立 Linux VM](../virtual-machines/linux/quick-create-cli.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="6ff07-154">A virtual machine (VM) tooa virtual network by reading hello [Create a Linux VM](../virtual-machines/linux/quick-create-cli.md) article.</span></span> <span data-ttu-id="6ff07-155">而不是在 hello 步驟中的 hello 文件建立 VNet 和子網路，您可以選取的 VM 的現有 VNet 和子網路 tooconnect。</span><span class="sxs-lookup"><span data-stu-id="6ff07-155">Instead of creating a VNet and subnet in hello steps of hello articles, you can select an existing VNet and subnet tooconnect a VM to.</span></span>
- <span data-ttu-id="6ff07-156">藉由讀取 hello hello 虛擬網路的虛擬網路 tooother[連接 Vnet](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md)發行項。</span><span class="sxs-lookup"><span data-stu-id="6ff07-156">hello virtual network tooother virtual networks by reading hello [Connect VNets](../vpn-gateway/vpn-gateway-howto-vnet-vnet-resource-manager-portal.md) article.</span></span>
- <span data-ttu-id="6ff07-157">使用站對站虛擬私人網路 (VPN) 或 ExpressRoute 電路 hello 虛擬網路 tooan 在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="6ff07-157">hello virtual network tooan on-premises network using a site-to-site virtual private network (VPN) or ExpressRoute circuit.</span></span> <span data-ttu-id="6ff07-158">深入了解如何藉由讀取 hello [VNet tooan 在內部部署網路使用站對站 VPN 連線](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md)和[連結 VNet tooan ExpressRoute 電路](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md)。</span><span class="sxs-lookup"><span data-stu-id="6ff07-158">Learn how by reading hello [Connect a VNet tooan on-premises network using a site-to-site VPN](../vpn-gateway/vpn-gateway-howto-multi-site-to-site-resource-manager-portal.md) and [Link a VNet tooan ExpressRoute circuit](../expressroute/expressroute-howto-linkvnet-portal-resource-manager.md).</span></span>
