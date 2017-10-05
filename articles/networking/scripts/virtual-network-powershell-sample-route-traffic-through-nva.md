---
title: "Azure PowerShell 指令碼範例 - 透過網路虛擬設備來路由傳送流量 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 透過防火牆網路虛擬設備來路由傳送流量。"
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 883d28dac72a66c2186d222f72b04d68e532cead
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="7c0c3-103">透過網路虛擬設備來路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="7c0c3-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="7c0c3-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="7c0c3-105">它也會建立一個已啟用 IP 轉送功能的 VM，以在兩個子網路之間路由傳送流量。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="7c0c3-106">執行此指令碼之後，您可以將網路軟體 (例如防火牆應用程式) 部署到 VM。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

<span data-ttu-id="7c0c3-107">您可以視需要使用 [Azure PowerShell 指南 (英文)](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-107">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7c0c3-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="7c0c3-108">Sample script</span></span>


<span data-ttu-id="7c0c3-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "透過網路虛擬設備來路由傳送流量")]</span><span class="sxs-lookup"><span data-stu-id="7c0c3-109">[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="7c0c3-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="7c0c3-110">Clean up deployment</span></span> 

<span data-ttu-id="7c0c3-111">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="7c0c3-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="7c0c3-112">Script explanation</span></span>

<span data-ttu-id="7c0c3-113">此指令碼會使用下列命令來建立資源群組、虛擬網路及網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="7c0c3-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="7c0c3-115">命令</span><span class="sxs-lookup"><span data-stu-id="7c0c3-115">Command</span></span> | <span data-ttu-id="7c0c3-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="7c0c3-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c0c3-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7c0c3-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="7c0c3-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7c0c3-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="7c0c3-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="7c0c3-120">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="7c0c3-121">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="7c0c3-121">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="7c0c3-122">建立後端和 DMZ 子網路。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-122">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="7c0c3-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="7c0c3-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="7c0c3-124">建立公用 IP 位址以從網際網路存取 VM。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-124">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="7c0c3-125">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="7c0c3-125">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="7c0c3-126">建立虛擬網路介面並為它啟用 IP 轉送功能。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-126">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="7c0c3-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="7c0c3-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="7c0c3-128">建立網路安全性群組 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-128">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="7c0c3-129">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="7c0c3-129">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="7c0c3-130">建立允許對 VM 進行 HTTP 和 HTTPS 連接埠輸入的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-130">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="7c0c3-131">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="7c0c3-131">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="7c0c3-132">將 NSG 和路由表與子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-132">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="7c0c3-133">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="7c0c3-133">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="7c0c3-134">為所有路由建立一個路由表。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-134">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="7c0c3-135">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="7c0c3-135">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="7c0c3-136">建立路由，以透過 VM 在子網路與網際網路之間路由傳送流量。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-136">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="7c0c3-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="7c0c3-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="7c0c3-138">建立虛擬機器，並將 NIC 連結到此虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-138">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="7c0c3-139">此命令也會指定要使用的虛擬機器映像和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-139">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="7c0c3-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7c0c3-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="7c0c3-141">刪除資源群組及其包含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-141">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c0c3-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7c0c3-142">Next steps</span></span>

<span data-ttu-id="7c0c3-143">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="7c0c3-144">您可以在 [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)中找到其他網路 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="7c0c3-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>