---
title: "PowerShell 指令碼範例-aaaAzure 建立多層應用程式的網路 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 為多層式應用程式建立虛擬網路。"
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
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="39769-103">為多層式應用程式建立網路</span><span class="sxs-lookup"><span data-stu-id="39769-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="39769-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="39769-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="39769-105">流量 toohello 前端子網路是有限的 tooHTTP 和 SSH，流量 toohello 時後端子是有限的 tooMySQL，3306 的連接埠。</span><span class="sxs-lookup"><span data-stu-id="39769-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="39769-106">執行 hello 指令碼之後, 您將擁有兩部虛擬機器，您可以部署 web 伺服器和 MySQL 軟體每個子網路的其中一個。</span><span class="sxs-lookup"><span data-stu-id="39769-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="39769-107">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="39769-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="39769-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="39769-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="39769-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="39769-109">Clean up deployment</span></span> 

<span data-ttu-id="39769-110">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="39769-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="39769-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="39769-111">Script explanation</span></span>

<span data-ttu-id="39769-112">此指令碼會使用下列命令 toocreate hello 資源群組、 虛擬網路和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="39769-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="39769-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="39769-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="39769-114">命令</span><span class="sxs-lookup"><span data-stu-id="39769-114">Command</span></span> | <span data-ttu-id="39769-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="39769-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="39769-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="39769-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="39769-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="39769-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="39769-118">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="39769-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="39769-119">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="39769-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="39769-120">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="39769-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="39769-121">建立後端子網路。</span><span class="sxs-lookup"><span data-stu-id="39769-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="39769-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="39769-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="39769-123">建立從 hello 網際網路的公用 IP 位址 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="39769-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="39769-124">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="39769-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="39769-125">建立虛擬網路介面，並將其附加 toohello 虛擬網路的前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="39769-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="39769-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="39769-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="39769-127">建立網路安全性群組 (NSG) 相關聯的 toohello 前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="39769-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="39769-128">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="39769-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="39769-129">建立 NSG 規則來允許或封鎖特定連接埠 toospecific 子網路。</span><span class="sxs-lookup"><span data-stu-id="39769-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="39769-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="39769-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="39769-131">建立虛擬機器並將附加 NIC tooeach VM。</span><span class="sxs-lookup"><span data-stu-id="39769-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="39769-132">此命令也會指定 hello 虛擬機器映像 toouse 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="39769-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="39769-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="39769-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="39769-134">刪除資源群組及其包含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="39769-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="39769-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39769-135">Next steps</span></span>

<span data-ttu-id="39769-136">如需有關 hello Azure PowerShell 的詳細資訊，請參閱[Azure PowerShell 文件](https://docs.microsoft.com/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="39769-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="39769-137">其他網路的 PowerShell 指令碼範例可以在 hello [Azure 網路概觀文件](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="39769-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
