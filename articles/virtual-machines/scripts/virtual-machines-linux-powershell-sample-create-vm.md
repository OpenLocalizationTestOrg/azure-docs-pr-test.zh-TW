---
title: "PowerShell 指令碼範例-aaaAzure 建立 Linux VM |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 建立 Linux VM"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/02/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 8ee2ee42aa68ee135a859b7eaead25811cf54095
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine-with-powershell"></a><span data-ttu-id="5d486-103">使用 PowerShell 建立完整設定的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5d486-103">Create a fully configured virtual machine with PowerShell</span></span>

<span data-ttu-id="5d486-104">此指令碼會建立具有 Ubuntu 作業系統的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d486-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="5d486-105">執行 hello 指令碼之後, 您可以透過 SSH 存取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d486-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5d486-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="5d486-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.ps1 "Create VM detailed")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5d486-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="5d486-107">Clean up deployment</span></span> 

<span data-ttu-id="5d486-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="5d486-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5d486-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="5d486-109">Script explanation</span></span>

<span data-ttu-id="5d486-110">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="5d486-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="5d486-111">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="5d486-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5d486-112">命令</span><span class="sxs-lookup"><span data-stu-id="5d486-112">Command</span></span> | <span data-ttu-id="5d486-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="5d486-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5d486-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5d486-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5d486-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5d486-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5d486-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5d486-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5d486-117">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="5d486-117">Creates a subnet configuration.</span></span> <span data-ttu-id="5d486-118">此設定可搭配 hello 虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="5d486-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="5d486-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5d486-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5d486-120">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="5d486-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5d486-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5d486-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5d486-122">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5d486-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5d486-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5d486-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5d486-124">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="5d486-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5d486-125">此設定時，使用的 toocreate NSG 規則建立 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="5d486-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="5d486-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5d486-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5d486-127">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="5d486-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="5d486-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5d486-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5d486-129">取得子網路資訊。</span><span class="sxs-lookup"><span data-stu-id="5d486-129">Gets subnet information.</span></span> <span data-ttu-id="5d486-130">建立網路介面時會使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="5d486-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5d486-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5d486-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5d486-132">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="5d486-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="5d486-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5d486-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5d486-134">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="5d486-134">Creates a VM configuration.</span></span> <span data-ttu-id="5d486-135">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="5d486-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5d486-136">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="5d486-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5d486-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5d486-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5d486-138">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="5d486-138">Create a virtual machine.</span></span> |
|[<span data-ttu-id="5d486-139">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5d486-139">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5d486-140">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="5d486-140">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5d486-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d486-141">Next steps</span></span>

<span data-ttu-id="5d486-142">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5d486-142">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5d486-143">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Linux VM 文件](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="5d486-143">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
