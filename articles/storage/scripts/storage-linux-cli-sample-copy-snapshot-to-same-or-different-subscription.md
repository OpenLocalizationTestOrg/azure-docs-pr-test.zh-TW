---
title: "Azure CLI 指令碼範例 - 使用 CLI 將受控磁碟快照集複製 (移動) 到相同或不同的訂用帳戶 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 使用 CLI 將受控磁碟快照集複製 (移動) 到相同或不同的訂用帳戶"
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
ms.openlocfilehash: 0127e342bd0c3afbe9de775399f5510814bff499
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="ecedf-103">使用 CLI將受控磁碟快照集複製到相同或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="ecedf-103">Copy snapshot of a managed disk to same or different subscription with CLI</span></span>

<span data-ttu-id="ecedf-104">此指令碼會將受控磁碟的快照集複製到相同或不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ecedf-104">This script copies a snapshot of a managed disk to same or different subscription.</span></span> <span data-ttu-id="ecedf-105">使用這個指令碼可將快照集移至與父快照集同區域但不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ecedf-105">Use this script to move a snapshot to different subscription in the same region as the parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ecedf-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="ecedf-106">Sample script</span></span>

<span data-ttu-id="ecedf-107">[!code-azurecli[主要](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "複製快照集")]</span><span class="sxs-lookup"><span data-stu-id="ecedf-107">[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="ecedf-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="ecedf-108">Script explanation</span></span>

<span data-ttu-id="ecedf-109">此指令碼會使用下列命令，使用來源快照集的識別碼在目標訂用帳戶中建立快照集。</span><span class="sxs-lookup"><span data-stu-id="ecedf-109">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="ecedf-110">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="ecedf-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="ecedf-111">命令</span><span class="sxs-lookup"><span data-stu-id="ecedf-111">Command</span></span> | <span data-ttu-id="ecedf-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="ecedf-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ecedf-113">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="ecedf-113">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="ecedf-114">使用快照集的名稱和資源群組屬性，取得快照集的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="ecedf-114">Gets all the properties of a snapshot using the name and resource group properties of the snapshot.</span></span> <span data-ttu-id="ecedf-115">使用 Id 屬性將快照集複製到不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="ecedf-115">Id property is used to copy the snapshot to different subscription.</span></span>  |
| [<span data-ttu-id="ecedf-116">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="ecedf-116">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="ecedf-117">在使用父快照集識別碼和名稱的不同訂用帳戶中建立快照集，以複製快照集。</span><span class="sxs-lookup"><span data-stu-id="ecedf-117">Copies a snapshot by creating a snapshot in different subscription using the Id and name of the parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="ecedf-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ecedf-118">Next steps</span></span>

[<span data-ttu-id="ecedf-119">從快照集建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="ecedf-119">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="ecedf-120">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="ecedf-120">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="ecedf-121">您可以在 [Azure Linux VM 文件](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器和受控磁碟 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="ecedf-121">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
