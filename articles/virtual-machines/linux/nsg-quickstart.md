---
title: "使用 Azure CLI 2.0 針對 Linux VM 開啟連接埠 | Microsoft Docs"
description: "了解如何使用 Azure Resource Manager 部署模型和 Azure CLI 2.0 對 Linux VM 開啟連接埠/建立端點"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: eef9842b-495a-46cf-99a6-74e49807e74e
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 08/21/2017
ms.author: iainfou
ms.openlocfilehash: d176187fe465264b5f433260de5178b48ca9dd4a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="open-ports-and-endpoints-to-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="073a7-103">使用 Azure CLI 針對 Linux VM 開啟連接埠和端點</span><span class="sxs-lookup"><span data-stu-id="073a7-103">Open ports and endpoints to a Linux VM with the Azure CLI</span></span>
<span data-ttu-id="073a7-104">您可以透過在子網路或 VM 網路介面上建立網路篩選，對 Azure 中的虛擬機器 (VM) 開啟連接埠或建立端點。</span><span class="sxs-lookup"><span data-stu-id="073a7-104">You open a port, or create an endpoint, to a virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="073a7-105">您可將控制輸入和輸出流量的這些篩選器放在可接收流量的資源所附加的網路安全性群組上。</span><span class="sxs-lookup"><span data-stu-id="073a7-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached to the resource that receives the traffic.</span></span> <span data-ttu-id="073a7-106">讓我們使用連接埠 80 上的 Web 流量的常見範例。</span><span class="sxs-lookup"><span data-stu-id="073a7-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="073a7-107">這篇文章說明如何使用 Azure CLI 2.0 來開啟連接埠至 VM。</span><span class="sxs-lookup"><span data-stu-id="073a7-107">This article shows you how to open a port to a VM with the Azure CLI 2.0.</span></span> <span data-ttu-id="073a7-108">您也可以使用 [Azure CLI 1.0](nsg-quickstart-nodejs.md) 來執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="073a7-108">You can also perform these steps with the [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="073a7-109">快速命令</span><span class="sxs-lookup"><span data-stu-id="073a7-109">Quick commands</span></span>
<span data-ttu-id="073a7-110">若要建立網路安全性群組和規則，您需要安裝 [Azure CLI 2.0](/cli/azure/install-az-cli2)，並且使用 [az login](/cli/azure/#login) 登入 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="073a7-110">To create a Network Security Group and rules you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="073a7-111">在下列範例中，請以您自己的值取代範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="073a7-111">In the following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="073a7-112">範例參數名稱包括 myResourceGroup、myNetworkSecurityGroup 和 myVnet。</span><span class="sxs-lookup"><span data-stu-id="073a7-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="073a7-113">使用 [az network nsg create](/cli/azure/network/nsg#create) 建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="073a7-113">Create the network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="073a7-114">下列範例會在 eastus 位置中建立名為 myNetworkSecurityGroup 的網路安全性群組：</span><span class="sxs-lookup"><span data-stu-id="073a7-114">The following example creates a network security group named *myNetworkSecurityGroup* in the *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="073a7-115">使用 [az network nsg rule create](/cli/azure/network/nsg/rule#create)新增規則以允許流向您 Web 伺服器的 HTTP 流量 (或針對自己的案例 (例如 SSH 存取或資料庫連接) 進行調整)。</span><span class="sxs-lookup"><span data-stu-id="073a7-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) to allow HTTP traffic to your webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="073a7-116">下列範例會建立名為 myNetworkSecurityGroupRule 的規則以允許連接埠 80 上的 TCP 流量︰</span><span class="sxs-lookup"><span data-stu-id="073a7-116">The following example creates a rule named *myNetworkSecurityGroupRule* to allow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="073a7-117">使用 [az network nic update](/cli/azure/network/nic#update)將「網路安全性群組」與 VM 的網路介面 (NIC) 建立關聯。</span><span class="sxs-lookup"><span data-stu-id="073a7-117">Associate the Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="073a7-118">下列範例將名為 myNic 的現有 NIC 與名為 myNetworkSecurityGroup 的網路安全性群組建立關聯：</span><span class="sxs-lookup"><span data-stu-id="073a7-118">The following example associates an existing NIC named *myNic* with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="073a7-119">或者，您也可以使用 [az network vnet subnet update](/cli/azure/network/vnet/subnet#update)將「網路安全性群組」與虛擬網路的子網路建立關聯，而不是只與單一 VM 上的網路介面建立關聯。</span><span class="sxs-lookup"><span data-stu-id="073a7-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just to the network interface on a single VM.</span></span> <span data-ttu-id="073a7-120">下列範例將 myVnet 虛擬網路中名為 mySubnet 的現有子網路，與名為 myNetworkSecurityGroup 的網路安全性群組建立關聯：</span><span class="sxs-lookup"><span data-stu-id="073a7-120">The following example associates an existing subnet named *mySubnet* in the *myVnet* virtual network with the Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="073a7-121">網路安全性群組的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="073a7-121">More information on Network Security Groups</span></span>
<span data-ttu-id="073a7-122">這裡的快速命令可讓您使流向您 VM 的流量開始正常運作。</span><span class="sxs-lookup"><span data-stu-id="073a7-122">The quick commands here allow you to get up and running with traffic flowing to your VM.</span></span> <span data-ttu-id="073a7-123">「網路安全性群組」提供許多絕佳的功能和細微性來控制對您資源的存取。</span><span class="sxs-lookup"><span data-stu-id="073a7-123">Network Security Groups provide many great features and granularity for controlling access to your resources.</span></span> <span data-ttu-id="073a7-124">您可以深入了解 [建立網路安全性群組和 ACL 規則](tutorial-virtual-network.md#secure-network-traffic)。</span><span class="sxs-lookup"><span data-stu-id="073a7-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="073a7-125">針對高可用性 Web 應用程式，您應該將 VM 放在 Azure Load Balancer 後方。</span><span class="sxs-lookup"><span data-stu-id="073a7-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="073a7-126">此負載平衡器會將流量分散到所有 VM，並具有提供流量篩選的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="073a7-126">The load balancer distributes traffic to VMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="073a7-127">如需詳細資訊，請參閱[如何平衡 Azure 中 Linux 虛擬機器的負載以建立高可用性應用程式](tutorial-load-balancer.md)。</span><span class="sxs-lookup"><span data-stu-id="073a7-127">For more information, see [How to load balance Linux virtual machines in Azure to create a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="073a7-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="073a7-128">Next steps</span></span>
<span data-ttu-id="073a7-129">在此範例中，您建立了簡單的規則來允許 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="073a7-129">In this example, you created a simple rule to allow HTTP traffic.</span></span> <span data-ttu-id="073a7-130">您可以從下列文章中，找到有關建立更詳細環境的資訊︰</span><span class="sxs-lookup"><span data-stu-id="073a7-130">You can find information on creating more detailed environments in the following articles:</span></span>

* [<span data-ttu-id="073a7-131">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="073a7-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="073a7-132">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="073a7-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
