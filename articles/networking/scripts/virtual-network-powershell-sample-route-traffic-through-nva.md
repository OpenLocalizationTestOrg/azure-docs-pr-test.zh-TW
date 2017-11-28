---
title: "aaaAzure PowerShell 指令碼範例透過網路的虛擬設備的路由傳送流量 |Microsoft 文件"
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
ms.openlocfilehash: 3b999f3289d654c00d5becb973e2883896457d52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="8c5bd-103">透過網路虛擬設備來路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="8c5bd-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="8c5bd-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="8c5bd-105">它也會將啟用的 tooroute 流量 hello 兩個子網路之間轉送 ip 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="8c5bd-106">執行 hello 指令碼之後，您可以部署網路的軟體，例如防火牆應用程式，toohello VM。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

<span data-ttu-id="8c5bd-107">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8c5bd-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="8c5bd-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.ps1 "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8c5bd-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="8c5bd-109">Clean up deployment</span></span> 

<span data-ttu-id="8c5bd-110">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```
## <a name="script-explanation"></a><span data-ttu-id="8c5bd-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="8c5bd-111">Script explanation</span></span>

<span data-ttu-id="8c5bd-112">此指令碼會使用下列命令 toocreate hello 資源群組、 虛擬網路和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="8c5bd-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="8c5bd-114">命令</span><span class="sxs-lookup"><span data-stu-id="8c5bd-114">Command</span></span> | <span data-ttu-id="8c5bd-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="8c5bd-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8c5bd-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8c5bd-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup)  | <span data-ttu-id="8c5bd-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8c5bd-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8c5bd-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="8c5bd-119">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="8c5bd-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8c5bd-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8c5bd-121">建立後端和 DMZ 子網路。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="8c5bd-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="8c5bd-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="8c5bd-123">建立從 hello 網際網路的公用 IP 位址 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="8c5bd-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="8c5bd-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="8c5bd-125">建立虛擬網路介面並為它啟用 IP 轉送功能。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="8c5bd-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="8c5bd-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="8c5bd-127">建立網路安全性群組 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="8c5bd-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="8c5bd-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="8c5bd-129">建立允許 HTTP 和 HTTPS 連接埠輸入 toohello VM 的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-129">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="8c5bd-130">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8c5bd-130">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig)| <span data-ttu-id="8c5bd-131">路由資料表 toosubnets 和相關聯 hello Nsg。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-131">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="8c5bd-132">New-AzureRmRouteTable</span><span class="sxs-lookup"><span data-stu-id="8c5bd-132">New-AzureRmRouteTable</span></span>](/powershell/module/azurerm.network/new-azurermroutetable)| <span data-ttu-id="8c5bd-133">為所有路由建立一個路由表。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="8c5bd-134">New-AzureRMRouteConfig</span><span class="sxs-lookup"><span data-stu-id="8c5bd-134">New-AzureRMRouteConfig</span></span>](/powershell/module/azurerm.network/new-azurermrouteconfig)| <span data-ttu-id="8c5bd-135">建立路由 tooroute hello 網際網路透過 hello VM 子網路之間的流量。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-135">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="8c5bd-136">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="8c5bd-136">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="8c5bd-137">建立虛擬機器，並附加 hello NIC tooit。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-137">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="8c5bd-138">此命令也會指定 hello 虛擬機器映像 toouse 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-138">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="8c5bd-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8c5bd-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup)  | <span data-ttu-id="8c5bd-140">刪除資源群組及其包含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8c5bd-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8c5bd-141">Next steps</span></span>

<span data-ttu-id="8c5bd-142">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="8c5bd-143">其他網路的 PowerShell 指令碼範例可以在 hello [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8c5bd-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
