---
title: "aaaAzure PowerShell 指令碼範例為建立 Windows VM NLB |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 建立 Windows VM NLB"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 60a48c5f243c8ff3ab886437ae45b21ce069ea4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="5bea7-103">對高可用性虛擬機器之間的流量進行負載平衡</span><span class="sxs-lookup"><span data-stu-id="5bea7-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="5bea7-104">此指令碼範例會建立所需的所有項目 toorun 數個 Windows Server 2016 的虛擬機器設定高可用性和負載平衡的設定。</span><span class="sxs-lookup"><span data-stu-id="5bea7-104">This script sample creates everything needed toorun several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="5bea7-105">之後執行 hello 指令碼，您將擁有三部虛擬機器，聯結 tooan Azure 可用性設定組，且可透過 Azure 負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5bea7-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5bea7-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="5bea7-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5bea7-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="5bea7-107">Clean up deployment</span></span> 

<span data-ttu-id="5bea7-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="5bea7-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5bea7-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="5bea7-109">Script explanation</span></span>

<span data-ttu-id="5bea7-110">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="5bea7-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="5bea7-111">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="5bea7-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5bea7-112">命令</span><span class="sxs-lookup"><span data-stu-id="5bea7-112">Command</span></span> | <span data-ttu-id="5bea7-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="5bea7-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5bea7-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5bea7-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5bea7-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5bea7-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5bea7-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5bea7-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5bea7-117">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="5bea7-117">Creates a subnet configuration.</span></span> <span data-ttu-id="5bea7-118">此設定可搭配 hello 虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="5bea7-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="5bea7-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5bea7-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5bea7-120">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5bea7-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5bea7-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5bea7-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5bea7-122">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5bea7-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5bea7-123">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="5bea7-123">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="5bea7-124">建立負載平衡器的前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="5bea7-124">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5bea7-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="5bea7-125">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="5bea7-126">建立負載平衡器的後端位址集區設定。</span><span class="sxs-lookup"><span data-stu-id="5bea7-126">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5bea7-127">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="5bea7-127">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="5bea7-128">建立負載平衡器的探查組態。</span><span class="sxs-lookup"><span data-stu-id="5bea7-128">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5bea7-129">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5bea7-129">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="5bea7-130">建立負載平衡器的規則組態。</span><span class="sxs-lookup"><span data-stu-id="5bea7-130">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5bea7-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5bea7-131">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="5bea7-132">建立負載平衡器的輸入 NAT 規則組態。</span><span class="sxs-lookup"><span data-stu-id="5bea7-132">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5bea7-133">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="5bea7-133">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="5bea7-134">建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5bea7-134">Creates a load balancer.</span></span> |
| [<span data-ttu-id="5bea7-135">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5bea7-135">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5bea7-136">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="5bea7-136">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5bea7-137">此設定時，使用的 toocreate NSG 規則建立 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="5bea7-137">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="5bea7-138">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5bea7-138">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5bea7-139">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="5bea7-139">Creates a network security group.</span></span> |
| [<span data-ttu-id="5bea7-140">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5bea7-140">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5bea7-141">取得子網路資訊。</span><span class="sxs-lookup"><span data-stu-id="5bea7-141">Gets subnet information.</span></span> <span data-ttu-id="5bea7-142">建立網路介面時會使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="5bea7-142">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5bea7-143">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5bea7-143">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5bea7-144">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="5bea7-144">Creates a network interface.</span></span> |
| [<span data-ttu-id="5bea7-145">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5bea7-145">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5bea7-146">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="5bea7-146">Creates a VM configuration.</span></span> <span data-ttu-id="5bea7-147">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="5bea7-147">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5bea7-148">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="5bea7-148">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5bea7-149">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5bea7-149">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5bea7-150">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5bea7-150">Create a virtual machine.</span></span> |
|[<span data-ttu-id="5bea7-151">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5bea7-151">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5bea7-152">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="5bea7-152">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5bea7-153">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5bea7-153">Next steps</span></span>

<span data-ttu-id="5bea7-154">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5bea7-154">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5bea7-155">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5bea7-155">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
