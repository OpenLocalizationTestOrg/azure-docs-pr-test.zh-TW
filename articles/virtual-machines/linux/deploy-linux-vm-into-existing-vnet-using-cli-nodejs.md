---
title: "aaaDeploy Linux Vm 到現有的網路與 Azure CLI 1.0 |Microsoft 文件"
description: "如何在現有的虛擬網路使用 Linux VM toodeploy hello Azure CLI 1.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a><span data-ttu-id="542c1-103">如何在 Linux 虛擬機器，在現有的 Azure 虛擬網路以 hello Azure CLI 1.0 toodeploy</span><span class="sxs-lookup"><span data-stu-id="542c1-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI 1.0</span></span>

<span data-ttu-id="542c1-104">本文章將示範如何 toouse Azure CLI 1.0 toodeploy 到現有的虛擬網路 (VNet) 的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="542c1-104">This article shows you how toouse Azure CLI 1.0 toodeploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="542c1-105">hello 需求如下：</span><span class="sxs-lookup"><span data-stu-id="542c1-105">hello requirements are:</span></span>

- [<span data-ttu-id="542c1-106">一個 Azure 帳戶</span><span class="sxs-lookup"><span data-stu-id="542c1-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="542c1-107">SSH 公開金鑰和私密金鑰檔案</span><span class="sxs-lookup"><span data-stu-id="542c1-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="542c1-108">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="542c1-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="542c1-109">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="542c1-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="542c1-110">[Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="542c1-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="542c1-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="542c1-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="542c1-112">快速命令</span><span class="sxs-lookup"><span data-stu-id="542c1-112">Quick Commands</span></span>

<span data-ttu-id="542c1-113">如果您需要 tooquickly 完成 hello 工作，下列區段的 hello 詳細資料所需的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="542c1-113">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="542c1-114">詳細資訊和內容的每個步驟可以找到 hello hello 文件的其餘部分[這裡啟動](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough)。</span><span class="sxs-lookup"><span data-stu-id="542c1-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="542c1-115">必要條件︰資源群組、VNet、具有 SSH 輸入的 NSG、子網路。</span><span class="sxs-lookup"><span data-stu-id="542c1-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="542c1-116">將任何範例換成您自己的設定。</span><span class="sxs-lookup"><span data-stu-id="542c1-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="542c1-117">部署 hello VM hello 虛擬網路基礎結構</span><span class="sxs-lookup"><span data-stu-id="542c1-117">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="542c1-118">詳細的逐步解說</span><span class="sxs-lookup"><span data-stu-id="542c1-118">Detailed walkthrough</span></span>

<span data-ttu-id="542c1-119">Azure 資產像是 hello Vnet 和網路安全性群組應為靜態和長時間存在很少部署的資源。</span><span class="sxs-lookup"><span data-stu-id="542c1-119">Azure assets like hello VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="542c1-120">部署的 VNet 之後, 可以重複使用由沒有任何負面影響 toohello 基礎結構的新部署。</span><span class="sxs-lookup"><span data-stu-id="542c1-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="542c1-121">將 VNet 想成是傳統硬體網路交換器。</span><span class="sxs-lookup"><span data-stu-id="542c1-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="542c1-122">您不需要的 tooconfigure 全新的硬體交換器每一次部署。</span><span class="sxs-lookup"><span data-stu-id="542c1-122">You would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="542c1-123">具有正確設定 VNet，您可以繼續 toodeploy 新伺服器到該 VNet 反覆數，如果有的話，hello VNet hello 生命週期所需的變更。</span><span class="sxs-lookup"><span data-stu-id="542c1-123">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="542c1-124">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="542c1-124">Create hello resource group</span></span>

<span data-ttu-id="542c1-125">首先，建立資源群組 tooorganize 您在本逐步解說中建立的所有項目。</span><span class="sxs-lookup"><span data-stu-id="542c1-125">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="542c1-126">如需有關資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="542c1-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="542c1-127">建立 hello VNet</span><span class="sxs-lookup"><span data-stu-id="542c1-127">Create hello VNet</span></span>

<span data-ttu-id="542c1-128">hello 第一個步驟是的 toobuild VNet toolaunch hello 到 Vm。</span><span class="sxs-lookup"><span data-stu-id="542c1-128">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="542c1-129">hello VNet 包含此逐步解說中的一個子網路。</span><span class="sxs-lookup"><span data-stu-id="542c1-129">hello VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="542c1-130">如需有關 Azure Vnet 的詳細資訊，請參閱[建立虛擬網路使用 Azure CLI hello](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="542c1-130">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="542c1-131">建立 hello 網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="542c1-131">Create hello network security group</span></span>

<span data-ttu-id="542c1-132">hello 子網路建立現有的網路安全性群組背後因此建立 hello 之前 hello 子網路的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="542c1-132">hello subnet is built behind an existing network security group so build hello network security group before hello subnet.</span></span> <span data-ttu-id="542c1-133">Azure 網路安全性群組是相等的 tooa hello 網路層級的防火牆。</span><span class="sxs-lookup"><span data-stu-id="542c1-133">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="542c1-134">如需有關 Azure 網路安全性群組的詳細資訊，請參閱[toocreate 網路安全性 hello Azure CLI 中群組的方式](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="542c1-134">For more information on Azure network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="542c1-135">新增輸入 SSH 允許規則</span><span class="sxs-lookup"><span data-stu-id="542c1-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="542c1-136">hello VM 需要的 hello 需要讓規則，允許輸入連接埠 22 流量 toobe 傳遞 hello 網路 tooport 22 hello VM 上的網際網路存取權。</span><span class="sxs-lookup"><span data-stu-id="542c1-136">hello VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="542c1-137">新增子網路 toohello VNet</span><span class="sxs-lookup"><span data-stu-id="542c1-137">Add a subnet toohello VNet</span></span>

<span data-ttu-id="542c1-138">Hello VNet 必須位於子網路內的 Vm。</span><span class="sxs-lookup"><span data-stu-id="542c1-138">VMs within hello VNet must be located in a subnet.</span></span> <span data-ttu-id="542c1-139">每一個 VNet 可以有多個子網路。</span><span class="sxs-lookup"><span data-stu-id="542c1-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="542c1-140">建立 hello 子網路，並與 hello 網路安全性群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="542c1-140">Create hello subnet and associate with hello network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="542c1-141">hello 子網路是現在新增 hello VNet 內，並與網路安全性群組 hello 和規則相關聯。</span><span class="sxs-lookup"><span data-stu-id="542c1-141">hello Subnet is now added inside hello VNet and associated with hello network security group and rule.</span></span>


## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="542c1-142">加入 VNic toohello 子網路</span><span class="sxs-lookup"><span data-stu-id="542c1-142">Add a VNic toohello subnet</span></span>

<span data-ttu-id="542c1-143">虛擬網路卡 (VNics) 是重要，因為您可以重複使用這些連接這些 toodifferent Vm。</span><span class="sxs-lookup"><span data-stu-id="542c1-143">Virtual network cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="542c1-144">這個方法會保持 hello VNic 當做靜態資源時可能是暫時的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="542c1-144">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="542c1-145">建立 VNic，並將它與 hello hello 先前步驟中建立的子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="542c1-145">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="542c1-146">部署至 hello VNet hello VM 和 NSG</span><span class="sxs-lookup"><span data-stu-id="542c1-146">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="542c1-147">您現在有 VNet 的 VNet 及藉由封鎖所有傳入的流量，除了連接埠 22 ssh 的 tooprotect hello 子網路的網路安全性群組內的子網路。</span><span class="sxs-lookup"><span data-stu-id="542c1-147">You now have a VNet and subnet inside that VNet, and a network security group acting tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="542c1-148">hello VM 現在可以部署在現有的網路基礎結構內。</span><span class="sxs-lookup"><span data-stu-id="542c1-148">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="542c1-149">使用 hello Azure CLI 和 hello`azure vm create`命令 hello Linux VM 是已部署的 toohello 現有的 Azure 資源群組、 VNet、 子網路和 VNic。</span><span class="sxs-lookup"><span data-stu-id="542c1-149">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="542c1-150">如需有關使用 hello CLI toodeploy 完成 VM 的詳細資訊，請參閱[使用 hello Azure CLI 建立完整的 Linux 環境](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="542c1-150">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="542c1-151">使用 hello CLI 旗標 toocall 出現有的資源，指示 Azure toodeploy hello VM hello 現有網路內。</span><span class="sxs-lookup"><span data-stu-id="542c1-151">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="542c1-152">VNet 和子網路部署之後，就可以在 Azure 區域內保持為靜態或永久性資源。</span><span class="sxs-lookup"><span data-stu-id="542c1-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="542c1-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="542c1-153">Next steps</span></span>

* [<span data-ttu-id="542c1-154">使用 Azure Resource Manager 範本 toocreate 特定部署</span><span class="sxs-lookup"><span data-stu-id="542c1-154">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="542c1-155">直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境</span><span class="sxs-lookup"><span data-stu-id="542c1-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="542c1-156">使用範本在 Azure 上建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="542c1-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
