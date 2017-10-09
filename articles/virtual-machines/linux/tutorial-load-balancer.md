---
title: "aaaHow tooload 平衡在 Azure 中的 Linux 虛擬機器 |Microsoft 文件"
description: "了解如何 toouse hello Azure 跨越三個 Linux Vm 的負載平衡器 toocreate 高度可用且安全的應用程式"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="7d3b0-103">如何 tooload 會平衡 Azure toocreate 中 Linux 虛擬機器的高可用性的應用程式</span><span class="sxs-lookup"><span data-stu-id="7d3b0-103">How tooload balance Linux virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="7d3b0-104">負載平衡會將傳入要求分散到多部虛擬機器，藉此提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="7d3b0-105">在本教學課程中，您會了解 hello 的不同元件 hello Azure 負載平衡器會將流量，以及提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="7d3b0-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="7d3b0-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d3b0-107">建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="7d3b0-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="7d3b0-108">建立負載平衡器健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="7d3b0-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="7d3b0-109">建立負載平衡器流量規則</span><span class="sxs-lookup"><span data-stu-id="7d3b0-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="7d3b0-110">使用雲端 init toocreate 基本 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="7d3b0-110">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="7d3b0-111">建立虛擬機器，並附加 tooa 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="7d3b0-112">檢視作用中的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-112">View a load balancer in action</span></span>
> * <span data-ttu-id="7d3b0-113">新增和移除虛擬機器的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7d3b0-114">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7d3b0-115">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7d3b0-116">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="7d3b0-117">Azure Load Balancer 概觀</span><span class="sxs-lookup"><span data-stu-id="7d3b0-117">Azure load balancer overview</span></span>
<span data-ttu-id="7d3b0-118">Azure Load Balancer 是 Layer-4 (TCP、UDP) 負載平衡器，可將連入流量分散於狀況良好的 VM 來提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="7d3b0-119">負載平衡器健全狀況探查監視每個 VM 上指定的連接埠，並只會發佈流量 tooan 操作的 VM。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="7d3b0-120">您可定義含有一或多個公用 IP 位址的前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="7d3b0-121">此前端 IP 組態可讓您的負載平衡器和應用程式 toobe 存取透過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="7d3b0-122">虛擬機器連接 tooa 負載平衡器使用他們的虛擬網路介面卡 (NIC)。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="7d3b0-123">toodistribute 流量 toohello Vm 後, 端位址集區包含 hello hello 虛擬 (Nic) 連線的 toohello 負載平衡器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="7d3b0-124">toocontrol hello 流量的流量，您會定義特定連接埠和通訊協定對應 tooyour Vm 的負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>

<span data-ttu-id="7d3b0-125">如果您遵循 hello 上一個教學課程太[建立虛擬機器規模集](tutorial-create-vmss.md)，為您建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-125">If you followed hello previous tutorial too[create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="7d3b0-126">所有這些元件已設定為您 hello 規模集的一部分。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-126">All these components were configured for you as part of hello scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="7d3b0-127">建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="7d3b0-127">Create Azure load balancer</span></span>
<span data-ttu-id="7d3b0-128">本節將詳細說明如何建立及設定 hello 負載平衡器的每個元件。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-128">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="7d3b0-129">請先使用 [az group create](/cli/azure/group#create) 建立資源群組，才可建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7d3b0-130">hello 下列範例會建立名為的資源群組*myResourceGroupLoadBalancer*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="7d3b0-130">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="7d3b0-131">建立公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7d3b0-131">Create a public IP address</span></span>
<span data-ttu-id="7d3b0-132">tooaccess 上的應用程式 hello 網際網路，您就需要公用 IP 位址 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-132">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="7d3b0-133">使用 [az network public-ip create](/cli/azure/network/public-ip#create) 建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="7d3b0-134">hello 下列範例會建立名為的公用 IP 位址*myPublicIP*在 hello *myResourceGroupLoadBalancer*資源群組：</span><span class="sxs-lookup"><span data-stu-id="7d3b0-134">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="7d3b0-135">建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-135">Create a load balancer</span></span>
<span data-ttu-id="7d3b0-136">使用 [az network lb create](/cli/azure/network/lb#create) 建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="7d3b0-137">hello 下列範例會建立名為負載平衡器*myLoadBalancer*和指派 hello *myPublicIP*位址 toohello 前端 IP 組態：</span><span class="sxs-lookup"><span data-stu-id="7d3b0-137">hello following example creates a load balancer named *myLoadBalancer* and assigns hello *myPublicIP* address toohello front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="7d3b0-138">建立健康狀態探查</span><span class="sxs-lookup"><span data-stu-id="7d3b0-138">Create a health probe</span></span>
<span data-ttu-id="7d3b0-139">tooallow hello 負載平衡器 toomonitor hello 狀態的應用程式，您可以使用健全狀況探查。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-139">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="7d3b0-140">hello 健全狀況探查以動態方式加入或移除 hello 負載平衡器輪替根據其回應 toohealth 檢查 Vm。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-140">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="7d3b0-141">根據預設，VM 會移除從 15 秒的間隔的兩個連續多次失敗後的 hello 負載平衡器發佈。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-141">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="7d3b0-142">您可根據通訊協定或您應用程式的特定健康狀態檢查頁面，建立健康狀態探查。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="7d3b0-143">hello 下列範例會建立 TCP 探查。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-143">hello following example creates a TCP probe.</span></span> <span data-ttu-id="7d3b0-144">您也可以建立自訂 HTTP 探查，以進行更精細的健康狀態檢查。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="7d3b0-145">時使用自訂的 HTTP 探查，您必須建立 hello 健康情況檢查 頁面上，例如*healthcheck.js*。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-145">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="7d3b0-146">必須傳回 hello 探查**HTTP 200 「 確定**回應 hello 負載平衡器 tookeep hello 中主機的旋轉。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-146">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="7d3b0-147">您使用 toocreate TCP 健全狀況探查， [az 網路 lb 探查建立](/cli/azure/network/lb/probe#create)。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-147">toocreate a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="7d3b0-148">hello 下列範例會建立名為健全狀況探查*myHealthProbe*:</span><span class="sxs-lookup"><span data-stu-id="7d3b0-148">hello following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="7d3b0-149">建立負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="7d3b0-149">Create a load balancer rule</span></span>
<span data-ttu-id="7d3b0-150">負載平衡器規則是使用的 toodefine 流量的分散式的 toohello Vm 的方式。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-150">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="7d3b0-151">您定義 hello 連入流量和 hello 後端 IP 集區 tooreceive hello 流量，以及 hello 必要的來源和目的地連接埠 hello 前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-151">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="7d3b0-152">toomake 確定只有狀況良好的 Vm 接收流量，您也定義 hello 健全狀況探查 toouse。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-152">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="7d3b0-153">使用 [az network lb rule create](/cli/azure/network/lb/rule#create) 建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="7d3b0-154">hello 下列範例會建立名為的規則*myLoadBalancerRule*，使用 hello *myHealthProbe*健全狀況探查和連接埠上的餘額流量*80*:</span><span class="sxs-lookup"><span data-stu-id="7d3b0-154">hello following example creates a rule named *myLoadBalancerRule*, uses hello *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a><span data-ttu-id="7d3b0-155">設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7d3b0-155">Configure virtual network</span></span>
<span data-ttu-id="7d3b0-156">您將一些 Vm 部署，並可以測試您平衡器之前，先建立 hello 支援的虛擬網路資源。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-156">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="7d3b0-157">如需有關虛擬網路的詳細資訊，請參閱 hello[管理 Azure 虛擬網路](tutorial-virtual-network.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-157">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="7d3b0-158">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="7d3b0-158">Create network resources</span></span>
<span data-ttu-id="7d3b0-159">使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="7d3b0-160">hello 下列範例會建立虛擬網路，名為*myVnet*與子網路，名為*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="7d3b0-160">hello following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="7d3b0-161">您使用 tooadd 網路安全性群組， [az 網路 nsg 建立](/cli/azure/network/nsg#create)。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-161">tooadd a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="7d3b0-162">hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="7d3b0-162">hello following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="7d3b0-163">使用 [az network nsg rule create](/cli/azure/network/nsg/rule#create) 建立網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="7d3b0-164">hello 下列範例會建立網路安全性群組規則命名為*myNetworkSecurityGroupRule*:</span><span class="sxs-lookup"><span data-stu-id="7d3b0-164">hello following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="7d3b0-165">使用 [az network nic create](/cli/azure/network/nic#create) 建立虛擬 NIC。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="7d3b0-166">hello 下列範例會建立三個虛擬 Nic。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-166">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="7d3b0-167">（每個 VM 的虛擬 NIC 建立 hello 下列中的應用程式的步驟）。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-167">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="7d3b0-168">您可以隨時建立其他虛擬 Nic 和 Vm，並將它們加入 toohello 負載平衡器：</span><span class="sxs-lookup"><span data-stu-id="7d3b0-168">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a><span data-ttu-id="7d3b0-169">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="7d3b0-170">建立 Cloud-init 組態</span><span class="sxs-lookup"><span data-stu-id="7d3b0-170">Create cloud-init config</span></span>
<span data-ttu-id="7d3b0-171">在上一個教學課程中[如何 toocustomize Linux 虛擬機器第一次開機](tutorial-automate-vm-deployment.md)，您學到如何使用雲端 init tooautomate VM 自訂。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-171">In a previous tutorial on [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with cloud-init.</span></span> <span data-ttu-id="7d3b0-172">您可以使用 hello 相同的雲端 init 組態檔案 tooinstall NGINX 並執行簡單的 ' Hello World' Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-172">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="7d3b0-173">您目前的殼層中建立名為*雲端 init.txt*和 hello 貼上下列組態。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-173">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="7d3b0-174">例如，在 hello 雲端 Shell 不在您本機電腦上建立 hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-174">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="7d3b0-175">輸入`sensible-editor cloud-init.txt`toocreate hello 檔案，並查看一份可用的編輯器。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-175">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="7d3b0-176">請確定已正確複製該 hello 整個雲端初始化檔案，特別是 hello 第一行：</span><span class="sxs-lookup"><span data-stu-id="7d3b0-176">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```

### <a name="create-virtual-machines"></a><span data-ttu-id="7d3b0-177">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-177">Create virtual machines</span></span>
<span data-ttu-id="7d3b0-178">tooimprove hello 高可用性的應用程式會將您的 Vm 放在可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-178">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="7d3b0-179">如需可用性設定組的詳細資訊，請參閱先前的 hello[如何 toocreate 高可用性虛擬機器](tutorial-availability-sets.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-179">For more information about availability sets, see hello previous [How toocreate highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="7d3b0-180">使用 [az vm availability-set create](/cli/azure/vm/availability-set#create) 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="7d3b0-181">hello 下列範例會建立可用性設定組具名*myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="7d3b0-181">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="7d3b0-182">現在您可以建立與 hello Vm [az vm 建立](/cli/azure/vm#create)。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-182">Now you can create hello VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="7d3b0-183">hello 下列範例會建立三個 Vm，如果它們尚不存在，會產生 SSH 金鑰：</span><span class="sxs-lookup"><span data-stu-id="7d3b0-183">hello following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

<span data-ttu-id="7d3b0-184">有 hello Azure CLI 會傳回 toohello 提示之後，繼續 toorun 的背景工作。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-184">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="7d3b0-185">hello`--no-wait`參數不會等到所有 hello 工作 toocomplete。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-185">hello `--no-wait` parameter does not wait for all hello tasks toocomplete.</span></span> <span data-ttu-id="7d3b0-186">它可能是另一個數分鐘才能存取 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-186">It may be another couple of minutes before you can access hello app.</span></span> <span data-ttu-id="7d3b0-187">hello 負載平衡器健全狀況探查會自動偵測 hello 應用程式在每個 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-187">hello load balancer health probe automatically detects when hello app is running on each VM.</span></span> <span data-ttu-id="7d3b0-188">一旦 hello 應用程式正在執行，hello 負載平衡器規則會啟動 toodistribute 流量。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-188">Once hello app is running, hello load balancer rule starts toodistribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="7d3b0-189">測試負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-189">Test load balancer</span></span>
<span data-ttu-id="7d3b0-190">取得您的負載平衡器的 hello 公用 IP 位址[az 網路公用 ip 顯示](/cli/azure/network/public-ip#show)。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-190">Obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="7d3b0-191">hello 下列範例會取得 IP 位址 hello *myPublicIP*稍早建立：</span><span class="sxs-lookup"><span data-stu-id="7d3b0-191">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="7d3b0-192">然後，您就可以 tooa 網頁瀏覽器中輸入 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-192">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="7d3b0-193">請記住，-花幾分鐘的時間 hello hello Vm toobe 準備 hello 負載平衡器開始 toodistribute 流量 toothem 之前。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-193">Remember - it takes a few minutes hello hello VMs toobe ready before hello load balancer starts toodistribute traffic toothem.</span></span> <span data-ttu-id="7d3b0-194">hello 應用程式會顯示，包括 hello hello VM 主機名稱的 hello 負載平衡器分散流量 tooas hello 下列範例中：</span><span class="sxs-lookup"><span data-stu-id="7d3b0-194">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![執行 Node.js 應用程式](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="7d3b0-196">toosee hello 負載平衡器會將流量分散到執行您的應用程式的所有三個 Vm，您可以強制重新整理您的 web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-196">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="7d3b0-197">新增和移除 VM</span><span class="sxs-lookup"><span data-stu-id="7d3b0-197">Add and remove VMs</span></span>
<span data-ttu-id="7d3b0-198">您可能需要 tooperform hello 執行您的應用程式，例如安裝作業系統更新的 Vm 上的維護。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-198">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="7d3b0-199">toodeal 使用增加的流量 tooyour 應用程式，您可能需要 tooadd 其他 Vm。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-199">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="7d3b0-200">這個區段會顯示如何 tooremove 或加入 VM 從 hello 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-200">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="7d3b0-201">從 hello 負載平衡器移除 VM</span><span class="sxs-lookup"><span data-stu-id="7d3b0-201">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="7d3b0-202">您可以從 hello 與後端位址集區移除 VM [az 網路 nic ip 設定的位址集區移除](/cli/azure/network/nic/ip-config/address-pool#remove)。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-202">You can remove a VM from hello backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="7d3b0-203">下列範例中移除的 hello hello 虛擬 NIC，供**myVM2**從*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="7d3b0-203">hello following example removes hello virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="7d3b0-204">toosee hello 負載平衡器會將流量分散到 hello 剩餘的兩個 Vm 執行您的應用程式您可以強制重新整理您的 web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-204">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="7d3b0-205">您現在可以在 hello VM，如安裝作業系統更新，或執行 VM 重新啟動電腦上執行維護。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-205">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="7d3b0-206">新增 VM toohello 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-206">Add a VM toohello load balancer</span></span>
<span data-ttu-id="7d3b0-207">之後執行 VM 維護，或者如果您需要 tooexpand 容量時，您可以加入 VM toohello 後端位址集區與[az 網路 nic ip 設定的位址集區新增](/cli/azure/network/nic/ip-config/address-pool#add)。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-207">After performing VM maintenance, or if you need tooexpand capacity, you can add a VM toohello backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="7d3b0-208">hello 下列範例會將 hello 虛擬 NIC，供**myVM2**太*myLoadBalancer*:</span><span class="sxs-lookup"><span data-stu-id="7d3b0-208">hello following example adds hello virtual NIC for **myVM2** too*myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="7d3b0-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7d3b0-209">Next steps</span></span>
<span data-ttu-id="7d3b0-210">在本教學課程中，您可以建立負載平衡器，並附加 Vm tooit。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-210">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="7d3b0-211">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="7d3b0-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7d3b0-212">建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="7d3b0-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="7d3b0-213">建立負載平衡器健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="7d3b0-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="7d3b0-214">建立負載平衡器流量規則</span><span class="sxs-lookup"><span data-stu-id="7d3b0-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="7d3b0-215">使用雲端 init toocreate 基本 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="7d3b0-215">Use cloud-init toocreate a basic Node.js app</span></span>
> * <span data-ttu-id="7d3b0-216">建立虛擬機器，並附加 tooa 負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-216">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="7d3b0-217">檢視作用中的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-217">View a load balancer in action</span></span>
> * <span data-ttu-id="7d3b0-218">新增和移除虛擬機器的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="7d3b0-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="7d3b0-219">前進 toohello 下一個教學課程 toolearn 有關 Azure 虛擬網路元件的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7d3b0-219">Advance toohello next tutorial toolearn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7d3b0-220">管理 VM 和虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7d3b0-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
