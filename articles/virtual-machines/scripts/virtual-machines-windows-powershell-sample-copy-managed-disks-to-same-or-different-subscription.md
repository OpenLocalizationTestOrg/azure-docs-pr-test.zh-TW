---
title: "Azure PowerShell 指令碼範例 - 將受控磁碟複製 (移動) 到相同或不同的訂用帳戶 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 將受控磁碟複製 (移動) 到相同或不同的訂用帳戶"
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
ms.openlocfilehash: 75beb35dc19fa530d9b2c19aed6040f74afafbc0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="copy-managed-disks-in-the-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="e9d5d-103">使用 PowerShell 複製相同訂用帳戶或不同訂用帳戶中的受控磁碟</span><span class="sxs-lookup"><span data-stu-id="e9d5d-103">Copy managed disks in the same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="e9d5d-104">此指令碼會在相同訂用帳戶或不同訂用帳戶中建立現有受控磁碟的複本。</span><span class="sxs-lookup"><span data-stu-id="e9d5d-104">This script creates a copy of an existing managed disk in the same subscription or different subscription.</span></span> <span data-ttu-id="e9d5d-105">新磁碟會建立在與父代受控磁碟相同的區域中。</span><span class="sxs-lookup"><span data-stu-id="e9d5d-105">The new disk is created in the same region as the parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e9d5d-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e9d5d-106">Sample script</span></span>

<span data-ttu-id="e9d5d-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "複製受控磁碟")]</span><span class="sxs-lookup"><span data-stu-id="e9d5d-107">[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="e9d5d-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e9d5d-108">Script explanation</span></span>

<span data-ttu-id="e9d5d-109">此指令碼會使用下列命令，在使用來源受控磁碟識別碼的目標訂用帳戶中，建立新的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="e9d5d-109">This script uses following commands to create a new managed disk in the target subscription using the Id of the source managed disk.</span></span> <span data-ttu-id="e9d5d-110">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="e9d5d-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="e9d5d-111">命令</span><span class="sxs-lookup"><span data-stu-id="e9d5d-111">Command</span></span> | <span data-ttu-id="e9d5d-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="e9d5d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e9d5d-113">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="e9d5d-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="e9d5d-114">建立用於磁碟建立的磁碟組態。</span><span class="sxs-lookup"><span data-stu-id="e9d5d-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="e9d5d-115">其中包含父代磁碟的資源識別碼以及與父代磁碟位置相同的位置。</span><span class="sxs-lookup"><span data-stu-id="e9d5d-115">It includes the resource Id of the parent disk and location that is same as the location of parent disk.</span></span>  |
| [<span data-ttu-id="e9d5d-116">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="e9d5d-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="e9d5d-117">使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="e9d5d-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="e9d5d-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e9d5d-118">Next steps</span></span>

[<span data-ttu-id="e9d5d-119">從受控磁碟建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="e9d5d-119">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="e9d5d-120">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e9d5d-120">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e9d5d-121">您可以在 [Azure Windows VM 文件](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 PowerShell 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="e9d5d-121">Additional virtual machine PowerShell script samples can be found in the [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>