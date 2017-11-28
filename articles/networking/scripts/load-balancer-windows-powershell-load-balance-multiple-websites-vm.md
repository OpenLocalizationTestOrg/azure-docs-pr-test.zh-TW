---
title: "aaaAzure PowerShell 指令碼範例-負載平衡的多個網站使用 Azure PowerShell |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-負載平衡的多個網站 toohello 相同的虛擬機器"
services: load-balancer
documentationcenter: load-balancer
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 316818964eb6928fe4163ef69eb7f05da2dc9636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="df0a8-103">進行多個網站的負載平衡</span><span class="sxs-lookup"><span data-stu-id="df0a8-103">Load balance multiple websites</span></span>

<span data-ttu-id="df0a8-104">此指令碼範例使用可用性設定組成員的兩個虛擬機器 (VM) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="df0a8-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="df0a8-105">負載平衡器會將兩個不同的流量導向 toohello 兩個 Vm 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="df0a8-105">A load balancer directs traffic for two separate IP addresses toohello two VMs.</span></span> <span data-ttu-id="df0a8-106">執行 hello 指令碼之後，可以部署 web 伺服器軟體 toohello Vm，裝載多個 web sites 中，每個都有它自己的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="df0a8-106">After running hello script, you could deploy web server software toohello VMs and host multiple web sites, each with its own IP address.</span></span>

<span data-ttu-id="df0a8-107">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="df0a8-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="df0a8-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="df0a8-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]

## <a name="clean-up-deployment"></a><span data-ttu-id="df0a8-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="df0a8-109">Clean up deployment</span></span> 

<span data-ttu-id="df0a8-110">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="df0a8-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="df0a8-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="df0a8-111">Script explanation</span></span>

<span data-ttu-id="df0a8-112">此指令碼會使用下列命令 toocreate 資源群組、 虛擬網路負載平衡器和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="df0a8-112">This script uses hello following commands toocreate a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="df0a8-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="df0a8-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="df0a8-114">命令</span><span class="sxs-lookup"><span data-stu-id="df0a8-114">Command</span></span> | <span data-ttu-id="df0a8-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="df0a8-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="df0a8-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="df0a8-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="df0a8-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="df0a8-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="df0a8-118">New-AzureRmAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="df0a8-118">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="df0a8-119">建立 Azure 可用性集 tooprovide 高可用性。</span><span class="sxs-lookup"><span data-stu-id="df0a8-119">Creates an Azure availability set tooprovide high availability.</span></span> |
| [<span data-ttu-id="df0a8-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="df0a8-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="df0a8-121">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="df0a8-121">Creates a subnet configuration.</span></span> <span data-ttu-id="df0a8-122">此設定可搭配 hello 虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="df0a8-122">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="df0a8-123">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="df0a8-123">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="df0a8-124">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="df0a8-124">Creates a virtual network.</span></span> |
| [<span data-ttu-id="df0a8-125">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="df0a8-125">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="df0a8-126">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="df0a8-126">Creates a public IP address.</span></span> |
| [<span data-ttu-id="df0a8-127">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="df0a8-127">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="df0a8-128">建立負載平衡器的前端 IP 設定。</span><span class="sxs-lookup"><span data-stu-id="df0a8-128">Creates a front end IP config for a load balancer.</span></span> |
| [<span data-ttu-id="df0a8-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="df0a8-129">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="df0a8-130">建立負載平衡器的後端位址集區設定。</span><span class="sxs-lookup"><span data-stu-id="df0a8-130">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="df0a8-131">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="df0a8-131">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="df0a8-132">建立 NLB 探查。</span><span class="sxs-lookup"><span data-stu-id="df0a8-132">Creates an NLB probe.</span></span> <span data-ttu-id="df0a8-133">NLB 探查是使用的 toomonitor hello NLB 集中每個 VM。</span><span class="sxs-lookup"><span data-stu-id="df0a8-133">An NLB probe is used toomonitor each VM in hello NLB set.</span></span> <span data-ttu-id="df0a8-134">如果任何 VM 變得無法存取，流量不是路由的 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="df0a8-134">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="df0a8-135">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="df0a8-135">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="df0a8-136">建立 NLB 規則。</span><span class="sxs-lookup"><span data-stu-id="df0a8-136">Creates an NLB rule.</span></span> <span data-ttu-id="df0a8-137">在此範例中，會為連接埠 80 建立規則。</span><span class="sxs-lookup"><span data-stu-id="df0a8-137">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="df0a8-138">HTTP 流量抵達 hello NLB 時，它是路由的 tooport 80 hello NLB 設定中的 hello Vm 的其中一個。</span><span class="sxs-lookup"><span data-stu-id="df0a8-138">As HTTP traffic arrives at hello NLB, it is routed tooport 80 one of hello VMs in hello NLB set.</span></span> |
| [<span data-ttu-id="df0a8-139">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="df0a8-139">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="df0a8-140">建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="df0a8-140">Creates a load balancer.</span></span> |
| [<span data-ttu-id="df0a8-141">New-AzureRmNetworkInterfaceIpConfig</span><span class="sxs-lookup"><span data-stu-id="df0a8-141">New-AzureRmNetworkInterfaceIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | <span data-ttu-id="df0a8-142">定義虛擬網路介面的進階功能。</span><span class="sxs-lookup"><span data-stu-id="df0a8-142">Defines advanced features for a virtual network interface.</span></span> |
| [<span data-ttu-id="df0a8-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="df0a8-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="df0a8-144">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="df0a8-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="df0a8-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="df0a8-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="df0a8-146">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="df0a8-146">Creates a VM configuration.</span></span> <span data-ttu-id="df0a8-147">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="df0a8-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="df0a8-148">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="df0a8-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="df0a8-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="df0a8-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="df0a8-150">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="df0a8-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="df0a8-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="df0a8-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="df0a8-152">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="df0a8-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="df0a8-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="df0a8-153">Next steps</span></span>

<span data-ttu-id="df0a8-154">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="df0a8-154">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="df0a8-155">其他網路的 PowerShell 指令碼範例可以在 hello [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="df0a8-155">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
