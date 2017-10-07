---
title: "aaaAzure PowerShell 指令碼範例-從相同或不同的訂用帳戶中的儲存體帳戶的 VHD 檔案建立受管理的磁碟 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例 - 從相同或不同訂用帳戶的儲存體帳戶的 VHD 檔案建立受控磁碟"
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
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 47acff274cdf79d6fc3cd685cda01cad3d14ca8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="2b93a-103">使用 PowerShell 從相同或不同訂用帳戶的儲存體帳戶的 VHD 檔案建立受控磁碟</span><span class="sxs-lookup"><span data-stu-id="2b93a-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="2b93a-104">此指令碼會從相同或不同訂用帳戶的儲存體帳戶中的 VHD 檔案，建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="2b93a-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="2b93a-105">使用此指令碼 tooimport 特製化 (無法一般化/執行過 sysprep) VHD toomanaged OS 磁碟 toocreate 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2b93a-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="2b93a-106">此外，使用它 tooimport 資料 VHD toomanaged 資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="2b93a-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="2b93a-107">請勿在短時間內從 VHD 檔案建立多個相同的受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="2b93a-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="2b93a-108">toocreate 管理從 vhd 檔案的磁碟建立 hello vhd 檔案的 blob 快照集，則會使用受管理的 toocreate 磁碟。</span><span class="sxs-lookup"><span data-stu-id="2b93a-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="2b93a-109">可以建立只有一個 blob 快照集，使磁碟建立失敗，一分鐘內到期的 toothrottling。</span><span class="sxs-lookup"><span data-stu-id="2b93a-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="2b93a-110">tooavoid 這項調整流速，建立[hello vhd 檔案從受管理的快照集](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)，然後使用 hello 管理快照集 toocreate 多個受管理的磁碟在短時間內。</span><span class="sxs-lookup"><span data-stu-id="2b93a-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2b93a-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="2b93a-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="2b93a-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="2b93a-112">Script explanation</span></span>

<span data-ttu-id="2b93a-113">此指令碼會使用下列命令 toocreate 受管理的磁碟從不同的訂用帳戶中的 VHD。</span><span class="sxs-lookup"><span data-stu-id="2b93a-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="2b93a-114">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="2b93a-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2b93a-115">命令</span><span class="sxs-lookup"><span data-stu-id="2b93a-115">Command</span></span> | <span data-ttu-id="2b93a-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="2b93a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2b93a-117">New-AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="2b93a-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="2b93a-118">建立用於磁碟建立的磁碟組態。</span><span class="sxs-lookup"><span data-stu-id="2b93a-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="2b93a-119">它包含儲存類型、 位置、 資源識別碼 hello 儲存體帳戶 hello 父 VHD 的儲存位置的 hello 父 VHD 的 VHD URI。</span><span class="sxs-lookup"><span data-stu-id="2b93a-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="2b93a-120">New-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="2b93a-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="2b93a-121">使用當作參數傳遞的磁碟組態、磁碟名稱和資源群組名稱來建立磁碟。</span><span class="sxs-lookup"><span data-stu-id="2b93a-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2b93a-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2b93a-122">Next steps</span></span>

[<span data-ttu-id="2b93a-123">將受控磁碟連結為 OS 磁碟以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="2b93a-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="2b93a-124">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="2b93a-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2b93a-125">其他虛擬機器的 PowerShell 指令碼範例可以在 hello [Azure Windows VM 文件](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="2b93a-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
