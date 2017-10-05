---
title: "Azure PowerShell 指令碼範例 - 將快照集匯出/複製成不同區域的儲存體帳戶當做 VHD | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 將快照集匯出/複製成不同區域的儲存體帳戶當做 VHD"
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
ms.openlocfilehash: a6bd0686842282ccd7ce0c31bb0152beb30bea66
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="4ce5f-103">使用 PowerShell 將受控快照集匯出/複製到不同區域的儲存體帳戶當做 VHD</span><span class="sxs-lookup"><span data-stu-id="4ce5f-103">Export/Copy managed snapshots as VHD to a storage account in different region with PowerShell</span></span>

<span data-ttu-id="4ce5f-104">此指令碼會將受控快照集匯出到不同區域的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ce5f-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="4ce5f-105">它會先產生快照集的 SAS URI，然後用它來將快照集複製到不同區域的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ce5f-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="4ce5f-106">使用此指令碼維護不同區域中受控磁碟的備份，以進行災害復原。</span><span class="sxs-lookup"><span data-stu-id="4ce5f-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4ce5f-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="4ce5f-107">Sample script</span></span>

<span data-ttu-id="4ce5f-108">[!code-powershell[主要](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "複製快照集")]</span><span class="sxs-lookup"><span data-stu-id="4ce5f-108">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="4ce5f-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="4ce5f-109">Script explanation</span></span>

<span data-ttu-id="4ce5f-110">此指令碼會使用下列命令來產生受控快照集的 SAS URI，並使用 SAS URI 將快照集複製到儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ce5f-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="4ce5f-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="4ce5f-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4ce5f-112">命令</span><span class="sxs-lookup"><span data-stu-id="4ce5f-112">Command</span></span> | <span data-ttu-id="4ce5f-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="4ce5f-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4ce5f-114">Grant-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="4ce5f-114">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="4ce5f-115">產生快照集的 SAS URI 並用它來將快照集複製到儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="4ce5f-115">Generates SAS URI for a snapshot that is used to copy it to a storage account.</span></span> |
| [<span data-ttu-id="4ce5f-116">New-AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="4ce5f-116">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="4ce5f-117">使用帳戶名稱與金鑰建立儲存體帳戶內容。</span><span class="sxs-lookup"><span data-stu-id="4ce5f-117">Creates a storage account context using the account name and key.</span></span> <span data-ttu-id="4ce5f-118">此內容可用來對儲存體帳戶執行讀取/寫入作業。</span><span class="sxs-lookup"><span data-stu-id="4ce5f-118">This context can be used to perform read/write operations on the storage account.</span></span> |
| [<span data-ttu-id="4ce5f-119">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="4ce5f-119">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="4ce5f-120">將快照集的底層 VHD 複製到儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="4ce5f-120">Copies the underlying VHD of a snapshot to a storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4ce5f-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ce5f-121">Next steps</span></span>

[<span data-ttu-id="4ce5f-122">從 VHD 建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="4ce5f-122">Create a managed disk from a VHD</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="4ce5f-123">從受控磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4ce5f-123">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="4ce5f-124">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4ce5f-124">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4ce5f-125">您可以在 [Azure Windows VM 文件](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="4ce5f-125">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>