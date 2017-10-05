---
title: "Azure CLI 指令碼範例 - 使用 VM 平衡流量負載以達到高可用性 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 使用 VM 平衡流量負載以達到高可用性"
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
ms.openlocfilehash: 69a7753cc75b028e2bf093053d9a5fc0890562e8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-to-vms-for-high-availability"></a><span data-ttu-id="3051c-103">使用 VM 平衡流量負載以達到高可用性</span><span class="sxs-lookup"><span data-stu-id="3051c-103">Load balance traffic to VMs for high availability</span></span>

<span data-ttu-id="3051c-104">此指令碼範例會建立所需的一切，以執行數部依據高可用性和負載平衡組態所設定的 Ubuntu 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3051c-104">This script sample creates everything needed to run several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="3051c-105">執行指令碼之後，您將擁有三部已加入至 Azure 可用性設定組並可透過 Azure Load Balancer 存取的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3051c-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3051c-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="3051c-106">Sample script</span></span>

<span data-ttu-id="3051c-107">[!code-azurecli-interactive[主要](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "快速建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="3051c-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3051c-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="3051c-108">Clean up deployment</span></span> 

<span data-ttu-id="3051c-109">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="3051c-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3051c-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="3051c-110">Script explanation</span></span>

<span data-ttu-id="3051c-111">此指令碼使用下列命令來建立資源群組、虛擬機器、可用性設定組、負載平衡器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="3051c-111">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="3051c-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="3051c-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3051c-113">命令</span><span class="sxs-lookup"><span data-stu-id="3051c-113">Command</span></span> | <span data-ttu-id="3051c-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="3051c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3051c-115">az group create</span><span class="sxs-lookup"><span data-stu-id="3051c-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="3051c-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3051c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3051c-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="3051c-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="3051c-118">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="3051c-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="3051c-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="3051c-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="3051c-120">建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3051c-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="3051c-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="3051c-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="3051c-122">建立 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="3051c-122">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="3051c-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="3051c-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="3051c-124">建立負載平衡器探查。</span><span class="sxs-lookup"><span data-stu-id="3051c-124">Creates a load balancer probe.</span></span> <span data-ttu-id="3051c-125">負載平衡器探查是用來監視負載平衡器集合中的每部 VM。</span><span class="sxs-lookup"><span data-stu-id="3051c-125">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="3051c-126">如有任何 VM 變得無法存取，就不會將流量路由至該 VM。</span><span class="sxs-lookup"><span data-stu-id="3051c-126">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="3051c-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="3051c-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="3051c-128">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="3051c-128">Creates a load balancer rule.</span></span> <span data-ttu-id="3051c-129">在此範例中，會為連接埠 80 建立規則。</span><span class="sxs-lookup"><span data-stu-id="3051c-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="3051c-130">HTTP 流量到達負載平衡器時，它會路由傳送至 LB 集內其中一部 VM 的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="3051c-130">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the LB set.</span></span> |
| [<span data-ttu-id="3051c-131">az network lb inbound-nat-rule create</span><span class="sxs-lookup"><span data-stu-id="3051c-131">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="3051c-132">建立負載平衡器網路位址轉譯 (NAT) 規則。</span><span class="sxs-lookup"><span data-stu-id="3051c-132">Creates load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="3051c-133">NAT 規則會將負載平衡器的連接埠對應至 VM 上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="3051c-133">NAT rules map a port of the load balancer to a port on a VM.</span></span> <span data-ttu-id="3051c-134">在此範例中，會為傳送到負載平衡器集合中每部 VM 的 SSH 流量建立 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="3051c-134">In this sample, a NAT rule is created for SSH traffic to each VM in the load balancer set.</span></span>  |
| [<span data-ttu-id="3051c-135">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="3051c-135">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="3051c-136">建立網路安全性群組 (NSG)，做為網際網路和虛擬機器之間的安全性界限。</span><span class="sxs-lookup"><span data-stu-id="3051c-136">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="3051c-137">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="3051c-137">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="3051c-138">建立允許輸入流量的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="3051c-138">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="3051c-139">在此範例中，會開放連接埠 22 供 SSH 流量使用。</span><span class="sxs-lookup"><span data-stu-id="3051c-139">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="3051c-140">az network nic create</span><span class="sxs-lookup"><span data-stu-id="3051c-140">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="3051c-141">建立虛擬網路卡，並將它連接至虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="3051c-141">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="3051c-142">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="3051c-142">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="3051c-143">建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="3051c-143">Creates an availability set.</span></span> <span data-ttu-id="3051c-144">可用性設定組可將虛擬機器分散到各個實體資源，讓整個集合不致受到萬一發生的失敗所影響，藉此來確保應用程式運作時間。</span><span class="sxs-lookup"><span data-stu-id="3051c-144">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="3051c-145">az vm create</span><span class="sxs-lookup"><span data-stu-id="3051c-145">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="3051c-146">建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="3051c-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="3051c-147">此命令也會指定要使用的虛擬機器映像和管理認證。</span><span class="sxs-lookup"><span data-stu-id="3051c-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="3051c-148">az group delete</span><span class="sxs-lookup"><span data-stu-id="3051c-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="3051c-149">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="3051c-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3051c-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3051c-150">Next steps</span></span>

<span data-ttu-id="3051c-151">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3051c-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="3051c-152">您可以在 [Azure 網路文件](../cli-samples.md)中找到其他 Azure 網路 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="3051c-152">Additional Azure Networking CLI script samples can be found in the [Azure Networking documentation](../cli-samples.md).</span></span>