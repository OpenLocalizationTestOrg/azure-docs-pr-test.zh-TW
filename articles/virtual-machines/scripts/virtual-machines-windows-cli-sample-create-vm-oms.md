---
title: "aaaAzure CLI 指令碼範例-使用 OMS 監視建立的 Windows Server 2016 VM |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立具有 OMS 監視的 Windows Server 2016 VM"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: rickstercdn
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/23/2017
ms.author: rclaus
ms.openlocfilehash: 4f070430ccc5d5402ed4a80ead3b78eff25dcd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="dc3c4-103">使用 Operations Management Suite 監視 VM</span><span class="sxs-lookup"><span data-stu-id="dc3c4-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="dc3c4-104">此指令碼會建立 Azure 虛擬機器、 安裝 hello Operations Management Suite (OMS) 代理程式，並註冊使用 OMS 工作區的 hello 系統。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="dc3c4-105">Hello 指令碼執行之後，將會出現在 hello OMS 主控台 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="dc3c4-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="dc3c4-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-monitor-oms.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dc3c4-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="dc3c4-107">Clean up deployment</span></span> 

<span data-ttu-id="dc3c4-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="dc3c4-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="dc3c4-109">Script explanation</span></span>

<span data-ttu-id="dc3c4-110">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="dc3c4-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dc3c4-112">命令</span><span class="sxs-lookup"><span data-stu-id="dc3c4-112">Command</span></span> | <span data-ttu-id="dc3c4-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="dc3c4-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dc3c4-114">az group create</span><span class="sxs-lookup"><span data-stu-id="dc3c4-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dc3c4-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dc3c4-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="dc3c4-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="dc3c4-117">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="dc3c4-118">此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="dc3c4-119">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="dc3c4-119">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="dc3c4-120">對虛擬機器執行 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-120">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="dc3c4-121">在此情況下，hello Operations Management Suite 代理程式延伸模組是使用的 tooinstall hello OMS 代理程式，並註冊 hello OMS 工作區中的 VM。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-121">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="dc3c4-122">az group delete</span><span class="sxs-lookup"><span data-stu-id="dc3c4-122">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="dc3c4-123">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-123">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dc3c4-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="dc3c4-124">Next steps</span></span>

<span data-ttu-id="dc3c4-125">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-125">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dc3c4-126">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Windows VM 文件](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="dc3c4-126">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
