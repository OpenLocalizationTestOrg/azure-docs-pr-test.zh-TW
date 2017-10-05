---
title: "Azure CLI 指令碼範例 - 從相同訂用帳戶的儲存體帳戶的 VHD 檔案建立受管理的磁碟 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 從相同訂用帳戶的儲存體帳戶的 VHD 檔案建立受管理的磁碟"
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
ms.openlocfilehash: 448636e87db126defc804a613bb61ff19a086ad9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-the-same-subscription-with-cli"></a><span data-ttu-id="4abb2-103">使用 CLI 從相同訂用帳戶的儲存體帳戶的 VHD 檔案建立受管理的磁碟</span><span class="sxs-lookup"><span data-stu-id="4abb2-103">Create a managed disk from a VHD file in a storage account in the same subscription with CLI</span></span>

<span data-ttu-id="4abb2-104">此指令碼會從相同訂用帳戶的儲存體帳戶的 VHD 檔案建立受管理的磁碟。</span><span class="sxs-lookup"><span data-stu-id="4abb2-104">This script creates a managed disk from a VHD file in a storage account in the same subscription.</span></span> <span data-ttu-id="4abb2-105">請使用此指令碼將特殊化 (未一般化/執行 sysprep) 的 VHD 匯入受控的作業系統磁碟，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="4abb2-105">Use this script to import a specialized (not generalized/sysprepped) VHD to managed OS disk to create a virtual machine.</span></span> <span data-ttu-id="4abb2-106">或者，用它將資料 VHD 匯入到受控資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="4abb2-106">Or, use it to import a data VHD to managed data disk.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4abb2-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="4abb2-107">Sample script</span></span>

<span data-ttu-id="4abb2-108">[!code-azurecli[主要](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "從 VHD 建立受控磁碟")]</span><span class="sxs-lookup"><span data-stu-id="4abb2-108">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-managed-data-disks-from-vhd/create-managed-data-disks-from-vhd.sh "Create managed disk from VHD")]</span></span>


## <a name="script-explanation"></a><span data-ttu-id="4abb2-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="4abb2-109">Script explanation</span></span>

<span data-ttu-id="4abb2-110">此指令碼使用下列命令從 VHD 建立受控磁碟。</span><span class="sxs-lookup"><span data-stu-id="4abb2-110">This script uses following commands to create a managed disk from a VHD.</span></span> <span data-ttu-id="4abb2-111">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="4abb2-111">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="4abb2-112">命令</span><span class="sxs-lookup"><span data-stu-id="4abb2-112">Command</span></span> | <span data-ttu-id="4abb2-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="4abb2-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4abb2-114">az disk create</span><span class="sxs-lookup"><span data-stu-id="4abb2-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="4abb2-115">在相同的訂用帳戶中使用儲存體帳戶的 VHD URI 受控磁碟</span><span class="sxs-lookup"><span data-stu-id="4abb2-115">Creates a managed disk using URI of a VHD in a storage account in the same subscription</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4abb2-116">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4abb2-116">Next steps</span></span>

[<span data-ttu-id="4abb2-117">將受控磁碟連結為作業系統磁碟以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="4abb2-117">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="4abb2-118">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4abb2-118">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4abb2-119">您可以在 [Azure Linux VM 文件](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器和受控磁碟 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="4abb2-119">Additional virtual machine and managed disks CLI script samples can be found in the [Azure Linux VM documentation](../../app-service-web/app-service-cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
