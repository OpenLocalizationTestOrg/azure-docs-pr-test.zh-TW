---
title: "Azure PowerShell 指令碼範例 - 使用 Azure PowerShell 進行多個網站的負載平衡 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 將多個網站負載平衡至相同的虛擬機器"
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
ms.openlocfilehash: d73cdc98ff279c3ee1b93443abe4b6c7c97786a2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-multiple-websites"></a><span data-ttu-id="0ac46-103">進行多個網站的負載平衡</span><span class="sxs-lookup"><span data-stu-id="0ac46-103">Load balance multiple websites</span></span>

<span data-ttu-id="0ac46-104">此指令碼範例使用可用性設定組成員的兩個虛擬機器 (VM) 建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0ac46-104">This script sample creates a virtual network with two virtual machines (VM) that are members of an availability set.</span></span> <span data-ttu-id="0ac46-105">負載平衡器會將兩個不同 IP 位址的流量傳送至這兩個 VM。</span><span class="sxs-lookup"><span data-stu-id="0ac46-105">A load balancer directs traffic for two separate IP addresses to the two VMs.</span></span> <span data-ttu-id="0ac46-106">執行指令碼之後，您可以將 Web 伺服器軟體部署至 VM 並主控多個網站 (各有自己的 IP 位址)。</span><span class="sxs-lookup"><span data-stu-id="0ac46-106">After running the script, you could deploy web server software to the VMs and host multiple web sites, each with its own IP address.</span></span>

<span data-ttu-id="0ac46-107">您可以視需要使用 [Azure PowerShell 指南 (英文)](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="0ac46-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0ac46-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="0ac46-108">Sample script</span></span>

<span data-ttu-id="0ac46-109">[!code-powershell[主要](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "進行多個網站的負載平衡")]</span><span class="sxs-lookup"><span data-stu-id="0ac46-109">[!code-powershell[main](../../../powershell_scripts/load-balancer/load-balance-multiple-web-sites-vm/load-balance-multiple-web-sites-vm.ps1  "Load balance multiple web sites")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0ac46-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="0ac46-110">Clean up deployment</span></span> 

<span data-ttu-id="0ac46-111">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="0ac46-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0ac46-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="0ac46-112">Script explanation</span></span>

<span data-ttu-id="0ac46-113">此指令碼使用下列命令建立資源群組、虛擬網路、負載平衡器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="0ac46-113">This script uses the following commands to create a resource group, virtual network, load balancer, and all related resources.</span></span> <span data-ttu-id="0ac46-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="0ac46-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0ac46-115">命令</span><span class="sxs-lookup"><span data-stu-id="0ac46-115">Command</span></span> | <span data-ttu-id="0ac46-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="0ac46-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0ac46-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ac46-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="0ac46-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0ac46-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0ac46-119">New-AzureRmAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="0ac46-119">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="0ac46-120">建立 Azure 可用性設定組以提供高可用性。</span><span class="sxs-lookup"><span data-stu-id="0ac46-120">Creates an Azure availability set to provide high availability.</span></span> |
| [<span data-ttu-id="0ac46-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="0ac46-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="0ac46-122">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="0ac46-122">Creates a subnet configuration.</span></span> <span data-ttu-id="0ac46-123">此組態可使用於虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="0ac46-123">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="0ac46-124">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="0ac46-124">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="0ac46-125">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="0ac46-125">Creates a virtual network.</span></span> |
| [<span data-ttu-id="0ac46-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="0ac46-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="0ac46-127">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0ac46-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="0ac46-128">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="0ac46-128">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="0ac46-129">建立負載平衡器的前端 IP 設定。</span><span class="sxs-lookup"><span data-stu-id="0ac46-129">Creates a front end IP config for a load balancer.</span></span> |
| [<span data-ttu-id="0ac46-130">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="0ac46-130">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="0ac46-131">建立負載平衡器的後端位址集區設定。</span><span class="sxs-lookup"><span data-stu-id="0ac46-131">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="0ac46-132">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="0ac46-132">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="0ac46-133">建立 NLB 探查。</span><span class="sxs-lookup"><span data-stu-id="0ac46-133">Creates an NLB probe.</span></span> <span data-ttu-id="0ac46-134">NLB 探查可用來監視 NLB 集合中的每部 VM。</span><span class="sxs-lookup"><span data-stu-id="0ac46-134">An NLB probe is used to monitor each VM in the NLB set.</span></span> <span data-ttu-id="0ac46-135">如有任何 VM 變得無法存取，就不會將流量路由至該 VM。</span><span class="sxs-lookup"><span data-stu-id="0ac46-135">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="0ac46-136">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="0ac46-136">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="0ac46-137">建立 NLB 規則。</span><span class="sxs-lookup"><span data-stu-id="0ac46-137">Creates an NLB rule.</span></span> <span data-ttu-id="0ac46-138">在此範例中，會為連接埠 80 建立規則。</span><span class="sxs-lookup"><span data-stu-id="0ac46-138">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="0ac46-139">當 HTTP 流量抵達 NLB 時，就會經由連接埠 80 將其路由傳送至 NLB 集合的其中一部 VM。</span><span class="sxs-lookup"><span data-stu-id="0ac46-139">As HTTP traffic arrives at the NLB, it is routed to port 80 one of the VMs in the NLB set.</span></span> |
| [<span data-ttu-id="0ac46-140">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="0ac46-140">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="0ac46-141">建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="0ac46-141">Creates a load balancer.</span></span> |
| [<span data-ttu-id="0ac46-142">New-AzureRmNetworkInterfaceIpConfig</span><span class="sxs-lookup"><span data-stu-id="0ac46-142">New-AzureRmNetworkInterfaceIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterfaceipconfig) | <span data-ttu-id="0ac46-143">定義虛擬網路介面的進階功能。</span><span class="sxs-lookup"><span data-stu-id="0ac46-143">Defines advanced features for a virtual network interface.</span></span> |
| [<span data-ttu-id="0ac46-144">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="0ac46-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="0ac46-145">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="0ac46-145">Creates a network interface.</span></span> |
| [<span data-ttu-id="0ac46-146">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="0ac46-146">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="0ac46-147">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="0ac46-147">Creates a VM configuration.</span></span> <span data-ttu-id="0ac46-148">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="0ac46-148">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="0ac46-149">建立 VM 時會使用此組態。</span><span class="sxs-lookup"><span data-stu-id="0ac46-149">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="0ac46-150">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="0ac46-150">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="0ac46-151">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0ac46-151">Create a virtual machine.</span></span> |
|[<span data-ttu-id="0ac46-152">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ac46-152">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0ac46-153">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="0ac46-153">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0ac46-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ac46-154">Next steps</span></span>

<span data-ttu-id="0ac46-155">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0ac46-155">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="0ac46-156">您可以在 [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)中找到其他網路 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="0ac46-156">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
