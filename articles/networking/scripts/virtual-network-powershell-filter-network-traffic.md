---
title: "Azure PowerShell 指令碼範例 - 篩選 VM 網路流量 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 篩選輸入和輸出 VM 網路流量。"
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
ms.openlocfilehash: e871ba2f370157936c2aaabc804dc9f5aea6d7ca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="47454-103">篩選輸入和輸出 VM 網路流量</span><span class="sxs-lookup"><span data-stu-id="47454-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="47454-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="47454-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="47454-105">傳送到前端子網路的輸入流量會限制為 HTTP 及 HTTPS，而從後端子網路傳送到網際網路的輸出流量則不受允許。</span><span class="sxs-lookup"><span data-stu-id="47454-105">Inbound network traffic to the front-end subnet is limited to HTTP, and HTTPS, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="47454-106">執行此指令碼之後，您將會有一部具有兩個 NIC 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="47454-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="47454-107">每個 NIC 會連線到不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="47454-107">Each NIC is connected to a different subnet.</span></span>

<span data-ttu-id="47454-108">您可以視需要使用 [Azure PowerShell 指南 (英文)](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="47454-108">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="47454-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="47454-109">Sample script</span></span>


<span data-ttu-id="47454-110">[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "篩選 VM 網路流量")]</span><span class="sxs-lookup"><span data-stu-id="47454-110">[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="47454-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="47454-111">Clean up deployment</span></span> 

<span data-ttu-id="47454-112">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="47454-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="47454-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="47454-113">Script explanation</span></span>

<span data-ttu-id="47454-114">此指令碼會使用下列命令來建立資源群組、虛擬網路及網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="47454-114">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="47454-115">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="47454-115">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="47454-116">命令</span><span class="sxs-lookup"><span data-stu-id="47454-116">Command</span></span> | <span data-ttu-id="47454-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="47454-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="47454-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="47454-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="47454-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="47454-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="47454-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="47454-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="47454-121">建立子網路設定物件</span><span class="sxs-lookup"><span data-stu-id="47454-121">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="47454-122">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="47454-122">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="47454-123">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="47454-123">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="47454-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="47454-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="47454-125">建立要指派給網路安全性群組的安全性規則。</span><span class="sxs-lookup"><span data-stu-id="47454-125">Creates security rules to be assigned to a network security group.</span></span> |
| [<span data-ttu-id="47454-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="47454-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="47454-127">建立對特定子網路允許或封鎖特定連接埠的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="47454-127">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="47454-128">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="47454-128">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="47454-129">將 NSG 與子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="47454-129">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="47454-130">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="47454-130">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="47454-131">建立公用 IP 位址以從網際網路存取 VM。</span><span class="sxs-lookup"><span data-stu-id="47454-131">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="47454-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="47454-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="47454-133">建立虛擬網路介面，並將它們連結到虛擬網路的前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="47454-133">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="47454-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="47454-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="47454-135">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="47454-135">Creates a VM configuration.</span></span> <span data-ttu-id="47454-136">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="47454-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="47454-137">建立 VM 時會使用此組態。</span><span class="sxs-lookup"><span data-stu-id="47454-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="47454-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="47454-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="47454-139">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="47454-139">Create a virtual machine.</span></span> |
|[<span data-ttu-id="47454-140">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="47454-140">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="47454-141">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="47454-141">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="47454-142">後續步驟</span><span class="sxs-lookup"><span data-stu-id="47454-142">Next steps</span></span>

<span data-ttu-id="47454-143">如需有關 Azure PowerShell 的詳細資訊，請參閱 [Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="47454-143">For more information on the Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="47454-144">您可以在 [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)中找到其他網路 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="47454-144">Additional networking PowerShell script samples can be found in the [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>