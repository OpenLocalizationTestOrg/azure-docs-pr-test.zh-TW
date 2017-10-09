---
title: "aaaAzure 虛擬網路和 Linux 虛擬機器 |Microsoft 文件"
description: "教學課程-使用 Azure CLI hello 管理 Azure 虛擬網路和 Linux 虛擬機器"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a><span data-ttu-id="7ebd1-103">使用 Azure CLI hello 管理 Azure 虛擬網路和 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7ebd1-103">Manage Azure Virtual Networks and Linux Virtual Machines with hello Azure CLI</span></span>

<span data-ttu-id="7ebd1-104">Azure 虛擬機器會使用 Azure 網路進行內部和外部的網路通訊。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="7ebd1-105">本教學課程會逐步部署兩部虛擬機器 (VM)，並設定這兩部 VM 的 Azure 網路功能。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="7ebd1-106">此教學課程中的 hello 範例假設 hello Vm 都裝載 web 應用程式與資料庫後端，但未在 hello 教學課程中部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-106">hello examples in this tutorial assume that hello VMs are hosting a web application with a database back-end, however an application is not deployed in hello tutorial.</span></span> <span data-ttu-id="7ebd1-107">在本教學課程中，您將了解如何：</span><span class="sxs-lookup"><span data-stu-id="7ebd1-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ebd1-108">部署虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7ebd1-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="7ebd1-109">在虛擬網路中建立子網路</span><span class="sxs-lookup"><span data-stu-id="7ebd1-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="7ebd1-110">附加虛擬機器 tooa 子網路</span><span class="sxs-lookup"><span data-stu-id="7ebd1-110">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="7ebd1-111">管理虛擬機器的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7ebd1-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="7ebd1-112">保護傳入的網際網路流量</span><span class="sxs-lookup"><span data-stu-id="7ebd1-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="7ebd1-113">確保 VM tooVM 流量的安全</span><span class="sxs-lookup"><span data-stu-id="7ebd1-113">Secure VM tooVM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7ebd1-114">如果您選擇 tooinstall，並在本機上使用 hello CLI，本教學課程需要您執行 hello Azure CLI 版本 2.0.4 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="7ebd1-115">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="7ebd1-116">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="7ebd1-117">VM 網路概觀</span><span class="sxs-lookup"><span data-stu-id="7ebd1-117">VM networking overview</span></span>

<span data-ttu-id="7ebd1-118">Azure 虛擬網路啟用安全的網路連線的虛擬機器之間，hello 網際網路及其他 Azure 服務，例如 Azure SQL database。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-118">Azure virtual networks enable secure network connections between virtual machines, hello internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="7ebd1-119">虛擬網路會被分割成邏輯區段，稱為子網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="7ebd1-120">子網路可用 toocontrol 網路流量，及做為安全性界限。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-120">Subnets are used toocontrol network flow, and as a security boundary.</span></span> <span data-ttu-id="7ebd1-121">在部署 VM 時，它通常會包含在虛擬網路介面，也就是附加的 tooa 子網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-121">When deploying a VM, it generally includes a virtual network interface, which is attached tooa subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="7ebd1-122">部署虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7ebd1-122">Deploy virtual network</span></span>

<span data-ttu-id="7ebd1-123">在本教學課程中，會建立一個具有兩個子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="7ebd1-124">一個是裝載 Web 應用程式的前端子網路，一個是裝載資料庫伺服器的後端子網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="7ebd1-125">建立虛擬網路前，請先使用 [az group create](/cli/azure/group#create) 建立資源群組。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7ebd1-126">hello 下列範例會建立名為的資源群組*myRGNetwork* hello eastus 位置中。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-126">hello following example creates a resource group named *myRGNetwork* in hello eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="7ebd1-127">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7ebd1-127">Create virtual network</span></span>

<span data-ttu-id="7ebd1-128">我們 hello [az 網路 vnet 建立](/cli/azure/network/vnet#create)命令 toocreate 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-128">Us hello [az network vnet create](/cli/azure/network/vnet#create) command toocreate a virtual network.</span></span> <span data-ttu-id="7ebd1-129">在此範例中，名為 hello 網路*mvVnet*和指定的位址首碼*10.0.0.0/16*。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-129">In this example, hello network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="7ebd1-130">也會建立名為 mySubnetFrontEnd 且首碼為 10.0.1.0/24 的子網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="7ebd1-131">稍後在本教學課程前端 VM 是已連線的 toothis 子網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-131">Later in this tutorial a front-end VM is connected toothis subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="7ebd1-132">建立子網路</span><span class="sxs-lookup"><span data-stu-id="7ebd1-132">Create subnet</span></span>

<span data-ttu-id="7ebd1-133">新的子網路加入 toohello 虛擬網路使用 hello [az vnet 子網路建立](/cli/azure/network/vnet/subnet#create)命令。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-133">A new subnet is added toohello virtual network using hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="7ebd1-134">在此範例中，名為 hello 子網路*mySubnetBackEnd*和指定的位址首碼*10.0.2.0/24*。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-134">In this example, hello subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="7ebd1-135">所有的後端服務都會使用此子網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="7ebd1-136">此時，已建立一個網路並分割成兩個子網路，一個用於前端的服務，另一個用於後端服務。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="7ebd1-137">在 hello 下一步 區段中，虛擬機器建立和連線 toothese 子網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-137">In hello next section, virtual machines are created and connected toothese subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="7ebd1-138">認識公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7ebd1-138">Understand public IP address</span></span>

<span data-ttu-id="7ebd1-139">公用 IP 位址允許存取的 Azure 資源 toobe hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-139">A public IP address allows Azure resources toobe accessible on hello internet.</span></span> <span data-ttu-id="7ebd1-140">在本節中的 hello 教學課程中，VM 會建立的 toodemonstrate toowork 與公用 IP 位址的方式。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-140">In this section of hello tutorial, a VM is created toodemonstrate how toowork with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="7ebd1-141">配置方法</span><span class="sxs-lookup"><span data-stu-id="7ebd1-141">Allocation method</span></span>

<span data-ttu-id="7ebd1-142">公用 IP 位址可以動態或靜態配置。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="7ebd1-143">預設是以動態方式配置公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="7ebd1-144">VM 解除配置時，就會釋放動態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="7ebd1-145">這個行為會包含 VM 解除配置的任何作業期間造成 hello IP 位址 toochange。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-145">This behavior causes hello IP address toochange during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="7ebd1-146">hello 配置方法可以設定 toostatic，後者可確保 hello IP 位址的保留期間，指派給 tooa VM，即使解除配置的狀態。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-146">hello allocation method can be set toostatic, which ensures that hello IP address remain assigned tooa VM, even during a deallocated state.</span></span> <span data-ttu-id="7ebd1-147">使用靜態配置的 IP 位址，無法指定本身 hello IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-147">When using a statically allocated IP address, hello IP address itself cannot be specified.</span></span> <span data-ttu-id="7ebd1-148">而是從可用位址集區配置一個給它。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="7ebd1-149">動態配置</span><span class="sxs-lookup"><span data-stu-id="7ebd1-149">Dynamic allocation</span></span>

<span data-ttu-id="7ebd1-150">Hello 與建立 VM 時[az vm 建立](/cli/azure/vm#create)命令時，是動態的 hello 預設公用 IP 位址配置方法。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-150">When creating a VM with hello [az vm create](/cli/azure/vm#create) command, hello default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="7ebd1-151">在下列範例的 hello，VM 會建立具有動態的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-151">In hello following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="7ebd1-152">靜態配置</span><span class="sxs-lookup"><span data-stu-id="7ebd1-152">Static allocation</span></span>

<span data-ttu-id="7ebd1-153">當建立虛擬機器使用 hello [az vm 建立](/cli/azure/vm#create)命令，包括 hello`--public-ip-address-allocation static`引數 tooassign 靜態公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-153">When creating a virtual machine using hello [az vm create](/cli/azure/vm#create) command, include hello `--public-ip-address-allocation static` argument tooassign a static public IP address.</span></span> <span data-ttu-id="7ebd1-154">這項作業不會示範在本教學課程中，不過 hello 下一節的動態配置的 IP 位址已變更的 tooa 靜態配置的位址。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-154">This operation is not demonstrated in this tutorial, however in hello next section a dynamically allocated IP address is changed tooa statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="7ebd1-155">變更配置方法</span><span class="sxs-lookup"><span data-stu-id="7ebd1-155">Change allocation method</span></span>

<span data-ttu-id="7ebd1-156">可以使用 hello 變更 hello IP 位址配置方法[az 網路公用 ip 更新](/cli/azure/network/public-ip#update)命令。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-156">hello IP address allocation method can be changed using hello [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="7ebd1-157">在此範例中，hello 的 hello 變更前端 VM 的 IP 位址配置方法 toostatic。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-157">In this example, hello IP address allocation method of hello front-end VM is changed toostatic.</span></span>

<span data-ttu-id="7ebd1-158">首先，取消配置 hello VM。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-158">First, deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="7ebd1-159">使用 hello [az 網路公用 ip 更新](/cli/azure/network/public-ip#update)命令 tooupdate hello 配置方法。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-159">Use hello [az network public-ip update](/cli/azure/network/public-ip#update) command tooupdate hello allocation method.</span></span> <span data-ttu-id="7ebd1-160">在此情況下，hello`--allocation-method`太設定*靜態*。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-160">In this case, hello `--allocation-method` is being set too*static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="7ebd1-161">啟動 hello VM。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-161">Start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="7ebd1-162">無公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7ebd1-162">No public IP address</span></span>

<span data-ttu-id="7ebd1-163">通常，VM 不需要 toobe 可以透過 hello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-163">Often, a VM does not need toobe accessible over hello internet.</span></span> <span data-ttu-id="7ebd1-164">toocreate VM 不含公用 IP 位址，使用 hello`--public-ip-address ""`引數以雙引號括住的空集合。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-164">toocreate a VM without a public IP address, use hello `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="7ebd1-165">此組態稍後會在本教學課程中示範。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="7ebd1-166">保護網路流量</span><span class="sxs-lookup"><span data-stu-id="7ebd1-166">Secure network traffic</span></span>

<span data-ttu-id="7ebd1-167">網路安全性群組 (NSG) 包含可允許或拒絕網路流量 tooresources 連接 tooAzure 虛擬網路 (VNet) 安全性規則的清單。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooAzure Virtual Networks (VNet).</span></span> <span data-ttu-id="7ebd1-168">Nsg 可以是相關聯的 toosubnets 或個別的網路介面。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-168">NSGs can be associated toosubnets or individual network interfaces.</span></span> <span data-ttu-id="7ebd1-169">NSG 相關聯的網路介面時，它將適用於僅 hello 相關聯的 VM。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-169">When an NSG is associated with a network interface, it applies only hello associated VM.</span></span> <span data-ttu-id="7ebd1-170">當 NSG 相關聯的 tooa 子網路，hello 規則適用於 tooall 資源連線的 toohello 子網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-170">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="7ebd1-171">網路安全性群組規則</span><span class="sxs-lookup"><span data-stu-id="7ebd1-171">Network security group rules</span></span>

<span data-ttu-id="7ebd1-172">NSG 規則定義允許或拒絕流量的網路連接埠。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="7ebd1-173">hello 規則可以包含來源和目的地 IP 位址範圍，以便控制特定的系統或子網路之間流量。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-173">hello rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="7ebd1-174">NSG 規則也包含優先順序 (介於 1 和 4096)。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="7ebd1-175">會評估 hello 依優先順序的規則。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-175">Rules are evaluated in hello order of priority.</span></span> <span data-ttu-id="7ebd1-176">優先順序 100 的規則會比優先順序 200 的規則優先評估。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="7ebd1-177">所有 NSG 都包含一組預設規則。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="7ebd1-178">無法刪除 hello 預設規則，但它們指派 hello 最低優先權，因為它們會覆寫由您所建立的 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-178">hello default rules cannot be deleted, but because they are assigned hello lowest priority, they can be overridden by hello rules that you create.</span></span>

- <span data-ttu-id="7ebd1-179">**虛擬網路** - 虛擬網路中的流量起始和結束同時允許輸入和輸出方向。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="7ebd1-180">**網際網路** - 允許輸出流量，但會封鎖輸入流量。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="7ebd1-181">**負載平衡器**-允許 Azure 負載平衡器 tooprobe hello 和健康狀態的 Vm 角色執行個體。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-181">**Load balancer** - Allow Azure’s load balancer tooprobe hello health of your VMs and role instances.</span></span> <span data-ttu-id="7ebd1-182">如果您不使用負載平衡的集合，則可以覆寫此規則。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="7ebd1-183">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="7ebd1-183">Create network security groups</span></span>

<span data-ttu-id="7ebd1-184">網路安全性群組可以在建立 hello 相同時間當作 VM 使用 hello [az vm 建立](/cli/azure/vm#create)命令。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-184">A network security group can be created at hello same time as a VM using hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="7ebd1-185">這樣一來，當 hello NSG 關聯的 hello Vm 網路介面，NSG 規則是連接埠上的自動建立 tooallow 流量*22*從任何來源。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-185">When doing so, hello NSG is associated with hello VMs network interface and an NSG rule is auto created tooallow traffic on port *22* from any source.</span></span> <span data-ttu-id="7ebd1-186">稍早在本教學課程中，前端 NSG 已使用自動建立的 hello hello 前端 VM。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-186">Earlier in this tutorial, hello front-end NSG was auto-created with hello front-end VM.</span></span> <span data-ttu-id="7ebd1-187">也會自動建立連接埠 22 的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="7ebd1-188">在某些情況下，可能會很有幫助 toopre-建立 NSG，例如當應該不會建立預設 SSH 規則，或當 hello NSG 應該附加的 tooa 子網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-188">In some cases, it may be helpful toopre-create an NSG, such as when default SSH rules should not be created, or when hello NSG should be attached tooa subnet.</span></span> 

<span data-ttu-id="7ebd1-189">使用 hello [az 網路 nsg 建立](/cli/azure/network/nsg#create)命令 toocreate 網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-189">Use hello [az network nsg create](/cli/azure/network/nsg#create) command toocreate a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="7ebd1-190">而不是建立 hello NSG tooa 網路介面的關聯，它是子網路相關聯。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-190">Instead of associating hello NSG tooa network interface, it is associated with a subnet.</span></span> <span data-ttu-id="7ebd1-191">在此組態中，任何附加的 toohello 子網路的 VM 會繼承 hello NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-191">In this configuration, any VM that is attached toohello subnet inherits hello NSG rules.</span></span>

<span data-ttu-id="7ebd1-192">更新 hello 現有子網路，名為*mySubnetBackEnd*與 hello 新的 NSG。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-192">Update hello existing subnet named *mySubnetBackEnd* with hello new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="7ebd1-193">現在建立虛擬機器，也就是附加的 toohello *mySubnetBackEnd*。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-193">Now create a virtual machine, which is attached toohello *mySubnetBackEnd*.</span></span> <span data-ttu-id="7ebd1-194">請注意該 hello`--nsg`引數的值為空的雙引號。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-194">Notice that hello `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="7ebd1-195">NSG 不需要建立以 hello VM toobe。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-195">An NSG does not need toobe created with hello VM.</span></span> <span data-ttu-id="7ebd1-196">hello VM 是附加的 toohello 後端子，是使用預先建立後端 NSG hello 保護。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-196">hello VM is attached toohello back-end subnet, which is protected with hello pre-created back-end NSG.</span></span> <span data-ttu-id="7ebd1-197">此 NSG 會套用 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-197">This NSG applies toohello VM.</span></span> <span data-ttu-id="7ebd1-198">另外而且請注意這裡該 hello`--public-ip-address`引數的值為空的雙引號。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-198">Also, notice here that hello `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="7ebd1-199">此組態會建立無公用 IP 位址的 VM。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="7ebd1-200">保護傳入的流量</span><span class="sxs-lookup"><span data-stu-id="7ebd1-200">Secure incoming traffic</span></span>

<span data-ttu-id="7ebd1-201">Hello 前端 VM 建立時，NSG 規則 tooallow 連入流量上建立通訊埠 22。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-201">When hello front-end VM was created, an NSG rule was created tooallow incoming traffic on port 22.</span></span> <span data-ttu-id="7ebd1-202">此規則可讓 SSH 連線 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-202">This rule allows SSH connections toohello VM.</span></span> <span data-ttu-id="7ebd1-203">在此範例中，應該也允許連接埠 80 上的流量。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="7ebd1-204">此設定可讓 web 應用程式 toobe hello VM 上的存取。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-204">This configuration allows a web application toobe accessed on hello VM.</span></span>

<span data-ttu-id="7ebd1-205">使用 hello [az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)命令 toocreate 規則; 連接埠*80*。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-205">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="7ebd1-206">hello 前端 VM 現在只有為連接埠上*22*和連接埠*80*。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-206">hello front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="7ebd1-207">其他所有的連入流量會在網路安全性群組 hello 遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-207">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="7ebd1-208">它可能會很有幫助 toovisualize hello NSG 規則設定。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-208">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="7ebd1-209">傳回 hello NSG 規則設定，以 hello [az 網路規則清單](/cli/azure/network/nsg/rule#list)命令。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-209">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="7ebd1-210">輸出：</span><span class="sxs-lookup"><span data-stu-id="7ebd1-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a><span data-ttu-id="7ebd1-211">確保 VM tooVM 流量的安全</span><span class="sxs-lookup"><span data-stu-id="7ebd1-211">Secure VM tooVM traffic</span></span>

<span data-ttu-id="7ebd1-212">網路安全性群組規則也可以套用在 VM 之間。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="7ebd1-213">針對此範例中，前端 VM 需要 toocommunicate 與 hello hello 連接埠上的後端 VM *22*和*3306*。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-213">For this example, hello front-end VM needs toocommunicate with hello back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="7ebd1-214">此設定可讓來自 SSH 連線 hello 前端 VM，而且也允許 hello 前端 VM toocommunicate 與後端 MySQL 資料庫上的 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-214">This configuration allows SSH connections from hello front-end VM, and also allow an application on hello front-end VM toocommunicate with a back-end MySQL database.</span></span> <span data-ttu-id="7ebd1-215">Hello 前端和後端的虛擬機器之間，應予封鎖所有其他流量。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-215">All other traffic should be blocked between hello front-end and back-end virtual machines.</span></span>

<span data-ttu-id="7ebd1-216">使用 hello [az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)命令 toocreate 規則; 連接埠 22。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-216">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port 22.</span></span> <span data-ttu-id="7ebd1-217">請注意該 hello`--source-address-prefix`引數指定的值*10.0.1.0/24*。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-217">Notice that hello `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="7ebd1-218">此組態可確保只有 hello 前端子網路的流量，允許透過 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-218">This configuration ensures that only traffic from hello front-end subnet is allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="7ebd1-219">現在新增連接埠 3306 上 MySQL 流量的規則。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="7ebd1-220">最後，因為 Nsg 預設規則允許所有流量 hello 的 Vm 之間相同的 VNet，規則可以建立 hello 後端 Nsg tooblock 所有流量。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-220">Finally, because NSGs have a default rule allowing all traffic between VMs in hello same VNet, a rule can be created for hello back-end NSGs tooblock all traffic.</span></span> <span data-ttu-id="7ebd1-221">在這裡看到該 hello`--priority`給定的值*300*，這是較低兩者 hello NSG 和 MySQL 的規則。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-221">Notice here that hello `--priority` is given a value of *300*, which is lower that both hello NSG and MySQL rules.</span></span> <span data-ttu-id="7ebd1-222">此組態可確保透過 hello NSG，仍允許 SSH 和 MySQL 的流量。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-222">This configuration ensures that SSH and MySQL traffic is still allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="7ebd1-223">hello 後端 VM 現在只有為連接埠上*22*和連接埠*3306*從 hello 前端子網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-223">hello back-end VM is now only accessible on port *22* and port *3306* from hello front-end subnet.</span></span> <span data-ttu-id="7ebd1-224">其他所有的連入流量會在網路安全性群組 hello 遭到封鎖。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-224">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="7ebd1-225">它可能會很有幫助 toovisualize hello NSG 規則設定。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-225">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="7ebd1-226">傳回 hello NSG 規則設定，以 hello [az 網路規則清單](/cli/azure/network/nsg/rule#list)命令。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-226">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="7ebd1-227">輸出：</span><span class="sxs-lookup"><span data-stu-id="7ebd1-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="7ebd1-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7ebd1-228">Next steps</span></span>

<span data-ttu-id="7ebd1-229">在本教學課程中，您可以建立並保護做為相關的 toovirtual 機器的 Azure 網路。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-229">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> <span data-ttu-id="7ebd1-230">您已了解如何︰</span><span class="sxs-lookup"><span data-stu-id="7ebd1-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="7ebd1-231">部署虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7ebd1-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="7ebd1-232">在虛擬網路中建立子網路</span><span class="sxs-lookup"><span data-stu-id="7ebd1-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="7ebd1-233">附加虛擬機器 tooa 子網路</span><span class="sxs-lookup"><span data-stu-id="7ebd1-233">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="7ebd1-234">管理虛擬機器的公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="7ebd1-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="7ebd1-235">保護傳入的網際網路流量</span><span class="sxs-lookup"><span data-stu-id="7ebd1-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="7ebd1-236">確保 VM tooVM 流量的安全</span><span class="sxs-lookup"><span data-stu-id="7ebd1-236">Secure VM tooVM traffic</span></span>

<span data-ttu-id="7ebd1-237">前進 toohello 下一個教學課程的 toolearn 有關使用 Azure 備份的虛擬機器上的資料。</span><span class="sxs-lookup"><span data-stu-id="7ebd1-237">Advance toohello next tutorial toolearn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="7ebd1-238">備份 Azure 中的 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="7ebd1-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
