---
title: "aaaAzure CLI 指令碼範例-使用 DSC 的 iis 中建立 Windows Server 2016 VM |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 使用 DSC 建立具有 IIS 的 Windows Server 2016 VM"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.custom: mvc
ms.openlocfilehash: 9883b5925dddca3dd53d083679a0e76d0fb982e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-iis-using-dsc"></a><span data-ttu-id="94d67-103">使用 DSC 建立具有 IIS 的 VM</span><span class="sxs-lookup"><span data-stu-id="94d67-103">Create a VM with IIS using DSC</span></span>

<span data-ttu-id="94d67-104">此指令碼會建立虛擬機器，並使用 hello Azure 虛擬機器 DSC 自訂指令碼延伸 tooinstall 及設定 IIS。</span><span class="sxs-lookup"><span data-stu-id="94d67-104">This script creates a virtual machine, and uses hello Azure Virtual Machine DSC custom script extension tooinstall and configure IIS.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="94d67-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="94d67-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-windows-iis-using-dsc/create-windows-iis-using-dsc.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="94d67-106">清除部署</span><span class="sxs-lookup"><span data-stu-id="94d67-106">Clean up deployment</span></span> 

<span data-ttu-id="94d67-107">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="94d67-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="94d67-108">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="94d67-108">Script explanation</span></span>

<span data-ttu-id="94d67-109">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="94d67-109">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="94d67-110">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="94d67-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="94d67-111">命令</span><span class="sxs-lookup"><span data-stu-id="94d67-111">Command</span></span> | <span data-ttu-id="94d67-112">注意事項</span><span class="sxs-lookup"><span data-stu-id="94d67-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="94d67-113">az group create</span><span class="sxs-lookup"><span data-stu-id="94d67-113">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="94d67-114">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="94d67-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="94d67-115">az vm create</span><span class="sxs-lookup"><span data-stu-id="94d67-115">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="94d67-116">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="94d67-116">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="94d67-117">此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="94d67-117">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="94d67-118">az vm extension set</span><span class="sxs-lookup"><span data-stu-id="94d67-118">az vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="94d67-119">新增 hello 自訂指令碼擴充 toohello 虛擬機器會叫用指令碼 tooinstall IIS。</span><span class="sxs-lookup"><span data-stu-id="94d67-119">Add hello Custom Script Extension toohello virtual machine which invokes a script tooinstall IIS.</span></span> |
| [<span data-ttu-id="94d67-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="94d67-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="94d67-121">建立網路安全性群組規則 tooallow 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="94d67-121">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="94d67-122">在此範例中，會開放連接埠 80 供 HTTP 流量使用。</span><span class="sxs-lookup"><span data-stu-id="94d67-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="94d67-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="94d67-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="94d67-124">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="94d67-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="94d67-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="94d67-125">Next steps</span></span>

<span data-ttu-id="94d67-126">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="94d67-126">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="94d67-127">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Windows VM 文件](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="94d67-127">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
