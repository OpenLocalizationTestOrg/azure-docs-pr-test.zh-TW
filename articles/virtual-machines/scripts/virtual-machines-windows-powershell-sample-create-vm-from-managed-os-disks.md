---
title: "aaaAzure PowerShell 指令碼範例-建立 VM，藉由附加為作業系統磁碟的受管理的磁碟 |Microsoft 文件"
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
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="0ac4b-103">使用現有受控 OS 磁碟搭配 PowerShell 以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0ac4b-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="0ac4b-104">此指令碼會連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="0ac4b-105">在先前案例中使用此指令碼︰</span><span class="sxs-lookup"><span data-stu-id="0ac4b-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="0ac4b-106">從不同訂用帳戶中的受控磁碟複製而來的現有受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="0ac4b-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="0ac4b-107">從特殊化 VHD 檔案建立的現有受控磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="0ac4b-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="0ac4b-108">從快照集建立的現有受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="0ac4b-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0ac4b-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="0ac4b-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="0ac4b-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="0ac4b-110">Clean up deployment</span></span> 

<span data-ttu-id="0ac4b-111">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="0ac4b-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="0ac4b-112">Script explanation</span></span>

<span data-ttu-id="0ac4b-113">此指令碼會使用下列命令 tooget 管理磁碟屬性中的 hello、 附加受管理的磁碟 tooa 新的 VM，並建立 VM。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="0ac4b-114">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="0ac4b-115">命令</span><span class="sxs-lookup"><span data-stu-id="0ac4b-115">Command</span></span> | <span data-ttu-id="0ac4b-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="0ac4b-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0ac4b-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="0ac4b-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="0ac4b-118">取得根據 hello 名稱和 hello 資源群組的磁碟的磁碟物件。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="0ac4b-119">Hello id 屬性會傳回磁碟物件是使用的 tooattach hello 磁碟 tooa 新的 VM</span><span class="sxs-lookup"><span data-stu-id="0ac4b-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="0ac4b-120">New-AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="0ac4b-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="0ac4b-121">建立 VM 組態。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-121">Creates a VM configuration.</span></span> <span data-ttu-id="0ac4b-122">此組態包括 VM 名稱、作業系統和系統管理認證等資訊。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="0ac4b-123">在建立 VM 時，會使用 hello 組態。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="0ac4b-124">Set-AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="0ac4b-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="0ac4b-125">附加的受管理的磁碟，做為作業系統磁碟 tooa 新虛擬機器使用 hello 磁碟 hello Id 屬性</span><span class="sxs-lookup"><span data-stu-id="0ac4b-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="0ac4b-126">New-AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="0ac4b-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="0ac4b-127">建立公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="0ac4b-128">New-AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="0ac4b-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="0ac4b-129">建立網路介面。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="0ac4b-130">New-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="0ac4b-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="0ac4b-131">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="0ac4b-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="0ac4b-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="0ac4b-133">移除資源群組及其內含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0ac4b-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ac4b-134">Next steps</span></span>

<span data-ttu-id="0ac4b-135">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0ac4b-136">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0ac4b-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
