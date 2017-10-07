---
title: "aaaAzure CLI 指令碼範例-負載平衡的多個網站以 hello Azure CLI |Microsoft 文件"
description: "Azure CLI 指令碼範例-負載平衡的多個網站 toohello 相同的虛擬機器"
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
ms.openlocfilehash: 136da5d1783fb9f9dc87f1ffad8eec7b95c6bd7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="99b2b-103">進行多個網站的負載平衡</span><span class="sxs-lookup"><span data-stu-id="99b2b-103">Load balance multiple websites</span></span>

<span data-ttu-id="99b2b-104">此指令碼範例使用可用性設定組成員的兩個虛擬機器 (VM) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="99b2b-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="99b2b-105">負載平衡器會將兩個不同的流量導向 toohello 兩個 Vm 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="99b2b-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="99b2b-106">執行 hello 指令碼之後，可以部署 web 伺服器軟體 toohello Vm，裝載多個 web sites 中，每個都有它自己的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="99b2b-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="99b2b-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="99b2b-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.sh  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="99b2b-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="99b2b-108">Clean up deployment</span></span> 

<span data-ttu-id="99b2b-109">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="99b2b-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="99b2b-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="99b2b-110">Script explanation</span></span>

<span data-ttu-id="99b2b-111">此指令碼會使用下列命令 toocreate 資源群組、 虛擬網路負載平衡器和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="99b2b-111">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="99b2b-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="99b2b-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="99b2b-113">命令</span><span class="sxs-lookup"><span data-stu-id="99b2b-113">Command</span></span> | <span data-ttu-id="99b2b-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="99b2b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="99b2b-115">az group create</span><span class="sxs-lookup"><span data-stu-id="99b2b-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="99b2b-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="99b2b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="99b2b-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="99b2b-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="99b2b-118">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="99b2b-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="99b2b-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="99b2b-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="99b2b-120">建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="99b2b-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="99b2b-121">az network lb create</span><span class="sxs-lookup"><span data-stu-id="99b2b-121">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="99b2b-122">建立 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="99b2b-122">Creates an Azure Load Balancer.</span></span> |
| [<span data-ttu-id="99b2b-123">az network lb probe create</span><span class="sxs-lookup"><span data-stu-id="99b2b-123">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="99b2b-124">建立負載平衡器探查。</span><span class="sxs-lookup"><span data-stu-id="99b2b-124">Creates a load balancer probe.</span></span> <span data-ttu-id="99b2b-125">負載平衡器探查是使用的 toomonitor hello 負載平衡器集內的每個 VM。</span><span class="sxs-lookup"><span data-stu-id="99b2b-125">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="99b2b-126">如果任何 VM 變得無法存取，流量不是路由的 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="99b2b-126">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="99b2b-127">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="99b2b-127">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="99b2b-128">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="99b2b-128">Creates a load balancer rule.</span></span> <span data-ttu-id="99b2b-129">在此範例中，會為連接埠 80 建立規則。</span><span class="sxs-lookup"><span data-stu-id="99b2b-129">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="99b2b-130">HTTP 流量抵達 hello 負載平衡器時，它是路由的 tooport 80 hello Vm hello 負載平衡器集內的其中一個。</span><span class="sxs-lookup"><span data-stu-id="99b2b-130">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="99b2b-131">az network lb frontend-ip create</span><span class="sxs-lookup"><span data-stu-id="99b2b-131">az network lb frontend-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/frontend-ip#create) | <span data-ttu-id="99b2b-132">建立 hello 負載平衡器的前端 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="99b2b-132">Create a frontend IP address for hello Load Balancer.</span></span> |
| [<span data-ttu-id="99b2b-133">az network lb address-pool create</span><span class="sxs-lookup"><span data-stu-id="99b2b-133">az network lb address-pool create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/address-pool#create) | <span data-ttu-id="99b2b-134">建立後端位址集區。</span><span class="sxs-lookup"><span data-stu-id="99b2b-134">Creates a backend address pool.</span></span> |
| [<span data-ttu-id="99b2b-135">az network nic create</span><span class="sxs-lookup"><span data-stu-id="99b2b-135">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="99b2b-136">建立虛擬網路介面卡，並將其附加 toohello 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="99b2b-136">Creates a virtual network card and attaches it toohello virtual network, and subnet.</span></span> |
| [<span data-ttu-id="99b2b-137">az vm availability-set create</span><span class="sxs-lookup"><span data-stu-id="99b2b-137">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="99b2b-138">建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="99b2b-138">Creates an availability set.</span></span> <span data-ttu-id="99b2b-139">可用性設定組來確保應用程式執行時間跨實體資源分配 hello 虛擬機器，使得發生失敗時，不受影響 hello 整個集合。</span><span class="sxs-lookup"><span data-stu-id="99b2b-139">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="99b2b-140">az network nic ip-config create</span><span class="sxs-lookup"><span data-stu-id="99b2b-140">az network nic ip-config create</span></span>](https://docs.microsoft.com/cli/azure/network/nic/ip-config#create) | <span data-ttu-id="99b2b-141">建立 IP 設定。</span><span class="sxs-lookup"><span data-stu-id="99b2b-141">Creates an IP confiuration.</span></span> <span data-ttu-id="99b2b-142">您必須啟用訂用帳戶的 hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic 功能。</span><span class="sxs-lookup"><span data-stu-id="99b2b-142">You must have hello Microsoft.Network/AllowMultipleIpConfigurationsPerNic feature enabled for your subscription.</span></span> <span data-ttu-id="99b2b-143">只能在一個設定可能會被指定為每個 NIC，使用 hello-請主要旗標 hello 主要 IP 設定。</span><span class="sxs-lookup"><span data-stu-id="99b2b-143">Only one configuration may be designated as hello primary IP configuration per NIC, using hello --make-primary flag.</span></span> |
| [<span data-ttu-id="99b2b-144">az vm create</span><span class="sxs-lookup"><span data-stu-id="99b2b-144">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="99b2b-145">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="99b2b-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="99b2b-146">此命令也會指定使用 hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="99b2b-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="99b2b-147">az group delete</span><span class="sxs-lookup"><span data-stu-id="99b2b-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="99b2b-148">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="99b2b-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="99b2b-149">後續步驟</span><span class="sxs-lookup"><span data-stu-id="99b2b-149">Next steps</span></span>

<span data-ttu-id="99b2b-150">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="99b2b-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="99b2b-151">其他網路功能的 CLI 指令碼範例可以在 hello [Azure 網路概觀文件](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="99b2b-151">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
