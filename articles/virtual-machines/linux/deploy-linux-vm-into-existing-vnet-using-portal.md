---
title: "aaaDeploy Linux Vm 到現有的網路與 Azure 入口網站 |Microsoft 文件"
description: "將 Linux VM 部署到現有 Azure 虛擬網路使用 hello 入口網站。"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 51272b8cdb1dc7f3fe768d2ebbf4ebe0d754cf19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-portal"></a><span data-ttu-id="a26df-103">如何 toodeploy Linux 虛擬機器在現有的 Azure 虛擬網路以 hello Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="a26df-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure portal</span></span>

<span data-ttu-id="a26df-104">本文章將示範如何 toodeploy 到現有的虛擬網路 (VNet) 的虛擬機器 (VM)。</span><span class="sxs-lookup"><span data-stu-id="a26df-104">This article shows you how toodeploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="a26df-105">像 VNet 和網路安全性群組之類的 Azure 資產應為鮮少部署的靜態且長久資源。</span><span class="sxs-lookup"><span data-stu-id="a26df-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="a26df-106">一旦部署的 VNet，可以重複使用的常數的使用不含任何不良影響 toohello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="a26df-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="a26df-107">考慮為傳統 VNet 硬體網路交換器-不需要的 tooconfigure 全新的硬體交換器每一次部署。</span><span class="sxs-lookup"><span data-stu-id="a26df-107">Thinking about a VNet as being a traditional hardware network switch - you would not need tooconfigure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="a26df-108">具有正確設定 VNet，您可以繼續 toodeploy 新伺服器到該 VNet 反覆數，如果有的話，hello VNet hello 生命週期所需的變更。</span><span class="sxs-lookup"><span data-stu-id="a26df-108">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="a26df-109">建立 hello 資源群組</span><span class="sxs-lookup"><span data-stu-id="a26df-109">Create hello resource group</span></span>

<span data-ttu-id="a26df-110">首先，建立資源群組 tooorganize 您在本逐步解說中建立的所有項目。</span><span class="sxs-lookup"><span data-stu-id="a26df-110">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="a26df-111">如需 Azure 資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="a26df-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-hello-vnet"></a><span data-ttu-id="a26df-113">建立 hello VNet</span><span class="sxs-lookup"><span data-stu-id="a26df-113">Create hello VNet</span></span>

<span data-ttu-id="a26df-114">接下來，建立 VNet toolaunch hello 到 Vm。</span><span class="sxs-lookup"><span data-stu-id="a26df-114">Next, build a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="a26df-115">hello VNet 包含一個子網路，而且是 hello 稍後步驟中此子網路與網路安全性群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="a26df-115">hello VNet contains one subnet and is associated with hello network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="a26df-117">加入 VNic toohello 子網路</span><span class="sxs-lookup"><span data-stu-id="a26df-117">Add a VNic toohello subnet</span></span>

<span data-ttu-id="a26df-118">虛擬網路卡 (VNics) 是重要，因為連接 toodifferent Vm。</span><span class="sxs-lookup"><span data-stu-id="a26df-118">Virtual network cards (VNics) are important as you can connect them toodifferent VMs.</span></span> <span data-ttu-id="a26df-119">這個方法會保持 hello VNic 當做靜態資源時可能是暫時的 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="a26df-119">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="a26df-120">建立 VNic，並將它與 hello hello 先前步驟中建立的子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="a26df-120">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-hello-network-security-group"></a><span data-ttu-id="a26df-122">建立 hello 網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="a26df-122">Create hello network security group</span></span>

<span data-ttu-id="a26df-123">Azure 網路安全性群組是相等的 tooa hello 網路層級的防火牆。</span><span class="sxs-lookup"><span data-stu-id="a26df-123">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="a26df-124">如需有關 Azure 網路安全性群組的詳細資訊，請參閱[什麼是網路安全性群組](../../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="a26df-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="a26df-126">新增輸入 SSH 允許規則</span><span class="sxs-lookup"><span data-stu-id="a26df-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="a26df-127">hello VM 需要從 hello 存取網際網路，因此規則，允許輸入連接埠 22 流量 toobe 通過上建立 VM 的 hello hello 網路 tooport 22。</span><span class="sxs-lookup"><span data-stu-id="a26df-127">hello VM needs access from hello internet, so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-hello-nsg-with-hello-subnet"></a><span data-ttu-id="a26df-129">將 hello NSG 與 hello 子網路產生關聯</span><span class="sxs-lookup"><span data-stu-id="a26df-129">Associate hello NSG with hello subnet</span></span>

<span data-ttu-id="a26df-130">Hello VNet 和建立 hello 子網路，請將 hello 網路安全性群組與 hello 子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="a26df-130">With hello VNet and hello subnet created, associate hello network security group with hello subnet.</span></span> <span data-ttu-id="a26df-131">網路安全性群組可以與整個子網路或個別的 VNic 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="a26df-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="a26df-132">Hello 防火牆篩選 hello 子網路層級的流量時，所有 VNics 和 hello 子網路內的 hello Vm 已都受到 hello 網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="a26df-132">With hello firewall filtering traffic at hello subnet level, all VNics and hello VMs within hello subnet are protected by hello network security group.</span></span> <span data-ttu-id="a26df-133">hello 另一種方法是 hello 網路安全性群組正在只單一 VNic 相關聯，並保護只在一個 VM。</span><span class="sxs-lookup"><span data-stu-id="a26df-133">hello other approach is hello network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="a26df-135">部署至 hello VNet hello VM 和 NSG</span><span class="sxs-lookup"><span data-stu-id="a26df-135">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="a26df-136">使用 hello Azure 入口網站，hello Linux VM 是已部署的 toohello 現有的 Azure 資源群組、 VNet、 子網路和 VNic。</span><span class="sxs-lookup"><span data-stu-id="a26df-136">Using hello Azure portal, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="a26df-138">藉由使用 hello 入口 toochoose 現有資源，您可以指示 Azure toodeploy hello VM hello 現有網路內。</span><span class="sxs-lookup"><span data-stu-id="a26df-138">By using hello portal toochoose existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="a26df-139">VNet 和子網路部署之後，就可以在 Azure 區域內保持為靜態或永久性資源。</span><span class="sxs-lookup"><span data-stu-id="a26df-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="a26df-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a26df-140">Next steps</span></span>

* [<span data-ttu-id="a26df-141">使用 Azure Resource Manager 範本 toocreate 特定部署</span><span class="sxs-lookup"><span data-stu-id="a26df-141">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="a26df-142">直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境</span><span class="sxs-lookup"><span data-stu-id="a26df-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="a26df-143">使用範本在 Azure 上建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="a26df-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
