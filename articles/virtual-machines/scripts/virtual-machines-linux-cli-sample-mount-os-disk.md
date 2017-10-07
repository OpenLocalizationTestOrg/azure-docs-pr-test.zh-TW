---
title: "CLI 指令碼範例掛接作業系統磁碟 aaaAzure |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 掛接作業系統磁碟"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5c614d09a64780575b70424d29052f1a6affec59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="69f0d-103">針對 VM 作業系統磁碟進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="69f0d-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="69f0d-104">此指令碼做為資料磁碟 tooa 第二個虛擬機器掛接 hello 失敗或問題的虛擬機器的作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="69f0d-104">This script mounts hello operating system disk of a failed or problematic virtual machine as a data disk tooa second virtual machine.</span></span> <span data-ttu-id="69f0d-105">在進行磁碟問題或復原資料的疑難排解時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="69f0d-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="69f0d-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="69f0d-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]

## <a name="script-explanation"></a><span data-ttu-id="69f0d-107">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="69f0d-107">Script explanation</span></span>

<span data-ttu-id="69f0d-108">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="69f0d-108">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="69f0d-109">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="69f0d-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="69f0d-110">命令</span><span class="sxs-lookup"><span data-stu-id="69f0d-110">Command</span></span> | <span data-ttu-id="69f0d-111">注意事項</span><span class="sxs-lookup"><span data-stu-id="69f0d-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="69f0d-112">az vm show</span><span class="sxs-lookup"><span data-stu-id="69f0d-112">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="69f0d-113">傳回虛擬機器清單。</span><span class="sxs-lookup"><span data-stu-id="69f0d-113">Return a list of virtual machines.</span></span> <span data-ttu-id="69f0d-114">在此情況下，hello 查詢選項是使用的 tooreturn hello 虛擬機器的作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="69f0d-114">In this case, hello query option is used tooreturn hello virtual machine operating system disk.</span></span> <span data-ttu-id="69f0d-115">接著，這個值會加入 tooa 變數名稱 'uri'。</span><span class="sxs-lookup"><span data-stu-id="69f0d-115">This value is then added tooa variable name ‘uri’.</span></span> |
| [<span data-ttu-id="69f0d-116">az vm delete</span><span class="sxs-lookup"><span data-stu-id="69f0d-116">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="69f0d-117">刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="69f0d-117">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="69f0d-118">az vm create</span><span class="sxs-lookup"><span data-stu-id="69f0d-118">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="69f0d-119">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="69f0d-119">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="69f0d-120">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="69f0d-120">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="69f0d-121">附加磁碟 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="69f0d-121">Attaches a disk tooa virtual machine.</span></span> |
| [<span data-ttu-id="69f0d-122">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="69f0d-122">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="69f0d-123">傳回 hello 虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="69f0d-123">Returns hello IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="69f0d-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="69f0d-124">Next steps</span></span>

<span data-ttu-id="69f0d-125">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="69f0d-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="69f0d-126">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="69f0d-126">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
