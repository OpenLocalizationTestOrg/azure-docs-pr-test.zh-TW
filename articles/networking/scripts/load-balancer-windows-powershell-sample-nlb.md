---
title: "Azure PowerShell 指令碼範例 - 為目標為 VM 的流量進行負載平衡以達到高可用性 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 為目標為 VM 的流量進行負載平衡以達到高可用性"
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
ms.openlocfilehash: c77def8906b151f2cc6e4bbc4188be8ecbeac732
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-to-vms-for-high-availability"></a><span data-ttu-id="35f46-103">為目標為 VM 的流量進行負載平衡以達到高可用性</span><span class="sxs-lookup"><span data-stu-id="35f46-103">Load balance traffic to VMs for high availability</span></span>

<span data-ttu-id="35f46-104">此指令碼範例會建立所需的一切，以執行數部依據高可用性和負載平衡組態所設定的 Windows 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="35f46-104">This script sample creates everything needed to run several Windows virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="35f46-105">執行指令碼之後，您將擁有三部已加入至 Azure 可用性設定組並可透過 Azure Load Balancer 存取的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="35f46-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

<span data-ttu-id="35f46-106">您可以視需要使用 [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) \(英文\) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="35f46-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="35f46-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="35f46-107">Sample script</span></span>

<span data-ttu-id="35f46-108">[!code-powershell[主要](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "快速建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="35f46-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="35f46-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="35f46-109">Clean up deployment</span></span> 

<span data-ttu-id="35f46-110">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="35f46-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="35f46-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="35f46-111">Script explanation</span></span>

<span data-ttu-id="35f46-112">此指令碼使用下列命令來建立資源群組、虛擬機器、可用性設定組、負載平衡器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="35f46-112">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="35f46-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="35f46-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="35f46-114">命令</span><span class="sxs-lookup"><span data-stu-id="35f46-114">Command</span></span> | <span data-ttu-id="35f46-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="35f46-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="35f46-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="35f46-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="35f46-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="35f46-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="35f46-118">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="35f46-118">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="35f46-119">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="35f46-119">Creates a subnet configuration.</span></span> <span data-ttu-id="35f46-120">此組態可使用於虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="35f46-120">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="35f46-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="35f46-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="35f46-122">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="35f46-122">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="35f46-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="35f46-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress)  | <span data-ttu-id="35f46-124">建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="35f46-124">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="35f46-125">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="35f46-125">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer)  | <span data-ttu-id="35f46-126">建立 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="35f46-126">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="35f46-127">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="35f46-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="35f46-128">建立負載平衡器探查。</span><span class="sxs-lookup"><span data-stu-id="35f46-128">Creates a load balancer probe.</span></span> <span data-ttu-id="35f46-129">負載平衡器探查是用來監視負載平衡器集合中的每部 VM。</span><span class="sxs-lookup"><span data-stu-id="35f46-129">A load balancer probe is used to monitor each VM in the load balancer set.</span></span> <span data-ttu-id="35f46-130">如有任何 VM 變得無法存取，就不會將流量路由至該 VM。</span><span class="sxs-lookup"><span data-stu-id="35f46-130">If any VM becomes inaccessible, traffic is not routed to the VM.</span></span> |
| [<span data-ttu-id="35f46-131">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="35f46-131">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="35f46-132">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="35f46-132">Creates an load balancer rule.</span></span> <span data-ttu-id="35f46-133">在此範例中，會為連接埠 80 建立規則。</span><span class="sxs-lookup"><span data-stu-id="35f46-133">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="35f46-134">HTTP 流量到達負載平衡器時，它會路由傳送至負載平衡器集內其中一個 VM 的連接埠 80。</span><span class="sxs-lookup"><span data-stu-id="35f46-134">As HTTP traffic arrives at the load balancer, it is routed to port 80 one of the VMs in the load balancer set.</span></span> |
| [<span data-ttu-id="35f46-135">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="35f46-135">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="35f46-136">建立負載平衡器網路位址轉譯 (NAT) 規則。</span><span class="sxs-lookup"><span data-stu-id="35f46-136">Creates a load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="35f46-137">NAT 規則會將負載平衡器的連接埠對應至 VM 上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="35f46-137">NAT rules map a port of the load balancer to a port on a VM.</span></span> <span data-ttu-id="35f46-138">在此範例中，會為傳送到負載平衡器集合中每部 VM 的 SSH 流量建立 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="35f46-138">In this sample, a NAT rule is created for SSH traffic to each VM in the load balancer set.</span></span>  |
| [<span data-ttu-id="35f46-139">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="35f46-139">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="35f46-140">建立網路安全性群組 (NSG)，做為網際網路和虛擬機器之間的安全性界限。</span><span class="sxs-lookup"><span data-stu-id="35f46-140">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="35f46-141">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="35f46-141">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="35f46-142">建立允許輸入流量的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="35f46-142">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="35f46-143">在此範例中，會開放連接埠 22 供 SSH 流量使用。</span><span class="sxs-lookup"><span data-stu-id="35f46-143">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="35f46-144">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="35f46-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="35f46-145">建立虛擬網路卡，並將它連接至虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="35f46-145">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="35f46-146">New-AzureRmAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="35f46-146">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="35f46-147">建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="35f46-147">Creates an availability set.</span></span> <span data-ttu-id="35f46-148">可用性設定組可將虛擬機器分散到各個實體資源，讓整個集合不致受到萬一發生的失敗所影響，藉此來確保應用程式運作時間。</span><span class="sxs-lookup"><span data-stu-id="35f46-148">Availability sets ensure application uptime by spreading the virtual machines across physical resources such that if failure occurs, the entire set is not effected.</span></span> |
| [<span data-ttu-id="35f46-149">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="35f46-149">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="35f46-150">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="35f46-150">Creates a VM configuration.</span></span> <span data-ttu-id="35f46-151">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="35f46-151">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="35f46-152">建立 VM 時會使用此組態。</span><span class="sxs-lookup"><span data-stu-id="35f46-152">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="35f46-153">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="35f46-153">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm)  | <span data-ttu-id="35f46-154">建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="35f46-154">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="35f46-155">此命令也會指定要使用的虛擬機器映像和管理認證。</span><span class="sxs-lookup"><span data-stu-id="35f46-155">This command also specifies the virtual machine image to be used and administrative credentials.</span></span>  |
| [<span data-ttu-id="35f46-156">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="35f46-156">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="35f46-157">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="35f46-157">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="35f46-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="35f46-158">Next steps</span></span>

<span data-ttu-id="35f46-159">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="35f46-159">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="35f46-160">您可以在 [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)中找到其他網路 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="35f46-160">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
