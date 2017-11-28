---
title: "Azure PowerShell 指令碼範例 - 從快照集建立受控磁碟 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 從快照集建立受控磁碟"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 9105d9dc06eea33b3a4e1eeea7fd793919166c9b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="c46d0-103">使用 PowerShell 從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="c46d0-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="c46d0-104">此指令碼會從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="c46d0-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="c46d0-105">使用它從 OS 和資料磁碟的快照集還原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c46d0-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="c46d0-106">從個別的快照集建立 OS 和資料受控磁碟，再連結受控磁碟以建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c46d0-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="c46d0-107">您也可以連結從快照集建立的資料磁碟，以還原現有 VM 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="c46d0-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c46d0-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c46d0-108">Sample script</span></span>

<span data-ttu-id="c46d0-109">[!code-powershell[主要](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "從快照集建立受控磁碟")]</span><span class="sxs-lookup"><span data-stu-id="c46d0-109">[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="c46d0-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c46d0-110">Script explanation</span></span>

<span data-ttu-id="c46d0-111">此指令碼使用下列命令從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="c46d0-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="c46d0-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="c46d0-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="c46d0-113">命令</span><span class="sxs-lookup"><span data-stu-id="c46d0-113">Command</span></span> | <span data-ttu-id="c46d0-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="c46d0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c46d0-115">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="c46d0-115">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="c46d0-116">取得快照集屬性。</span><span class="sxs-lookup"><span data-stu-id="c46d0-116">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="c46d0-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="c46d0-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="c46d0-118">建立用於磁碟建立的磁碟組態。</span><span class="sxs-lookup"><span data-stu-id="c46d0-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="c46d0-119">其中包含父代快照集的資源識別碼、與父代快照集位置相同的位置和儲存體類型。</span><span class="sxs-lookup"><span data-stu-id="c46d0-119">It includes the resource Id of the parent snapshot, location that is same as the location of parent snapshot and the storage type.</span></span>  |
| [<span data-ttu-id="c46d0-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="c46d0-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="c46d0-121">使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="c46d0-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="c46d0-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c46d0-122">Next steps</span></span>

[<span data-ttu-id="c46d0-123">從受控磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="c46d0-123">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="c46d0-124">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c46d0-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="c46d0-125">您可以在 [Azure Windows VM 文件](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="c46d0-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>