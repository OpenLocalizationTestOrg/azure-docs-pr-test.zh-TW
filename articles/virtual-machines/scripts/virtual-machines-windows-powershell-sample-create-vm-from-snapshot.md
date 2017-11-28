---
title: "Azure PowerShell 指令碼範例 - 從快照集建立 VM | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 從快照集建立 VM"
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
ms.openlocfilehash: 63d108bbfd0f58f8a40bf1c7c8649e3a1f7ed288
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="11110-103">使用 PowerShell 從快照集建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="11110-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="11110-104">此指令碼會從 OS 磁碟的快照集建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="11110-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="11110-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="11110-105">Sample script</span></span>

<span data-ttu-id="11110-106">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "從受控 OS 磁碟建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="11110-106">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="11110-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="11110-107">Clean up deployment</span></span> 

<span data-ttu-id="11110-108">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="11110-108">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="11110-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="11110-109">Script explanation</span></span>

<span data-ttu-id="11110-110">此指令碼會使用下列命令來取得快照集屬性、從快照集建立受控磁碟，以及建立 VM。</span><span class="sxs-lookup"><span data-stu-id="11110-110">This script uses the following commands to get snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="11110-111">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="11110-111">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="11110-112">命令</span><span class="sxs-lookup"><span data-stu-id="11110-112">Command</span></span> | <span data-ttu-id="11110-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="11110-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="11110-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="11110-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="11110-115">使用快照集名稱來取得快照集。</span><span class="sxs-lookup"><span data-stu-id="11110-115">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="11110-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="11110-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="11110-117">建立磁碟組態。</span><span class="sxs-lookup"><span data-stu-id="11110-117">Creates a disk configuration.</span></span> <span data-ttu-id="11110-118">此組態可使用於磁碟建立程序。</span><span class="sxs-lookup"><span data-stu-id="11110-118">This configuration is used with the disk creation process.</span></span> |
| [<span data-ttu-id="11110-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="11110-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="11110-120">建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="11110-120">Creates a managed disk.</span></span> |
| [<span data-ttu-id="11110-121">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="11110-121">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="11110-122">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="11110-122">Creates a VM configuration.</span></span> <span data-ttu-id="11110-123">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="11110-123">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="11110-124">建立 VM 時會使用此組態。</span><span class="sxs-lookup"><span data-stu-id="11110-124">The configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="11110-125">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="11110-125">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="11110-126">將受控磁碟當作 OS 磁碟連結至虛擬機器</span><span class="sxs-lookup"><span data-stu-id="11110-126">Attaches the managed disk as OS disk to the virtual machine</span></span> |
| [<span data-ttu-id="11110-127">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="11110-127">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="11110-128">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="11110-128">Creates a public IP address.</span></span> |
| [<span data-ttu-id="11110-129">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="11110-129">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="11110-130">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="11110-130">Creates a network interface.</span></span> |
| [<span data-ttu-id="11110-131">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="11110-131">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="11110-132">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="11110-132">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="11110-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="11110-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="11110-134">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="11110-134">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="11110-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="11110-135">Next steps</span></span>

<span data-ttu-id="11110-136">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="11110-136">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="11110-137">您可以在 [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="11110-137">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>