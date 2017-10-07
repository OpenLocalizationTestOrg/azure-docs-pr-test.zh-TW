---
title: "PowerShell 指令碼範例-aaaAzure 複製 （移動） 磁碟 toosame 或管理不同訂用帳戶 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-複製 （移動） 管理磁碟 toosame 或不同的訂用帳戶"
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 5a92118e10a14615e5b1713f1b90188b37b05305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="e8419-103">受管理的複本磁碟區在 hello 相同訂用帳戶或不同的訂用帳戶使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="e8419-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="e8419-104">此指令碼會建立 hello 現有受管理磁碟的副本相同訂用帳戶或其他訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8419-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="e8419-105">hello 會建立新磁碟在 hello 相同與 hello 父區域管理磁碟。</span><span class="sxs-lookup"><span data-stu-id="e8419-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e8419-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e8419-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="e8419-107">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e8419-107">Script explanation</span></span>

<span data-ttu-id="e8419-108">此指令碼會使用下列命令 toocreate hello 目標訂用帳戶使用的新受管理的磁碟 hello 識別碼 hello 來源的受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="e8419-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="e8419-109">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="e8419-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e8419-110">命令</span><span class="sxs-lookup"><span data-stu-id="e8419-110">Command</span></span> | <span data-ttu-id="e8419-111">注意事項</span><span class="sxs-lookup"><span data-stu-id="e8419-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8419-112">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="e8419-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="e8419-113">建立用於磁碟建立的磁碟組態。</span><span class="sxs-lookup"><span data-stu-id="e8419-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="e8419-114">它包含 hello 資源識別碼 hello 父磁碟以及父磁碟的 hello 位置相同的位置。</span><span class="sxs-lookup"><span data-stu-id="e8419-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="e8419-115">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="e8419-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="e8419-116">使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="e8419-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="e8419-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8419-117">Next steps</span></span>

[<span data-ttu-id="e8419-118">從受控磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e8419-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="e8419-119">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e8419-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e8419-120">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e8419-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
