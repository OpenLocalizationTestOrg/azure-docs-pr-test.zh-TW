---
title: "Azure CLI 指令碼範例 - 建立 Docker 主機 | Microsoft Docs"
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
ms.openlocfilehash: e8704824dec66d724f2d30dab4d6bdf019c6b206
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-vm-with-docker"></a><span data-ttu-id="9c12f-103">建立含 Docker 功能的 VM</span><span class="sxs-lookup"><span data-stu-id="9c12f-103">Create a VM with Docker</span></span>

<span data-ttu-id="9c12f-104">這個指令碼會建立啟用 Docker 功能的虛擬機器，並啟動執行 NGINX 的 Docker 容器。</span><span class="sxs-lookup"><span data-stu-id="9c12f-104">This script creates a virtual machine with Docker enabled and starts a Docker container running NGINX.</span></span> <span data-ttu-id="9c12f-105">執行這個指令碼之後，您可以透過 Azure 虛擬機器的 FQDN 存取 NGINX Web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9c12f-105">After running the script, you can access the NGINX web server through the FQDN of the Azure virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9c12f-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="9c12f-106">Sample script</span></span>

<span data-ttu-id="9c12f-107">[!code-azurecli-interactive[主要](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker 主機")]</span><span class="sxs-lookup"><span data-stu-id="9c12f-107">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-docker-host/create-docker-host.sh "Docker Host")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="9c12f-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="9c12f-108">Clean up deployment</span></span> 

<span data-ttu-id="9c12f-109">執行下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="9c12f-109">Run the following command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9c12f-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="9c12f-110">Script explanation</span></span>

<span data-ttu-id="9c12f-111">此指令碼會使用下列命令來建立部署。</span><span class="sxs-lookup"><span data-stu-id="9c12f-111">This script uses the following commands to create the deployment.</span></span> <span data-ttu-id="9c12f-112">下表中的每個項目都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="9c12f-112">Each item in the table links to command specific documentation.</span></span>

| <span data-ttu-id="9c12f-113">命令</span><span class="sxs-lookup"><span data-stu-id="9c12f-113">Command</span></span> | <span data-ttu-id="9c12f-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="9c12f-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9c12f-115">az group create</span><span class="sxs-lookup"><span data-stu-id="9c12f-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9c12f-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="9c12f-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9c12f-117">az vm create</span><span class="sxs-lookup"><span data-stu-id="9c12f-117">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9c12f-118">建立虛擬機器，並將它連線到網路卡、虛擬網路、子網路及網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="9c12f-118">Creates the virtual machine and connects it to the network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="9c12f-119">此命令也會指定要使用的虛擬機器映像和管理認證。</span><span class="sxs-lookup"><span data-stu-id="9c12f-119">This command also specifies the virtual machine image to be used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="9c12f-120">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="9c12f-120">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/vm#open-port) | <span data-ttu-id="9c12f-121">建立網路安全性群組規則以允許輸入流量。</span><span class="sxs-lookup"><span data-stu-id="9c12f-121">Creates a network security group rule to allow inbound traffic.</span></span> <span data-ttu-id="9c12f-122">在此範例中，會開放連接埠 80 供 HTTP 流量使用。</span><span class="sxs-lookup"><span data-stu-id="9c12f-122">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="9c12f-123">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="9c12f-123">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9c12f-124">對 VM 新增並執行虛擬機器擴充功能。</span><span class="sxs-lookup"><span data-stu-id="9c12f-124">Adds and runs a virtual machine extension to a VM.</span></span> <span data-ttu-id="9c12f-125">在此範例中，使用 Docker VM 延伸模組來設定 Docker 主機。</span><span class="sxs-lookup"><span data-stu-id="9c12f-125">In this sample, the Docker VM extension is used to configure a Docker host.</span></span>|
| [<span data-ttu-id="9c12f-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="9c12f-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9c12f-127">刪除資源群組，包括所有巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="9c12f-127">Deletes a resource group, including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9c12f-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c12f-128">Next steps</span></span>

<span data-ttu-id="9c12f-129">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="9c12f-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9c12f-130">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="9c12f-130">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
