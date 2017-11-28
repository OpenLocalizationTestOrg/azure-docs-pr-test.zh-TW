---
title: "Azure PowerShell 指令碼範例 - 建立 Windows VM NLB | Microsoft Docs"
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
ms.openlocfilehash: 25bcbbcd1615e01a384825d7bd1582a528e91f71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="load-balance-traffic-between-highly-available-virtual-machines"></a><span data-ttu-id="5b39c-103">對高可用性虛擬機器之間的流量進行負載平衡</span><span class="sxs-lookup"><span data-stu-id="5b39c-103">Load balance traffic between highly available virtual machines</span></span>

<span data-ttu-id="5b39c-104">此指令碼範例會建立一切所需，以執行數個依據高可用性和負載平衡組態所設定的 Windows Server 2016 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5b39c-104">This script sample creates everything needed to run several Windows Server 2016 virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="5b39c-105">執行指令碼之後，您將擁有三部已加入至 Azure 可用性設定組並可透過 Azure Load Balancer 存取的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5b39c-105">After running the script, you will have three virtual machines, joined to an Azure Availability Set, and accessible through an Azure Load Balancer.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5b39c-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="5b39c-106">Sample script</span></span>

<span data-ttu-id="5b39c-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "建立 VM NLB")]</span><span class="sxs-lookup"><span data-stu-id="5b39c-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.ps1 "Create VM NLB")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="5b39c-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="5b39c-108">Clean up deployment</span></span> 

<span data-ttu-id="5b39c-109">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="5b39c-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5b39c-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="5b39c-110">Script explanation</span></span>

<span data-ttu-id="5b39c-111">此指令碼會使用下列命令來建立部署。</span><span class="sxs-lookup"><span data-stu-id="5b39c-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="5b39c-112">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="5b39c-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5b39c-113">命令</span><span class="sxs-lookup"><span data-stu-id="5b39c-113">Command</span></span> | <span data-ttu-id="5b39c-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="5b39c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5b39c-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5b39c-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5b39c-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5b39c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5b39c-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5b39c-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5b39c-118">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="5b39c-118">Creates a subnet configuration.</span></span> <span data-ttu-id="5b39c-119">此組態可使用於虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="5b39c-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="5b39c-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5b39c-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5b39c-121">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5b39c-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5b39c-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5b39c-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5b39c-123">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5b39c-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5b39c-124">New-AzureRmLoadBalancerFrontendIpConfig</span><span class="sxs-lookup"><span data-stu-id="5b39c-124">New-AzureRmLoadBalancerFrontendIpConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig) | <span data-ttu-id="5b39c-125">建立負載平衡器的前端 IP 組態。</span><span class="sxs-lookup"><span data-stu-id="5b39c-125">Creates a front-end IP configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5b39c-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span><span class="sxs-lookup"><span data-stu-id="5b39c-126">New-AzureRmLoadBalancerBackendAddressPoolConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig) | <span data-ttu-id="5b39c-127">建立負載平衡器的後端位址集區設定。</span><span class="sxs-lookup"><span data-stu-id="5b39c-127">Creates a backend address pool configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5b39c-128">New-AzureRmLoadBalancerProbeConfig</span><span class="sxs-lookup"><span data-stu-id="5b39c-128">New-AzureRmLoadBalancerProbeConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerprobeconfig) | <span data-ttu-id="5b39c-129">建立負載平衡器的探查組態。</span><span class="sxs-lookup"><span data-stu-id="5b39c-129">Creates a probe configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5b39c-130">New-AzureRmLoadBalancerRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5b39c-130">New-AzureRmLoadBalancerRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerruleconfig) | <span data-ttu-id="5b39c-131">建立負載平衡器的規則組態。</span><span class="sxs-lookup"><span data-stu-id="5b39c-131">Creates a rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5b39c-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5b39c-132">New-AzureRmLoadBalancerInboundNatRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancerinboundnatruleconfig) | <span data-ttu-id="5b39c-133">建立負載平衡器的輸入 NAT 規則組態。</span><span class="sxs-lookup"><span data-stu-id="5b39c-133">Creates an inbound NAT rule configuration for a load balancer.</span></span> |
| [<span data-ttu-id="5b39c-134">New-AzureRmLoadBalancer</span><span class="sxs-lookup"><span data-stu-id="5b39c-134">New-AzureRmLoadBalancer</span></span>](/powershell/module/azurerm.network/new-azurermloadbalancer) | <span data-ttu-id="5b39c-135">建立負載平衡器。</span><span class="sxs-lookup"><span data-stu-id="5b39c-135">Creates a load balancer.</span></span> |
| [<span data-ttu-id="5b39c-136">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5b39c-136">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5b39c-137">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="5b39c-137">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5b39c-138">建立 NSG 時，此組態用來建立 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="5b39c-138">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="5b39c-139">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5b39c-139">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5b39c-140">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="5b39c-140">Creates a network security group.</span></span> |
| [<span data-ttu-id="5b39c-141">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5b39c-141">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5b39c-142">取得子網路資訊。</span><span class="sxs-lookup"><span data-stu-id="5b39c-142">Gets subnet information.</span></span> <span data-ttu-id="5b39c-143">建立網路介面時會使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="5b39c-143">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5b39c-144">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5b39c-144">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5b39c-145">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="5b39c-145">Creates a network interface.</span></span> |
| [<span data-ttu-id="5b39c-146">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5b39c-146">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5b39c-147">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="5b39c-147">Creates a VM configuration.</span></span> <span data-ttu-id="5b39c-148">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="5b39c-148">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5b39c-149">建立 VM 時會使用此組態。</span><span class="sxs-lookup"><span data-stu-id="5b39c-149">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5b39c-150">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5b39c-150">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5b39c-151">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5b39c-151">Create a virtual machine.</span></span> |
|[<span data-ttu-id="5b39c-152">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5b39c-152">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5b39c-153">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="5b39c-153">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5b39c-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5b39c-154">Next steps</span></span>

<span data-ttu-id="5b39c-155">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5b39c-155">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5b39c-156">您可以在 [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="5b39c-156">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
