---
title: "CLI 指令碼範例-aaaAzure 複製 （移動） 磁碟 toosame 或管理不同訂用帳戶 |Microsoft 文件"
description: "Azure CLI 指令碼範例-複製 （移動） 管理磁碟 toosame 或不同的訂用帳戶"
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="37daa-103">複製 toosame 受管理的磁碟或不同的訂用帳戶使用 CLI</span><span class="sxs-lookup"><span data-stu-id="37daa-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="37daa-104">此指令碼將複製的受管理的磁碟 toosame 或不同的訂用帳戶，但在 hello 相同區域。</span><span class="sxs-lookup"><span data-stu-id="37daa-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="37daa-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="37daa-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="37daa-106">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="37daa-106">Script explanation</span></span>

<span data-ttu-id="37daa-107">此指令碼會使用下列命令 toocreate hello 目標訂用帳戶使用的新受管理的磁碟 hello 識別碼 hello 來源的受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="37daa-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="37daa-108">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="37daa-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="37daa-109">命令</span><span class="sxs-lookup"><span data-stu-id="37daa-109">Command</span></span> | <span data-ttu-id="37daa-110">注意事項</span><span class="sxs-lookup"><span data-stu-id="37daa-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="37daa-111">az disk show</span><span class="sxs-lookup"><span data-stu-id="37daa-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="37daa-112">取得所有受管理的磁碟使用的 hello 受管理磁碟 hello 名稱和資源群組屬性 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="37daa-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="37daa-113">Id 屬性是使用的 toocopy hello 管理磁碟 toodifferent 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="37daa-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="37daa-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="37daa-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="37daa-115">將受管理的磁碟複製藉由使用識別碼和名稱的不同訂用帳戶中建立新的受管理的磁碟 hello 父管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="37daa-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="37daa-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37daa-116">Next steps</span></span>

[<span data-ttu-id="37daa-117">從受控磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="37daa-117">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="37daa-118">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="37daa-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="37daa-119">其他虛擬機器和受管理的磁碟 CLI 指令碼範例可以在 hello [Azure Linux VM 文件](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="37daa-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
