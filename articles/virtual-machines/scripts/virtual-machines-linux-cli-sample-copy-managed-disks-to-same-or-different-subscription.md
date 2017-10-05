---
title: "Azure CLI 指令碼範例 - 將受控磁碟複製 (移動) 到相同或不同的訂用帳戶 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 將受控磁碟複製 (移動) 到相同或不同的訂用帳戶"
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
ms.openlocfilehash: dcf92babf84872ffbbba81127952f8422104c723
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="copy-managed-disks-to-same-or-different-subscription-with-cli"></a><span data-ttu-id="bde72-103">使用 CLI將受控磁碟複製到相同或不同的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="bde72-103">Copy managed disks to same or different subscription with CLI</span></span>

<span data-ttu-id="bde72-104">此指令碼會將受控磁碟複製到相同的訂用帳戶，或同區域的不同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bde72-104">This script copies a managed disk to same or different subscription but in the same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bde72-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="bde72-105">Sample script</span></span>

<span data-ttu-id="bde72-106">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "複製受控磁碟")]</span><span class="sxs-lookup"><span data-stu-id="bde72-106">[!code-azurecli[main](../../../cli_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="bde72-107">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="bde72-107">Script explanation</span></span>

<span data-ttu-id="bde72-108">此指令碼會使用下列命令，在使用來源受控磁碟識別碼的目標訂用帳戶中，建立新的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="bde72-108">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="bde72-109">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="bde72-109">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bde72-110">命令</span><span class="sxs-lookup"><span data-stu-id="bde72-110">Command</span></span> | <span data-ttu-id="bde72-111">注意事項</span><span class="sxs-lookup"><span data-stu-id="bde72-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bde72-112">az disk show</span><span class="sxs-lookup"><span data-stu-id="bde72-112">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="bde72-113">使用受控磁碟的名稱和資源群組屬性，取得受控磁碟的所有屬性。</span><span class="sxs-lookup"><span data-stu-id="bde72-113">Gets all the properties of a managed disk using the name and resource group properties of the managed disk.</span></span> <span data-ttu-id="bde72-114">使用 Id 屬性將受控磁碟複製到不同的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="bde72-114">Id property is used to copy the managed disk to different subscription.</span></span>  |
| [<span data-ttu-id="bde72-115">az disk create</span><span class="sxs-lookup"><span data-stu-id="bde72-115">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="bde72-116">使用父受控磁碟的識別碼和名稱，在不同的訂閱中建立一個新的受控磁碟管，來複製受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="bde72-116">Copies a managed disk by creating a new managed disk in different subscription using Id and name the parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="bde72-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bde72-117">Next steps</span></span>

[<span data-ttu-id="bde72-118">從受控磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bde72-118">Create a virtual machine from a managed disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="bde72-119">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="bde72-119">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bde72-120">您可以在 [Azure Linux VM 文件](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器和受控磁碟 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="bde72-120">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
