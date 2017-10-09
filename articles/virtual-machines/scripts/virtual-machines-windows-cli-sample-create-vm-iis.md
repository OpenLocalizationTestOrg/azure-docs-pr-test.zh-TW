---
title: "aaaAzure CLI 指令碼範例的安裝 IIS |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 安裝 IIS"
services: virtual-machines-Windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-machines-Windows
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-Windows
ms.workload: infrastructure
ms.date: 02/28/2017
ms.author: nepeters
ms.openlocfilehash: 2fabc9522f424cab4c672084ba8bedfd623c87cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="quick-create-a-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="f807a-103">快速建立虛擬機器以 hello Azure CLI</span><span class="sxs-lookup"><span data-stu-id="f807a-103">Quick Create a virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="f807a-104">此指令碼建立執行 Windows Server 2016 的 Azure 虛擬機器，並使用 hello Azure 虛擬機器自訂指令碼擴充 tooinstall IIS。</span><span class="sxs-lookup"><span data-stu-id="f807a-104">This script creates an Azure Virtual Machine running Windows Server 2016, and uses hello Azure Virtual Machine Custom Script Extension tooinstall IIS.</span></span> <span data-ttu-id="f807a-105">執行 hello 指令碼之後, 您可以存取 hello 預設 IIS 網站上 hello 虛擬機器的 hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="f807a-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f807a-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="f807a-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-windows-iis/create-vm-windows-iis.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="f807a-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="f807a-107">Clean up deployment</span></span> 

<span data-ttu-id="f807a-108">執行下列命令 tooremove hello 資源群組、 VM 和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="f807a-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup --yes
```

## <a name="script-explanation"></a><span data-ttu-id="f807a-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="f807a-109">Script explanation</span></span>

<span data-ttu-id="f807a-110">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器的 hello 和所有相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="f807a-110">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="f807a-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="f807a-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f807a-112">命令</span><span class="sxs-lookup"><span data-stu-id="f807a-112">Command</span></span> | <span data-ttu-id="f807a-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="f807a-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f807a-114">az group create</span><span class="sxs-lookup"><span data-stu-id="f807a-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="f807a-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="f807a-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="f807a-116">az vm create</span><span class="sxs-lookup"><span data-stu-id="f807a-116">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="f807a-117">建立 hello 虛擬機器，並將它連接 toohello 網路卡、 虛擬網路、 子網路和網路安全性群組。</span><span class="sxs-lookup"><span data-stu-id="f807a-117">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and network security group.</span></span> <span data-ttu-id="f807a-118">此命令也會指定使用 hello 虛擬機器映像 toobe 和系統管理認證。</span><span class="sxs-lookup"><span data-stu-id="f807a-118">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="f807a-119">az vm open-port</span><span class="sxs-lookup"><span data-stu-id="f807a-119">az vm open-port</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="f807a-120">建立網路安全性群組規則 tooallow 輸入流量。</span><span class="sxs-lookup"><span data-stu-id="f807a-120">Creates a network security group rule tooallow inbound traffic.</span></span> <span data-ttu-id="f807a-121">在此範例中，會開放連接埠 80 供 HTTP 流量使用。</span><span class="sxs-lookup"><span data-stu-id="f807a-121">In this sample, port 80 is opened for HTTP traffic.</span></span> |
| [<span data-ttu-id="f807a-122">azure vm extension set</span><span class="sxs-lookup"><span data-stu-id="f807a-122">azure vm extension set</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f807a-123">新增並執行虛擬機器擴充功能 tooa VM。</span><span class="sxs-lookup"><span data-stu-id="f807a-123">Adds and runs a virtual machine extension tooa VM.</span></span> <span data-ttu-id="f807a-124">在此範例中，hello 自訂指令碼延伸模組是使用的 tooinstall IIS。</span><span class="sxs-lookup"><span data-stu-id="f807a-124">In this sample, hello custom script extension is used tooinstall IIS.</span></span>|
| [<span data-ttu-id="f807a-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="f807a-125">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="f807a-126">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="f807a-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f807a-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f807a-127">Next steps</span></span>

<span data-ttu-id="f807a-128">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="f807a-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="f807a-129">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Windows VM 文件](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f807a-129">Additional virtual machine CLI script samples can be found in hello [Azure Windows VM documentation](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
