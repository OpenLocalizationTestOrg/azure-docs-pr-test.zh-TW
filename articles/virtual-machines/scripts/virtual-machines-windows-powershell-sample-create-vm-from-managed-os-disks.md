---
title: "Azure PowerShell 指令碼範例 - 連結受控磁碟作為 OS 磁碟以建立 VM | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 連結受控磁碟作為 OS 磁碟以建立 VM"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: ec532811e94647c8a04b9faf9474f6749969f83e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="2b519-103">使用現有受控 OS 磁碟搭配 PowerShell 以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2b519-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="2b519-104">此指令碼會連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2b519-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="2b519-105">在先前案例中使用此指令碼︰</span><span class="sxs-lookup"><span data-stu-id="2b519-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="2b519-106">從不同訂用帳戶中的受控磁碟複製而來的現有受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="2b519-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="2b519-107">從特殊化 VHD 檔案建立的現有受控磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="2b519-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="2b519-108">從快照集建立的現有受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="2b519-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2b519-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="2b519-109">Sample script</span></span>

<span data-ttu-id="2b519-110">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "從快照集建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="2b519-110">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2b519-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="2b519-111">Clean up deployment</span></span> 

<span data-ttu-id="2b519-112">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="2b519-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2b519-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="2b519-113">Script explanation</span></span>

<span data-ttu-id="2b519-114">此指令碼會使用下列命令來取得受控磁碟屬性、將受控磁碟連結至新的 VM，以及建立 VM。</span><span class="sxs-lookup"><span data-stu-id="2b519-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="2b519-115">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="2b519-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2b519-116">命令</span><span class="sxs-lookup"><span data-stu-id="2b519-116">Command</span></span> | <span data-ttu-id="2b519-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="2b519-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2b519-118">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="2b519-118">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="2b519-119">根據磁碟的名稱和資源群組取得磁碟物件。</span><span class="sxs-lookup"><span data-stu-id="2b519-119">Gets disk object based on the name and the resource group of a disk.</span></span> <span data-ttu-id="2b519-120">傳回物件的 Id 屬性用來將磁碟連結至新的 VM</span><span class="sxs-lookup"><span data-stu-id="2b519-120">Id property of the returned disk object is used to attach the disk to a new VM</span></span> |
| [<span data-ttu-id="2b519-121">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="2b519-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="2b519-122">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="2b519-122">Creates a VM configuration.</span></span> <span data-ttu-id="2b519-123">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="2b519-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="2b519-124">建立 VM 時會使用此組態。</span><span class="sxs-lookup"><span data-stu-id="2b519-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="2b519-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="2b519-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="2b519-126">使用磁碟的 Id 屬性將受控磁碟當作 OS 磁碟連結至新的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2b519-126">Attaches a managed disk using the Id property of the disk as OS disk to a new virtual machine</span></span> |
| [<span data-ttu-id="2b519-127">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="2b519-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="2b519-128">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2b519-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="2b519-129">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="2b519-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="2b519-130">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="2b519-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="2b519-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="2b519-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="2b519-132">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2b519-132">Create a virtual machine.</span></span> |
|[<span data-ttu-id="2b519-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2b519-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="2b519-134">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="2b519-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2b519-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b519-135">Next steps</span></span>

<span data-ttu-id="2b519-136">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="2b519-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2b519-137">您可以在 [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="2b519-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>