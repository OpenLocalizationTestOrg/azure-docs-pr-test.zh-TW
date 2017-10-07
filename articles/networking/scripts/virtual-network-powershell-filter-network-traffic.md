---
title: "aaaAzure PowerShell 指令碼範例篩選條件的 VM 網路流量 |Microsoft 文件"
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
ms.openlocfilehash: 39eae6a43a8dc7f9fc616ef3ec50f95443fd3547
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="06178-103">篩選輸入和輸出 VM 網路流量</span><span class="sxs-lookup"><span data-stu-id="06178-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="06178-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="06178-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="06178-105">輸入網路流量 toohello 前端子網路是有限的 tooHTTP 和 HTTPS，而輸出流量，不允許網際網路從 hello 後端子 toohello。</span><span class="sxs-lookup"><span data-stu-id="06178-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, and HTTPS, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="06178-106">執行 hello 指令碼之後，您必須有兩個 Nic 的一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="06178-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="06178-107">每個 NIC 已連線的 tooa 不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="06178-107">Each NIC is connected tooa different subnet.</span></span>

<span data-ttu-id="06178-108">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="06178-108">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="06178-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="06178-109">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/filter-network-traffic/filter-network-traffic.ps1  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="06178-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="06178-110">Clean up deployment</span></span> 

<span data-ttu-id="06178-111">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="06178-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="06178-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="06178-112">Script explanation</span></span>

<span data-ttu-id="06178-113">此指令碼會使用下列命令 toocreate hello 資源群組、 虛擬網路和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="06178-113">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="06178-114">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="06178-114">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="06178-115">命令</span><span class="sxs-lookup"><span data-stu-id="06178-115">Command</span></span> | <span data-ttu-id="06178-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="06178-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="06178-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06178-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="06178-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="06178-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="06178-119">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="06178-119">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="06178-120">建立子網路設定物件</span><span class="sxs-lookup"><span data-stu-id="06178-120">Creates a subnet configuration object</span></span> |
| [<span data-ttu-id="06178-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="06178-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="06178-122">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="06178-122">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="06178-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="06178-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="06178-124">建立安全性規則 toobe 指派 tooa 網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="06178-124">Creates security rules toobe assigned tooa network security group.</span></span> |
| [<span data-ttu-id="06178-125">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="06178-125">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) |<span data-ttu-id="06178-126">建立 NSG 規則來允許或封鎖特定連接埠 toospecific 子網路。</span><span class="sxs-lookup"><span data-stu-id="06178-126">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="06178-127">Set-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="06178-127">Set-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="06178-128">將關聯 Nsg toosubnets。</span><span class="sxs-lookup"><span data-stu-id="06178-128">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="06178-129">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="06178-129">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="06178-130">建立從 hello 網際網路的公用 IP 位址 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="06178-130">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="06178-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="06178-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="06178-132">建立虛擬網路介面，並將其附加 toohello 虛擬網路的前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="06178-132">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="06178-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="06178-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="06178-134">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="06178-134">Creates a VM configuration.</span></span> <span data-ttu-id="06178-135">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="06178-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="06178-136">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="06178-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="06178-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="06178-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="06178-138">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="06178-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="06178-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="06178-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="06178-140">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="06178-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="06178-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="06178-141">Next steps</span></span>

<span data-ttu-id="06178-142">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="06178-142">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="06178-143">其他網路的 PowerShell 指令碼範例可以在 hello [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="06178-143">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
