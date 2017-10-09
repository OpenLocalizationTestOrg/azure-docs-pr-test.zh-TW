---
title: "CLI 指令碼範例-aaaAzure 建立 Docker 主機 |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 建立 Docker 主機"
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
ms.date: 03/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 7df2561c428ff5d3ab0a0d53c8e046781996be77
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="c577c-103">建立含 Docker 功能的 VM</span><span class="sxs-lookup"><span data-stu-id="c577c-103">Create a VM with Docker</span></span>

<span data-ttu-id="c577c-104">這個指令碼會建立啟用 Docker 功能的虛擬機器，並啟動執行 NGINX 的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="c577c-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="c577c-105">執行 hello 指令碼之後, 您可以透過 hello hello Azure 虛擬機器的 FQDN 存取 hello NGINX 網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="c577c-105">After running hello script, you can access hello NGINX web server through hello FQDN of hello Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c577c-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c577c-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]

## <a name="clean-up-deployment"></a><span data-ttu-id="c577c-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="c577c-107">Clean up deployment</span></span> 

<span data-ttu-id="c577c-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="c577c-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c577c-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c577c-109">Script explanation</span></span>

<span data-ttu-id="c577c-110">此指令碼會使用下列命令 toocreate hello 部署的 hello。</span><span class="sxs-lookup"><span data-stu-id="c577c-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="c577c-111">Hello 資料表中的每個項目連結 toocommand 特定文件。</span><span class="sxs-lookup"><span data-stu-id="c577c-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c577c-112">命令</span><span class="sxs-lookup"><span data-stu-id="c577c-112">Command</span></span> | <span data-ttu-id="c577c-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="c577c-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c577c-114">az group create</span><span class="sxs-lookup"><span data-stu-id="c577c-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c577c-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c577c-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c577c-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="c577c-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c577c-117">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="c577c-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="c577c-118">此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="c577c-118">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="c577c-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="c577c-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="c577c-120">建立網路安全性群組規則 tooallow 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="c577c-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="c577c-121">在此範例中，會開放連接埠 80 供 HTTP 流量使用。</span><span class="sxs-lookup"><span data-stu-id="c577c-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="c577c-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="c577c-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c577c-123">新增並執行虛擬機器擴充功能 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="c577c-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="c577c-124">在此範例中，hello Docker VM 擴充功能是使用的 tooconfigure Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="c577c-124">In this sample, hello Docker VM extension is used tooconfigure a Docker host.</span></span>|
| [<span data-ttu-id="c577c-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="c577c-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c577c-126">刪除資源群組，包括所有巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="c577c-126">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c577c-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c577c-127">Next steps</span></span>

<span data-ttu-id="c577c-128">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c577c-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c577c-129">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c577c-129">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
