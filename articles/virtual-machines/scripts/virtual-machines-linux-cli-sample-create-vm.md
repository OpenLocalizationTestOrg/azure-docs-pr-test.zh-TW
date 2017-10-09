---
title: "CLI 指令碼範例-aaaAzure 建立 Linux VM |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立 Linux VM"
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
ms.openlocfilehash: c9855204a85cc0f6cd758a1d20121fbeea070943
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="a608c-103">建立完整設定的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a608c-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="a608c-104">此指令碼會建立具有 Ubuntu 作業系統的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a608c-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="a608c-105">執行 hello 指令碼之後, 您可以透過 SSH 存取 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a608c-105">After running hello script, you can access hello virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a608c-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="a608c-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="a608c-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="a608c-107">Clean up deployment</span></span> 

<span data-ttu-id="a608c-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="a608c-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a608c-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="a608c-109">Script explanation</span></span>

<span data-ttu-id="a608c-110">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="a608c-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="a608c-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="a608c-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="a608c-112">命令</span><span class="sxs-lookup"><span data-stu-id="a608c-112">Command</span></span> | <span data-ttu-id="a608c-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="a608c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a608c-114">az group create</span><span class="sxs-lookup"><span data-stu-id="a608c-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a608c-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a608c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a608c-116">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="a608c-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="a608c-117">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="a608c-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="a608c-118">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="a608c-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="a608c-119">建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a608c-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="a608c-120">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="a608c-120">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="a608c-121">建立網路安全性群組 (NSG)，也就是 hello 網際網路和 hello 虛擬機器的安全性界限。</span><span class="sxs-lookup"><span data-stu-id="a608c-121">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="a608c-122">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="a608c-122">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="a608c-123">建立 NSG 規則 tooallow 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="a608c-123">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="a608c-124">在此範例中，會開放連接埠 22 供 SSH 流量使用。</span><span class="sxs-lookup"><span data-stu-id="a608c-124">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="a608c-125">az network nic create</span><span class="sxs-lookup"><span data-stu-id="a608c-125">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="a608c-126">建立虛擬網路介面卡，並將其附加 toohello 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="a608c-126">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="a608c-127">az vm create</span><span class="sxs-lookup"><span data-stu-id="a608c-127">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="a608c-128">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和 NSG。</span><span class="sxs-lookup"><span data-stu-id="a608c-128">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="a608c-129">此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="a608c-129">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="a608c-130">az group delete</span><span class="sxs-lookup"><span data-stu-id="a608c-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a608c-131">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="a608c-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a608c-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a608c-132">Next steps</span></span>

<span data-ttu-id="a608c-133">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a608c-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a608c-134">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a608c-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
