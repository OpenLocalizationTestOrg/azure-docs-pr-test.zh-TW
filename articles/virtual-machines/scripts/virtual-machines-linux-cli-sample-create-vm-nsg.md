---
title: "aaaAzure CLI 指令碼範例-建立兩個 Vm 的內部和外部 NSG |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立兩個分別具有內部和外部 NSG 的 VM"
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
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="889f9-103">保護虛擬機器之間的網路流量</span><span class="sxs-lookup"><span data-stu-id="889f9-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="889f9-104">此指令碼會建立兩個虛擬機器及保護在連入流量 tooboth。</span><span class="sxs-lookup"><span data-stu-id="889f9-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="889f9-105">其中一個虛擬機器可以存取 hello 網際網路以及網路安全性群組 (NSG) 設定 tooallow 流量通訊埠 22 和連接埠 80 上。</span><span class="sxs-lookup"><span data-stu-id="889f9-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 22 and port 80.</span></span> <span data-ttu-id="889f9-106">hello 第二個虛擬機器不能存取在 hello 網際網路，並已設定的 NSG tooonly 允許從 hello 第一部虛擬機器的流量。</span><span class="sxs-lookup"><span data-stu-id="889f9-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="889f9-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="889f9-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="889f9-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="889f9-108">Clean up deployment</span></span> 

<span data-ttu-id="889f9-109">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="889f9-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="889f9-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="889f9-110">Script explanation</span></span>

<span data-ttu-id="889f9-111">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="889f9-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="889f9-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="889f9-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="889f9-113">命令</span><span class="sxs-lookup"><span data-stu-id="889f9-113">Command</span></span> | <span data-ttu-id="889f9-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="889f9-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="889f9-115">az group create</span><span class="sxs-lookup"><span data-stu-id="889f9-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="889f9-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="889f9-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="889f9-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="889f9-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="889f9-118">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="889f9-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="889f9-119">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="889f9-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="889f9-120">建立子網路。</span><span class="sxs-lookup"><span data-stu-id="889f9-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="889f9-121">az vm create</span><span class="sxs-lookup"><span data-stu-id="889f9-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="889f9-122">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="889f9-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="889f9-123">此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="889f9-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="889f9-124">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="889f9-124">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="889f9-125">傳回網路安全性群組規則的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="889f9-125">Returns information about a network security group rule.</span></span> <span data-ttu-id="889f9-126">在此範例中，hello 規則名稱會儲存在變數中以便稍後在 hello 指令碼中使用。</span><span class="sxs-lookup"><span data-stu-id="889f9-126">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="889f9-127">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="889f9-127">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="889f9-128">更新 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="889f9-128">Updates an NSG rule.</span></span> <span data-ttu-id="889f9-129">在此範例中，hello 後端規則是更新的 toopass 只能從 hello 前端子網路的流量通過。</span><span class="sxs-lookup"><span data-stu-id="889f9-129">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="889f9-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="889f9-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="889f9-131">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="889f9-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="889f9-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="889f9-132">Next steps</span></span>

<span data-ttu-id="889f9-133">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="889f9-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="889f9-134">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="889f9-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
