---
title: "aaaOpen 連接埠 tooa Linux VM，使用 Azure CLI 2.0 |Microsoft 文件"
description: "深入了解如何 tooopen 連接埠建立端點 tooyour Linux VM / 使用 hello Azure 資源管理員部署模型和 hello Azure CLI 2.0"
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
ms.openlocfilehash: c79b31206e97558171609cf033bb3cb3370777c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-and-endpoints-tooa-linux-vm-with-hello-azure-cli"></a><span data-ttu-id="ab8a4-103">使用 Azure CLI hello 開啟連接埠和端點 tooa Linux VM</span><span class="sxs-lookup"><span data-stu-id="ab8a4-103">Open ports and endpoints tooa Linux VM with hello Azure CLI</span></span>
<span data-ttu-id="ab8a4-104">您開啟通訊埠，或建立端點，tooa Azure 虛擬機器 (VM) 中藉由建立子網路或 VM 網路介面上的網路篩選條件。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="ab8a4-105">您收到 hello 流量的網路安全性群組附加 toohello 資源上放置控制輸入與輸出流量，這些篩選器。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="ab8a4-106">讓我們使用連接埠 80 上的 Web 流量的常見範例。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="ab8a4-107">本文章將示範如何 tooopen 以 hello Azure CLI 2.0 連接埠 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-107">This article shows you how tooopen a port tooa VM with hello Azure CLI 2.0.</span></span> <span data-ttu-id="ab8a4-108">您也可以執行下列步驟以 hello [Azure CLI 1.0](nsg-quickstart-nodejs.md)。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-108">You can also perform these steps with hello [Azure CLI 1.0](nsg-quickstart-nodejs.md).</span></span>


## <a name="quick-commands"></a><span data-ttu-id="ab8a4-109">快速命令</span><span class="sxs-lookup"><span data-stu-id="ab8a4-109">Quick commands</span></span>
<span data-ttu-id="ab8a4-110">toocreate 網路安全性的群組和規則，您需要最新 hello [Azure CLI 2.0](/cli/azure/install-az-cli2)安裝並登入 tooan Azure 帳戶使用[az 登入](/cli/azure/#login)。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-110">toocreate a Network Security Group and rules you need hello latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in tooan Azure account using [az login](/cli/azure/#login).</span></span>

<span data-ttu-id="ab8a4-111">在 hello 下列範例中，會取代您自己的值的範例參數名稱。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-111">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="ab8a4-112">範例參數名稱包括 myResourceGroup、myNetworkSecurityGroup 和 myVnet。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-112">Example parameter names include *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="ab8a4-113">建立 hello 與網路安全性群組[az 網路 nsg 建立](/cli/azure/network/nsg#create)。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-113">Create hello network security group with [az network nsg create](/cli/azure/network/nsg#create).</span></span> <span data-ttu-id="ab8a4-114">hello 下列範例會建立名為的網路安全性群組*myNetworkSecurityGroup*在 hello *eastus*位置：</span><span class="sxs-lookup"><span data-stu-id="ab8a4-114">hello following example creates a network security group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
az network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="ab8a4-115">新增具有規則[az 網路 nsg 規則建立](/cli/azure/network/nsg/rule#create)tooallow HTTP 流量 tooyour 網頁伺服器 （或 調整成您自己的案例，例如 SSH 存取或資料庫連線）。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-115">Add a rule with [az network nsg rule create](/cli/azure/network/nsg/rule#create) tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="ab8a4-116">hello 下列範例會建立名為的規則*myNetworkSecurityGroupRule* tooallow TCP 連接埠 80 上的流量：</span><span class="sxs-lookup"><span data-stu-id="ab8a4-116">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
az network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --priority 1000 \
    --destination-port-range 80
```

<span data-ttu-id="ab8a4-117">關聯 hello 網路安全性群組與您的 VM 網路介面 (NIC) [az 網路 nic 更新](/cli/azure/network/nic#update)。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-117">Associate hello Network Security Group with your VM's network interface (NIC) with [az network nic update](/cli/azure/network/nic#update).</span></span> <span data-ttu-id="ab8a4-118">hello 下列範例將名為現有 NIC *myNic* hello 名為的網路安全性群組與*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="ab8a4-118">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network nic update \
    --resource-group myResourceGroup \
    --name myNic \
    --network-security-group myNetworkSecurityGroup
```

<span data-ttu-id="ab8a4-119">或者，您可以將您的網路安全性群組與虛擬網路子網路與[az 網路 vnet 子網路更新](/cli/azure/network/vnet/subnet#update)而不是只 toohello 網路介面上之單一 VM。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-119">Alternatively, you can associate your Network Security Group with a virtual network subnet with [az network vnet subnet update](/cli/azure/network/vnet/subnet#update) rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="ab8a4-120">hello 下列範例將現有的子網路，名為*mySubnet*在 hello *myVnet* hello 名為的網路安全性群組與虛擬網路*myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="ab8a4-120">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
az network vnet subnet update \
    --resource-group myResourceGroup \
    --vnet-name myVnet \
    --name mySubnet \
    --network-security-group myNetworkSecurityGroup
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="ab8a4-121">網路安全性群組的詳細資訊</span><span class="sxs-lookup"><span data-stu-id="ab8a4-121">More information on Network Security Groups</span></span>
<span data-ttu-id="ab8a4-122">這裡 hello 快速命令可讓您設定 tooget 和流量流動 tooyour VM 執行。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-122">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="ab8a4-123">網路安全性群組可提供許多很棒的功能和控制存取 tooyour 資源的資料粒度。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-123">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="ab8a4-124">您可以深入了解 [建立網路安全性群組和 ACL 規則](tutorial-virtual-network.md#secure-network-traffic)。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-124">You can read more about [creating a Network Security Group and ACL rules here](tutorial-virtual-network.md#secure-network-traffic).</span></span>

<span data-ttu-id="ab8a4-125">針對高可用性 Web 應用程式，您應該將 VM 放在 Azure Load Balancer 後方。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-125">For highly available web applications, you should place your VMs behind an Azure Load Balancer.</span></span> <span data-ttu-id="ab8a4-126">hello 負載平衡器會將流量 tooVMs，以提供的流量篩選的網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-126">hello load balancer distributes traffic tooVMs, with a Network Security Group that provides traffic filtering.</span></span> <span data-ttu-id="ab8a4-127">如需詳細資訊，請參閱[如何 tooload 平衡 Linux 虛擬機器中 Azure toocreate 高可用性的應用程式](tutorial-load-balancer.md)。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-127">For more information, see [How tooload balance Linux virtual machines in Azure toocreate a highly available application](tutorial-load-balancer.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ab8a4-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ab8a4-128">Next steps</span></span>
<span data-ttu-id="ab8a4-129">在此範例中，您可以建立簡單的規則 tooallow HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="ab8a4-129">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="ab8a4-130">您可以找到有關 hello 下列文件中建立更詳細的環境：</span><span class="sxs-lookup"><span data-stu-id="ab8a4-130">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="ab8a4-131">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="ab8a4-131">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="ab8a4-132">什麼是網路安全性群組 (NSG)？</span><span class="sxs-lookup"><span data-stu-id="ab8a4-132">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
