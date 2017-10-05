---
title: "Azure CLI 指令碼範例 - 使用 Azure CLI 進行多個網站的負載平衡 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 使用相同的虛擬機器進行多個網站的負載平衡"
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
ms.openlocfilehash: c5a584b33025122033b930822ae0a0864a7ec1cb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="26225-103">進行多個網站的負載平衡</span><span class="sxs-lookup"><span data-stu-id="26225-103">Load balance multiple websites</span></span>

<span data-ttu-id="26225-104">此指令碼範例使用可用性設定組成員的兩個虛擬機器 (VM) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="26225-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="26225-105">負載平衡器會將兩個不同 IP 位址的流量傳送至這兩個 VM。</span><span class="sxs-lookup"><span data-stu-id="26225-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="26225-106">執行指令碼之後，您可以將 Web 伺服器軟體部署至 VM 並主控多個網站 (各有自己的 IP 位址)。</span><span class="sxs-lookup"><span data-stu-id="26225-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="26225-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="26225-107">Sample script</span></span>


<span data-ttu-id="26225-108">[!code-azurecli-interactive[主要](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "進行多個網站的負載平衡")]</span><span class="sxs-lookup"><span data-stu-id="26225-108">[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="26225-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="26225-109">Clean up deployment</span></span> 

<span data-ttu-id="26225-110">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="26225-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="26225-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="26225-111">Script explanation</span></span>

<span data-ttu-id="26225-112">此指令碼使用下列命令建立資源群組、虛擬網路、負載平衡器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="26225-112">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="26225-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="26225-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="26225-114">命令</span><span class="sxs-lookup"><span data-stu-id="26225-114">Command</span></span> | <span data-ttu-id="26225-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="26225-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="26225-116">az group create</span><span class="sxs-lookup"><span data-stu-id="26225-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="26225-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="26225-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="26225-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="26225-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="26225-119">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="26225-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="26225-120">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="26225-120">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="26225-121">建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="26225-121">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="26225-122">az network lb create</span><span class="sxs-lookup"><span data-stu-id="26225-122">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="26225-123">建立 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="26225-123">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="26225-124">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="26225-124">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="26225-125">建立負載平衡器探查。</span><span class="sxs-lookup"><span data-stu-id="26225-125">Creates a load balancer probe.</span></span> <span data-ttu-id="26225-126">負載平衡器探查是用來監視負載平衡器集合中的每部 VM。</span><span class="sxs-lookup"><span data-stu-id="26225-126">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="26225-127">如有任何 VM 變得無法存取，就不會將流量路由至該 VM。</span><span class="sxs-lookup"><span data-stu-id="26225-127">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="26225-128">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="26225-128">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="26225-129">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="26225-129">Creates a load balancer rule.</span></span> <span data-ttu-id="26225-130">在此範例中，會為連接埠 80 建立規則。</span><span class="sxs-lookup"><span data-stu-id="26225-130">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="26225-131">HTTP 流量到達負載平衡器時，它會路由傳送至負載平衡器集內其中一個 VM 的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="26225-131">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span></span> |
| [<span data-ttu-id="26225-132">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="26225-132">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="26225-133">建立負載平衡器的前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="26225-133">Create a frontend IP address for the Load Balancer.</span></span> |
| [<span data-ttu-id="26225-134">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="26225-134">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="26225-135">建立後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="26225-135">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="26225-136">az network nic create</span><span class="sxs-lookup"><span data-stu-id="26225-136">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="26225-137">建立虛擬網路卡，並將它連結至虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="26225-137">Creates a virtual network card and attaches it to the virtual network, and subnet.</span></span> |
| [<span data-ttu-id="26225-138">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="26225-138">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="26225-139">建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="26225-139">Creates an availability set.</span></span> <span data-ttu-id="26225-140">可用性設定組可將虛擬機器分散到各個實體資源，讓整個集合不致受到萬一發生的失敗所影響，藉此來確保應用程式運作時間。</span><span class="sxs-lookup"><span data-stu-id="26225-140">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="26225-141">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="26225-141">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="26225-142">建立 IP 設定。</span><span class="sxs-lookup"><span data-stu-id="26225-142">Creates an IP confiuration.</span></span> <span data-ttu-id="26225-143">您的訂用帳戶必須啟用 Microsoft.Network/AllowMultipleIpConfigurationsPerNic 功能。</span><span class="sxs-lookup"><span data-stu-id="26225-143">You must have the Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="26225-144">每個 NIC 只能指定一個設定作為主要 IP 設定 (使用 --make-primary 旗標)。</span><span class="sxs-lookup"><span data-stu-id="26225-144">Only one configuration may be designated as the primary IP configuration per NIC, using the --make-primary flag.</span></span> |
| [<span data-ttu-id="26225-145">az vm create</span><span class="sxs-lookup"><span data-stu-id="26225-145">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="26225-146">建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="26225-146">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="26225-147">此命令也會指定要使用的虛擬機器映像和管理認證。</span><span class="sxs-lookup"><span data-stu-id="26225-147">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="26225-148">az group delete</span><span class="sxs-lookup"><span data-stu-id="26225-148">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="26225-149">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="26225-149">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="26225-150">後續步驟</span><span class="sxs-lookup"><span data-stu-id="26225-150">Next steps</span></span>

<span data-ttu-id="26225-151">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="26225-151">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="26225-152">您可以在 [Azure 網路概觀文件](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)中找到其他網路 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="26225-152">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
