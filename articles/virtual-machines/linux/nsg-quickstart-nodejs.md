---
title: "使用 Azure CLI 1.0 針對 Linux VM 開啟連接埠 | Microsoft Docs"
description: "了解如何使用 Azure Resource Manager 部署模型和 Azure CLI 1.0 對 Linux VM 開啟連接埠 / 建立端點"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 847bc76c37ed929851712ba1c12463a01032e267
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="opening-ports-and-endpoints-to-a-linux-vm-in-azure-using-the-azure-cli-10"></a><span data-ttu-id="69cf2-103">在 Azure 中使用 Azure CLI 1.0 針對 Linux VM 開啟連接埠和端點</span><span class="sxs-lookup"><span data-stu-id="69cf2-103">Opening ports and endpoints to a Linux VM in Azure using the Azure CLI 1.0</span></span>
<span data-ttu-id="69cf2-104">您可以透過在子網路或 VM 網路介面上建立網路篩選，對 Azure 中的虛擬機器 (VM) 開啟連接埠或建立端點。</span><span class="sxs-lookup"><span data-stu-id="69cf2-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="69cf2-105">您可將控制輸入和輸出流量的這些篩選器放在可接收流量的資源所附加的網路安全性群組上。</span><span class="sxs-lookup"><span data-stu-id="69cf2-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="69cf2-106">讓我們使用連接埠 80 上的 Web 流量的常見範例。</span><span class="sxs-lookup"><span data-stu-id="69cf2-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="69cf2-107">這篇文章說明如何使用 Azure CLI 1.0 來開啟連接埠至 VM。</span><span class="sxs-lookup"><span data-stu-id="69cf2-107">This article shows you how to open a port to a VM using the Azure CLI 1.0.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="69cf2-108">用以完成工作的 CLI 版本</span><span class="sxs-lookup"><span data-stu-id="69cf2-108">CLI versions to complete the task</span></span>
<span data-ttu-id="69cf2-109">您可以使用下列其中一個 CLI 版本來完成工作︰</span><span class="sxs-lookup"><span data-stu-id="69cf2-109">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="69cf2-110">[Azure CLI 1.0](#quick-commands) – 適用於傳統和資源管理部署模型的 CLI (本文章)</span><span class="sxs-lookup"><span data-stu-id="69cf2-110">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="69cf2-111">[Azure CLI 2.0](nsg-quickstart.md) - 適用於資源管理部署模型的新一代 CLI</span><span class="sxs-lookup"><span data-stu-id="69cf2-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="69cf2-112">快速命令</span><span class="sxs-lookup"><span data-stu-id="69cf2-112">Quick commands</span></span>
<span data-ttu-id="69cf2-113">若要建立「網路安全性群組」和規則，您需要安裝 [the Azure CLI 1.0](../../cli-install-nodejs.md) 和使用 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="69cf2-113">To create a Network Security Group and rules you need [the Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="69cf2-114">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="69cf2-114">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="69cf2-115">範例參數名稱包括 myResourceGroup、myNetworkSecurityGroup 和 myVnet。</span><span class="sxs-lookup"><span data-stu-id="69cf2-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="69cf2-116">適當地輸入您自己的名稱和位置來建立「網路安全性群組」。</span><span class="sxs-lookup"><span data-stu-id="69cf2-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="69cf2-117">下列範例會在 eastus 位置中建立名為 myNetworkSecurityGroup 的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="69cf2-117">The following example creates a Network Security Group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="69cf2-118">新增規則以允許流向您 Web 伺服器的 HTTP 流量 (或針對自己的案例 (例如 SSH 存取或資料庫連接) 進行調整)。</span><span class="sxs-lookup"><span data-stu-id="69cf2-118">Add a rule to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="69cf2-119">下列範例會建立名為 myNetworkSecurityGroupRule 的規則以允許連接埠 80 上的 TCP 流量︰</span><span class="sxs-lookup"><span data-stu-id="69cf2-119">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="69cf2-120">將「網路安全性群組」與 VM 的網路介面 (NIC) 建立關聯。</span><span class="sxs-lookup"><span data-stu-id="69cf2-120">Associate the Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="69cf2-121">下列範例將名為 myNic 的現有 NIC 與名為 myNetworkSecurityGroup 的網路安全性群組建立關聯：</span><span class="sxs-lookup"><span data-stu-id="69cf2-121">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="69cf2-122">或者，您也可以將「網路安全性群組」與虛擬網路的子網路建立關聯，而不是只與單一 VM 上的網路介面建立關聯。</span><span class="sxs-lookup"><span data-stu-id="69cf2-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="69cf2-123">下列範例將 myVnet 虛擬網路中名為 mySubnet 的現有子網路，與名為 myNetworkSecurityGroup 的網路安全性群組建立關聯：</span><span class="sxs-lookup"><span data-stu-id="69cf2-123">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="69cf2-124">網路安全性群組的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="69cf2-124">More information on Network Security Groups</span></span>
<span data-ttu-id="69cf2-125">這裡的快速命令可讓您使流向您 VM 的流量開始正常運作。</span><span class="sxs-lookup"><span data-stu-id="69cf2-125">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="69cf2-126">「網路安全性群組」提供許多絕佳的功能和細微性來控制對您資源的存取。</span><span class="sxs-lookup"><span data-stu-id="69cf2-126">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="69cf2-127">您可以深入了解 [建立網路安全性群組和 ACL 規則](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="69cf2-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="69cf2-128">您可以在 Azure Resource Manager 範本中定義網路安全性群組和 ACL 規則。</span><span class="sxs-lookup"><span data-stu-id="69cf2-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="69cf2-129">深入了解 [使用範本建立網路安全性群組](../../virtual-network/virtual-networks-create-nsg-arm-template.md)。</span><span class="sxs-lookup"><span data-stu-id="69cf2-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="69cf2-130">如果您需要使用連接埠轉送來將唯一的外部連接埠對應至您 VM 上的內部連接埠，請使用負載平衡器和「網路位址轉譯」(NAT) 規則。</span><span class="sxs-lookup"><span data-stu-id="69cf2-130">If you need to use port-forwarding to map a unique external port to an internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="69cf2-131">例如，您可能會想要對外公開 TCP 連接埠 8080，然後讓流量導向到 VM 上的 TCP 連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="69cf2-131">For example, you may want to expose TCP port 8080 externally and have traffic directed to TCP port 80 on a VM.</span></span> <span data-ttu-id="69cf2-132">您可以深入了解 [建立網際網路面向的負載平衡器](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="69cf2-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="69cf2-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69cf2-133">Next steps</span></span>
<span data-ttu-id="69cf2-134">在此範例中，您建立了簡單的規則來允許 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="69cf2-134">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="69cf2-135">您可以從下列文章中，找到有關建立更詳細環境的資訊︰</span><span class="sxs-lookup"><span data-stu-id="69cf2-135">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="69cf2-136">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="69cf2-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="69cf2-137">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="69cf2-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="69cf2-138">負載平衡器的 Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="69cf2-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

