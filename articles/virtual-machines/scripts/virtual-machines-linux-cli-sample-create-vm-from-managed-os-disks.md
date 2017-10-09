---
title: "aaaAzure CLI 指令碼範例-建立 VM，藉由附加為作業系統磁碟的受管理的磁碟 |Microsoft 文件"
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
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="fb77e-103">使用現有受控 OS 磁碟搭配 CLI 以建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fb77e-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="fb77e-104">此指令碼會連結現有受控磁碟作為 OS 磁碟，以建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fb77e-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="fb77e-105">在先前案例中使用此指令碼︰</span><span class="sxs-lookup"><span data-stu-id="fb77e-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="fb77e-106">從不同訂用帳戶中的受控磁碟複製而來的現有受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="fb77e-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="fb77e-107">從特殊化 VHD 檔案建立的現有受控磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="fb77e-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="fb77e-108">從快照集建立的現有受控 OS 磁碟建立 VM</span><span class="sxs-lookup"><span data-stu-id="fb77e-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fb77e-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="fb77e-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="fb77e-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="fb77e-110">Clean up deployment</span></span> 

<span data-ttu-id="fb77e-111">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="fb77e-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="fb77e-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="fb77e-112">Script explanation</span></span>

<span data-ttu-id="fb77e-113">此指令碼會使用下列命令 tooget 管理磁碟屬性中的 hello、 附加受管理的磁碟 tooa 新的 VM，並建立 VM。</span><span class="sxs-lookup"><span data-stu-id="fb77e-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="fb77e-114">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="fb77e-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fb77e-115">命令</span><span class="sxs-lookup"><span data-stu-id="fb77e-115">Command</span></span> | <span data-ttu-id="fb77e-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="fb77e-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fb77e-117">az disk show</span><span class="sxs-lookup"><span data-stu-id="fb77e-117">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="fb77e-118">使用磁碟名稱和資源群組名稱取得受控磁碟屬性。</span><span class="sxs-lookup"><span data-stu-id="fb77e-118">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="fb77e-119">Id 屬性都是使用的 tooattach 受管理的磁碟 tooa 新的 VM</span><span class="sxs-lookup"><span data-stu-id="fb77e-119">Id property is used tooattach a managed disk tooa new VM</span></span> |
| [<span data-ttu-id="fb77e-120">az vm create</span><span class="sxs-lookup"><span data-stu-id="fb77e-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="fb77e-121">建立使用受控 OS 磁碟的 VM</span><span class="sxs-lookup"><span data-stu-id="fb77e-121">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="fb77e-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fb77e-122">Next steps</span></span>

<span data-ttu-id="fb77e-123">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fb77e-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fb77e-124">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="fb77e-124">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
