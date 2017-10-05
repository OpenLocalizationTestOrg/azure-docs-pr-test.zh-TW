---
title: "Azure PowerShell 指令碼範例 - 從相同或不同訂用帳戶的儲存體帳戶的 VHD 檔案建立受控磁碟 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 從相同或不同訂用帳戶的儲存體帳戶的 VHD 檔案建立受控磁碟"
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
ms.openlocfilehash: b9c3d2e8dbf5caa525f82955aceb615cb1c28e93
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="0b678-103">使用 PowerShell 從相同或不同訂用帳戶的儲存體帳戶的 VHD 檔案建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="0b678-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="0b678-104">此指令碼會從相同或不同訂用帳戶的儲存體帳戶中的 VHD 檔案，建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="0b678-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="0b678-105">使用此指令碼可將專用 (非一般化/已執行過 Sysprep) 的 VHD 匯入至受控 OS 磁碟，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0b678-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="0b678-106">同時，用它將資料 VHD 匯入到受控資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="0b678-106">Also, use it to import a data VHD to managed data disk.</span></span> 

<span data-ttu-id="0b678-107">請勿在短時間內從 VHD 檔案建立多個相同的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="0b678-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="0b678-108">若要從 VHD 檔案建立受控磁碟，會建立 VHD 檔案的 Blob 快照集，然後將它用於建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="0b678-108">To create managed disks from a vhd file, blob snapshot of the vhd file is created and then it is used to create managed disks.</span></span> <span data-ttu-id="0b678-109">一分鐘內只能建立一個 Blob 快照集，這會導致磁碟建立因節流而失敗。</span><span class="sxs-lookup"><span data-stu-id="0b678-109">Only one blob snapshot can be created in a minute that causes disk creation failures due to throttling.</span></span> <span data-ttu-id="0b678-110">若要避免進行此節流，請[從 VHD 檔案建立受控快照集](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)，然後使用受控快照集在短時間內建立多個受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="0b678-110">To avoid this throttling, create a [managed snapshot from the vhd file](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use the managed snapshot to create multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="0b678-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="0b678-111">Sample script</span></span>

<span data-ttu-id="0b678-112">[!code-powershell[主要](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "從 VHD 建立受控磁碟")]</span><span class="sxs-lookup"><span data-stu-id="0b678-112">[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="0b678-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="0b678-113">Script explanation</span></span>

<span data-ttu-id="0b678-114">此指令碼使用下列命令從不同訂用帳戶的 VHD 建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="0b678-114">This script uses following commands to create a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="0b678-115">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="0b678-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0b678-116">命令</span><span class="sxs-lookup"><span data-stu-id="0b678-116">Command</span></span> | <span data-ttu-id="0b678-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="0b678-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0b678-118">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="0b678-118">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="0b678-119">建立用於磁碟建立的磁碟組態。</span><span class="sxs-lookup"><span data-stu-id="0b678-119">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="0b678-120">它包含儲存體類型、位置、儲存父 VHD 所在儲存體帳戶的資源識別碼、父 VHD 的 VHD URI。</span><span class="sxs-lookup"><span data-stu-id="0b678-120">It includes storage type, location, resource Id of the storage account where the parent VHD is stored, VHD URI of the parent VHD.</span></span> |
| [<span data-ttu-id="0b678-121">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="0b678-121">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="0b678-122">使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="0b678-122">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0b678-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0b678-123">Next steps</span></span>

[<span data-ttu-id="0b678-124">將受控磁碟連結為 OS 磁碟以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="0b678-124">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="0b678-125">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0b678-125">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="0b678-126">您可以在 [Azure Windows VM 文件](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="0b678-126">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>