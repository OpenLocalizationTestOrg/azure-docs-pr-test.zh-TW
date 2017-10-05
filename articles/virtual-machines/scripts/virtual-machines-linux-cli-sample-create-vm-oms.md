---
title: "Azure CLI 指令碼範例 - 建立具有 OMS 監視的 Linux VM | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 建立具有 OMS 監視的 Linux VM"
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
ms.openlocfilehash: 31bfcc532a7d1ea418fb9a15ec882963d1913756
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-a-vm-with-operations-management-suite"></a><span data-ttu-id="b8bc4-103">使用 Operations Management Suite 監視 VM</span><span class="sxs-lookup"><span data-stu-id="b8bc4-103">Monitor a VM with Operations Management Suite</span></span>

<span data-ttu-id="b8bc4-104">此指令碼會建立 Azure 虛擬機器、安裝 Operations Management Suite (OMS) 代理程式，並向 OMS 工作區註冊系統。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-104">This script creates an Azure Virtual Machine, installs the Operations Management Suite (OMS) agent, and enrolls the system with an OMS workspace.</span></span> <span data-ttu-id="b8bc4-105">執行此指令碼後，就能在 OMS 主控台中看到虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-105">Once the script has run, the virtual machine will be visible in the OMS console.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="b8bc4-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="b8bc4-106">Sample script</span></span>

<span data-ttu-id="b8bc4-107">[!code-azurecli-interactive[主要](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "快速建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="b8bc4-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-monitor-oms/create-vm-monitor-oms.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="b8bc4-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="b8bc4-108">Clean up deployment</span></span> 

<span data-ttu-id="b8bc4-109">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="b8bc4-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="b8bc4-110">Script explanation</span></span>

<span data-ttu-id="b8bc4-111">此指令碼使用下列命令來建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="b8bc4-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="b8bc4-113">命令</span><span class="sxs-lookup"><span data-stu-id="b8bc4-113">Command</span></span> | <span data-ttu-id="b8bc4-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="b8bc4-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="b8bc4-115">az group create</span><span class="sxs-lookup"><span data-stu-id="b8bc4-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="b8bc4-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="b8bc4-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="b8bc4-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="b8bc4-118">建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="b8bc4-119">此命令也會指定要使用的虛擬機器映像和管理認證。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="b8bc4-120">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="b8bc4-120">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b8bc4-121">對虛擬機器執行 VM 擴充功能。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-121">Runs a VM extension against a virtual machine.</span></span> <span data-ttu-id="b8bc4-122">在此情況下，會使用 Operations Management Suite 代理程式擴充功能來安裝 OMS 代理程式，並在 OMS 工作區中註冊 VM。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-122">In this case, the Operations Management Suite agent extension is used to install the OMS agent and enroll the VM in an OMS workspace.</span></span> |
| [<span data-ttu-id="b8bc4-123">az group delete</span><span class="sxs-lookup"><span data-stu-id="b8bc4-123">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="b8bc4-124">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-124">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="b8bc4-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b8bc4-125">Next steps</span></span>

<span data-ttu-id="b8bc4-126">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-126">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="b8bc4-127">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="b8bc4-127">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
