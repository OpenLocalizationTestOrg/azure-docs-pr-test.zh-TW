---
title: "使用 Azure 入口網站將 Linux VM 部署至現有網路 | Microsoft Docs"
description: "使用入口網站將 Linux VM 部署至現有 Azure 虛擬網路。"
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
ms.openlocfilehash: 964c0fc41773b50a9fbe476df47460484c2ada66
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-deploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-the-azure-portal"></a><span data-ttu-id="2122e-103">如何使用 Azure 入口網站將 Linux 虛擬機器部署至現有的 Azure 虛擬網路</span><span class="sxs-lookup"><span data-stu-id="2122e-103">How to deploy a Linux virtual machine into an existing Azure Virtual Network with the Azure portal</span></span>

<span data-ttu-id="2122e-104">此文章說明如何將虛擬機器 (VM) 部署至現有虛擬網路 (VNet)。</span><span class="sxs-lookup"><span data-stu-id="2122e-104">This article shows you how to deploy a virtual machine (VM) into an existing virtual network (VNet).</span></span> <span data-ttu-id="2122e-105">像 VNet 和網路安全性群組之類的 Azure 資產應為鮮少部署的靜態且長久資源。</span><span class="sxs-lookup"><span data-stu-id="2122e-105">Azure assets like VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="2122e-106">VNet 部署之後，即可在不斷重新部署時重複使用，完全不會對基礎結構造成負面影響。</span><span class="sxs-lookup"><span data-stu-id="2122e-106">Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects to the infrastructure.</span></span> <span data-ttu-id="2122e-107">將 VNet 想像成傳統的硬體網路交換器，您就不需要在每次部署時設定全新的硬體交換器。</span><span class="sxs-lookup"><span data-stu-id="2122e-107">Thinking about a VNet as being a traditional hardware network switch - you would not need to configure a brand new hardware switch with each deployment.</span></span>  

<span data-ttu-id="2122e-108">有了正確設定的 VNet，您就可以一次又一次地將新的伺服器部署至該 VNet，整個 VNet 生命週期內所需的變動極少 (如果有的話)。</span><span class="sxs-lookup"><span data-stu-id="2122e-108">With a correctly configured VNet, you can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.</span></span>

## <a name="create-the-resource-group"></a><span data-ttu-id="2122e-109">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="2122e-109">Create the resource group</span></span>

<span data-ttu-id="2122e-110">首先，建立資源群組來組織我們在本逐步解說中建立的所有項目。</span><span class="sxs-lookup"><span data-stu-id="2122e-110">First, create a resource group to organize everything you create in this walkthrough.</span></span> <span data-ttu-id="2122e-111">如需 Azure 資源群組的詳細資訊，請參閱 [Azure Resource Manager 概觀](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="2122e-111">For more information about Azure resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

![createResourceGroup](./media/deploy-linux-vm-into-existing-vnet-using-portal/createResourceGroup.png)


## <a name="create-the-vnet"></a><span data-ttu-id="2122e-113">建立 VNet</span><span class="sxs-lookup"><span data-stu-id="2122e-113">Create the VNet</span></span>

<span data-ttu-id="2122e-114">接下來，建置要將 VM 送入的 VNet。</span><span class="sxs-lookup"><span data-stu-id="2122e-114">Next, build a VNet to launch the VMs into.</span></span> <span data-ttu-id="2122e-115">VNet 包含一個子網路，且會在稍後步驟中與含此子網路的網路安全性群組相關聯。</span><span class="sxs-lookup"><span data-stu-id="2122e-115">The VNet contains one subnet and is associated with the network security group with this subnet in a later step.</span></span>

![createVNet](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNet.png)

## <a name="add-a-vnic-to-the-subnet"></a><span data-ttu-id="2122e-117">將 VNic 新增至子網路</span><span class="sxs-lookup"><span data-stu-id="2122e-117">Add a VNic to the subnet</span></span>

<span data-ttu-id="2122e-118">虛擬網路卡 (VNic) 很重要，因為您可以將它們連接至不同的 VM。</span><span class="sxs-lookup"><span data-stu-id="2122e-118">Virtual network cards (VNics) are important as you can connect them to different VMs.</span></span> <span data-ttu-id="2122e-119">此方法既可讓 VM 為暫時性，又可將 VNic 保持為靜態資源。</span><span class="sxs-lookup"><span data-stu-id="2122e-119">This approach keeps the VNic as a static resource while the VMs can be temporary.</span></span> <span data-ttu-id="2122e-120">建立 VNic，並將它與先前步驟中建立的子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="2122e-120">Create a VNic and associate it with the subnet created in the previous step.</span></span>

![createVNic](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVNic.png)

## <a name="create-the-network-security-group"></a><span data-ttu-id="2122e-122">建立網路安全性群組</span><span class="sxs-lookup"><span data-stu-id="2122e-122">Create the network security group</span></span>

<span data-ttu-id="2122e-123">Azure 網路安全性群組相當於網路層的防火牆。</span><span class="sxs-lookup"><span data-stu-id="2122e-123">Azure network security groups are equivalent to a firewall at the network layer.</span></span> <span data-ttu-id="2122e-124">如需有關 Azure 網路安全性群組的詳細資訊，請參閱[什麼是網路安全性群組](../../virtual-network/virtual-networks-nsg.md)。</span><span class="sxs-lookup"><span data-stu-id="2122e-124">For more information on Azure network security groups, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md).</span></span>

![createNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/createNSG.png)

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="2122e-126">新增輸入 SSH 允許規則</span><span class="sxs-lookup"><span data-stu-id="2122e-126">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="2122e-127">由於需要從網際網路存取 VM，因此會建立一個規則來允許輸入連接埠 22 流量通過網路流向 VM 的連接埠 22。</span><span class="sxs-lookup"><span data-stu-id="2122e-127">The VM needs access from the internet, so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the VM is created.</span></span>

![createInboundSSH](./media/deploy-linux-vm-into-existing-vnet-using-portal/createInboundSSH.png)

## <a name="associate-the-nsg-with-the-subnet"></a><span data-ttu-id="2122e-129">將 NSG 與子網路產生關聯</span><span class="sxs-lookup"><span data-stu-id="2122e-129">Associate the NSG with the subnet</span></span>

<span data-ttu-id="2122e-130">建立 VNet 和子網路後，請將網路安全性群組與子網路產生關聯。</span><span class="sxs-lookup"><span data-stu-id="2122e-130">With the VNet and the subnet created, associate the network security group with the subnet.</span></span> <span data-ttu-id="2122e-131">網路安全性群組可以與整個子網路或個別的 VNic 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="2122e-131">Network security groups can be associated with either an entire subnet or an individual VNic.</span></span> <span data-ttu-id="2122e-132">有了篩選子網路層級流量的防火牆，子網路內所有的 VNic 與 VM 會受到網路安全性群組的保護。</span><span class="sxs-lookup"><span data-stu-id="2122e-132">With the firewall filtering traffic at the subnet level, all VNics and the VMs within the subnet are protected by the network security group.</span></span> <span data-ttu-id="2122e-133">另一個方法是讓網路安全性群組只與單一 VNic 相關聯，並僅保護一個 VM。</span><span class="sxs-lookup"><span data-stu-id="2122e-133">The other approach is the network security group being associated with just a single VNic and protecting just one VM.</span></span>

![associateNSG](./media/deploy-linux-vm-into-existing-vnet-using-portal/associateNSG.png)


## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a><span data-ttu-id="2122e-135">將 VM 部署至 VNet 和 NSG</span><span class="sxs-lookup"><span data-stu-id="2122e-135">Deploy the VM into the VNet and NSG</span></span>

<span data-ttu-id="2122e-136">您可以使用 Azure 入口網站，將 Linux VM 部署至現有的 Azure 資源群組、VNet、子網路和 VNic。</span><span class="sxs-lookup"><span data-stu-id="2122e-136">Using the Azure portal, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.</span></span>

![createVM](./media/deploy-linux-vm-into-existing-vnet-using-portal/createVM.png)

<span data-ttu-id="2122e-138">您可以使用入口網站來選擇現有的資源，來指示 Azure 將 VM 部署在現有的網路內。</span><span class="sxs-lookup"><span data-stu-id="2122e-138">By using the portal to choose existing resources, you instruct Azure to deploy the VM inside the existing network.</span></span> <span data-ttu-id="2122e-139">VNet 和子網路部署之後，就可以在 Azure 區域內保持為靜態或永久性資源。</span><span class="sxs-lookup"><span data-stu-id="2122e-139">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="2122e-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2122e-140">Next steps</span></span>

* [<span data-ttu-id="2122e-141">使用 Azure Resource Manager 範本和 Azure CLI 部署和管理虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2122e-141">Use an Azure Resource Manager template to create a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="2122e-142">直接使用 Azure CLI 命令，建立自訂的 Linux VM 環境</span><span class="sxs-lookup"><span data-stu-id="2122e-142">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="2122e-143">使用範本在 Azure 上建立 Linux VM</span><span class="sxs-lookup"><span data-stu-id="2122e-143">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
