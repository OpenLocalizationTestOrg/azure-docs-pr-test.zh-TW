---
title: "Azure CLI 指令碼範例 - 連結受控磁碟作為 OS 磁碟以建立 VM | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 連結受控磁碟作為 OS 磁碟以建立 VM | Microsoft Docs"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 18eefee869b243b35d4426c226eff5f48cd490a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="bc762-103">使用現有受控 OS 磁碟搭配 CLI 以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="bc762-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="bc762-104">此指令碼會連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="bc762-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="bc762-105">在先前案例中使用此指令碼︰</span><span class="sxs-lookup"><span data-stu-id="bc762-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="bc762-106">從不同訂用帳戶中的受控磁碟複製而來的現有受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="bc762-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="bc762-107">從特殊化 VHD 檔案建立的現有受控磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="bc762-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="bc762-108">從快照集建立的現有受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="bc762-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="bc762-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="bc762-109">Sample script</span></span>

<span data-ttu-id="bc762-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "從受控磁碟建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="bc762-110">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="bc762-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="bc762-111">Clean up deployment</span></span> 

<span data-ttu-id="bc762-112">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="bc762-112">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="bc762-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="bc762-113">Script explanation</span></span>

<span data-ttu-id="bc762-114">此指令碼會使用下列命令來取得受控磁碟屬性、將受控磁碟連結至新的 VM，以及建立 VM。</span><span class="sxs-lookup"><span data-stu-id="bc762-114">This script uses the following commands to get managed disk properties, attach a managed disk to a new VM and create a VM.</span></span> <span data-ttu-id="bc762-115">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="bc762-115">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="bc762-116">命令</span><span class="sxs-lookup"><span data-stu-id="bc762-116">Command</span></span> | <span data-ttu-id="bc762-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="bc762-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="bc762-118">az disk show</span><span class="sxs-lookup"><span data-stu-id="bc762-118">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="bc762-119">使用磁碟名稱和資源群組名稱取得受控磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="bc762-119">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="bc762-120">Id 屬性用來將受控磁碟連結至新的 VM</span><span class="sxs-lookup"><span data-stu-id="bc762-120">Id property is used to attach a managed disk to a new VM</span></span> |
| [<span data-ttu-id="bc762-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="bc762-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="bc762-122">建立使用受控 OS 磁碟的 VM</span><span class="sxs-lookup"><span data-stu-id="bc762-122">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="bc762-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc762-123">Next steps</span></span>

<span data-ttu-id="bc762-124">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="bc762-124">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="bc762-125">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="bc762-125">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
