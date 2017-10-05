---
title: "Azure CLI 指令碼範例 - 從快照集建立受控磁碟 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 從快照集建立受控磁碟"
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
ms.openlocfilehash: 68e17ae9e5d82da7f9be9d36e3e2324a2aeadbc4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="a8dd6-103">使用 CLI 從快照集建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="a8dd6-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="a8dd6-104">此指令碼會從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a8dd6-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="a8dd6-105">使用它從 OS 和資料磁碟的快照集還原虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a8dd6-105">Use it to restore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="a8dd6-106">從個別的快照集建立 OS 和資料受控磁碟，再連結受控磁碟以建立新的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a8dd6-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="a8dd6-107">您也可以連結從快照集建立的資料磁碟，以還原現有 VM 的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="a8dd6-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a8dd6-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="a8dd6-108">Sample script</span></span>

<span data-ttu-id="a8dd6-109">[!code-azurecli[主要](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "從快照集建立受控磁碟")]</span><span class="sxs-lookup"><span data-stu-id="a8dd6-109">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="a8dd6-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="a8dd6-110">Script explanation</span></span>

<span data-ttu-id="a8dd6-111">此指令碼使用下列命令從快照集建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a8dd6-111">This script uses following commands to create a managed disk from a snapshot.</span></span> <span data-ttu-id="a8dd6-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="a8dd6-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a8dd6-113">命令</span><span class="sxs-lookup"><span data-stu-id="a8dd6-113">Command</span></span> | <span data-ttu-id="a8dd6-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="a8dd6-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a8dd6-115">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="a8dd6-115">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="a8dd6-116">使用快照集的名稱和資源群組屬性，取得快照集的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="a8dd6-116">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="a8dd6-117">使用 Id 屬性建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="a8dd6-117">Id property is used to create managed disk.</span></span>  |
| [<span data-ttu-id="a8dd6-118">az disk create</span><span class="sxs-lookup"><span data-stu-id="a8dd6-118">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="a8dd6-119">使用受管理快照集的快照集識別碼建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="a8dd6-119">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a8dd6-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8dd6-120">Next steps</span></span>

[<span data-ttu-id="a8dd6-121">將受控磁碟連結為作業系統磁碟以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a8dd6-121">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="a8dd6-122">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a8dd6-122">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a8dd6-123">您可以在 [Azure Linux VM 文件](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器和受控磁碟 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="a8dd6-123">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
