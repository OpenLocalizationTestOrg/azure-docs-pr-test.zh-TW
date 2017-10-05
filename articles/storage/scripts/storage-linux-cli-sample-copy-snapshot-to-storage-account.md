---
title: "Azure CLI 指令碼範例 - 將快照集匯出/複製成不同區域儲存體帳戶的 VHD | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 將快照集匯出/複製成相同或不同訂用帳戶之儲存體帳戶的 VHD"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: fafb74af5f02f74036c770934c5e33f1b8a5593e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-to-a-storage-account-in-different-region-with-cli"></a><span data-ttu-id="f65bb-103">使用 CLI 將受管理的快照集匯出/複製到不同區域的儲存體帳戶當做 VHD</span><span class="sxs-lookup"><span data-stu-id="f65bb-103">Export/Copy managed snapshots as VHD to a storage account in different region with CLI</span></span>

<span data-ttu-id="f65bb-104">此指令碼會將受管理的快照集匯出到不同區域的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f65bb-104">This script exports a managed snapshot to a storage account in different region.</span></span> <span data-ttu-id="f65bb-105">它會先產生快照集的 SAS URI，然後用它來將快照集複製到不同區域的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f65bb-105">It first generates the SAS URI of the snapshot and then uses it to copy it to a storage account in different region.</span></span> <span data-ttu-id="f65bb-106">使用此指令碼維護不同區域中受控磁碟的備份，以進行災害復原。</span><span class="sxs-lookup"><span data-stu-id="f65bb-106">Use this script to maintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f65bb-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="f65bb-107">Sample script</span></span>

<span data-ttu-id="f65bb-108">[!code-azurecli[主要](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "複製快照集")]</span><span class="sxs-lookup"><span data-stu-id="f65bb-108">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="f65bb-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="f65bb-109">Script explanation</span></span>

<span data-ttu-id="f65bb-110">此指令碼會使用下列命令來產生受控快照集的 SAS URI，並使用 SAS URI 將快照集複製到儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="f65bb-110">This script uses following commands to generate SAS URI for a managed snapshot and copies the snapshot to a storage account using SAS URI.</span></span> <span data-ttu-id="f65bb-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="f65bb-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="f65bb-112">命令</span><span class="sxs-lookup"><span data-stu-id="f65bb-112">Command</span></span> | <span data-ttu-id="f65bb-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="f65bb-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f65bb-114">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="f65bb-114">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="f65bb-115">產生唯讀 SAS，用來將基礎 VHD 檔案複製到儲存體帳戶，或將它下載到內部部署。</span><span class="sxs-lookup"><span data-stu-id="f65bb-115">Generates read-only SAS that is used to copy underlying VHD file to a storage account or download it to on-premises</span></span>  |
| [<span data-ttu-id="f65bb-116">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="f65bb-116">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="f65bb-117">以非同步方式在儲存體帳戶間複製 blob</span><span class="sxs-lookup"><span data-stu-id="f65bb-117">Copies a blob asynchronously from one storage account to another</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f65bb-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f65bb-118">Next steps</span></span>

[<span data-ttu-id="f65bb-119">從 VHD 建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="f65bb-119">Create a managed disk from a VHD</span></span>](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="f65bb-120">從受控磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="f65bb-120">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="f65bb-121">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f65bb-121">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f65bb-122">您可以在 [Azure Linux VM 文件](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器和受控磁碟 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="f65bb-122">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
