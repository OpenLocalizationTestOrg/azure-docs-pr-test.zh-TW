---
title: "aaaAzure CLI 指令碼範例-使用 NGINX 建立 Linux VM |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 使用 NGINX 建立 Linux VM"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 9166ccfd4f2e6eea731a8dc6956575d9f8f85488
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-nginx"></a><span data-ttu-id="c9608-103">使用 NGINX 建立 VM</span><span class="sxs-lookup"><span data-stu-id="c9608-103">Create a VM with NGINX</span></span>

<span data-ttu-id="c9608-104">此指令碼會建立 Azure 虛擬機器，並使用 hello Azure 虛擬機器自訂指令碼擴充 tooinstall NGINX。</span><span class="sxs-lookup"><span data-stu-id="c9608-104">This script creates an Azure Virtual Machine and uses hello Azure Virtual Machine Custom Script Extension tooinstall NGINX.</span></span> <span data-ttu-id="c9608-105">執行 hello 指令碼之後, 您可以存取示範網站 hello 虛擬機器的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="c9608-105">After running hello script, you can access a demo website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="c9608-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="c9608-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nginx/create-vm-nginx.sh "Quick Create VM")]

## <a name="custom-script-extension"></a><span data-ttu-id="c9608-107">自訂指令碼延伸模組</span><span class="sxs-lookup"><span data-stu-id="c9608-107">Custom Script Extension</span></span>

<span data-ttu-id="c9608-108">hello 自訂指令碼延伸模組複製到 hello 虛擬機器上的此指令碼。</span><span class="sxs-lookup"><span data-stu-id="c9608-108">hello custom script extension copies this script onto hello virtual machine.</span></span> <span data-ttu-id="c9608-109">hello 指令碼接著會執行 tooinstall 和 NGINX 網頁伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="c9608-109">hello script is then run tooinstall and configure an NGINX web server.</span></span> 

```bash
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="clean-up-deployment"></a><span data-ttu-id="c9608-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="c9608-110">Clean up deployment</span></span> 

<span data-ttu-id="c9608-111">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="c9608-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="c9608-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="c9608-112">Script explanation</span></span>

<span data-ttu-id="c9608-113">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="c9608-113">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="c9608-114">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="c9608-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="c9608-115">命令</span><span class="sxs-lookup"><span data-stu-id="c9608-115">Command</span></span> | <span data-ttu-id="c9608-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="c9608-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="c9608-117">az group create</span><span class="sxs-lookup"><span data-stu-id="c9608-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="c9608-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="c9608-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="c9608-119">az vm create</span><span class="sxs-lookup"><span data-stu-id="c9608-119">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="c9608-120">建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="c9608-120">Creates hello virtual machine.</span></span> <span data-ttu-id="c9608-121">此命令也會指定使用，hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="c9608-121">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="c9608-122">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="c9608-122">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="c9608-123">建立網路安全性群組規則 tooallow 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="c9608-123">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="c9608-124">在此範例中，會開放連接埠 80 供 HTTP 流量使用。</span><span class="sxs-lookup"><span data-stu-id="c9608-124">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="c9608-125">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="c9608-125">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c9608-126">新增並執行虛擬機器擴充功能 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="c9608-126">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="c9608-127">在此範例中，hello 自訂指令碼延伸模組是使用的 tooinstall NGINX。</span><span class="sxs-lookup"><span data-stu-id="c9608-127">In this sample, hello custom script extension is used tooinstall NGINX.</span></span>|
| [<span data-ttu-id="c9608-128">az group delete</span><span class="sxs-lookup"><span data-stu-id="c9608-128">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="c9608-129">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="c9608-129">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="c9608-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c9608-130">Next steps</span></span>

<span data-ttu-id="c9608-131">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="c9608-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="c9608-132">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c9608-132">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
