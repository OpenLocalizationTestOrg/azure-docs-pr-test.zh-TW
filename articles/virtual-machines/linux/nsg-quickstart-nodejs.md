---
title: "aaaOpen 連接埠 tooa Linux VM 與 Azure CLI 1.0 |Microsoft 文件"
description: "深入了解如何 tooopen 連接埠建立端點 tooyour Linux VM / 使用 hello Azure 資源管理員部署模型和 hello Azure CLI 1.0"
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
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="7c80b-103">開啟連接埠和端點 tooa Linux VM 在 Azure 中使用 hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="7c80b-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="7c80b-104">您開啟通訊埠，或建立端點，tooa Azure 虛擬機器 (VM) 中藉由建立子網路或 VM 網路介面上的網路篩選條件。</span><span class="sxs-lookup"><span data-stu-id="7c80b-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="7c80b-105">您收到 hello 流量的網路安全性群組附加 toohello 資源上放置控制輸入與輸出流量，這些篩選器。</span><span class="sxs-lookup"><span data-stu-id="7c80b-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="7c80b-106">讓我們使用連接埠 80 上的 Web 流量的常見範例。</span><span class="sxs-lookup"><span data-stu-id="7c80b-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="7c80b-107">本文章將示範如何連接埠 tooa VM 使用 tooopen hello Azure CLI 1.0。</span><span class="sxs-lookup"><span data-stu-id="7c80b-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="7c80b-108">CLI 版本 toocomplete hello 工作</span><span class="sxs-lookup"><span data-stu-id="7c80b-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="7c80b-109">您可以完成 hello 工作使用其中一種 hello 遵循 CLI 版本：</span><span class="sxs-lookup"><span data-stu-id="7c80b-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="7c80b-110">[Azure CLI 1.0](#quick-commands) – 我們 CLI hello 傳統和資源管理部署模型 （此文件）</span><span class="sxs-lookup"><span data-stu-id="7c80b-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="7c80b-111">[Azure CLI 2.0](nsg-quickstart.md) -hello 資源管理部署模型我們下一個層代 CLI</span><span class="sxs-lookup"><span data-stu-id="7c80b-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="7c80b-112">快速命令</span><span class="sxs-lookup"><span data-stu-id="7c80b-112">Quick commands</span></span>
<span data-ttu-id="7c80b-113">toocreate 網路安全性群組規則您需要和[hello Azure CLI 1.0](../../cli-install-nodejs.md)已安裝且正在使用的 Resource Manager 模式：</span><span class="sxs-lookup"><span data-stu-id="7c80b-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="7c80b-114">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="7c80b-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="7c80b-115">範例參數名稱包括 myResourceGroup、myNetworkSecurityGroup 和 myVnet。</span><span class="sxs-lookup"><span data-stu-id="7c80b-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="7c80b-116">適當地輸入您自己的名稱和位置來建立「網路安全性群組」。</span><span class="sxs-lookup"><span data-stu-id="7c80b-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="7c80b-117">hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="7c80b-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="7c80b-118">新增規則 tooallow HTTP 流量 tooyour 網頁伺服器 （或 調整成您自己的案例，例如 SSH 存取或資料庫連線）。</span><span class="sxs-lookup"><span data-stu-id="7c80b-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="7c80b-119">hello 下列範例會建立名為的規則*myNetworkSecurityGroupRule* tooallow TCP 連接埠 80 上的流量：</span><span class="sxs-lookup"><span data-stu-id="7c80b-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

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

<span data-ttu-id="7c80b-120">將 hello 網路安全性群組與您的 VM 網路介面 (NIC) 產生關聯。</span><span class="sxs-lookup"><span data-stu-id="7c80b-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="7c80b-121">hello 下列範例將名為現有 NIC *myNic* hello 名為的網路安全性群組與*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="7c80b-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="7c80b-122">或者，您可以將您的網路安全性群組與虛擬網路子網路，而不是只 toohello 網路介面上之單一 VM。</span><span class="sxs-lookup"><span data-stu-id="7c80b-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="7c80b-123">hello 下列範例將現有的子網路，名為*mySubnet*在 hello *myVnet* hello 名為的網路安全性群組與虛擬網路*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="7c80b-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="7c80b-124">網路安全性群組的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="7c80b-124">More information on Network Security Groups</span></span>
<span data-ttu-id="7c80b-125">這裡 hello 快速命令可讓您設定 tooget 和流量流動 tooyour VM 執行。</span><span class="sxs-lookup"><span data-stu-id="7c80b-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="7c80b-126">網路安全性群組可提供許多很棒的功能和控制存取 tooyour 資源的資料粒度。</span><span class="sxs-lookup"><span data-stu-id="7c80b-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="7c80b-127">您可以深入了解 [建立網路安全性群組和 ACL 規則](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="7c80b-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="7c80b-128">您可以在 Azure Resource Manager 範本中定義網路安全性群組和 ACL 規則。</span><span class="sxs-lookup"><span data-stu-id="7c80b-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="7c80b-129">深入了解 [使用範本建立網路安全性群組](../../virtual-network/virtual-networks-create-nsg-arm-template.md)。</span><span class="sxs-lookup"><span data-stu-id="7c80b-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="7c80b-130">如果您需要 toouse 唯一外部連接埠 tooan 內部連接埠的連接埠轉送 toomap VM 上，使用 負載平衡器和網路位址轉譯 (NAT) 規則。</span><span class="sxs-lookup"><span data-stu-id="7c80b-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="7c80b-131">例如，您可能想 tooexpose TCP 連接埠 8080 外部並且流量導向 tooTCP 連接埠 80 上的 VM。</span><span class="sxs-lookup"><span data-stu-id="7c80b-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="7c80b-132">您可以深入了解 [建立網際網路面向的負載平衡器](../../load-balancer/load-balancer-get-started-internet-arm-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="7c80b-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c80b-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7c80b-133">Next steps</span></span>
<span data-ttu-id="7c80b-134">在此範例中，您可以建立簡單的規則 tooallow HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="7c80b-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="7c80b-135">您可以找到有關 hello 下列文件中建立更詳細的環境：</span><span class="sxs-lookup"><span data-stu-id="7c80b-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="7c80b-136">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="7c80b-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="7c80b-137">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="7c80b-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="7c80b-138">負載平衡器的 Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="7c80b-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

