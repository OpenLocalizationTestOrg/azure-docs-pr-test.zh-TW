---
title: "aaaAzure CLI 指令碼範例透過網路的虛擬設備的路由傳送流量 |Microsoft 文件"
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
ms.openlocfilehash: 981d6073be04a7ebaf96b657fbab8a378e7a995e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="route-traffic-through-a-network-virtual-appliance"></a><span data-ttu-id="f122d-103">透過網路虛擬設備來路由傳送流量</span><span class="sxs-lookup"><span data-stu-id="f122d-103">Route traffic through a network virtual appliance</span></span>

<span data-ttu-id="f122d-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="f122d-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="f122d-105">它也會將啟用的 tooroute 流量 hello 兩個子網路之間轉送 ip 建立 VM。</span><span class="sxs-lookup"><span data-stu-id="f122d-105">It also creates a VM with IP forwarding enabled tooroute traffic between hello two subnets.</span></span> <span data-ttu-id="f122d-106">執行 hello 指令碼之後，您可以部署網路的軟體，例如防火牆應用程式，toohello VM。</span><span class="sxs-lookup"><span data-stu-id="f122d-106">After running hello script you can deploy network software, such as a firewall application, toohello VM.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="f122d-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="f122d-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/route-traffic-through-nva/route-traffic-through-nva.sh "Route traffic through a network virtual appliance")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f122d-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="f122d-108">Clean up deployment</span></span> 

<span data-ttu-id="f122d-109">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="f122d-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="f122d-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="f122d-110">Script explanation</span></span>

<span data-ttu-id="f122d-111">此指令碼會使用下列命令 toocreate hello 資源群組、 虛擬網路和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="f122d-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="f122d-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="f122d-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="f122d-113">命令</span><span class="sxs-lookup"><span data-stu-id="f122d-113">Command</span></span> | <span data-ttu-id="f122d-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="f122d-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f122d-115">az group create</span><span class="sxs-lookup"><span data-stu-id="f122d-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="f122d-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f122d-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f122d-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="f122d-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="f122d-118">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="f122d-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="f122d-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="f122d-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="f122d-120">建立後端和 DMZ 子網路。</span><span class="sxs-lookup"><span data-stu-id="f122d-120">Creates back-end and DMZ subnets.</span></span> |
| [<span data-ttu-id="f122d-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="f122d-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="f122d-122">建立從 hello 網際網路的公用 IP 位址 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="f122d-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="f122d-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="f122d-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="f122d-124">建立虛擬網路介面並為它啟用 IP 轉送功能。</span><span class="sxs-lookup"><span data-stu-id="f122d-124">Creates a virtual network interface and enable IP forwarding for it.</span></span> |
| [<span data-ttu-id="f122d-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="f122d-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="f122d-126">建立網路安全性群組 (NSG)。</span><span class="sxs-lookup"><span data-stu-id="f122d-126">Creates a network security group (NSG).</span></span> |
| [<span data-ttu-id="f122d-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="f122d-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) | <span data-ttu-id="f122d-128">建立允許 HTTP 和 HTTPS 連接埠輸入 toohello VM 的 NSG 規則。</span><span class="sxs-lookup"><span data-stu-id="f122d-128">Creates NSG rules that allow HTTP and HTTPS ports inbound toohello VM.</span></span> |
| [<span data-ttu-id="f122d-129">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="f122d-129">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update)| <span data-ttu-id="f122d-130">路由資料表 toosubnets 和相關聯 hello Nsg。</span><span class="sxs-lookup"><span data-stu-id="f122d-130">Associates hello NSGs and route tables toosubnets.</span></span> |
| [<span data-ttu-id="f122d-131">az network route-table create</span><span class="sxs-lookup"><span data-stu-id="f122d-131">az network route-table create</span></span>](/cli/azure/network/route-table#create)| <span data-ttu-id="f122d-132">為所有路由建立一個路由表。</span><span class="sxs-lookup"><span data-stu-id="f122d-132">Creates a route table for all routes.</span></span> |
| [<span data-ttu-id="f122d-133">az network route-table route create</span><span class="sxs-lookup"><span data-stu-id="f122d-133">az network route-table route create</span></span>](/cli/azure/network/route-table/route#create)| <span data-ttu-id="f122d-134">建立路由 tooroute hello 網際網路透過 hello VM 子網路之間的流量。</span><span class="sxs-lookup"><span data-stu-id="f122d-134">Creates routes tooroute traffic between subnets and hello Internet through hello VM.</span></span> |
| [<span data-ttu-id="f122d-135">az vm create</span><span class="sxs-lookup"><span data-stu-id="f122d-135">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="f122d-136">建立虛擬機器，並附加 hello NIC tooit。</span><span class="sxs-lookup"><span data-stu-id="f122d-136">Creates a virtual machine and attaches hello NIC tooit.</span></span> <span data-ttu-id="f122d-137">此命令也會指定 hello 虛擬機器映像 toouse 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="f122d-137">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="f122d-138">az group delete</span><span class="sxs-lookup"><span data-stu-id="f122d-138">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="f122d-139">刪除資源群組及其包含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="f122d-139">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f122d-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f122d-140">Next steps</span></span>

<span data-ttu-id="f122d-141">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f122d-141">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="f122d-142">其他網路功能的 CLI 指令碼範例可以在 hello [Azure 網路概觀文件](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="f122d-142">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
