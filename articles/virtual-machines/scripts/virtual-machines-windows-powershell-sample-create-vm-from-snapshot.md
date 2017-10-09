---
title: "aaaAzure PowerShell 指令碼範例-從快照集建立的 VM |Microsoft 文件"
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
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="e73d6-103">使用 PowerShell 從快照集建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e73d6-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="e73d6-104">此指令碼會從 OS 磁碟的快照集建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e73d6-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e73d6-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e73d6-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e73d6-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="e73d6-106">Clean up deployment</span></span> 

<span data-ttu-id="e73d6-107">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="e73d6-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e73d6-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e73d6-108">Script explanation</span></span>

<span data-ttu-id="e73d6-109">此指令碼會使用下列命令 tooget 快照集屬性，從快照集建立受管理的磁碟，並建立 VM 的 hello。</span><span class="sxs-lookup"><span data-stu-id="e73d6-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="e73d6-110">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="e73d6-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e73d6-111">命令</span><span class="sxs-lookup"><span data-stu-id="e73d6-111">Command</span></span> | <span data-ttu-id="e73d6-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="e73d6-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e73d6-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="e73d6-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="e73d6-114">使用快照集名稱來取得快照集。</span><span class="sxs-lookup"><span data-stu-id="e73d6-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="e73d6-115">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="e73d6-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="e73d6-116">建立磁碟組態。</span><span class="sxs-lookup"><span data-stu-id="e73d6-116">Creates a disk configuration.</span></span> <span data-ttu-id="e73d6-117">此設定可搭配 hello 磁碟建立程序。</span><span class="sxs-lookup"><span data-stu-id="e73d6-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="e73d6-118">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="e73d6-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="e73d6-119">建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="e73d6-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="e73d6-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="e73d6-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="e73d6-121">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="e73d6-121">Creates a VM configuration.</span></span> <span data-ttu-id="e73d6-122">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="e73d6-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="e73d6-123">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="e73d6-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="e73d6-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="e73d6-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="e73d6-125">附加 hello 受管理的磁碟做為作業系統磁碟 toohello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e73d6-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="e73d6-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="e73d6-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="e73d6-127">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e73d6-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="e73d6-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="e73d6-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="e73d6-129">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="e73d6-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="e73d6-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="e73d6-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="e73d6-131">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e73d6-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="e73d6-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e73d6-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e73d6-133">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="e73d6-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e73d6-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e73d6-134">Next steps</span></span>

<span data-ttu-id="e73d6-135">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e73d6-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e73d6-136">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e73d6-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
