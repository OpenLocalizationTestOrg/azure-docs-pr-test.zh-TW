---
title: "Azure CLI 指令碼範例 - 掛接作業系統磁碟 | Microsoft Docs"
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
ms.openlocfilehash: b54a94d833644ebfae4c1fac59e4753ab723ced4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-a-vms-operating-system-disk"></a><span data-ttu-id="23487-103">針對 VM 作業系統磁碟進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="23487-103">Troubleshoot a VMs operating system disk</span></span>

<span data-ttu-id="23487-104">此指令碼會將已失敗或有問題之虛擬機器的作業系統磁碟當做資料磁碟，掛接到第二部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="23487-104">This script mounts the operating system disk of a failed or problematic virtual machine as a data disk to a second virtual machine.</span></span> <span data-ttu-id="23487-105">在進行磁碟問題或復原資料的疑難排解時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="23487-105">This can be useful when troubleshooting disk issues or recovering data.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="23487-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="23487-106">Sample script</span></span>

<span data-ttu-id="23487-107">[!code-azurecli-interactive[主要](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "快速建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="23487-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/mount-os-disk/mount-os-disk.sh "Quick Create VM")]</span></span>

## <a name="script-explanation"></a><span data-ttu-id="23487-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="23487-108">Script explanation</span></span>

<span data-ttu-id="23487-109">此指令碼使用下列命令來建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="23487-109">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="23487-110">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="23487-110">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="23487-111">命令</span><span class="sxs-lookup"><span data-stu-id="23487-111">Command</span></span> | <span data-ttu-id="23487-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="23487-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="23487-113">az vm show</span><span class="sxs-lookup"><span data-stu-id="23487-113">az vm show</span></span>](https://docs.microsoft.com/cli/azure/vm#show) | <span data-ttu-id="23487-114">傳回虛擬機器清單。</span><span class="sxs-lookup"><span data-stu-id="23487-114">Return a list of virtual machines.</span></span> <span data-ttu-id="23487-115">此案例使用查詢選項來傳回虛擬機器的作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="23487-115">In this case, the query option is used to return the virtual machine operating system disk.</span></span> <span data-ttu-id="23487-116">接著將此值新增至 'uri' 變數名稱。</span><span class="sxs-lookup"><span data-stu-id="23487-116">This value is then added to a variable name ‘uri’.</span></span> |
| [<span data-ttu-id="23487-117">az vm delete</span><span class="sxs-lookup"><span data-stu-id="23487-117">az vm delete</span></span>](https://docs.microsoft.com/cli/azure/vm#delete) | <span data-ttu-id="23487-118">刪除虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="23487-118">Deletes a virtual machine.</span></span> |
| [<span data-ttu-id="23487-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="23487-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="23487-120">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="23487-120">Creates a virtual machine.</span></span>  |
| [<span data-ttu-id="23487-121">az vm disk attach</span><span class="sxs-lookup"><span data-stu-id="23487-121">az vm disk attach</span></span>](https://docs.microsoft.com/cli/azure/vm/disk#attach) | <span data-ttu-id="23487-122">將磁碟連接至虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="23487-122">Attaches a disk to a virtual machine.</span></span> |
| [<span data-ttu-id="23487-123">az vm list-ip-addresses</span><span class="sxs-lookup"><span data-stu-id="23487-123">az vm list-ip-addresses</span></span>](https://docs.microsoft.com/cli/azure/vm#list-ip-addresses) | <span data-ttu-id="23487-124">傳回虛擬機器的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="23487-124">Returns the IP addresses of a virtual machine.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="23487-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="23487-125">Next steps</span></span>

<span data-ttu-id="23487-126">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="23487-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="23487-127">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="23487-127">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
