---
title: "Azure PowerShell 指令碼範例 - 將受控磁碟快照集複製 (移動) 到相同或不同的訂用帳戶 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 將受控磁碟快照集複製 (移動) 到相同或不同的訂用帳戶"
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
ms.openlocfilehash: 69b9b4ed86117f7fe561e7e70227e60e6a9d858e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="copy-snapshot-of-a-managed-disk-in-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="5adc9-103">使用 PowerShell 複製相同訂用帳戶或不同訂用帳戶中的受控磁碟快照集</span><span class="sxs-lookup"><span data-stu-id="5adc9-103">Copy snapshot of a managed disk in same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="5adc9-104">此指令碼會在相同訂用帳戶或不同訂用帳戶中建立快照集的複本。</span><span class="sxs-lookup"><span data-stu-id="5adc9-104">This script creates a copy of a snapshot in the same same subscription or different subscription.</span></span> <span data-ttu-id="5adc9-105">使用此指令碼將快照集移至不同的訂用帳戶以供進行資料保留。</span><span class="sxs-lookup"><span data-stu-id="5adc9-105">Use this script to move a snapshot to different subscription for data retention.</span></span> <span data-ttu-id="5adc9-106">將快照集儲存到不同的訂用帳戶中可保護您不因在主要訂用帳戶中意外刪除快照集而產生損失。</span><span class="sxs-lookup"><span data-stu-id="5adc9-106">Storing snapshots in different subscription protect you from accidental deletion of snapshots in your main subscription.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5adc9-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="5adc9-107">Sample script</span></span>

<span data-ttu-id="5adc9-108">[!code-powershell[主要](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "複製快照集")]</span><span class="sxs-lookup"><span data-stu-id="5adc9-108">[!code-powershell[main](../../../powershell_scripts/storage/copy-snapshot-to-same-or-different-subscription/copy-snapshot-to-same-or-different-subscription.ps1 "Copy snapshot")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="5adc9-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="5adc9-109">Script explanation</span></span>

<span data-ttu-id="5adc9-110">此指令碼會使用下列命令，使用來源快照集的識別碼在目標訂用帳戶中建立快照集。</span><span class="sxs-lookup"><span data-stu-id="5adc9-110">This script uses following commands to create a snapshot in the target subscription using the Id of the source snapshot.</span></span> <span data-ttu-id="5adc9-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="5adc9-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5adc9-112">命令</span><span class="sxs-lookup"><span data-stu-id="5adc9-112">Command</span></span> | <span data-ttu-id="5adc9-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="5adc9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5adc9-114">New-AzureRmSnapshotConfig</span><span class="sxs-lookup"><span data-stu-id="5adc9-114">New-AzureRmSnapshotConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmSnapshotConfig) | <span data-ttu-id="5adc9-115">建立用於建立快照集的快照集組態。</span><span class="sxs-lookup"><span data-stu-id="5adc9-115">Creates snapshot configuration that is used for snapshot creation.</span></span> <span data-ttu-id="5adc9-116">其中包含父代快照集的資源識別碼以及與父代快照集位置相同的位置。</span><span class="sxs-lookup"><span data-stu-id="5adc9-116">It includes the resource Id of the parent snapshot and location that is same as the parent snapshot.</span></span>  |
| [<span data-ttu-id="5adc9-117">New-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="5adc9-117">New-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="5adc9-118">使用當作參數傳遞的快照集組態、快照集名稱和資源群組名稱來建立快照集。</span><span class="sxs-lookup"><span data-stu-id="5adc9-118">Creates a snapshot using snapshot configuration, snapshot name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="5adc9-119">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5adc9-119">Next steps</span></span>

[<span data-ttu-id="5adc9-120">從快照集建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="5adc9-120">Create a virtual machine from a snapshot</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="5adc9-121">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5adc9-121">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5adc9-122">您可以在 [Azure Windows VM 文件](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="5adc9-122">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>