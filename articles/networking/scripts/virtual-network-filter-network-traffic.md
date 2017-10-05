---
title: "Azure CLI 指令碼範例 - 篩選 VM 網路流量 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 篩選輸入和輸出 VM 網路流量。"
services: virtual-network
documentationcenter: virtual-network
author: jimdial
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: jdial
ms.openlocfilehash: 68ee013cff4e0be15af30239e0314f779f50177a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="fd1a4-103">篩選輸入和輸出 VM 網路流量</span><span class="sxs-lookup"><span data-stu-id="fd1a4-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="fd1a4-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="fd1a4-105">傳送到前端子網路的輸入流量會限制為 HTTP、HTTPS 及 SSH，而從後端子網路傳送到網際網路的輸出流量則不受允許。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-105">Inbound network traffic to the front-end subnet is limited to HTTP, HTTPS and SSH, while outbound traffic to the Internet from the back-end subnet is not permitted.</span></span> <span data-ttu-id="fd1a4-106">執行此指令碼之後，您將會有一部具有兩個 NIC 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-106">After running the script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="fd1a4-107">每個 NIC 會連線到不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-107">Each NIC is connected to a different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fd1a4-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="fd1a4-108">Sample script</span></span>


<span data-ttu-id="fd1a4-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "篩選 VM 網路流量")]</span><span class="sxs-lookup"><span data-stu-id="fd1a4-109">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="fd1a4-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="fd1a4-110">Clean up deployment</span></span> 

<span data-ttu-id="fd1a4-111">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-111">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="fd1a4-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="fd1a4-112">Script explanation</span></span>

<span data-ttu-id="fd1a4-113">此指令碼會使用下列命令來建立資源群組、虛擬網路及網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-113">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="fd1a4-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-114">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="fd1a4-115">命令</span><span class="sxs-lookup"><span data-stu-id="fd1a4-115">Command</span></span> | <span data-ttu-id="fd1a4-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="fd1a4-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fd1a4-117">az group create</span><span class="sxs-lookup"><span data-stu-id="fd1a4-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="fd1a4-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="fd1a4-119">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="fd1a4-119">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="fd1a4-120">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-120">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="fd1a4-121">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="fd1a4-121">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="fd1a4-122">建立後端子網路。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-122">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="fd1a4-123">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="fd1a4-123">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="fd1a4-124">將 NSG 與子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-124">Associates NSGs to subnets.</span></span> |
| [<span data-ttu-id="fd1a4-125">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="fd1a4-125">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="fd1a4-126">建立公用 IP 位址以從網際網路存取 VM。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-126">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="fd1a4-127">az network nic create</span><span class="sxs-lookup"><span data-stu-id="fd1a4-127">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="fd1a4-128">建立虛擬網路介面，並將它們連結到虛擬網路的前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-128">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="fd1a4-129">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="fd1a4-129">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="fd1a4-130">建立與前端和後端子網路關聯的網路安全性群組 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-130">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="fd1a4-131">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="fd1a4-131">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="fd1a4-132">建立對特定子網路允許或封鎖特定連接埠的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-132">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="fd1a4-133">az vm create</span><span class="sxs-lookup"><span data-stu-id="fd1a4-133">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="fd1a4-134">建立虛擬機器，並將 NIC 連結到每個 VM。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-134">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="fd1a4-135">此命令也會指定要使用的虛擬機器映像和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-135">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="fd1a4-136">az group delete</span><span class="sxs-lookup"><span data-stu-id="fd1a4-136">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="fd1a4-137">刪除資源群組及其包含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-137">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="fd1a4-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="fd1a4-138">Next steps</span></span>

<span data-ttu-id="fd1a4-139">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="fd1a4-139">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="fd1a4-140">您可以在 [Azure 網路概觀文件](../cli-samples.md)中找到其他網路 CLI 指令碼範例</span><span class="sxs-lookup"><span data-stu-id="fd1a4-140">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>