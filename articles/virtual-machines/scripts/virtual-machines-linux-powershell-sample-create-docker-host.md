---
title: "aaaAzure PowerShell 指令碼範例-Docker |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - Docker"
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
ms.openlocfilehash: 556093d3cfaecda352ff52cce96728fc0e723a39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-docker-host-with-powershell"></a><span data-ttu-id="e0b8f-103">用 PowerShell 建立 Docker 主機</span><span class="sxs-lookup"><span data-stu-id="e0b8f-103">Create a Docker host with PowerShell</span></span>

<span data-ttu-id="e0b8f-104">這個指令碼會建立啟用 Docker 功能的虛擬機器，並啟動執行 NGINX 的容器。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-104">This script creates a virtual machine with Docker enabled and starts a container running NGINX.</span></span> <span data-ttu-id="e0b8f-105">執行 hello 指令碼之後, 您可以透過 hello hello Azure 虛擬機器的 FQDN 存取 hello NGINX 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e0b8f-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e0b8f-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-docker-host/create-docker-host.ps1 "Create Docker host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e0b8f-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="e0b8f-107">Clean up deployment</span></span> 

<span data-ttu-id="e0b8f-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e0b8f-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e0b8f-109">Script explanation</span></span>

<span data-ttu-id="e0b8f-110">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="e0b8f-111">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e0b8f-112">命令</span><span class="sxs-lookup"><span data-stu-id="e0b8f-112">Command</span></span> | <span data-ttu-id="e0b8f-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="e0b8f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e0b8f-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e0b8f-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e0b8f-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e0b8f-116">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e0b8f-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e0b8f-117">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-117">Creates a subnet configuration.</span></span> <span data-ttu-id="e0b8f-118">此設定可搭配 hello 虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="e0b8f-119">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="e0b8f-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="e0b8f-120">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="e0b8f-121">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e0b8f-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="e0b8f-122">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="e0b8f-123">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="e0b8f-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="e0b8f-124">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="e0b8f-125">此設定時，使用的 toocreate NSG 規則建立 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="e0b8f-126">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="e0b8f-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="e0b8f-127">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="e0b8f-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="e0b8f-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="e0b8f-129">取得子網路資訊。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-129">Gets subnet information.</span></span> <span data-ttu-id="e0b8f-130">建立網路介面時會使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="e0b8f-131">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e0b8f-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="e0b8f-132">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="e0b8f-133">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="e0b8f-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="e0b8f-134">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-134">Creates a VM configuration.</span></span> <span data-ttu-id="e0b8f-135">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="e0b8f-136">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="e0b8f-137">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="e0b8f-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="e0b8f-138">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="e0b8f-139">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="e0b8f-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="e0b8f-140">新增 VM 延伸模組 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="e0b8f-141">在此範例中，hello Docker 延伸模組使用的 tooconfigure Docker 並執行 NGINX Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-141">In this sample, hello Docker extension is used tooconfigure Docker and run an NGINX Docker container.</span></span> |
|[<span data-ttu-id="e0b8f-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e0b8f-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e0b8f-143">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e0b8f-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e0b8f-144">Next steps</span></span>

<span data-ttu-id="e0b8f-145">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e0b8f-146">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Linux VM 文件](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e0b8f-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
