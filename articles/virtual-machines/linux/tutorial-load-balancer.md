---
title: "如何在 Azure 中平衡 Linux 虛擬機器的負載 | Microsoft Docs"
description: "了解如何使用 Azure Load Balancer，跨三部 Linux VM 建立高可用性且安全的應用程式"
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
ms.openlocfilehash: 7b3a089d2f6386afcc46cbc4377594be0d758fc6
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-load-balance-linux-virtual-machines-in-azure-to-create-a-highly-available-application"></a><span data-ttu-id="64543-103">如何平衡 Azure 中 Linux 虛擬機器的負載以建立高可用性應用程式</span><span class="sxs-lookup"><span data-stu-id="64543-103">How to load balance Linux virtual machines in Azure to create a highly available application</span></span>
<span data-ttu-id="64543-104">負載平衡會將傳入要求分散到多部虛擬機器，藉此提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="64543-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="64543-105">在本教學課程中，您會了解 Azure Load Balancer 的不同元件，以分散流量並提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="64543-105">In this tutorial, you learn about the different components of the Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="64543-106">您會了解如何：</span><span class="sxs-lookup"><span data-stu-id="64543-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="64543-107">建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="64543-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="64543-108">建立負載平衡器健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="64543-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="64543-109">建立負載平衡器流量規則</span><span class="sxs-lookup"><span data-stu-id="64543-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="64543-110">使用 cloud-init 建立基本的 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="64543-110">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="64543-111">建立虛擬機器並連結至負載平衡器</span><span class="sxs-lookup"><span data-stu-id="64543-111">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="64543-112">檢視作用中的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="64543-112">View a load balancer in action</span></span>
> * <span data-ttu-id="64543-113">新增和移除虛擬機器的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="64543-113">Add and remove VMs from a load balancer</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="64543-114">如果您選擇在本機安裝和使用 CLI，本教學課程會要求您執行 Azure CLI 2.0.4 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="64543-114">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="64543-115">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="64543-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="64543-116">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="64543-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="azure-load-balancer-overview"></a><span data-ttu-id="64543-117">Azure Load Balancer 概觀</span><span class="sxs-lookup"><span data-stu-id="64543-117">Azure load balancer overview</span></span>
<span data-ttu-id="64543-118">Azure Load Balancer 是 Layer-4 (TCP、UDP) 負載平衡器，可將連入流量分散於狀況良好的 VM 來提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="64543-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="64543-119">負載平衡器健康狀態探查會監視每部 VM 上指定的連接埠，且只會將流量分散至作業 VM。</span><span class="sxs-lookup"><span data-stu-id="64543-119">A load balancer health probe monitors a given port on each VM and only distributes traffic to an operational VM.</span></span>

<span data-ttu-id="64543-120">您可定義含有一或多個公用 IP 位址的前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="64543-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="64543-121">此前端 IP 組態允許透過網際網路存取您的負載平衡器和應用程式。</span><span class="sxs-lookup"><span data-stu-id="64543-121">This front-end IP configuration allows your load balancer and applications to be accessible over the Internet.</span></span> 

<span data-ttu-id="64543-122">虛擬機器會使用他其虛擬網路介面卡 (NIC) 連線至負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="64543-122">Virtual machines connect to a load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="64543-123">若要將流量分散至 VM，後端位址集區包含已連線至負載平衡器之虛擬 (NIC) 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="64543-123">To distribute traffic to the VMs, a back-end address pool contains the IP addresses of the virtual (NICs) connected to the load balancer.</span></span>

<span data-ttu-id="64543-124">為了控制流量，您可以定義特定連接埠的負載平衡器規則以及對應至您的 VM 的通訊協定。</span><span class="sxs-lookup"><span data-stu-id="64543-124">To control the flow of traffic, you define load balancer rules for specific ports and protocols that map to your VMs.</span></span>

<span data-ttu-id="64543-125">如果您依照先前的教學課程來[建立虛擬機器擴展集](tutorial-create-vmss.md)，則會為您建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="64543-125">If you followed the previous tutorial to [create a virtual machine scale set](tutorial-create-vmss.md), a load balancer was created for you.</span></span> <span data-ttu-id="64543-126">系統已為您將上述所有元件設定為擴展集的一部分。</span><span class="sxs-lookup"><span data-stu-id="64543-126">All these components were configured for you as part of the scale set.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="64543-127">建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="64543-127">Create Azure load balancer</span></span>
<span data-ttu-id="64543-128">本節將詳細說明如何建立及設定負載平衡器的每個元件。</span><span class="sxs-lookup"><span data-stu-id="64543-128">This section details how you can create and configure each component of the load balancer.</span></span> <span data-ttu-id="64543-129">請先使用 [az group create](/cli/azure/group#create) 建立資源群組，才可建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="64543-129">Before you can create your load balancer, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="64543-130">下列範例會在 eastus 位置建立名為 myResourceGroupLoadBalancer 的資源群組：</span><span class="sxs-lookup"><span data-stu-id="64543-130">The following example creates a resource group named *myResourceGroupLoadBalancer* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="64543-131">建立公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="64543-131">Create a public IP address</span></span>
<span data-ttu-id="64543-132">若要存取網際網路上您的應用程式，您需要負載平衡器的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="64543-132">To access your app on the Internet, you need a public IP address for the load balancer.</span></span> <span data-ttu-id="64543-133">使用 [az network public-ip create](/cli/azure/network/public-ip#create) 建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="64543-133">Create a public IP address with [az network public-ip create](/cli/azure/network/public-ip#create).</span></span> <span data-ttu-id="64543-134">下列範例會在 myResourceGroupLoadBalancer 資源群組中建立名為 myPublicIP 的公用 IP 位址：</span><span class="sxs-lookup"><span data-stu-id="64543-134">The following example creates a public IP address named *myPublicIP* in the *myResourceGroupLoadBalancer* resource group:</span></span>

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="64543-135">建立負載平衡器</span><span class="sxs-lookup"><span data-stu-id="64543-135">Create a load balancer</span></span>
<span data-ttu-id="64543-136">使用 [az network lb create](/cli/azure/network/lb#create) 建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="64543-136">Create a load balancer with [az network lb create](/cli/azure/network/lb#create).</span></span> <span data-ttu-id="64543-137">下列範例會建立名為 myLoadBalancer 的負載平衡器並將 myPublicIP 位址指派給前端 IP 組態：</span><span class="sxs-lookup"><span data-stu-id="64543-137">The following example creates a load balancer named *myLoadBalancer* and assigns the *myPublicIP* address to the front-end IP configuration:</span></span>

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a><span data-ttu-id="64543-138">建立健康狀態探查</span><span class="sxs-lookup"><span data-stu-id="64543-138">Create a health probe</span></span>
<span data-ttu-id="64543-139">若要讓負載平衡器監視您應用程式的狀態，請使用健康狀態探查。</span><span class="sxs-lookup"><span data-stu-id="64543-139">To allow the load balancer to monitor the status of your app, you use a health probe.</span></span> <span data-ttu-id="64543-140">健康狀態探查會根據 VM 對健康狀態檢查的回應，以動態方式從負載平衡器輪替中新增或移除 VM。</span><span class="sxs-lookup"><span data-stu-id="64543-140">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="64543-141">根據預設，在 15 秒的間隔內連續發生兩次失敗後，VM 就會從負載平衡器分配中移除。</span><span class="sxs-lookup"><span data-stu-id="64543-141">By default, a VM is removed from the load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="64543-142">您可根據通訊協定或您應用程式的特定健康狀態檢查頁面，建立健康狀態探查。</span><span class="sxs-lookup"><span data-stu-id="64543-142">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="64543-143">下列範例會建立 TCP 探查。</span><span class="sxs-lookup"><span data-stu-id="64543-143">The following example creates a TCP probe.</span></span> <span data-ttu-id="64543-144">您也可以建立自訂 HTTP 探查，以進行更精細的健康狀態檢查。</span><span class="sxs-lookup"><span data-stu-id="64543-144">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="64543-145">使用自訂 HTTP 探查時，您必須建立健康狀態檢查頁面，例如 healthcheck.js。</span><span class="sxs-lookup"><span data-stu-id="64543-145">When using a custom HTTP probe, you must create the health check page, such as *healthcheck.js*.</span></span> <span data-ttu-id="64543-146">此探查必須對負載平衡器傳回 **HTTP 200 OK** 回應，以將主機保留在輪替中。</span><span class="sxs-lookup"><span data-stu-id="64543-146">The probe must return an **HTTP 200 OK** response for the load balancer to keep the host in rotation.</span></span>

<span data-ttu-id="64543-147">若要建立 TCP 健康狀態探查，請使用 [az network lb probe create](/cli/azure/network/lb/probe#create)。</span><span class="sxs-lookup"><span data-stu-id="64543-147">To create a TCP health probe, you use [az network lb probe create](/cli/azure/network/lb/probe#create).</span></span> <span data-ttu-id="64543-148">下列範例會建立名為 myHealthProbe 的健康狀態探查：</span><span class="sxs-lookup"><span data-stu-id="64543-148">The following example creates a health probe named *myHealthProbe*:</span></span>

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="64543-149">建立負載平衡器規則</span><span class="sxs-lookup"><span data-stu-id="64543-149">Create a load balancer rule</span></span>
<span data-ttu-id="64543-150">負載平衡器規則用來定義如何將流量分散至 VM。</span><span class="sxs-lookup"><span data-stu-id="64543-150">A load balancer rule is used to define how traffic is distributed to the VMs.</span></span> <span data-ttu-id="64543-151">您可定義連入流量的前端 IP 組態及後端 IP 集區來接收流量，以及所需的來源和目的地連接埠。</span><span class="sxs-lookup"><span data-stu-id="64543-151">You define the front-end IP configuration for the incoming traffic and the back-end IP pool to receive the traffic, along with the required source and destination port.</span></span> <span data-ttu-id="64543-152">若要確定只有狀況良好的 VM 可接收流量，您也可定義要使用的健康狀態探查。</span><span class="sxs-lookup"><span data-stu-id="64543-152">To make sure only healthy VMs receive traffic, you also define the health probe to use.</span></span>

<span data-ttu-id="64543-153">使用 [az network lb rule create](/cli/azure/network/lb/rule#create) 建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="64543-153">Create a load balancer rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="64543-154">下列範例會建立名為 myLoadBalancerRule 的規則、使用 myHealthProbe 健康狀態探查，以及平衡連接埠 80 上的流量︰</span><span class="sxs-lookup"><span data-stu-id="64543-154">The following example creates a rule named *myLoadBalancerRule*, uses the *myHealthProbe* health probe, and balances traffic on port *80*:</span></span>

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


## <a name="configure-virtual-network"></a><span data-ttu-id="64543-155">設定虛擬網路</span><span class="sxs-lookup"><span data-stu-id="64543-155">Configure virtual network</span></span>
<span data-ttu-id="64543-156">請先建立支援的虛擬網路資源，才可部署一些 VM 及測試您的平衡器。</span><span class="sxs-lookup"><span data-stu-id="64543-156">Before you deploy some VMs and can test your balancer, create the supporting virtual network resources.</span></span> <span data-ttu-id="64543-157">如需虛擬網路的詳細資訊，請參閱[管理 Azure 虛擬網路](tutorial-virtual-network.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="64543-157">For more information about virtual networks, see the [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="64543-158">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="64543-158">Create network resources</span></span>
<span data-ttu-id="64543-159">使用 [az network vnet create](/cli/azure/network/vnet#create) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="64543-159">Create a virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="64543-160">下列範例會建立名為 myVnet 的虛擬網路和名為 mySubnet 的子網路：</span><span class="sxs-lookup"><span data-stu-id="64543-160">The following example creates a virtual network named *myVnet* with a subnet named *mySubnet*:</span></span>

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

<span data-ttu-id="64543-161">若要新增網路安全性群組，請使用 [az network nsg create](/cli/azure/network/nsg#create)。</span><span class="sxs-lookup"><span data-stu-id="64543-161">To add a network security group, you use [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="64543-162">下列範例建立名為 myNetworkSecurityGroup 的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="64543-162">The following example creates a network security group named *myNetworkSecurityGroup*:</span></span>

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="64543-163">使用 [az network nsg rule create](/cli/azure/network/nsg/rule#create) 建立網路安全性群組規則。</span><span class="sxs-lookup"><span data-stu-id="64543-163">Create a network security group rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="64543-164">下列範例建立名為 myNetworkSecurityGroupRule 的網路安全性群組規則：</span><span class="sxs-lookup"><span data-stu-id="64543-164">The following example creates a network security group rule named *myNetworkSecurityGroupRule*:</span></span>

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

<span data-ttu-id="64543-165">使用 [az network nic create](/cli/azure/network/nic#create) 建立虛擬 NIC。</span><span class="sxs-lookup"><span data-stu-id="64543-165">Virtual NICs are created with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="64543-166">下列範例會建立三個虛擬 NIC。</span><span class="sxs-lookup"><span data-stu-id="64543-166">The following example creates three virtual NICs.</span></span> <span data-ttu-id="64543-167">(您在下列步驟中針對應用程式建立的每部 VM 都有一個虛擬 NIC)。</span><span class="sxs-lookup"><span data-stu-id="64543-167">(One virtual NIC for each VM you create for your app in the following steps).</span></span> <span data-ttu-id="64543-168">您可以隨時建立其他虛擬 NIC 和 VM，並將它們新增至負載平衡器︰</span><span class="sxs-lookup"><span data-stu-id="64543-168">You can create additional virtual NICs and VMs at any time and add them to the load balancer:</span></span>

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

## <a name="create-virtual-machines"></a><span data-ttu-id="64543-169">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="64543-169">Create virtual machines</span></span>

### <a name="create-cloud-init-config"></a><span data-ttu-id="64543-170">建立 Cloud-init 組態</span><span class="sxs-lookup"><span data-stu-id="64543-170">Create cloud-init config</span></span>
<span data-ttu-id="64543-171">在[如何在首次開機時自訂 Linux 虛擬機器](tutorial-automate-vm-deployment.md)的先前教學課程中，您已了解如何使用 cloud-init 自動進行 VM 自訂。</span><span class="sxs-lookup"><span data-stu-id="64543-171">In a previous tutorial on [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md), you learned how to automate VM customization with cloud-init.</span></span> <span data-ttu-id="64543-172">您可以使用相同的 cloud-init 組態檔來安裝 NGINX 和執行簡單的 'Hello World' Node.js 應用程式。</span><span class="sxs-lookup"><span data-stu-id="64543-172">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span>

<span data-ttu-id="64543-173">您目前的殼層中，建立名為 cloud-init.txt 的檔案，並貼上下列組態。</span><span class="sxs-lookup"><span data-stu-id="64543-173">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="64543-174">例如，在 Cloud Shell 中建立不在本機電腦上的檔案。</span><span class="sxs-lookup"><span data-stu-id="64543-174">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="64543-175">輸入 `sensible-editor cloud-init.txt` 可建立檔案，並查看可用的編輯器清單。</span><span class="sxs-lookup"><span data-stu-id="64543-175">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="64543-176">請確定已正確複製整個 cloud-init 檔案，特別是第一行：</span><span class="sxs-lookup"><span data-stu-id="64543-176">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

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

### <a name="create-virtual-machines"></a><span data-ttu-id="64543-177">建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="64543-177">Create virtual machines</span></span>
<span data-ttu-id="64543-178">若要改善您應用程式的高可用性，請將 VM 放在可用性設定組中。</span><span class="sxs-lookup"><span data-stu-id="64543-178">To improve the high availability of your app, place your VMs in an availability set.</span></span> <span data-ttu-id="64543-179">如需可用性設定組的詳細資訊，請參閱[如何建立高可用性虛擬機器](tutorial-availability-sets.md)。</span><span class="sxs-lookup"><span data-stu-id="64543-179">For more information about availability sets, see the previous [How to create highly available virtual machines](tutorial-availability-sets.md) tutorial.</span></span>

<span data-ttu-id="64543-180">使用 [az vm availability-set create](/cli/azure/vm/availability-set#create) 建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="64543-180">Create an availability set with [az vm availability-set create](/cli/azure/vm/availability-set#create).</span></span> <span data-ttu-id="64543-181">下列範例會建立名為 myAvailabilitySet 的可用性設定組：</span><span class="sxs-lookup"><span data-stu-id="64543-181">The following example creates an availability set named *myAvailabilitySet*:</span></span>

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

<span data-ttu-id="64543-182">您現在可以使用 [az vm create](/cli/azure/vm#create) 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="64543-182">Now you can create the VMs with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="64543-183">下列範例會建立三部 VM 並產生 SSH 金鑰 (如果尚未存在的話)︰</span><span class="sxs-lookup"><span data-stu-id="64543-183">The following example creates three VMs and generates SSH keys if they do not already exist:</span></span>

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

<span data-ttu-id="64543-184">在 Azure CLI 將您返回提示字元之後，背景工作會繼續執行。</span><span class="sxs-lookup"><span data-stu-id="64543-184">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="64543-185">`--no-wait` 參數不會等待所有工作完成。</span><span class="sxs-lookup"><span data-stu-id="64543-185">The `--no-wait` parameter does not wait for all the tasks to complete.</span></span> <span data-ttu-id="64543-186">可能需要再等候幾分鐘，才能存取應用程式。</span><span class="sxs-lookup"><span data-stu-id="64543-186">It may be another couple of minutes before you can access the app.</span></span> <span data-ttu-id="64543-187">負載平衡器會自動偵測應用程式何時在每部 VM 上執行。</span><span class="sxs-lookup"><span data-stu-id="64543-187">The load balancer health probe automatically detects when the app is running on each VM.</span></span> <span data-ttu-id="64543-188">當應用程式正在執行時，負載平衡器規則就開始分配流量。</span><span class="sxs-lookup"><span data-stu-id="64543-188">Once the app is running, the load balancer rule starts to distribute traffic.</span></span>


## <a name="test-load-balancer"></a><span data-ttu-id="64543-189">測試負載平衡器</span><span class="sxs-lookup"><span data-stu-id="64543-189">Test load balancer</span></span>
<span data-ttu-id="64543-190">使用 [az network public-ip show](/cli/azure/network/public-ip#show) 取得負載平衡器的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="64543-190">Obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="64543-191">下列範例會取得稍早建立的 myPublicIP IP 位址︰</span><span class="sxs-lookup"><span data-stu-id="64543-191">The following example obtains the IP address for *myPublicIP* created earlier:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="64543-192">接著，您可以在 Web 瀏覽器中輸入公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="64543-192">You can then enter the public IP address in to a web browser.</span></span> <span data-ttu-id="64543-193">請記住，負載平衡器開始將流量分散給 VM 之前，VM 需要花幾分鐘的時間才會就緒。</span><span class="sxs-lookup"><span data-stu-id="64543-193">Remember - it takes a few minutes the the VMs to be ready before the load balancer starts to distribute traffic to them.</span></span> <span data-ttu-id="64543-194">應用程式隨即顯示，包括負載平衡器分散流量之 VM 的主機名稱，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="64543-194">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to as in the following example:</span></span>

![執行 Node.js 應用程式](./media/tutorial-load-balancer/running-nodejs-app.png)

<span data-ttu-id="64543-196">若要查看負載平衡器如何將流量分散於執行您應用程式的這三部 VM，您可以強制重新整理您的 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="64543-196">To see the load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="64543-197">新增和移除 VM</span><span class="sxs-lookup"><span data-stu-id="64543-197">Add and remove VMs</span></span>
<span data-ttu-id="64543-198">您可能需要在執行您應用程式的 VM 上執行維護，例如安裝 OS 更新。</span><span class="sxs-lookup"><span data-stu-id="64543-198">You may need to perform maintenance on the VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="64543-199">若要處理您應用程式增加的流量，您可能需要新增額外的 VM。</span><span class="sxs-lookup"><span data-stu-id="64543-199">To deal with increased traffic to your app, you may need to add additional VMs.</span></span> <span data-ttu-id="64543-200">本節說明如何在負載平衡器中移除或新增 VM。</span><span class="sxs-lookup"><span data-stu-id="64543-200">This section shows you how to remove or add a VM from the load balancer.</span></span>

### <a name="remove-a-vm-from-the-load-balancer"></a><span data-ttu-id="64543-201">從負載平衡器移除 VM</span><span class="sxs-lookup"><span data-stu-id="64543-201">Remove a VM from the load balancer</span></span>
<span data-ttu-id="64543-202">您可以使用 [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove) 從後端位址集區移除 VM。</span><span class="sxs-lookup"><span data-stu-id="64543-202">You can remove a VM from the backend address pool with [az network nic ip-config address-pool remove](/cli/azure/network/nic/ip-config/address-pool#remove).</span></span> <span data-ttu-id="64543-203">下列範例會從 myLoadBalancer 移除myVM2 的虛擬 NIC：</span><span class="sxs-lookup"><span data-stu-id="64543-203">The following example removes the virtual NIC for **myVM2** from *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

<span data-ttu-id="64543-204">若要查看負載平衡器如何將流量分散到其餘兩部執行您應用程式的 VM，您可以強制重新整理您的 Web 瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="64543-204">To see the load balancer distribute traffic across the remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="64543-205">您現在可以在 VM 上執行維護，例如安裝 OS 更新或執行 VM 重新開機。</span><span class="sxs-lookup"><span data-stu-id="64543-205">You can now perform maintenance on the VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-to-the-load-balancer"></a><span data-ttu-id="64543-206">將 VM 新增至負載平衡器</span><span class="sxs-lookup"><span data-stu-id="64543-206">Add a VM to the load balancer</span></span>
<span data-ttu-id="64543-207">在執行 VM 維護之後，或者如果需要擴充容量，您可以使用 [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add) 將 VM 新增至後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="64543-207">After performing VM maintenance, or if you need to expand capacity, you can add a VM to the backend address pool with [az network nic ip-config address-pool add](/cli/azure/network/nic/ip-config/address-pool#add).</span></span> <span data-ttu-id="64543-208">下列範例會將 myVM2 的虛擬 NIC 新增至 myLoadBalancer：</span><span class="sxs-lookup"><span data-stu-id="64543-208">The following example adds the virtual NIC for **myVM2** to *myLoadBalancer*:</span></span>

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a><span data-ttu-id="64543-209">後續步驟</span><span class="sxs-lookup"><span data-stu-id="64543-209">Next steps</span></span>
<span data-ttu-id="64543-210">在本教學課程中，您建立負載平衡器，並將 VM 連結到它。</span><span class="sxs-lookup"><span data-stu-id="64543-210">In this tutorial, you created a load balancer and attached VMs to it.</span></span> <span data-ttu-id="64543-211">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="64543-211">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="64543-212">建立 Azure Load Balancer</span><span class="sxs-lookup"><span data-stu-id="64543-212">Create an Azure load balancer</span></span>
> * <span data-ttu-id="64543-213">建立負載平衡器健全狀況探查</span><span class="sxs-lookup"><span data-stu-id="64543-213">Create a load balancer health probe</span></span>
> * <span data-ttu-id="64543-214">建立負載平衡器流量規則</span><span class="sxs-lookup"><span data-stu-id="64543-214">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="64543-215">使用 cloud-init 建立基本的 Node.js 應用程式</span><span class="sxs-lookup"><span data-stu-id="64543-215">Use cloud-init to create a basic Node.js app</span></span>
> * <span data-ttu-id="64543-216">建立虛擬機器並連結至負載平衡器</span><span class="sxs-lookup"><span data-stu-id="64543-216">Create virtual machines and attach to a load balancer</span></span>
> * <span data-ttu-id="64543-217">檢視作用中的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="64543-217">View a load balancer in action</span></span>
> * <span data-ttu-id="64543-218">新增和移除虛擬機器的負載平衡器</span><span class="sxs-lookup"><span data-stu-id="64543-218">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="64543-219">請前進到下一個教學課程，以深入了解 Azure 虛擬網路元件。</span><span class="sxs-lookup"><span data-stu-id="64543-219">Advance to the next tutorial to learn more about Azure virtual network components.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="64543-220">管理 VM 和虛擬網路</span><span class="sxs-lookup"><span data-stu-id="64543-220">Manage VMs and virtual networks</span></span>](tutorial-virtual-network.md)
