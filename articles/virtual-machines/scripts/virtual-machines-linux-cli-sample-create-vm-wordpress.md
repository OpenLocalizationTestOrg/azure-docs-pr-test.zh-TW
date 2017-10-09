---
title: "aaaAzure CLI 指令碼範例-使用 WordPress 建立 Linux VM |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 使用 WordPress 建立 Linux VM"
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
ms.openlocfilehash: 2c5c03d08b6d5d27eb8c505b1dbd817eda5f2fc4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-wordpress"></a><span data-ttu-id="7a6ec-103">建立含 WordPress 的 VM</span><span class="sxs-lookup"><span data-stu-id="7a6ec-103">Create a VM with WordPress</span></span>

<span data-ttu-id="7a6ec-104">此指令碼會建立虛擬機器，然後再使用 hello Azure 虛擬機器自訂指令碼延伸 tooinstall WordPress。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-104">This script creates a virtual machine, and then uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="7a6ec-105">執行 hello 指令碼之後, 您可以存取 hello WordPress 設定站台`http://<public IP of VM>/wordpress`。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7a6ec-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="7a6ec-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7a6ec-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="7a6ec-107">Clean up deployment</span></span> 

<span data-ttu-id="7a6ec-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7a6ec-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="7a6ec-109">Script explanation</span></span>

<span data-ttu-id="7a6ec-110">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="7a6ec-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7a6ec-112">命令</span><span class="sxs-lookup"><span data-stu-id="7a6ec-112">Command</span></span> | <span data-ttu-id="7a6ec-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="7a6ec-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7a6ec-114">az group create</span><span class="sxs-lookup"><span data-stu-id="7a6ec-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="7a6ec-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7a6ec-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="7a6ec-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="7a6ec-117">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="7a6ec-118">此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="7a6ec-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="7a6ec-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="7a6ec-120">建立網路安全性群組規則 tooallow 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="7a6ec-121">在此範例中，會開放連接埠 80 供 HTTP 流量使用。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="7a6ec-122">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="7a6ec-122">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="7a6ec-123">新增 hello 自訂指令碼擴充 toohello 虛擬機器，這會叫用指令碼 tooinstall WordPress。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-123">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
| [<span data-ttu-id="7a6ec-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="7a6ec-124">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="7a6ec-125">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7a6ec-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7a6ec-126">Next steps</span></span>

<span data-ttu-id="7a6ec-127">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-127">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7a6ec-128">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="7a6ec-128">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
