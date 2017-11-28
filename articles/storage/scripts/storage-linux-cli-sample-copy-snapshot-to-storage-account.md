---
title: "CLI 指令碼範例做為不同的區域中的 VHD tooa 儲存體帳戶匯出/複製快照集 aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例-匯出/複製快照集，與相同或不同的訂用帳戶中的 VHD tooa 儲存體帳戶"
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
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a><span data-ttu-id="ae0ad-103">匯出/受管理的快照集以複製 VHD tooa 儲存體帳戶中不同的區域與 CLI</span><span class="sxs-lookup"><span data-stu-id="ae0ad-103">Export/Copy managed snapshots as VHD tooa storage account in different region with CLI</span></span>

<span data-ttu-id="ae0ad-104">此指令碼匯出不同的區域中的受管理的快照集 tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae0ad-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="ae0ad-105">它第一次會產生 hello hello 快照集的 SAS URI，然後使用它 toocopy 它 tooa 不同地區中的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae0ad-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="ae0ad-106">此指令碼 toomaintain 中使用備份的受管理的磁碟不同地區的災害復原。</span><span class="sxs-lookup"><span data-stu-id="ae0ad-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ae0ad-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="ae0ad-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="ae0ad-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="ae0ad-108">Script explanation</span></span>

<span data-ttu-id="ae0ad-109">此指令碼，會使用下列命令 toogenerate managed 快照和複本 hello 的 SAS URI 的快照集使用 SAS URI tooa 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="ae0ad-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="ae0ad-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="ae0ad-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ae0ad-111">命令</span><span class="sxs-lookup"><span data-stu-id="ae0ad-111">Command</span></span> | <span data-ttu-id="ae0ad-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="ae0ad-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ae0ad-113">az snapshot grant-access</span><span class="sxs-lookup"><span data-stu-id="ae0ad-113">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="ae0ad-114">產生已使用的 toocopy 基礎 VHD 檔案 tooa 儲存體帳戶，或下載它的唯讀 SAS tooon 內部部署</span><span class="sxs-lookup"><span data-stu-id="ae0ad-114">Generates read-only SAS that is used toocopy underlying VHD file tooa storage account or download it tooon-premises</span></span>  |
| [<span data-ttu-id="ae0ad-115">az storage blob copy start</span><span class="sxs-lookup"><span data-stu-id="ae0ad-115">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="ae0ad-116">以非同步方式將 blob 複製從一個儲存體帳戶 tooanother</span><span class="sxs-lookup"><span data-stu-id="ae0ad-116">Copies a blob asynchronously from one storage account tooanother</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ae0ad-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ae0ad-117">Next steps</span></span>

[<span data-ttu-id="ae0ad-118">從 VHD 建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="ae0ad-118">Create a managed disk from a VHD</span></span>](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="ae0ad-119">從受控磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ae0ad-119">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="ae0ad-120">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ae0ad-120">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ae0ad-121">其他虛擬機器和受管理的磁碟 CLI 指令碼範例可以在 hello [Azure Linux VM 文件](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ae0ad-121">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
