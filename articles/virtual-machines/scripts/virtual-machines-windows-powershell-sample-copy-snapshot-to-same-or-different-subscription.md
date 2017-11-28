---
title: "aaaAzure PowerShell 指令碼範例複製 （移動） 快照集的受管理的磁碟 toosame 或不同的訂用帳戶 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例的受管理的磁碟 toosame 或不同的訂用帳戶的複本 （移動） 快照集"
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
ms.openlocfilehash: d7b8a71cc09d1950271f472e89b95bb551323be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="d96df-103">使用 PowerShell 複製相同訂用帳戶或不同訂用帳戶中的受控磁碟快照集</span><span class="sxs-lookup"><span data-stu-id="d96df-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="d96df-104">此指令碼會建立一份快照集在 hello 相同的同一個訂用帳戶或其他訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d96df-104">This script creates a copy of a snapshot in hello same same subscription or different subscription.</span></span> <span data-ttu-id="d96df-105">使用此指令碼 toomove 快照 toodifferent 訂用帳戶資料保留的。</span><span class="sxs-lookup"><span data-stu-id="d96df-105">Use this script toomove a snapshot toodifferent subscription for data retention.</span></span> <span data-ttu-id="d96df-106">將快照集儲存到不同的訂用帳戶中可保護您不因在主要訂用帳戶中意外刪除快照集而產生損失。</span><span class="sxs-lookup"><span data-stu-id="d96df-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="d96df-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="d96df-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="d96df-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="d96df-108">Script explanation</span></span>

<span data-ttu-id="d96df-109">此指令碼，會使用下列命令 toocreate hello 目標訂用帳戶的使用中的快照集 hello hello 來源快照集的識別碼。</span><span class="sxs-lookup"><span data-stu-id="d96df-109">This script uses following commands toocreate a snapshot in hello target subscription using hello Id of hello source snapshot.</span></span> <span data-ttu-id="d96df-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="d96df-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="d96df-111">命令</span><span class="sxs-lookup"><span data-stu-id="d96df-111">Command</span></span> | <span data-ttu-id="d96df-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="d96df-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d96df-113">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="d96df-113">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="d96df-114">建立用於建立快照集的快照集組態。</span><span class="sxs-lookup"><span data-stu-id="d96df-114">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="d96df-115">它包含 hello 資源識別碼 hello 父快照集和相同 hello 父快照集的位置。</span><span class="sxs-lookup"><span data-stu-id="d96df-115">It includes hello resource Id of hello parent snapshot and location that is same as hello parent snapshot.</span></span>  |
| [<span data-ttu-id="d96df-116">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="d96df-116">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="d96df-117">使用當作參數傳遞的快照集組態、快照集名稱和資源群組名稱來建立快照集。</span><span class="sxs-lookup"><span data-stu-id="d96df-117">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="d96df-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d96df-118">Next steps</span></span>

[<span data-ttu-id="d96df-119">從快照集建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="d96df-119">Create a virtual machine from a snapshot</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="d96df-120">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="d96df-120">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="d96df-121">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="d96df-121">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
