---
title: "PowerShell 指令碼範例做為不同的區域中的 VHD tooa 儲存體帳戶匯出/複製快照集 aaaAzure |Microsoft 文件"
description: "Azure PowerShell 指令碼範例做為相同的不同區域中的 VHD tooa 儲存體帳戶匯出/複製快照集"
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
ms.openlocfilehash: 3b3e38c6b06bfa1e117f4e913dfc09443a795196
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="e9fcb-103">匯出/受管理的快照集以複製 VHD tooa 儲存體帳戶中不同的區域，使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="e9fcb-103">Export/Copy managed snapshots as VHD tooa storage account in different region with PowerShell</span></span>

<span data-ttu-id="e9fcb-104">此指令碼匯出不同的區域中的受管理的快照集 tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9fcb-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="e9fcb-105">它第一次會產生 hello hello 快照集的 SAS URI，然後使用它 toocopy 它 tooa 不同地區中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9fcb-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="e9fcb-106">此指令碼 toomaintain 中使用備份的受管理的磁碟不同地區的災害復原。</span><span class="sxs-lookup"><span data-stu-id="e9fcb-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e9fcb-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e9fcb-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="e9fcb-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e9fcb-108">Script explanation</span></span>

<span data-ttu-id="e9fcb-109">此指令碼，會使用下列命令 toogenerate managed 快照和複本 hello 的 SAS URI 的快照集使用 SAS URI tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9fcb-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="e9fcb-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="e9fcb-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e9fcb-111">命令</span><span class="sxs-lookup"><span data-stu-id="e9fcb-111">Command</span></span> | <span data-ttu-id="e9fcb-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="e9fcb-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e9fcb-113">Grant-AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="e9fcb-113">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="e9fcb-114">產生的快照，不使用的 toocopy SAS URI 它 tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="e9fcb-114">Generates SAS URI for a snapshot that is used toocopy it tooa storage account.</span></span> |
| [<span data-ttu-id="e9fcb-115">New-AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="e9fcb-115">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="e9fcb-116">建立使用 hello 帳戶名稱和金鑰的儲存體帳戶內容。</span><span class="sxs-lookup"><span data-stu-id="e9fcb-116">Creates a storage account context using hello account name and key.</span></span> <span data-ttu-id="e9fcb-117">這個內容可以是使用的 tooperform hello 儲存體帳戶上的讀取/寫入作業。</span><span class="sxs-lookup"><span data-stu-id="e9fcb-117">This context can be used tooperform read/write operations on hello storage account.</span></span> |
| [<span data-ttu-id="e9fcb-118">Start-AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="e9fcb-118">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="e9fcb-119">複製 hello 基礎 VHD 的快照集 tooa 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="e9fcb-119">Copies hello underlying VHD of a snapshot tooa storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e9fcb-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9fcb-120">Next steps</span></span>

[<span data-ttu-id="e9fcb-121">從 VHD 建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="e9fcb-121">Create a managed disk from a VHD</span></span>](./../scripts/storage-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="e9fcb-122">從受控磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e9fcb-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="e9fcb-123">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e9fcb-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e9fcb-124">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e9fcb-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
