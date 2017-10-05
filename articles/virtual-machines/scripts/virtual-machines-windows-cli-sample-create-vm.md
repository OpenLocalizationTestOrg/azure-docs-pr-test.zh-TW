---
title: "Azure CLI 指令碼範例 - 建立 Windows Server VM | Microsoft Docs"
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
ms.openlocfilehash: 9690e743e498a55d7339b6f51861fac37c9b0f56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="fc1c0-103">使用 Azure CLI 建立虛擬機器</span><span class="sxs-lookup"><span data-stu-id="fc1c0-103">Create a virtual machine with the Azure CLI</span></span>

<span data-ttu-id="fc1c0-104">此指令碼會建立執行 Windows Server 2016 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-104">This script creates an Azure Virtual Machine running Windows Server 2016.</span></span> <span data-ttu-id="fc1c0-105">執行指令碼之後，您就能透過遠端桌面連線存取該虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-105">After running the script, you can access the virtual machine through a Remote Desktop connection.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fc1c0-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="fc1c0-106">Sample script</span></span>

<span data-ttu-id="fc1c0-107">[!code-azurecli-interactive[主要](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "快速建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="fc1c0-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-windows-vm-detailed.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fc1c0-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="fc1c0-108">Clean up deployment</span></span> 

<span data-ttu-id="fc1c0-109">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="fc1c0-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="fc1c0-110">Script explanation</span></span>

<span data-ttu-id="fc1c0-111">此指令碼使用下列命令來建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="fc1c0-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="fc1c0-113">命令</span><span class="sxs-lookup"><span data-stu-id="fc1c0-113">Command</span></span> | <span data-ttu-id="fc1c0-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="fc1c0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fc1c0-115">az group create</span><span class="sxs-lookup"><span data-stu-id="fc1c0-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="fc1c0-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fc1c0-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="fc1c0-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="fc1c0-118">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="fc1c0-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="fc1c0-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="fc1c0-120">建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="fc1c0-121">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="fc1c0-121">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="fc1c0-122">建立網路安全性群組 (NSG)，做為網際網路和虛擬機器之間的安全性界限。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-122">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="fc1c0-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="fc1c0-123">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="fc1c0-124">建立虛擬網路卡，並將它連接至虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-124">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="fc1c0-125">az vm create</span><span class="sxs-lookup"><span data-stu-id="fc1c0-125">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="fc1c0-126">建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-126">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="fc1c0-127">此命令也會指定要使用的虛擬機器映像和管理認證。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-127">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="fc1c0-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="fc1c0-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="fc1c0-129">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fc1c0-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fc1c0-130">Next steps</span></span>

<span data-ttu-id="fc1c0-131">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fc1c0-132">您可以在 [Azure Windows VM 文件](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="fc1c0-132">Additional virtual machine CLI script samples can be found in the [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
