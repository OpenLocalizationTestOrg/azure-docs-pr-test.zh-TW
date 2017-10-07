---
title: "CLI 指令碼範例提供高可用性的負載平衡流量 tooVMs aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例-負載平衡流量 tooVMs 高可用性"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a><span data-ttu-id="7fe77-103">負載平衡流量 tooVMs 高可用性</span><span class="sxs-lookup"><span data-stu-id="7fe77-103">Load balance traffic tooVMs for high availability</span></span>

<span data-ttu-id="7fe77-104">此指令碼範例會建立所需的所有項目 toorun 數個 Ubuntu 虛擬機器設定高可用性和負載平衡的設定。</span><span class="sxs-lookup"><span data-stu-id="7fe77-104">This script sample creates everything needed toorun several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="7fe77-105">之後執行 hello 指令碼，您將擁有三部虛擬機器，聯結 tooan Azure 可用性設定組，且可透過 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="7fe77-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7fe77-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="7fe77-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7fe77-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="7fe77-107">Clean up deployment</span></span> 

<span data-ttu-id="7fe77-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="7fe77-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7fe77-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="7fe77-109">Script explanation</span></span>

<span data-ttu-id="7fe77-110">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器、 可用性設定組中，負載平衡器和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="7fe77-110">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="7fe77-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="7fe77-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7fe77-112">命令</span><span class="sxs-lookup"><span data-stu-id="7fe77-112">Command</span></span> | <span data-ttu-id="7fe77-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="7fe77-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7fe77-114">az group create</span><span class="sxs-lookup"><span data-stu-id="7fe77-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7fe77-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7fe77-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7fe77-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="7fe77-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="7fe77-117">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="7fe77-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="7fe77-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="7fe77-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="7fe77-119">建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="7fe77-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="7fe77-120">az network lb create</span><span class="sxs-lookup"><span data-stu-id="7fe77-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="7fe77-121">建立 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="7fe77-121">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="7fe77-122">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="7fe77-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="7fe77-123">建立負載平衡器探查。</span><span class="sxs-lookup"><span data-stu-id="7fe77-123">Creates a load balancer probe.</span></span> <span data-ttu-id="7fe77-124">負載平衡器探查是使用的 toomonitor hello 負載平衡器集內的每個 VM。</span><span class="sxs-lookup"><span data-stu-id="7fe77-124">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="7fe77-125">如果任何 VM 變得無法存取，流量不是路由的 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="7fe77-125">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="7fe77-126">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="7fe77-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="7fe77-127">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="7fe77-127">Creates a load balancer rule.</span></span> <span data-ttu-id="7fe77-128">在此範例中，會為連接埠 80 建立規則。</span><span class="sxs-lookup"><span data-stu-id="7fe77-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="7fe77-129">HTTP 流量抵達 hello 負載平衡器時，它是路由的 tooport 80 hello Vm hello LB 集內的其中一個。</span><span class="sxs-lookup"><span data-stu-id="7fe77-129">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello LB set.</span></span> |
| [<span data-ttu-id="7fe77-130">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="7fe77-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="7fe77-131">建立負載平衡器網路位址轉譯 (NAT) 規則。</span><span class="sxs-lookup"><span data-stu-id="7fe77-131">Creates load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="7fe77-132">NAT 規則對應 hello 負載平衡器 tooa 連接埠在 VM 上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="7fe77-132">NAT rules map a port of hello load balancer tooa port on a VM.</span></span> <span data-ttu-id="7fe77-133">在此範例中，會為在 hello 負載平衡器集 SSH 流量 tooeach VM 建立 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="7fe77-133">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello load balancer set.</span></span>  |
| [<span data-ttu-id="7fe77-134">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="7fe77-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="7fe77-135">建立網路安全性群組 (NSG)，也就是 hello 網際網路和 hello 虛擬機器的安全性界限。</span><span class="sxs-lookup"><span data-stu-id="7fe77-135">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="7fe77-136">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="7fe77-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="7fe77-137">建立 NSG 規則 tooallow 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="7fe77-137">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="7fe77-138">在此範例中，會開放連接埠 22 供 SSH 流量使用。</span><span class="sxs-lookup"><span data-stu-id="7fe77-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="7fe77-139">az network nic create</span><span class="sxs-lookup"><span data-stu-id="7fe77-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="7fe77-140">建立虛擬網路介面卡，並將其附加 toohello 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="7fe77-140">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="7fe77-141">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="7fe77-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="7fe77-142">建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="7fe77-142">Creates an availability set.</span></span> <span data-ttu-id="7fe77-143">可用性設定組來確保應用程式執行時間跨實體資源分配 hello 虛擬機器，使得發生失敗時，不受影響 hello 整個集合。</span><span class="sxs-lookup"><span data-stu-id="7fe77-143">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="7fe77-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="7fe77-144">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="7fe77-145">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="7fe77-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="7fe77-146">此命令也會指定使用 hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="7fe77-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="7fe77-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="7fe77-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="7fe77-148">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="7fe77-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7fe77-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7fe77-149">Next steps</span></span>

<span data-ttu-id="7fe77-150">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7fe77-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7fe77-151">其他的 Azure 網路 CLI 指令碼範例可以在 hello [Azure 網路文件](../cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="7fe77-151">Additional Azure Networking CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
