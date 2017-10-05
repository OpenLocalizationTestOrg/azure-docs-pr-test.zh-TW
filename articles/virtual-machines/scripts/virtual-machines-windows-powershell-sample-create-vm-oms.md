---
title: "Azure PowerShell 指令碼範例 - OMS | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - OMS"
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
ms.date: 03/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9f876be46f5214b12d6a46e54509ba3541f819c5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="02d21-103">使用 PowerShell 建立 Operations Management Suite 監視的 VM</span><span class="sxs-lookup"><span data-stu-id="02d21-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="02d21-104">此指令碼會建立 Azure 虛擬機器、安裝 Operations Management Suite (OMS) 代理程式，並向 OMS 工作區註冊系統。</span><span class="sxs-lookup"><span data-stu-id="02d21-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="02d21-105">執行此指令碼後，就能在 OMS 主控台中看到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="02d21-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span> <span data-ttu-id="02d21-106">此外，您需要更新 OMS 工作區識別碼和工作區金鑰。</span><span class="sxs-lookup"><span data-stu-id="02d21-106">Also, you need to update the OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="02d21-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="02d21-107">Sample script</span></span>

<span data-ttu-id="02d21-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "建立 VM OMS")]</span><span class="sxs-lookup"><span data-stu-id="02d21-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="02d21-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="02d21-109">Clean up deployment</span></span> 

<span data-ttu-id="02d21-110">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="02d21-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="02d21-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="02d21-111">Script explanation</span></span>

<span data-ttu-id="02d21-112">此指令碼會使用下列命令來建立部署。</span><span class="sxs-lookup"><span data-stu-id="02d21-112">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="02d21-113">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="02d21-113">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="02d21-114">命令</span><span class="sxs-lookup"><span data-stu-id="02d21-114">Command</span></span> | <span data-ttu-id="02d21-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="02d21-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="02d21-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="02d21-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="02d21-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="02d21-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="02d21-118">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="02d21-118">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="02d21-119">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="02d21-119">Creates a subnet configuration.</span></span> <span data-ttu-id="02d21-120">此組態可使用於虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="02d21-120">This configuration is used with the virtual network creation process.</span></span> |
| [<span data-ttu-id="02d21-121">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="02d21-121">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="02d21-122">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="02d21-122">Creates a virtual network.</span></span> |
| [<span data-ttu-id="02d21-123">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="02d21-123">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="02d21-124">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="02d21-124">Creates a public IP address.</span></span> |
| [<span data-ttu-id="02d21-125">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="02d21-125">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="02d21-126">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="02d21-126">Creates a network security group rule configuration.</span></span> <span data-ttu-id="02d21-127">建立 NSG 時，此組態用來建立 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="02d21-127">This configuration is used to create an NSG rule when the NSG is created.</span></span> |
| [<span data-ttu-id="02d21-128">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="02d21-128">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="02d21-129">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="02d21-129">Creates a network security group.</span></span> |
| [<span data-ttu-id="02d21-130">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="02d21-130">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="02d21-131">取得子網路資訊。</span><span class="sxs-lookup"><span data-stu-id="02d21-131">Gets subnet information.</span></span> <span data-ttu-id="02d21-132">建立網路介面時會使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="02d21-132">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="02d21-133">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="02d21-133">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="02d21-134">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="02d21-134">Creates a network interface.</span></span> |
| [<span data-ttu-id="02d21-135">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="02d21-135">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="02d21-136">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="02d21-136">Creates a VM configuration.</span></span> <span data-ttu-id="02d21-137">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="02d21-137">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="02d21-138">建立 VM 時會使用此組態。</span><span class="sxs-lookup"><span data-stu-id="02d21-138">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="02d21-139">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="02d21-139">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="02d21-140">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="02d21-140">Create a virtual machine.</span></span> |
| [<span data-ttu-id="02d21-141">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="02d21-141">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="02d21-142">將 VM 擴充功能新增至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="02d21-142">Add a VM extension to the virtual machine.</span></span> <span data-ttu-id="02d21-143">在此情況下，會使用 Operations Management Suite 代理程式擴充功能來安裝 OMS 代理程式，並在 OMS 工作區中註冊 VM。</span><span class="sxs-lookup"><span data-stu-id="02d21-143">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="02d21-144">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="02d21-144">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="02d21-145">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="02d21-145">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="02d21-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02d21-146">Next steps</span></span>

<span data-ttu-id="02d21-147">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="02d21-147">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="02d21-148">您可以在 [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="02d21-148">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
