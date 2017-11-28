---
title: "aaaAzure PowerShell 指令碼範例為建立快照集 VHD toocreate 從多個受管理的相同磁碟在短時間內 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-建立快照集 VHD toocreate 從多個受管理的相同磁碟在短時間內"
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
ms.openlocfilehash: 0a13e399b692f32b3772add39fe5b5c023808c5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="14cb7-103">建立快照集 VHD toocreate 從多個受管理的相同磁碟小型一段時間內使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="14cb7-103">Create a snapshot from a VHD toocreate multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="14cb7-104">此指令碼會從相同或不同訂用帳戶的儲存體帳戶中的 VHD 檔案，建立快照集。</span><span class="sxs-lookup"><span data-stu-id="14cb7-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="14cb7-105">使用此指令碼 tooimport 特製化 (無法一般化/執行過 sysprep) VHD tooa 快照集，然後再使用多個受管理的相同磁碟 hello 快照 toocreate 在短時間內。</span><span class="sxs-lookup"><span data-stu-id="14cb7-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD tooa snapshot and then use hello snapshot toocreate multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="14cb7-106">此外，使用 tooimport 資料 VHD tooa 快照集，然後再使用多個受管理的磁碟 hello 快照 toocreate 在短時間內。</span><span class="sxs-lookup"><span data-stu-id="14cb7-106">Also, use it tooimport a data VHD tooa snapshot and then use hello snapshot toocreate multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="14cb7-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="14cb7-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="14cb7-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="14cb7-108">Script explanation</span></span>

<span data-ttu-id="14cb7-109">此指令碼會使用下列命令 toocreate 受管理的磁碟從不同的訂用帳戶中的 VHD。</span><span class="sxs-lookup"><span data-stu-id="14cb7-109">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="14cb7-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="14cb7-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="14cb7-111">命令</span><span class="sxs-lookup"><span data-stu-id="14cb7-111">Command</span></span> | <span data-ttu-id="14cb7-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="14cb7-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="14cb7-113">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="14cb7-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="14cb7-114">建立用於磁碟建立的磁碟組態。</span><span class="sxs-lookup"><span data-stu-id="14cb7-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="14cb7-115">它包含存放裝置類型、 位置、 hello hello 父 VHD 的儲存位置的儲存體帳戶的資源 Id 和 hello 父系 VHD 的 VHD URI。</span><span class="sxs-lookup"><span data-stu-id="14cb7-115">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, and VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="14cb7-116">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="14cb7-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="14cb7-117">使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="14cb7-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="14cb7-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="14cb7-118">Next steps</span></span>

[<span data-ttu-id="14cb7-119">從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="14cb7-119">Create a managed disk from snapshot</span></span>](./../../storage/scripts/storage-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="14cb7-120">將受控磁碟連結為 OS 磁碟以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="14cb7-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="14cb7-121">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="14cb7-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="14cb7-122">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="14cb7-122">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
