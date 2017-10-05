---
title: "Azure PowerShell 指令碼範例 - 從 VHD 建立快照集以在短時間內建立多個相同的受控磁碟 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 從 VHD 建立快照集以在短時間內建立多個相同的受控磁碟"
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
ms.openlocfilehash: 02a69abd6c17ce765996379309e22afad82c4e10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-snapshot-from-a-vhd-to-create-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="b6ebe-103">使用 PowerShell 從 VHD 建立快照集以在短時間內建立多個相同的受控磁碟</span><span class="sxs-lookup"><span data-stu-id="b6ebe-103">Create a snapshot from a VHD to create multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="b6ebe-104">此指令碼會從相同或不同訂用帳戶的儲存體帳戶中的 VHD 檔案，建立快照集。</span><span class="sxs-lookup"><span data-stu-id="b6ebe-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="b6ebe-105">使用此指令碼將特製化 (非一般化/已執行過 sysprep) VHD 匯入到快照集，然後使用快照集在短時間內建立多個相同的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="b6ebe-105">Use this script to import a specialized (not generalized/sysprepped) VHD to a snapshot and then use the snapshot to create multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="b6ebe-106">此外，使用它將資料 VHD 匯入到快照集，然後使用快照集在短時間內建立多個受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="b6ebe-106">Also, use it to import a data VHD to a snapshot and then use the snapshot to create multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b6ebe-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b6ebe-107">Sample script</span></span>

<span data-ttu-id="b6ebe-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "從 VHD 建立快照集")]</span><span class="sxs-lookup"><span data-stu-id="b6ebe-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="b6ebe-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b6ebe-109">Script explanation</span></span>

<span data-ttu-id="b6ebe-110">此指令碼使用下列命令從不同訂用帳戶的 VHD 建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="b6ebe-110">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="b6ebe-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="b6ebe-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b6ebe-112">命令</span><span class="sxs-lookup"><span data-stu-id="b6ebe-112">Command</span></span> | <span data-ttu-id="b6ebe-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="b6ebe-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b6ebe-114">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="b6ebe-114">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="b6ebe-115">建立用於磁碟建立的磁碟組態。</span><span class="sxs-lookup"><span data-stu-id="b6ebe-115">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="b6ebe-116">其中包含儲存體類型、位置、儲存父代 VHD 之儲存體帳戶的資源識別碼，以及父代 VHD 的 VHD URI。</span><span class="sxs-lookup"><span data-stu-id="b6ebe-116">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, and VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="b6ebe-117">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="b6ebe-117">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="b6ebe-118">使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="b6ebe-118">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b6ebe-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b6ebe-119">Next steps</span></span>

[<span data-ttu-id="b6ebe-120">從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="b6ebe-120">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="b6ebe-121">將受控磁碟連結為 OS 磁碟以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="b6ebe-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="b6ebe-122">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b6ebe-122">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="b6ebe-123">您可以在 [Azure Windows VM 文件](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="b6ebe-123">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>