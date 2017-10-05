---
title: "Azure PowerShell 指令碼範例 - IIS 搭配 DSC | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - IIS 搭配 DSC"
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
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: 38476119c88aa7d4f6578fc1e3756e11951e804a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="3e50b-103">使用 PowerShell 建立 IIS VM</span><span class="sxs-lookup"><span data-stu-id="3e50b-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="3e50b-104">此指令碼會建立執行 Windows Server 2016 的 Azure 虛擬機器，然後使用 Azure 虛擬機器 DSC 擴充功能來安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="3e50b-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses the Azure Virtual Machine DSC Extension to install IIS.</span></span> <span data-ttu-id="3e50b-105">執行指令碼之後，您可以在虛擬機器的公用 IP 位址上存取預設的 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="3e50b-105">After running the script, you can access the default IIS website on the public IP address of the virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="3e50b-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="3e50b-106">Sample script</span></span>

<span data-ttu-id="3e50b-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "建立 VM IIS DSC")]</span><span class="sxs-lookup"><span data-stu-id="3e50b-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="3e50b-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="3e50b-108">Clean up deployment</span></span> 

<span data-ttu-id="3e50b-109">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="3e50b-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="3e50b-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="3e50b-110">Script explanation</span></span>

<span data-ttu-id="3e50b-111">此指令碼會使用下列命令來建立部署。</span><span class="sxs-lookup"><span data-stu-id="3e50b-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="3e50b-112">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="3e50b-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="3e50b-113">命令</span><span class="sxs-lookup"><span data-stu-id="3e50b-113">Command</span></span> | <span data-ttu-id="3e50b-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="3e50b-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="3e50b-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3e50b-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="3e50b-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3e50b-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="3e50b-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="3e50b-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="3e50b-118">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="3e50b-118">Creates a subnet configuration.</span></span> <span data-ttu-id="3e50b-119">此組態可使用於虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="3e50b-119">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="3e50b-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="3e50b-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="3e50b-121">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="3e50b-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="3e50b-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="3e50b-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="3e50b-123">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3e50b-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="3e50b-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="3e50b-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="3e50b-125">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="3e50b-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="3e50b-126">建立 NSG 時，此組態用來建立 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="3e50b-126">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="3e50b-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="3e50b-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="3e50b-128">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="3e50b-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="3e50b-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="3e50b-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="3e50b-130">取得子網路資訊。</span><span class="sxs-lookup"><span data-stu-id="3e50b-130">Gets subnet information.</span></span> <span data-ttu-id="3e50b-131">建立網路介面時會使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="3e50b-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="3e50b-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="3e50b-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="3e50b-133">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="3e50b-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="3e50b-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="3e50b-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="3e50b-135">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="3e50b-135">Creates a VM configuration.</span></span> <span data-ttu-id="3e50b-136">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="3e50b-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="3e50b-137">建立 VM 時會使用此組態。</span><span class="sxs-lookup"><span data-stu-id="3e50b-137">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="3e50b-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="3e50b-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="3e50b-139">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3e50b-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="3e50b-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="3e50b-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="3e50b-141">將 VM 擴充功能新增至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3e50b-141">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="3e50b-142">此範例使用自訂指令碼擴充功能來安裝 IIS。</span><span class="sxs-lookup"><span data-stu-id="3e50b-142">In this sample, the custom script extension is used to install IIS.</span></span> |
|[<span data-ttu-id="3e50b-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="3e50b-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="3e50b-144">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="3e50b-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="3e50b-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3e50b-145">Next steps</span></span>

<span data-ttu-id="3e50b-146">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="3e50b-146">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="3e50b-147">您可以在 [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="3e50b-147">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
