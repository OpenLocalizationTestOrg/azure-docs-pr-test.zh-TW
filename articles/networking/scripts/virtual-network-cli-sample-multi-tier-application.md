---
title: "aaaAzure CLI 指令碼範例-建立多層應用程式的網路 |Microsoft 文件"
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
ms.openlocfilehash: deeb3f459499cebd1b8ded6a299eb759d49cf08d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="c9f50-103">為多層式應用程式建立網路</span><span class="sxs-lookup"><span data-stu-id="c9f50-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="c9f50-104">此指令碼範例會建立一個具有前端和後端子網路的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="c9f50-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="c9f50-105">流量 toohello 前端子網路是有限的 tooHTTP 和 SSH，流量 toohello 時後端子是有限的 tooMySQL，3306 的連接埠。</span><span class="sxs-lookup"><span data-stu-id="c9f50-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="c9f50-106">執行 hello 指令碼之後, 您將擁有兩部虛擬機器，您可以部署 web 伺服器和 MySQL 軟體每個子網路的其中一個。</span><span class="sxs-lookup"><span data-stu-id="c9f50-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]


## <a name="sample-script"></a><span data-ttu-id="c9f50-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c9f50-107">Sample script</span></span>


[!code-azurecli-interactive[main](../../../cli_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.sh  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c9f50-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="c9f50-108">Clean up deployment</span></span> 

<span data-ttu-id="c9f50-109">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="c9f50-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name MyResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="c9f50-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c9f50-110">Script explanation</span></span>

<span data-ttu-id="c9f50-111">此指令碼會使用下列命令 toocreate hello 資源群組、 虛擬網路和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="c9f50-111">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="c9f50-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="c9f50-112">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="c9f50-113">命令</span><span class="sxs-lookup"><span data-stu-id="c9f50-113">Command</span></span> | <span data-ttu-id="c9f50-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="c9f50-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c9f50-115">az group create</span><span class="sxs-lookup"><span data-stu-id="c9f50-115">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="c9f50-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c9f50-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c9f50-117">az network vnet create</span><span class="sxs-lookup"><span data-stu-id="c9f50-117">az network vnet create</span></span>](/cli/azure/network/vnet#create) | <span data-ttu-id="c9f50-118">建立 Azure 虛擬網路和前端子網路。</span><span class="sxs-lookup"><span data-stu-id="c9f50-118">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="c9f50-119">az network subnet create</span><span class="sxs-lookup"><span data-stu-id="c9f50-119">az network subnet create</span></span>](/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="c9f50-120">建立後端子網路。</span><span class="sxs-lookup"><span data-stu-id="c9f50-120">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="c9f50-121">az network public-ip create</span><span class="sxs-lookup"><span data-stu-id="c9f50-121">az network public-ip create</span></span>](/cli/azure/network/public-ip#create) | <span data-ttu-id="c9f50-122">建立從 hello 網際網路的公用 IP 位址 tooaccess hello VM。</span><span class="sxs-lookup"><span data-stu-id="c9f50-122">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="c9f50-123">az network nic create</span><span class="sxs-lookup"><span data-stu-id="c9f50-123">az network nic create</span></span>](/cli/azure/network/nic#create) | <span data-ttu-id="c9f50-124">建立虛擬網路介面，並將其附加 toohello 虛擬網路的前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="c9f50-124">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c9f50-125">az network nsg create</span><span class="sxs-lookup"><span data-stu-id="c9f50-125">az network nsg create</span></span>](/cli/azure/network/nsg#create) | <span data-ttu-id="c9f50-126">建立網路安全性群組 (NSG) 相關聯的 toohello 前端和後端子網路。</span><span class="sxs-lookup"><span data-stu-id="c9f50-126">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="c9f50-127">az network nsg rule create</span><span class="sxs-lookup"><span data-stu-id="c9f50-127">az network nsg rule create</span></span>](/cli/azure/network/nsg/rule#create) |<span data-ttu-id="c9f50-128">建立 NSG 規則來允許或封鎖特定連接埠 toospecific 子網路。</span><span class="sxs-lookup"><span data-stu-id="c9f50-128">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="c9f50-129">az vm create</span><span class="sxs-lookup"><span data-stu-id="c9f50-129">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="c9f50-130">建立虛擬機器並將附加 NIC tooeach VM。</span><span class="sxs-lookup"><span data-stu-id="c9f50-130">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="c9f50-131">此命令也會指定 hello 虛擬機器映像 toouse 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="c9f50-131">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="c9f50-132">az group delete</span><span class="sxs-lookup"><span data-stu-id="c9f50-132">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="c9f50-133">刪除資源群組及其包含的所有資源。</span><span class="sxs-lookup"><span data-stu-id="c9f50-133">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c9f50-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9f50-134">Next steps</span></span>

<span data-ttu-id="c9f50-135">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c9f50-135">For more information on hello Azure CLI, see [Azure CLI documentation](/cli/azure/overview).</span></span>

<span data-ttu-id="c9f50-136">其他網路功能的 CLI 指令碼範例可以在 hello [Azure 網路概觀文件](../cli-samples.md)</span><span class="sxs-lookup"><span data-stu-id="c9f50-136">Additional networking CLI script samples can be found in hello [Azure Networking Overview documentation](../cli-samples.md)</span></span>
