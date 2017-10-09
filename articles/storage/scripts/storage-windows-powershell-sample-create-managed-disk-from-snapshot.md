---
title: "aaaAzure PowerShell 指令碼範例-從快照集建立受管理的磁碟 |Microsoft 文件"
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
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="e3218-103">使用 PowerShell 從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="e3218-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="e3218-104">此指令碼會從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="e3218-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="e3218-105">使用 toorestore OS 和資料磁碟的快照中的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e3218-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="e3218-106">從個別的快照集建立 OS 和資料受控磁碟，再連結受控磁碟以建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e3218-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="e3218-107">您也可以連結從快照集建立的資料磁碟，以還原現有 VM 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="e3218-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e3218-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e3218-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="e3218-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e3218-109">Script explanation</span></span>

<span data-ttu-id="e3218-110">此指令碼會使用下列命令 toocreate 受管理的磁碟，從快照集。</span><span class="sxs-lookup"><span data-stu-id="e3218-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="e3218-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="e3218-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e3218-112">命令</span><span class="sxs-lookup"><span data-stu-id="e3218-112">Command</span></span> | <span data-ttu-id="e3218-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="e3218-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e3218-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="e3218-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="e3218-115">取得快照集屬性。</span><span class="sxs-lookup"><span data-stu-id="e3218-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="e3218-116">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="e3218-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="e3218-117">建立用於磁碟建立的磁碟組態。</span><span class="sxs-lookup"><span data-stu-id="e3218-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="e3218-118">它包含 hello 的資源 Id hello 父快照集，做為父快照式和 hello 儲存體類型 hello 位置相同的位置。</span><span class="sxs-lookup"><span data-stu-id="e3218-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="e3218-119">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="e3218-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="e3218-120">使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="e3218-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="e3218-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e3218-121">Next steps</span></span>

[<span data-ttu-id="e3218-122">從受控磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e3218-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="e3218-123">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e3218-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e3218-124">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e3218-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
