---
title: "aaaUse vm 的內部 DNS 名稱解析與 hello Azure CLI 2.0 |Microsoft 文件"
description: "Toocreate 虛擬網路介面卡的方式，以及用於在 Azure 上以 hello Azure CLI 2.0 的 VM 名稱解析的內部 DNS"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: b3c4bfd3ab698f7b25d763ba9e60dd7984f6269d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-virtual-network-interface-cards-and-use-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="7a3e4-103">在 Azure 上建立虛擬網路介面卡並使用內部 DNS 進行 VM 名稱解析</span><span class="sxs-lookup"><span data-stu-id="7a3e4-103">Create virtual network interface cards and use internal DNS for VM name resolution on Azure</span></span>
<span data-ttu-id="7a3e4-104">本文章將示範如何 tooset 靜態內部 DNS 名稱適用於 Linux Vm 使用虛擬網路介面卡 (vNics) 和標籤名稱，DNS hello Azure CLI 2.0。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-104">This article shows you how tooset static internal DNS names for Linux VMs using virtual network interface cards (vNics) and DNS label names with hello Azure CLI 2.0.</span></span> <span data-ttu-id="7a3e4-105">您也可以執行下列步驟以 hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-105">You can also perform these steps with hello [Azure CLI 1.0](static-dns-name-resolution-for-linux-on-azure-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7a3e4-106">靜態 DNS 名稱是用於永久基礎結構服務，例如 Jenkins 組建伺服器，它用於這份文件或 Git 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-106">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="7a3e4-107">hello 需求如下：</span><span class="sxs-lookup"><span data-stu-id="7a3e4-107">hello requirements are:</span></span>

* [<span data-ttu-id="7a3e4-108">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="7a3e4-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="7a3e4-109">SSH 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="7a3e4-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quick-commands"></a><span data-ttu-id="7a3e4-110">快速命令</span><span class="sxs-lookup"><span data-stu-id="7a3e4-110">Quick commands</span></span>
<span data-ttu-id="7a3e4-111">如果您需要 tooquickly 完成 hello 工作，下列區段的 hello 詳細資料所需的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-111">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="7a3e4-112">詳細資訊和內容的每個步驟可以在 hello hello 文件的其餘部分[這裡啟動](#detailed-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-112">More detailed information and context for each step can be found in hello rest of hello document, [starting here](#detailed-walkthrough).</span></span> <span data-ttu-id="7a3e4-113">tooperform 這些步驟，您需要 hello 最新[Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-113">tooperform these steps, you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="7a3e4-114">先決條件︰資源群組、虛擬網路與子網路、具有 SSH 輸入的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-114">Pre-Requirements: Resource Group, virtual network and subnet, Network Security Group with SSH inbound.</span></span>

### <a name="create-a-virtual-network-interface-card-with-a-static-internal-dns-name"></a><span data-ttu-id="7a3e4-115">使用靜態內部 DNS 名稱來建立虛擬網路介面卡</span><span class="sxs-lookup"><span data-stu-id="7a3e4-115">Create a virtual network interface card with a static internal DNS name</span></span>
<span data-ttu-id="7a3e4-116">建立與 hello vNic [az 網路 nic 建立](/cli/azure/network/nic#create)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-116">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="7a3e4-117">hello `--internal-dns-name` CLI 旗標適用於設定 hello DNS 標籤，可提供 hello hello 虛擬網路介面卡 (vNic) 的靜態 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-117">hello `--internal-dns-name` CLI flag is for setting hello DNS label, which provides hello static DNS name for hello virtual network interface card (vNic).</span></span> <span data-ttu-id="7a3e4-118">hello 下列範例會建立名為 vNic `myNic`，將它連接 toohello`myVnet`虛擬網路，並建立呼叫的內部 DNS 名稱記錄`jenkins`:</span><span class="sxs-lookup"><span data-stu-id="7a3e4-118">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

### <a name="deploy-a-vm-and-connect-hello-vnic"></a><span data-ttu-id="7a3e4-119">部署 VM，並連接 hello vNic</span><span class="sxs-lookup"><span data-stu-id="7a3e4-119">Deploy a VM and connect hello vNic</span></span>
<span data-ttu-id="7a3e4-120">使用 [az vm create](/cli/azure/vm#create) 來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-120">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="7a3e4-121">hello`--nics`旗標在 hello 部署 tooAzure 期間連線 hello vNic toohello VM。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-121">hello `--nics` flag connects hello vNic toohello VM during hello deployment tooAzure.</span></span> <span data-ttu-id="7a3e4-122">hello 下列範例會建立名為的 VM`myVM`與 Azure 受管理磁碟和名為附加 hello vNic`myNic`從前面步驟中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a3e4-122">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="7a3e4-123">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="7a3e4-123">Detailed walkthrough</span></span>

<span data-ttu-id="7a3e4-124">完整的持續整合與連續部署 (CiCd) 在 Azure 上的基礎結構需要特定伺服器 toobe 靜態或長時間執行的伺服器。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-124">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span> <span data-ttu-id="7a3e4-125">建議您使用 Azure 資產像 hello 虛擬網路與網路安全性群組是靜態的而且長時間存在很少部署的資源。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-125">It is recommended that Azure assets like hello virtual networks and Network Security Groups are static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="7a3e4-126">部署虛擬網路之後可以重複使用由沒有任何負面影響 toohello 基礎結構的新部署。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-126">Once a virtual network has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="7a3e4-127">您可以稍後加入 Git 儲存機制伺服器或 Jenkins automation 伺服器提供您開發或測試環境的 CiCd toothis 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-127">You can later add a Git repository server or a Jenkins automation server delivers CiCd toothis virtual network for your development or test environments.</span></span>  

<span data-ttu-id="7a3e4-128">僅可在 Azure 虛擬網路內解析內部 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-128">Internal DNS names are only resolvable inside an Azure virtual network.</span></span> <span data-ttu-id="7a3e4-129">Hello DNS 名稱是內部的因為它們不是解析 toohello 外部網際網路上，提供額外的安全性 toohello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-129">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="7a3e4-130">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-130">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="7a3e4-131">範例參數名稱包含 `myResourceGroup`、`myNic` 和 `myVM`。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-131">Example parameter names include `myResourceGroup`, `myNic`, and `myVM`.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="7a3e4-132">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="7a3e4-132">Create hello resource group</span></span>
<span data-ttu-id="7a3e4-133">首先，建立具有 hello 資源群組[az 群組建立](/cli/azure/group#create)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-133">First, create hello resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="7a3e4-134">hello 下列範例會建立名為的資源群組`myResourceGroup`在 hello`westus`位置：</span><span class="sxs-lookup"><span data-stu-id="7a3e4-134">hello following example creates a resource group named `myResourceGroup` in hello `westus` location:</span></span>

```azurecli
az group create --name myResourceGroup --location westus
```

## <a name="create-hello-virtual-network"></a><span data-ttu-id="7a3e4-135">建立 hello 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="7a3e4-135">Create hello virtual network</span></span>

<span data-ttu-id="7a3e4-136">hello 下一個步驟是的 toobuild 虛擬網路 toolaunch hello 到 Vm。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-136">hello next step is toobuild a virtual network toolaunch hello VMs into.</span></span> <span data-ttu-id="7a3e4-137">hello 虛擬網路包含一個子網路對於此逐步解說。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-137">hello virtual network contains one subnet for this walkthrough.</span></span> <span data-ttu-id="7a3e4-138">如需有關 Azure 虛擬網路的詳細資訊，請參閱[建立虛擬網路使用 Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-138">For more information on Azure virtual networks, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="7a3e4-139">建立 hello 虛擬網路與[az 網路 vnet 建立](/cli/azure/network/vnet#create)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-139">Create hello virtual network with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="7a3e4-140">hello 下列範例會建立虛擬網路，名為`myVnet`和名為的子網路`mySubnet`:</span><span class="sxs-lookup"><span data-stu-id="7a3e4-140">hello following example creates a virtual network named `myVnet` and subnet named `mySubnet`:</span></span>

```azurecli
az network vnet create \
    --resource-group myResourceGroup \
    --name myVnet \
    --address-prefix 192.168.0.0/16 \
    --subnet-name mySubnet \
    --subnet-prefix 192.168.1.0/24
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="7a3e4-141">建立 hello 網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="7a3e4-141">Create hello Network Security Group</span></span>
<span data-ttu-id="7a3e4-142">Azure 網路安全性群組是相等的 tooa hello 網路層級的防火牆。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-142">Azure Network Security Groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="7a3e4-143">如需網路安全性群組的詳細資訊，請參閱[toocreate Nsg 中的如何 hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-143">For more information about Network Security Groups, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> 

<span data-ttu-id="7a3e4-144">建立 hello 與網路安全性群組[az 網路 nsg 建立](/cli/azure/network/nsg#create)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-144">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="7a3e4-145">hello 下列範例會建立名為的網路安全性群組`myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="7a3e4-145">hello following example creates a network security group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --name myNetworkSecurityGroup
```

## <a name="add-an-inbound-rule-tooallow-ssh"></a><span data-ttu-id="7a3e4-146">新增輸入的規則 tooallow SSH</span><span class="sxs-lookup"><span data-stu-id="7a3e4-146">Add an inbound rule tooallow SSH</span></span>
<span data-ttu-id="7a3e4-147">新增輸入的規則 hello 與網路安全性群組[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-147">Add an inbound rule for hello network security group with [az network nsg rule create](/cli/azure/network/nsg/rule#create).</span></span> <span data-ttu-id="7a3e4-148">hello 下列範例會建立名為的規則`myRuleAllowSSH`:</span><span class="sxs-lookup"><span data-stu-id="7a3e4-148">hello following example creates a rule named `myRuleAllowSSH`:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myRuleAllowSSH \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --source-address-prefix '*' \
    --source-port-range '*' \
    --destination-address-prefix '*' \
    --destination-port-range 22 \
    --access allow
```

## <a name="associate-hello-subnet-with-hello-network-security-group"></a><span data-ttu-id="7a3e4-149">Hello 子網路建立關聯以 hello 網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="7a3e4-149">Associate hello subnet with hello Network Security Group</span></span>
<span data-ttu-id="7a3e4-150">以網路安全性群組，hello tooassociate hello 子網路使用[az 網路 vnet 子網路更新](/cli/azure/network/vnet/subnet#update)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-150">tooassociate hello subnet with hello Network Security Group, use [az network vnet subnet update](/cli/azure/network/vnet/subnet#update).</span></span> <span data-ttu-id="7a3e4-151">hello 下列範例將 hello 子網路名稱`mySubnet`hello 名為的網路安全性群組與`myNetworkSecurityGroup`:</span><span class="sxs-lookup"><span data-stu-id="7a3e4-151">hello following example associates hello subnet name `mySubnet` with hello Network Security Group named `myNetworkSecurityGroup`:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```


## <a name="create-hello-virtual-network-interface-card-and-static-dns-names"></a><span data-ttu-id="7a3e4-152">建立 hello 虛擬網路介面卡和靜態 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="7a3e4-152">Create hello virtual network interface card and static DNS names</span></span>
<span data-ttu-id="7a3e4-153">Azure 是非常有彈性，但 toouse VM 名稱解析的 DNS 名稱，您需要 toocreate 虛擬網路介面卡 (vNics)，包括 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-153">Azure is very flexible, but toouse DNS names for VM name resolution, you need toocreate virtual network interface cards (vNics) that include a DNS label.</span></span> <span data-ttu-id="7a3e4-154">vNics 而言很重要，因為您可以重複使用這些連接這些 toodifferent Vm hello 基礎結構的整個週期。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-154">vNics are important as you can reuse them by connecting them toodifferent VMs over hello infrastructure lifecycle.</span></span> <span data-ttu-id="7a3e4-155">這個方法會保持 hello vNic 當做靜態資源時可能是暫時的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-155">This approach keeps hello vNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="7a3e4-156">使用標記 hello vNic 上的 DNS，我們將無法 tooenable hello VNet 中的其他 Vm 所傳來的簡單名稱解析。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-156">By using DNS labeling on hello vNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span> <span data-ttu-id="7a3e4-157">使用可解析名稱可讓其他 Vm tooaccess hello automation 伺服器 hello DNS 名稱`Jenkins`或 hello Git 伺服器`gitrepo`。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-157">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  

<span data-ttu-id="7a3e4-158">建立與 hello vNic [az 網路 nic 建立](/cli/azure/network/nic#create)。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-158">Create hello vNic with [az network nic create](/cli/azure/network/nic#create).</span></span> <span data-ttu-id="7a3e4-159">hello 下列範例會建立名為 vNic `myNic`，將它連接 toohello`myVnet`虛擬網路，名為`myVnet`，並建立呼叫的內部 DNS 名稱記錄`jenkins`:</span><span class="sxs-lookup"><span data-stu-id="7a3e4-159">hello following example creates a vNic named `myNic`, connects it toohello `myVnet` virtual network named `myVnet`, and creates an internal DNS name record called `jenkins`:</span></span>

```azurecli
az network nic create \
    --resource-group myResourceGroup \
    --name myNic \
    --vnet-name myVnet \
    --subnet mySubnet \
    --internal-dns-name jenkins
```

## <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="7a3e4-160">部署 hello VM hello 虛擬網路基礎結構</span><span class="sxs-lookup"><span data-stu-id="7a3e4-160">Deploy hello VM into hello virtual network infrastructure</span></span>
<span data-ttu-id="7a3e4-161">我們現在有了虛擬網路和子網路，網路安全性群組做為防火牆 tooprotect 我們的子網路透過 SSH 和 vNic 封鎖所有傳入的流量，除了連接埠 22。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-161">We now have a virtual network and subnet, a Network Security Group acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH, and a vNic.</span></span> <span data-ttu-id="7a3e4-162">您現在可以在這個現有的網路基礎結構內部署 VM。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-162">You can now deploy a VM inside this existing network infrastructure.</span></span>

<span data-ttu-id="7a3e4-163">使用 [az vm create](/cli/azure/vm#create) 來建立 VM。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-163">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> <span data-ttu-id="7a3e4-164">hello 下列範例會建立名為的 VM`myVM`與 Azure 受管理磁碟和名為附加 hello vNic`myNic`從前面步驟中的 hello:</span><span class="sxs-lookup"><span data-stu-id="7a3e4-164">hello following example creates a VM named `myVM` with Azure Managed Disks and attaches hello vNic named `myNic` from hello preceding step:</span></span>

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --nics myNic \
    --image UbuntuLTS \
    --admin-username azureuser \
    --ssh-key-value ~/.ssh/id_rsa.pub
```

<span data-ttu-id="7a3e4-165">使用 hello CLI 旗標 toocall 出現有的資源，我們指示 Azure toodeploy hello VM hello 現有網路內。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-165">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="7a3e4-166">tooreiterate，一旦部署 VNet 和子網路，他們可以保留為您的 Azure 區域內的靜態或永久資源。</span><span class="sxs-lookup"><span data-stu-id="7a3e4-166">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="7a3e4-167">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a3e4-167">Next steps</span></span>
* [<span data-ttu-id="7a3e4-168">直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境</span><span class="sxs-lookup"><span data-stu-id="7a3e4-168">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="7a3e4-169">使用範本在 Azure 上建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="7a3e4-169">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
