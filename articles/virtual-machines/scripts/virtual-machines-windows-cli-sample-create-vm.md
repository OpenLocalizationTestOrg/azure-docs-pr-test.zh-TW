---
title: "aaaAzure CLI 指令碼範例為建立 Windows Server VM |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立 Windows Server VM"
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
ms.openlocfilehash: f4cb431a68c911f877f5af87c393849bd8d2676a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="e7bfa-103">建立虛擬機器以 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e7bfa-103">Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="e7bfa-104">此指令碼會建立執行 Windows Server 2016 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="e7bfa-105">執行 hello 指令碼之後, 您可以透過遠端桌面連線存取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-105">After running hello script, you can access hello virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e7bfa-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e7bfa-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e7bfa-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="e7bfa-107">Clean up deployment</span></span> 

<span data-ttu-id="e7bfa-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="e7bfa-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e7bfa-109">Script explanation</span></span>

<span data-ttu-id="e7bfa-110">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="e7bfa-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e7bfa-112">命令</span><span class="sxs-lookup"><span data-stu-id="e7bfa-112">Command</span></span> | <span data-ttu-id="e7bfa-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="e7bfa-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e7bfa-114">az group create</span><span class="sxs-lookup"><span data-stu-id="e7bfa-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e7bfa-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e7bfa-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="e7bfa-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="e7bfa-117">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="e7bfa-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="e7bfa-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="e7bfa-119">建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="e7bfa-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="e7bfa-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="e7bfa-121">建立網路安全性群組 (NSG)，也就是 hello 網際網路和 hello 虛擬機器的安全性界限。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="e7bfa-122">az network nic create</span><span class="sxs-lookup"><span data-stu-id="e7bfa-122">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="e7bfa-123">建立虛擬網路介面卡，並將其附加 toohello 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-123">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="e7bfa-124">az vm create</span><span class="sxs-lookup"><span data-stu-id="e7bfa-124">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="e7bfa-125">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-125">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="e7bfa-126">此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-126">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="e7bfa-127">az group delete</span><span class="sxs-lookup"><span data-stu-id="e7bfa-127">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="e7bfa-128">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e7bfa-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e7bfa-129">Next steps</span></span>

<span data-ttu-id="e7bfa-130">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e7bfa-131">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Windows VM 文件](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="e7bfa-131">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
