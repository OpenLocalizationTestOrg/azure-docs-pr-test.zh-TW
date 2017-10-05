---
title: "Azure CLI 指令碼範例 - 建立兩個分別具有內部和外部 NSG 的 VM | Microsoft Docs"
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
ms.openlocfilehash: 7bd8c315ab0b7b3bcbbd9ebc8f17728079611f9c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="37782-103">保護虛擬機器之間的網路流量</span><span class="sxs-lookup"><span data-stu-id="37782-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="37782-104">此指令碼會建立兩部虛擬機器，並保護兩者的傳入流量。</span><span class="sxs-lookup"><span data-stu-id="37782-104">This script creates two virtual machines and secures incoming traffic to both.</span></span> <span data-ttu-id="37782-105">一部虛擬機器可在網際網路上存取，並已將網路安全性群組 (NSG) 設定為允許連接埠 22 和連接埠 80 上的流量。</span><span class="sxs-lookup"><span data-stu-id="37782-105">One virtual machine is accessible on the internet and has a network security group (NSG) configured to allow traffic on port 22 and port 80.</span></span> <span data-ttu-id="37782-106">第二部虛擬機器則無法在網際網路上存取，並已將 NSG 設定為只允許來自第一部虛擬機器的流量。</span><span class="sxs-lookup"><span data-stu-id="37782-106">The second virtual machine is not accessible on the internet, and has an NSG configured to only allow traffic from the first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="37782-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="37782-107">Sample script</span></span>

<span data-ttu-id="37782-108">[!code-azurecli-interactive[主要](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "使用 NSG 建立 VM")]</span><span class="sxs-lookup"><span data-stu-id="37782-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="37782-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="37782-109">Clean up deployment</span></span> 

<span data-ttu-id="37782-110">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="37782-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="37782-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="37782-111">Script explanation</span></span>

<span data-ttu-id="37782-112">此指令碼使用下列命令來建立資源群組、虛擬機器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="37782-112">This script uses the following commands to create a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="37782-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="37782-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="37782-114">命令</span><span class="sxs-lookup"><span data-stu-id="37782-114">Command</span></span> | <span data-ttu-id="37782-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="37782-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="37782-116">az group create</span><span class="sxs-lookup"><span data-stu-id="37782-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="37782-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="37782-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="37782-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="37782-118">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="37782-119">建立 Azure 虛擬網路和子網路。</span><span class="sxs-lookup"><span data-stu-id="37782-119">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="37782-120">az network vnet subnet create</span><span class="sxs-lookup"><span data-stu-id="37782-120">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="37782-121">建立子網路。</span><span class="sxs-lookup"><span data-stu-id="37782-121">Creates a subnet.</span></span> |
| [<span data-ttu-id="37782-122">az vm create</span><span class="sxs-lookup"><span data-stu-id="37782-122">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="37782-123">建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及 NSG。</span><span class="sxs-lookup"><span data-stu-id="37782-123">Creates the virtual machine and connects it to the network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="37782-124">此命令也會指定要使用的虛擬機器映像和管理認證。</span><span class="sxs-lookup"><span data-stu-id="37782-124">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="37782-125">az network nsg rule list</span><span class="sxs-lookup"><span data-stu-id="37782-125">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="37782-126">傳回網路安全性群組規則的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="37782-126">Returns information about a network security group rule.</span></span> <span data-ttu-id="37782-127">在此範例中，規則名稱會儲存在變數中，以供稍後在指令碼中使用。</span><span class="sxs-lookup"><span data-stu-id="37782-127">In this sample, the rule name is stored in a variable for use later in the script.</span></span> |
| [<span data-ttu-id="37782-128">az network nsg rule update</span><span class="sxs-lookup"><span data-stu-id="37782-128">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="37782-129">更新 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="37782-129">Updates an NSG rule.</span></span> <span data-ttu-id="37782-130">此範例會將後端規則更新為只傳遞來自前端子網路的流量。</span><span class="sxs-lookup"><span data-stu-id="37782-130">In this sample, the back-end rule is updated to pass through traffic only from the front-end subnet.</span></span> |
| [<span data-ttu-id="37782-131">az group delete</span><span class="sxs-lookup"><span data-stu-id="37782-131">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="37782-132">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="37782-132">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="37782-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="37782-133">Next steps</span></span>

<span data-ttu-id="37782-134">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="37782-134">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="37782-135">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="37782-135">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
