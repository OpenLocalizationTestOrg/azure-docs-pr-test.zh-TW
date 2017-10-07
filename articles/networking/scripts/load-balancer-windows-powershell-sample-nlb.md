---
title: "PowerShell 指令碼範例提供高可用性的負載平衡流量 tooVMs aaaAzure |Microsoft 文件"
description: "Azure PowerShell 指令碼範例提供高可用性的負載平衡流量 tooVMs"
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
ms.openlocfilehash: 332c39e1aad071ca6f7ce420ccc1f423ef647d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a><span data-ttu-id="b0ce7-103">負載平衡流量 tooVMs 高可用性</span><span class="sxs-lookup"><span data-stu-id="b0ce7-103">Load balance traffic tooVMs for high availability</span></span>

<span data-ttu-id="b0ce7-104">此指令碼範例會建立所需的所有項目 toorun 數個 Windows 虛擬機器設定高可用性和負載平衡的設定。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-104">This script sample creates everything needed toorun several Windows virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="b0ce7-105">之後執行 hello 指令碼，您將擁有三部虛擬機器，聯結 tooan Azure 可用性設定組，且可透過 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

<span data-ttu-id="b0ce7-106">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b0ce7-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b0ce7-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="b0ce7-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="b0ce7-108">Clean up deployment</span></span> 

<span data-ttu-id="b0ce7-109">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b0ce7-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b0ce7-110">Script explanation</span></span>

<span data-ttu-id="b0ce7-111">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器、 可用性設定組中，負載平衡器和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="b0ce7-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="b0ce7-113">命令</span><span class="sxs-lookup"><span data-stu-id="b0ce7-113">Command</span></span> | <span data-ttu-id="b0ce7-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="b0ce7-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b0ce7-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b0ce7-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="b0ce7-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b0ce7-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="b0ce7-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="b0ce7-118">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-118">Creates a subnet configuration.</span></span> <span data-ttu-id="b0ce7-119">此設定可搭配 hello 虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-119">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="b0ce7-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="b0ce7-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="b0ce7-121">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-121">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="b0ce7-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="b0ce7-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress)  | <span data-ttu-id="b0ce7-123">建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-123">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="b0ce7-124">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="b0ce7-124">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer)  | <span data-ttu-id="b0ce7-125">建立 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-125">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="b0ce7-126">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="b0ce7-126">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="b0ce7-127">建立負載平衡器探查。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-127">Creates a load balancer probe.</span></span> <span data-ttu-id="b0ce7-128">負載平衡器探查是使用的 toomonitor hello 負載平衡器集內的每個 VM。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-128">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="b0ce7-129">如果任何 VM 變得無法存取，流量不是路由的 toohello VM。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-129">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="b0ce7-130">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="b0ce7-130">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="b0ce7-131">建立負載平衡器規則。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-131">Creates an load balancer rule.</span></span> <span data-ttu-id="b0ce7-132">在此範例中，會為連接埠 80 建立規則。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-132">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="b0ce7-133">HTTP 流量抵達 hello 負載平衡器時，它是路由的 tooport 80 hello Vm hello 負載平衡器集內的其中一個。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-133">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello load balancer set.</span></span> |
| [<span data-ttu-id="b0ce7-134">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="b0ce7-134">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="b0ce7-135">建立負載平衡器網路位址轉譯 (NAT) 規則。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-135">Creates a load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="b0ce7-136">NAT 規則對應 hello 負載平衡器 tooa 連接埠在 VM 上的連接埠。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-136">NAT rules map a port of hello load balancer tooa port on a VM.</span></span> <span data-ttu-id="b0ce7-137">在此範例中，會為在 hello 負載平衡器集 SSH 流量 tooeach VM 建立 NAT 規則。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-137">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello load balancer set.</span></span>  |
| [<span data-ttu-id="b0ce7-138">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="b0ce7-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="b0ce7-139">建立網路安全性群組 (NSG)，也就是 hello 網際網路和 hello 虛擬機器的安全性界限。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-139">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="b0ce7-140">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="b0ce7-140">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="b0ce7-141">建立 NSG 規則 tooallow 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-141">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="b0ce7-142">在此範例中，會開放連接埠 22 供 SSH 流量使用。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-142">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="b0ce7-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="b0ce7-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="b0ce7-144">建立虛擬網路介面卡，並將其附加 toohello 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-144">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="b0ce7-145">New-AzureRmAvailabilitySet</span><span class="sxs-lookup"><span data-stu-id="b0ce7-145">New-AzureRmAvailabilitySet</span></span>](/powershell/module/azurerm.compute/new-azurermavailabilityset) | <span data-ttu-id="b0ce7-146">建立可用性設定組。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-146">Creates an availability set.</span></span> <span data-ttu-id="b0ce7-147">可用性設定組來確保應用程式執行時間跨實體資源分配 hello 虛擬機器，使得發生失敗時，不受影響 hello 整個集合。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-147">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="b0ce7-148">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="b0ce7-148">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="b0ce7-149">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-149">Creates a VM configuration.</span></span> <span data-ttu-id="b0ce7-150">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-150">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="b0ce7-151">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-151">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="b0ce7-152">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="b0ce7-152">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm)  | <span data-ttu-id="b0ce7-153">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-153">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="b0ce7-154">此命令也會指定使用 hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-154">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="b0ce7-155">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="b0ce7-155">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="b0ce7-156">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-156">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b0ce7-157">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b0ce7-157">Next steps</span></span>

<span data-ttu-id="b0ce7-158">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-158">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="b0ce7-159">其他網路的 PowerShell 指令碼範例可以在 hello [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b0ce7-159">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
