---
title: "CLI 指令碼範例複製 （移動） 快照集的受管理的磁碟 toosame 或不同的訂用帳戶使用 CLI aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例-受管理的磁碟 toosame 或不同的訂用帳戶使用 CLI 的複本 （移動） 快照集"
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
ms.openlocfilehash: f214ab1fc1cb2cb42479d82e455f20a8cc55c83d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="152bc-103">受管理的磁碟 toosame 或不同的訂用帳戶使用 CLI 的快照集複製</span><span class="sxs-lookup"><span data-stu-id="152bc-103">Copy snapshot of a managed disk toosame or different subscription with CLI</span></span>

<span data-ttu-id="152bc-104">此指令碼將複製的受管理的磁碟 toosame 或不同的訂用帳戶的快照集。</span><span class="sxs-lookup"><span data-stu-id="152bc-104">This script copies a snapshot of a managed disk toosame or different subscription.</span></span> <span data-ttu-id="152bc-105">使用此指令碼 toomove 快照式 toodifferent 訂閱 hello 與 hello 父快照集相同的區域。</span><span class="sxs-lookup"><span data-stu-id="152bc-105">Use this script toomove a snapshot toodifferent subscription in hello same region as hello parent snapshot.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="152bc-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="152bc-106">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="152bc-107">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="152bc-107">Script explanation</span></span>

<span data-ttu-id="152bc-108">此指令碼，會使用下列命令 toocreate hello 目標訂用帳戶的使用中的快照集 hello hello 來源快照集的識別碼。</span><span class="sxs-lookup"><span data-stu-id="152bc-108">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="152bc-109">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="152bc-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="152bc-110">命令</span><span class="sxs-lookup"><span data-stu-id="152bc-110">Command</span></span> | <span data-ttu-id="152bc-111">注意事項</span><span class="sxs-lookup"><span data-stu-id="152bc-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="152bc-112">az snapshot show</span><span class="sxs-lookup"><span data-stu-id="152bc-112">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="152bc-113">取得所有快照集使用 hello 名稱 hello 內容和 hello 快照集的資源群組屬性。</span><span class="sxs-lookup"><span data-stu-id="152bc-113">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="152bc-114">Id 屬性是使用的 toocopy hello 快照 toodifferent 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="152bc-114">Id property is used toocopy hello snapshot toodifferent subscription.</span></span>  |
| [<span data-ttu-id="152bc-115">az snapshot create</span><span class="sxs-lookup"><span data-stu-id="152bc-115">az snapshot create</span></span>](https://docs.microsoft.com/cli/azure/snapshot#create) | <span data-ttu-id="152bc-116">複製識別碼和名稱，藉由使用不同訂用帳戶中建立快照集的快照集 hello hello 父快照集。</span><span class="sxs-lookup"><span data-stu-id="152bc-116">Copies a snapshot by creating a snapshot in different subscription using hello Id and name of hello parent snapshot.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="152bc-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="152bc-117">Next steps</span></span>

[<span data-ttu-id="152bc-118">從快照集建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="152bc-118">Create a virtual machine from a snapshot</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="152bc-119">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="152bc-119">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="152bc-120">其他虛擬機器和受管理的磁碟 CLI 指令碼範例可以在 hello [Azure Linux VM 文件](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="152bc-120">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
