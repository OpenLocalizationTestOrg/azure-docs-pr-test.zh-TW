---
title: "Azure CLI 指令碼範例 - 建立 Linux VM | Microsoft Docs"
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
ms.openlocfilehash: dc7e7276bcea32c59c67a42dedaffcedfd0cf907
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-fully-configured-virtual-machine"></a><span data-ttu-id="a26d8-103">建立完整設定的虛擬機器</span><span class="sxs-lookup"><span data-stu-id="a26d8-103">Create a fully configured virtual machine</span></span>

<span data-ttu-id="a26d8-104">此指令碼會建立具有 Ubuntu 作業系統的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a26d8-104">This script creates an Azure Virtual Machine with an Ubuntu operating system.</span></span> <span data-ttu-id="a26d8-105">執行指令碼之後，您可以透過 SSH 存取虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a26d8-105">After running the script, you can access the virtual machine over SSH.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="a26d8-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="a26d8-106">Sample script</span></span>

<span data-ttu-id="a26d8-107">[!code-azurecli-interactive[主要](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "快速建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="a26d8-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-detailed/create-vm-detailed.sh "Quick Create VM")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="a26d8-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="a26d8-108">Clean up deployment</span></span> 

<span data-ttu-id="a26d8-109">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="a26d8-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="a26d8-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="a26d8-110">Script explanation</span></span>

<span data-ttu-id="a26d8-111">此指令碼使用下列命令來建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="a26d8-111">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="a26d8-112">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="a26d8-112">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="a26d8-113">命令</span><span class="sxs-lookup"><span data-stu-id="a26d8-113">Command</span></span> | <span data-ttu-id="a26d8-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="a26d8-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="a26d8-115">az group create</span><span class="sxs-lookup"><span data-stu-id="a26d8-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="a26d8-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="a26d8-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="a26d8-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="a26d8-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="a26d8-118">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="a26d8-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="a26d8-119">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="a26d8-119">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="a26d8-120">建立具有靜態 IP 位址和相關聯 DNS 名稱的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="a26d8-120">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="a26d8-121">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="a26d8-121">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="a26d8-122">建立網路安全性群組 (NSG)，做為網際網路和虛擬機器之間的安全性界限。</span><span class="sxs-lookup"><span data-stu-id="a26d8-122">Creates a network security group (NSG), which is a security boundary between the internet and the virtual machine.</span></span> |
| [<span data-ttu-id="a26d8-123">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="a26d8-123">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="a26d8-124">建立允許輸入流量的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="a26d8-124">Creates an NSG rule to allow inbound traffic.</span></span> <span data-ttu-id="a26d8-125">在此範例中，會開放連接埠 22 供 SSH 流量使用。</span><span class="sxs-lookup"><span data-stu-id="a26d8-125">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="a26d8-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="a26d8-126">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="a26d8-127">建立虛擬網路卡，並將它連接至虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="a26d8-127">Creates a virtual network card and attaches it to the virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="a26d8-128">az vm create</span><span class="sxs-lookup"><span data-stu-id="a26d8-128">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="a26d8-129">建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="a26d8-129">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="a26d8-130">此命令也會指定要使用的虛擬機器映像和管理認證。</span><span class="sxs-lookup"><span data-stu-id="a26d8-130">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="a26d8-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="a26d8-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="a26d8-132">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="a26d8-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="a26d8-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a26d8-133">Next steps</span></span>

<span data-ttu-id="a26d8-134">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="a26d8-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="a26d8-135">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="a26d8-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
