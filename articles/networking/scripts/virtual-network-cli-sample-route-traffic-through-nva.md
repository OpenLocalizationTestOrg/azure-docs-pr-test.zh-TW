---
title: "Azure CLI 指令碼範例 - 透過網路虛擬設備來路由傳送流量 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 透過防火牆網路虛擬設備來路由傳送流量。"
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
ms.openlocfilehash: 78091b515c00591a4af8d807945475b6be50188a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="22c77-103">透過網路虛擬設備來路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="22c77-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="22c77-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="22c77-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="22c77-105">它也會建立一個已啟用 IP 轉送功能的 VM，以在兩個子網路之間路由傳送流量。</span><span class="sxs-lookup"><span data-stu-id="22c77-105">It also creates a VM with IP forwarding enabled to route traffic between the two subnets.</span></span> <span data-ttu-id="22c77-106">執行此指令碼之後，您可以將網路軟體 (例如防火牆應用程式) 部署到 VM。</span><span class="sxs-lookup"><span data-stu-id="22c77-106">After running the script you can deploy network software, such as a firewall application, to the VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="22c77-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="22c77-107">Sample script</span></span>


<span data-ttu-id="22c77-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "透過網路虛擬設備來路由傳送流量")]</span><span class="sxs-lookup"><span data-stu-id="22c77-108">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="22c77-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="22c77-109">Clean up deployment</span></span> 

<span data-ttu-id="22c77-110">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="22c77-110">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="22c77-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="22c77-111">Script explanation</span></span>

<span data-ttu-id="22c77-112">此指令碼會使用下列命令來建立資源群組、虛擬網路及網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="22c77-112">This script uses the following commands to create a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="22c77-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="22c77-113">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="22c77-114">命令</span><span class="sxs-lookup"><span data-stu-id="22c77-114">Command</span></span> | <span data-ttu-id="22c77-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="22c77-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="22c77-116">az group create</span><span class="sxs-lookup"><span data-stu-id="22c77-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="22c77-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="22c77-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="22c77-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="22c77-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="22c77-119">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="22c77-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="22c77-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="22c77-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="22c77-121">建立後端和 DMZ 子網路。</span><span class="sxs-lookup"><span data-stu-id="22c77-121">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="22c77-122">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="22c77-122">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="22c77-123">建立公用 IP 位址以從網際網路存取 VM。</span><span class="sxs-lookup"><span data-stu-id="22c77-123">Creates a public IP address to access the VM from the Internet.</span></span> |
| [<span data-ttu-id="22c77-124">az network nic create</span><span class="sxs-lookup"><span data-stu-id="22c77-124">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="22c77-125">建立虛擬網路介面並為它啟用 IP 轉送功能。</span><span class="sxs-lookup"><span data-stu-id="22c77-125">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="22c77-126">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="22c77-126">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="22c77-127">建立網路安全性群組 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="22c77-127">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="22c77-128">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="22c77-128">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="22c77-129">建立允許對 VM 進行 HTTP 和 HTTPS 連接埠輸入的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="22c77-129">Creates NSG rules that allow HTTP and HTTPS ports inbound to the VM.</span></span> |
| [<span data-ttu-id="22c77-130">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="22c77-130">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="22c77-131">將 NSG 和路由表與子網路建立關聯。</span><span class="sxs-lookup"><span data-stu-id="22c77-131">Associates the NSGs and route tables to subnets.</span></span> |
| [<span data-ttu-id="22c77-132">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="22c77-132">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="22c77-133">為所有路由建立一個路由表。</span><span class="sxs-lookup"><span data-stu-id="22c77-133">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="22c77-134">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="22c77-134">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="22c77-135">建立路由，以透過 VM 在子網路與網際網路之間路由傳送流量。</span><span class="sxs-lookup"><span data-stu-id="22c77-135">Creates routes to route traffic between subnets and the Internet through the VM.</span></span> |
| [<span data-ttu-id="22c77-136">az vm create</span><span class="sxs-lookup"><span data-stu-id="22c77-136">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="22c77-137">建立虛擬機器，並將 NIC 連結到此虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="22c77-137">Creates a virtual machine and attaches the NIC to it.</span></span> <span data-ttu-id="22c77-138">此命令也會指定要使用的虛擬機器映像和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="22c77-138">This command also specifies the virtual machine image to use and administrative credentials.</span></span> |
| [<span data-ttu-id="22c77-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="22c77-139">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="22c77-140">刪除資源群組及其包含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="22c77-140">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="22c77-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22c77-141">Next steps</span></span>

<span data-ttu-id="22c77-142">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="22c77-142">For more information on the Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="22c77-143">您可以在 [Azure 網路概觀文件](../cli-samples.md)中找到其他網路 CLI 指令碼範例</span><span class="sxs-lookup"><span data-stu-id="22c77-143">Additional networking CLI script samples can be found in the [Azure Networking Overview documentation](../cli-samples.md)</span></span>