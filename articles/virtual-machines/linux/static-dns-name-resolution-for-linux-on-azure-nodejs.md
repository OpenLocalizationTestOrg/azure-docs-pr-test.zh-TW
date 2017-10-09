---
title: "aaaUsing vm 的內部 DNS 名稱在 Azure 上的解析 |Microsoft 文件"
description: "在 Azure 上針對 VM 名稱解析使用內部 DNS。"
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
ms.devlang: na
ms.topic: article
ms.date: 12/05/2016
ms.author: v-livech
ms.openlocfilehash: 94fd6577aa51ce5db4dc26649b415ddeeb410eb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-internal-dns-for-vm-name-resolution-on-azure"></a><span data-ttu-id="e9093-103">在 Azure 上針對 VM 名稱解析使用內部 DNS</span><span class="sxs-lookup"><span data-stu-id="e9093-103">Using internal DNS for VM name resolution on Azure</span></span>

<span data-ttu-id="e9093-104">本文將說明如何 tooset 靜態內部 DNS 命名適用於 Linux Vm 使用虛擬 NIC 卡 (VNic) 和標籤的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="e9093-104">This article shows how tooset static internal DNS names for Linux VMs using Virtual NIC cards (VNic) and DNS label names.</span></span> <span data-ttu-id="e9093-105">靜態 DNS 名稱是用於永久基礎結構服務，例如 Jenkins 組建伺服器，它用於這份文件或 Git 伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9093-105">Static DNS names are used for permanent infrastructure services like a Jenkins build server, which is used for this document, or a Git server.</span></span>

<span data-ttu-id="e9093-106">hello 需求如下：</span><span class="sxs-lookup"><span data-stu-id="e9093-106">hello requirements are:</span></span>

* [<span data-ttu-id="e9093-107">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="e9093-107">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
* [<span data-ttu-id="e9093-108">SSH 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="e9093-108">SSH public and private key files</span></span>](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="e9093-109">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="e9093-109">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="e9093-110">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="e9093-110">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="e9093-111">[Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="e9093-111">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="e9093-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="e9093-112">[Azure CLI 2.0](static-dns-name-resolution-for-linux-on-azure.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="e9093-113">快速命令</span><span class="sxs-lookup"><span data-stu-id="e9093-113">Quick commands</span></span>

<span data-ttu-id="e9093-114">如果您需要 tooquickly 完成 hello 工作，下列區段的 hello 詳細資料所需的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="e9093-114">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="e9093-115">詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](#detailed-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="e9093-115">More detailed information and context for each step can be found hello rest of hello document, [starting here](#detailed-walkthrough).</span></span>  

<span data-ttu-id="e9093-116">必要條件︰資源群組、VNet、具有 SSH 輸入的 NSG、子網路。</span><span class="sxs-lookup"><span data-stu-id="e9093-116">Pre-Requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span>

### <a name="create-a-vnic-with-a-static-internal-dns-name"></a><span data-ttu-id="e9093-117">使用靜態內部 DNS 名稱建立 VNic</span><span class="sxs-lookup"><span data-stu-id="e9093-117">Create a VNic with a static internal DNS name</span></span>

<span data-ttu-id="e9093-118">hello `-r` cli 旗標適用於設定 hello DNS 標籤，可提供 hello VNic hello 靜態 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="e9093-118">hello `-r` cli flag is for setting hello DNS label, which provides hello static DNS name for hello VNic.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

### <a name="deploy-hello-vm-into-hello-vnet-nsg-and-connect-hello-vnic"></a><span data-ttu-id="e9093-119">部署到 hello VNet，NSG hello VM，以及連線 hello VNic</span><span class="sxs-lookup"><span data-stu-id="e9093-119">Deploy hello VM into hello VNet, NSG and, connect hello VNic</span></span>

<span data-ttu-id="e9093-120">hello`-N`連接 hello VNic toohello hello 部署 tooAzure 期間的新 VM。</span><span class="sxs-lookup"><span data-stu-id="e9093-120">hello `-N` connects hello VNic toohello new VM during hello deployment tooAzure.</span></span>

```azurecli
azure vm create jenkins \
-g myResourceGroup \
-l westus \
-y linux \
-Q Debian \
-o myStorageAcct \
-u myAdminUser \
-M ~/.ssh/id_rsa.pub \
-F myVNet \
-j mySubnet \
-N jenkinsVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="e9093-121">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="e9093-121">Detailed walkthrough</span></span>

<span data-ttu-id="e9093-122">完整的持續整合與連續部署 (CiCd) 在 Azure 上的基礎結構需要特定伺服器 toobe 靜態或長時間執行的伺服器。</span><span class="sxs-lookup"><span data-stu-id="e9093-122">A full continuous integration and continuous deployment (CiCd) infrastructure on Azure requires certain servers toobe static or long-lived servers.</span></span>  <span data-ttu-id="e9093-123">建議您使用 Azure 資產，例如 hello 虛擬網路 (Vnet) 和網路安全性群組 (Nsg)，應為靜態和長時間存在很少部署的資源。</span><span class="sxs-lookup"><span data-stu-id="e9093-123">It is recommended that Azure assets like hello Virtual Networks (VNets) and Network Security Groups (NSGs), should be static and long lived resources that are rarely deployed.</span></span>  <span data-ttu-id="e9093-124">部署的 VNet 之後, 可以重複使用由沒有任何負面影響 toohello 基礎結構的新部署。</span><span class="sxs-lookup"><span data-stu-id="e9093-124">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span>  <span data-ttu-id="e9093-125">加入 toothis 靜態網路 Git 儲存機制中伺服器與 Jenkins 自動化傳遞 CiCd tooyour 開發或測試環境。</span><span class="sxs-lookup"><span data-stu-id="e9093-125">Adding toothis static network a Git repository server and a Jenkins automation server delivers CiCd tooyour development or test environments.</span></span>  

<span data-ttu-id="e9093-126">僅可在 Azure 虛擬網路內解析內部 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="e9093-126">Internal DNS names are only resolvable inside an Azure virtual network.</span></span>  <span data-ttu-id="e9093-127">Hello DNS 名稱是內部的因為它們不是解析 toohello 外部網際網路上，提供額外的安全性 toohello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="e9093-127">Because hello DNS names are internal, they are not resolvable toohello outside internet, providing additional security toohello infrastructure.</span></span>

<span data-ttu-id="e9093-128">_將任何範例換成您自己的名稱。_</span><span class="sxs-lookup"><span data-stu-id="e9093-128">_Replace any examples with your own naming._</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="e9093-129">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="e9093-129">Create hello Resource group</span></span>

<span data-ttu-id="e9093-130">資源群組是需要的 tooorganize 我們在本逐步解說中建立的所有項目。</span><span class="sxs-lookup"><span data-stu-id="e9093-130">A Resource Group is needed tooorganize everything we create in this walkthrough.</span></span>  <span data-ttu-id="e9093-131">如需 Azure 資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e9093-131">For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure group create myResourceGroup \
--location westus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="e9093-132">建立 hello VNet</span><span class="sxs-lookup"><span data-stu-id="e9093-132">Create hello VNet</span></span>

<span data-ttu-id="e9093-133">hello 第一個步驟是的 toobuild VNet toolaunch hello 到 Vm。</span><span class="sxs-lookup"><span data-stu-id="e9093-133">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span>  <span data-ttu-id="e9093-134">hello VNet 包含此逐步解說中的一個子網路。</span><span class="sxs-lookup"><span data-stu-id="e9093-134">hello VNet contains one subnet for this walkthrough.</span></span>  <span data-ttu-id="e9093-135">如需有關 Azure Vnet 的詳細資訊，請參閱[建立虛擬網路使用 Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e9093-135">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network vnet create myVNet \
--resource-group myResourceGroup \
--address-prefixes 10.10.0.0/24 \
--location westus
```

## <a name="create-hello-nsg"></a><span data-ttu-id="e9093-136">建立 hello NSG</span><span class="sxs-lookup"><span data-stu-id="e9093-136">Create hello NSG</span></span>

<span data-ttu-id="e9093-137">hello 子網路是內建背後現有的網路安全性群組，所以我們建置 hello NSG 之前 hello 子網路。</span><span class="sxs-lookup"><span data-stu-id="e9093-137">hello Subnet is built behind an existing Network Security Group so we build hello NSG before hello Subnet.</span></span>  <span data-ttu-id="e9093-138">Azure 的 Nsg 是相等的 tooa hello 網路層級的防火牆。</span><span class="sxs-lookup"><span data-stu-id="e9093-138">Azure NSGs are equivalent tooa firewall at hello network layer.</span></span>  <span data-ttu-id="e9093-139">如需有關 Azure Nsg 的詳細資訊，請參閱[toocreate Nsg 中的如何 hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e9093-139">For more information on Azure NSGs, see [How toocreate NSGs in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure network nsg create myNSG \
--resource-group myResourceGroup \
--location westus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="e9093-140">新增輸入 SSH 允許規則</span><span class="sxs-lookup"><span data-stu-id="e9093-140">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="e9093-141">hello Linux VM 需要的 hello 需要讓規則，允許輸入連接埠 22 流量 toobe 傳遞 hello 網路 tooport 22 hello Linux VM 上的網際網路存取權。</span><span class="sxs-lookup"><span data-stu-id="e9093-141">hello Linux VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello Linux VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
--resource-group myResourceGroup \
--nsg-name myNSG \
--access Allow \
--protocol Tcp \
--direction Inbound \
--priority 100 \
--source-address-prefix * \
--source-port-range * \
--destination-address-prefix 10.10.0.0/24 \
--destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="e9093-142">新增子網路 toohello VNet</span><span class="sxs-lookup"><span data-stu-id="e9093-142">Add a subnet toohello VNet</span></span>

<span data-ttu-id="e9093-143">Hello VNet 必須位於子網路內的 Vm。</span><span class="sxs-lookup"><span data-stu-id="e9093-143">VMs within hello VNet must be located in a subnet.</span></span>  <span data-ttu-id="e9093-144">每一個 VNet 可以有多個子網路。</span><span class="sxs-lookup"><span data-stu-id="e9093-144">Each VNet can have multiple subnets.</span></span>  <span data-ttu-id="e9093-145">建立 hello 子網路，並將 hello 子網路與 hello NSG tooadd 防火牆 toohello 子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="e9093-145">Create hello subnet and associate hello subnet with hello NSG tooadd a firewall toohello subnet.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
--resource-group myResourceGroup \
--vnet-name myVNet \
--address-prefix 10.10.0.0/26 \
--network-security-group-name myNSG
```

<span data-ttu-id="e9093-146">現在 hello 子網路是新增 hello VNet 內，並與 hello NSG 與 hello NSG 規則相關聯。</span><span class="sxs-lookup"><span data-stu-id="e9093-146">hello Subnet is now added inside hello VNet and associated with hello NSG and hello NSG rule.</span></span>

## <a name="creating-static-dns-names"></a><span data-ttu-id="e9093-147">建立靜態 DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="e9093-147">Creating static DNS names</span></span>

<span data-ttu-id="e9093-148">Azure 是非常有彈性，但 toouse Vm 名稱解析的 DNS 名稱，您需要的 toocreate 它們當做虛擬網路卡 (VNics) 使用 DNS 標籤。</span><span class="sxs-lookup"><span data-stu-id="e9093-148">Azure is very flexible, but toouse DNS names for VMs name resolution, you need toocreate them as Virtual network cards (VNics) using DNS labeling.</span></span>  <span data-ttu-id="e9093-149">VNics 而言很重要，因為您可以重複使用這些連接這些 toodifferent Vm 期間 hello Vm 可能是暫時性，維持 hello VNic 為靜態的資源。</span><span class="sxs-lookup"><span data-stu-id="e9093-149">VNics are important as you can reuse them by connecting them toodifferent VMs, which keeps hello VNic as a static resource while hello VMs can be temporary.</span></span>  <span data-ttu-id="e9093-150">使用標記 hello VNic 上的 DNS，我們將無法 tooenable hello VNet 中的其他 Vm 所傳來的簡單名稱解析。</span><span class="sxs-lookup"><span data-stu-id="e9093-150">By using DNS labeling on hello VNic, we are able tooenable simple name resolution from other VMs in hello VNet.</span></span>  <span data-ttu-id="e9093-151">使用可解析名稱可讓其他 Vm tooaccess hello automation 伺服器 hello DNS 名稱`Jenkins`或 hello Git 伺服器`gitrepo`。</span><span class="sxs-lookup"><span data-stu-id="e9093-151">Using resolvable names enables other VMs tooaccess hello automation server by hello DNS name `Jenkins` or hello Git server as `gitrepo`.</span></span>  <span data-ttu-id="e9093-152">建立 VNic，並將它與 hello hello 上一個步驟中建立子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="e9093-152">Create a VNic and associate it with hello Subnet created in hello previous step.</span></span>

```azurecli
azure network nic create jenkinsVNic \
-g myResourceGroup \
-l westus \
-m myVNet \
-k mySubNet \
-r jenkins
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="e9093-153">部署至 hello VNet hello VM 和 NSG</span><span class="sxs-lookup"><span data-stu-id="e9093-153">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="e9093-154">我們現在有 VNet，而該 VNet 和我們的子網路防火牆 tooprotect 作為透過 ssh 封鎖所有傳入的流量，除了連接埠 22 NSG 內部的子網路。</span><span class="sxs-lookup"><span data-stu-id="e9093-154">We now have a VNet, a subnet inside that VNet, and an NSG acting as a firewall tooprotect our subnet by blocking all inbound traffic except port 22 for SSH.</span></span>  <span data-ttu-id="e9093-155">hello VM 現在可以部署在現有的網路基礎結構內。</span><span class="sxs-lookup"><span data-stu-id="e9093-155">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="e9093-156">使用 hello Azure CLI 和 hello`azure vm create`命令 hello Linux VM 是已部署的 toohello 現有的 Azure 資源群組、 VNet、 子網路和 VNic。</span><span class="sxs-lookup"><span data-stu-id="e9093-156">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>  <span data-ttu-id="e9093-157">如需有關使用 hello CLI toodeploy 完成 VM 的詳細資訊，請參閱[使用 hello Azure CLI 建立完整的 Linux 環境](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e9093-157">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>

```azurecli
azure vm create jenkins \
--resource-group myResourceGroup myVM \
--location westus \
--os-type linux \
--image-urn Debian \
--storage-account-name mystorageaccount \
--admin-username myAdminUser \
--ssh-publickey-file ~/.ssh/id_rsa.pub \
--vnet-name myVNet \
--vnet-subnet-name mySubnet \
--nic-name jenkinsVNic
```

<span data-ttu-id="e9093-158">使用 hello CLI 旗標 toocall 出現有的資源，我們指示 Azure toodeploy hello VM hello 現有網路內。</span><span class="sxs-lookup"><span data-stu-id="e9093-158">By using hello CLI flags toocall out existing resources, we instruct Azure toodeploy hello VM inside hello existing network.</span></span>  <span data-ttu-id="e9093-159">tooreiterate，一旦部署 VNet 和子網路，他們可以保留為您的 Azure 區域內的靜態或永久資源。</span><span class="sxs-lookup"><span data-stu-id="e9093-159">tooreiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="e9093-160">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9093-160">Next steps</span></span>
* [<span data-ttu-id="e9093-161">直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境</span><span class="sxs-lookup"><span data-stu-id="e9093-161">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [<span data-ttu-id="e9093-162">使用範本在 Azure 上建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="e9093-162">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
