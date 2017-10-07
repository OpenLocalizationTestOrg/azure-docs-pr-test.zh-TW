---
title: "aaaAzure CLI 指令碼範例篩選條件的 VM 網路流量 |Microsoft 文件"
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
ms.openlocfilehash: c2f14e54bc96c99420b4300d1c24a457ac8c948c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="filter-inbound-and-outbound-vm-network-traffic"></a><span data-ttu-id="2c5a8-103">篩選輸入和輸出 VM 網路流量</span><span class="sxs-lookup"><span data-stu-id="2c5a8-103">Filter inbound and outbound VM network traffic</span></span>

<span data-ttu-id="2c5a8-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="2c5a8-105">輸入網路流量 toohello 前端子網路是有限的 tooHTTP、 HTTPS 和 SSH 時傳出流量的 toohello 不允許網際網路從 hello 後端子。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-105">Inbound network traffic toohello front-end subnet is limited tooHTTP, HTTPS and SSH, while outbound traffic toohello Internet from hello back-end subnet is not permitted.</span></span> <span data-ttu-id="2c5a8-106">執行 hello 指令碼之後，您必須有兩個 Nic 的一部虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-106">After running hello script, you will have one virtual machine with two NICs.</span></span> <span data-ttu-id="2c5a8-107">每個 NIC 已連線的 tooa 不同的子網路。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-107">Each NIC is connected tooa different subnet.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="2c5a8-108">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="2c5a8-108">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/filter-network-traffic/filter-network-traffic.sh  "Filter VM network traffic")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2c5a8-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="2c5a8-109">Clean up deployment</span></span> 

<span data-ttu-id="2c5a8-110">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="2c5a8-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="2c5a8-111">Script explanation</span></span>

<span data-ttu-id="2c5a8-112">此指令碼會使用下列命令 toocreate hello 資源群組、 虛擬網路和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="2c5a8-113">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="2c5a8-114">命令</span><span class="sxs-lookup"><span data-stu-id="2c5a8-114">Command</span></span> | <span data-ttu-id="2c5a8-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="2c5a8-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2c5a8-116">az group create</span><span class="sxs-lookup"><span data-stu-id="2c5a8-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="2c5a8-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2c5a8-118">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="2c5a8-118">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="2c5a8-119">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="2c5a8-120">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="2c5a8-120">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="2c5a8-121">建立後端子網路。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="2c5a8-122">az network vnet subnet update</span><span class="sxs-lookup"><span data-stu-id="2c5a8-122">az network vnet subnet update</span></span>](/cli/azure/network/vnet/subnet#update) | <span data-ttu-id="2c5a8-123">將關聯 Nsg toosubnets。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-123">Associates NSGs toosubnets.</span></span> |
| [<span data-ttu-id="2c5a8-124">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="2c5a8-124">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="2c5a8-125">建立從 hello 網際網路的公用 IP 位址 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-125">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="2c5a8-126">az network nic create</span><span class="sxs-lookup"><span data-stu-id="2c5a8-126">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="2c5a8-127">建立虛擬網路介面，並將其附加 toohello 虛擬網路的前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-127">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="2c5a8-128">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="2c5a8-128">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="2c5a8-129">建立網路安全性群組 (NSG) 相關聯的 toohello 前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-129">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="2c5a8-130">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="2c5a8-130">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="2c5a8-131">建立 NSG 規則來允許或封鎖特定連接埠 toospecific 子網路。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-131">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="2c5a8-132">az vm create</span><span class="sxs-lookup"><span data-stu-id="2c5a8-132">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="2c5a8-133">建立虛擬機器並將附加 NIC tooeach VM。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-133">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="2c5a8-134">此命令也會指定 hello 虛擬機器映像 toouse 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-134">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="2c5a8-135">az group delete</span><span class="sxs-lookup"><span data-stu-id="2c5a8-135">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="2c5a8-136">刪除資源群組及其包含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-136">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2c5a8-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2c5a8-137">Next steps</span></span>

<span data-ttu-id="2c5a8-138">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="2c5a8-138">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="2c5a8-139">其他網路功能的 CLI 指令碼範例可以在 hello [Azure 網路概觀文件](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="2c5a8-139">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
