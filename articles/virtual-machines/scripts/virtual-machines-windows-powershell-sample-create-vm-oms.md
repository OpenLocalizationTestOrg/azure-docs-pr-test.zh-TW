---
title: "aaaAzure PowerShell 指令碼範例-OMS |Microsoft 文件"
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
ms.openlocfilehash: 1eeafbe743013e97bf3fcefb5ce87f72cb503a4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="8fbaa-103">使用 PowerShell 建立 Operations Management Suite 監視的 VM</span><span class="sxs-lookup"><span data-stu-id="8fbaa-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="8fbaa-104">此指令碼會建立 Azure 虛擬機器、 安裝 hello Operations Management Suite (OMS) 代理程式，並註冊使用 OMS 工作區的 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="8fbaa-105">Hello 指令碼執行之後，將會出現在 hello OMS 主控台 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span> <span data-ttu-id="8fbaa-106">此外，您需要 tooupdate hello OMS 工作區識別碼和工作區金鑰。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-106">Also, you need tooupdate hello OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="8fbaa-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="8fbaa-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="8fbaa-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="8fbaa-108">Clean up deployment</span></span> 

<span data-ttu-id="8fbaa-109">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="8fbaa-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="8fbaa-110">Script explanation</span></span>

<span data-ttu-id="8fbaa-111">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-111">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="8fbaa-112">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-112">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="8fbaa-113">命令</span><span class="sxs-lookup"><span data-stu-id="8fbaa-113">Command</span></span> | <span data-ttu-id="8fbaa-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="8fbaa-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="8fbaa-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8fbaa-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="8fbaa-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="8fbaa-117">New-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8fbaa-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8fbaa-118">建立子網路組態。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-118">Creates a subnet configuration.</span></span> <span data-ttu-id="8fbaa-119">此設定可搭配 hello 虛擬網路建立程序。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-119">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="8fbaa-120">New-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="8fbaa-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="8fbaa-121">建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="8fbaa-122">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="8fbaa-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="8fbaa-123">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="8fbaa-124">New-AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="8fbaa-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="8fbaa-125">建立網路安全性群組規則組態。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="8fbaa-126">此設定時，使用的 toocreate NSG 規則建立 hello NSG。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-126">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="8fbaa-127">New-AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="8fbaa-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="8fbaa-128">建立網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="8fbaa-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="8fbaa-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="8fbaa-130">取得子網路資訊。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-130">Gets subnet information.</span></span> <span data-ttu-id="8fbaa-131">建立網路介面時會使用此資訊。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="8fbaa-132">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="8fbaa-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="8fbaa-133">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="8fbaa-134">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="8fbaa-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="8fbaa-135">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-135">Creates a VM configuration.</span></span> <span data-ttu-id="8fbaa-136">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="8fbaa-137">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-137">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="8fbaa-138">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="8fbaa-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="8fbaa-139">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="8fbaa-140">Set-AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="8fbaa-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="8fbaa-141">新增 VM 延伸模組 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-141">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="8fbaa-142">在此情況下，hello Operations Management Suite 代理程式延伸模組是使用的 tooinstall hello OMS 代理程式，並註冊 hello OMS 工作區中的 VM。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-142">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="8fbaa-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="8fbaa-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="8fbaa-144">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="8fbaa-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8fbaa-145">Next steps</span></span>

<span data-ttu-id="8fbaa-146">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-146">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="8fbaa-147">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="8fbaa-147">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
