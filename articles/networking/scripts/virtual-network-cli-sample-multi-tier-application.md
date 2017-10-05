---
title: "Azure CLI 指令碼範例 - 為多層式應用程式建立網路 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 為多層式應用程式建立虛擬網路。"
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
ms.openlocfilehash: de65d820f2d9eea49b58185c81d815675fd76740
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="1be2b-103">為多層式應用程式建立網路</span><span class="sxs-lookup"><span data-stu-id="1be2b-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="1be2b-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="1be2b-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="1be2b-105">傳送到前端子網路的流量會限制為 HTTP 和 SSH，而傳送到後端子網路的流量則限制為 MySQL 且連接埠為 3306。</span><span class="sxs-lookup"><span data-stu-id="1be2b-105">Traffic to the front-end subnet is limited to HTTP and SSH, while traffic to the back-end subnet is limited to MySQL, port 3306.</span></span> <span data-ttu-id="1be2b-106">執行此指令碼之後，您將有兩部虛擬機器，每個子網路中各有一部，可供您在其中部署 Web 伺服器和 MySQL 軟體。</span><span class="sxs-lookup"><span data-stu-id="1be2b-106">After running the script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="1be2b-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="1be2b-107">Sample script</span></span>


<span data-ttu-id="1be2b-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "多層式應用程式的虛擬網路")]</span><span class="sxs-lookup"><span data-stu-id="1be2b-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="1be2b-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="1be2b-109">Clean up deployment</span></span> 

<span data-ttu-id="1be2b-110">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="1be2b-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="1be2b-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="1be2b-111">Script explanation</span></span>

<span data-ttu-id="1be2b-112">此指令碼會使用下列命令來建立資源群組、虛擬網路及網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="1be2b-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="1be2b-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="1be2b-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="1be2b-114">命令</span><span class="sxs-lookup"><span data-stu-id="1be2b-114">Command</span></span> | <span data-ttu-id="1be2b-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="1be2b-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="1be2b-116">az group create</span><span class="sxs-lookup"><span data-stu-id="1be2b-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="1be2b-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="1be2b-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="1be2b-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="1be2b-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="1be2b-119">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="1be2b-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="1be2b-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="1be2b-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="1be2b-121">建立後端子網路。</span><span class="sxs-lookup"><span data-stu-id="1be2b-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="1be2b-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="1be2b-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="1be2b-123">建立公用 IP 位址以從網際網路存取 VM。</span><span class="sxs-lookup"><span data-stu-id="1be2b-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="1be2b-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="1be2b-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="1be2b-125">建立虛擬網路介面，並將它們連結到虛擬網路的前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="1be2b-125">Creates virtual network interfaces and attaches them to the virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="1be2b-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="1be2b-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="1be2b-127">建立與前端和後端子網路關聯的網路安全性群組 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="1be2b-127">Creates network security groups (NSG) that are associated to the front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="1be2b-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="1be2b-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="1be2b-129">建立對特定子網路允許或封鎖特定連接埠的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="1be2b-129">Creates NSG rules that allow or block specific ports to specific subnets.</span></span> |
| [<span data-ttu-id="1be2b-130">az vm create</span><span class="sxs-lookup"><span data-stu-id="1be2b-130">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="1be2b-131">建立虛擬機器，並將 NIC 連結到每個 VM。</span><span class="sxs-lookup"><span data-stu-id="1be2b-131">Creates virtual machines and attaches a NIC to each VM.</span></span> <span data-ttu-id="1be2b-132">此命令也會指定要使用的虛擬機器映像和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="1be2b-132">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="1be2b-133">az group delete</span><span class="sxs-lookup"><span data-stu-id="1be2b-133">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="1be2b-134">刪除資源群組及其包含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="1be2b-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="1be2b-135">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1be2b-135">Next steps</span></span>

<span data-ttu-id="1be2b-136">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="1be2b-136">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="1be2b-137">您可以在 [Azure 網路概觀文件](../cli-samples.md)中找到其他網路 CLI 指令碼範例</span><span class="sxs-lookup"><span data-stu-id="1be2b-137">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>