---
title: "CLI 指令碼範例-aaaAzure 部署 hello Load-Balanced 虛擬 Machin 規模集中的 LAMP 堆疊 |Microsoft 文件"
description: "使用自訂指令碼延伸 toodeploy hello LAMP 堆疊中的負載平衡的虛擬機器擴展集在 Azure 上的 =。"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: allclark
manager: douge
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/05/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: d5278db809faaa0997a08b00a53387d754fce3d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-hello-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="de3be-103">部署負載平衡的虛擬機器規模集中的 hello LAMP 堆疊</span><span class="sxs-lookup"><span data-stu-id="de3be-103">Deploy hello LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="de3be-104">這個範例會建立虛擬機器規模集，並套用 hello 規模集中的每部虛擬機器執行自訂指令碼 toodeploy hello LAMP 堆疊的擴充功能。</span><span class="sxs-lookup"><span data-stu-id="de3be-104">This example creates a virtual machine scale set and applies an extension that runs a custom script toodeploy hello LAMP stack on each virtual machine in hello scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="de3be-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="de3be-105">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]

## <a name="connect"></a><span data-ttu-id="de3be-106">連線</span><span class="sxs-lookup"><span data-stu-id="de3be-106">Connect</span></span>

<span data-ttu-id="de3be-107">使用此程式碼 toosee，tooconnect tooyour Vm 和您的小數位數的設定。</span><span class="sxs-lookup"><span data-stu-id="de3be-107">Use this code toosee how tooconnect tooyour VMs and your scale set.</span></span>

[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access hello virtual machine scale set")]

## <a name="clean-up-deployment"></a><span data-ttu-id="de3be-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="de3be-108">Clean up deployment</span></span> 

<span data-ttu-id="de3be-109">執行下列命令 tooremove hello 資源群組、 hello 擴展集 Vm，以及所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="de3be-109">Run hello following command tooremove hello resource group, hello scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="de3be-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="de3be-110">Script explanation</span></span>

<span data-ttu-id="de3be-111">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器、 可用性設定組中，負載平衡器和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="de3be-111">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="de3be-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="de3be-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="de3be-113">命令</span><span class="sxs-lookup"><span data-stu-id="de3be-113">Command</span></span> | <span data-ttu-id="de3be-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="de3be-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="de3be-115">az group create</span><span class="sxs-lookup"><span data-stu-id="de3be-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="de3be-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="de3be-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="de3be-117">az vmss create</span><span class="sxs-lookup"><span data-stu-id="de3be-117">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="de3be-118">建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="de3be-118">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="de3be-119">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="de3be-119">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="de3be-120">新增負載平衡端點</span><span class="sxs-lookup"><span data-stu-id="de3be-120">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="de3be-121">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="de3be-121">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="de3be-122">建立 hello 自訂指令碼執行的 VM 部署的 hello 擴充功能</span><span class="sxs-lookup"><span data-stu-id="de3be-122">Create hello extension that runs hello custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="de3be-123">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="de3be-123">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="de3be-124">套用 hello 延伸模組之前，已部署的 hello VM 執行個體上執行自訂指令碼 hello toohello 規模集。</span><span class="sxs-lookup"><span data-stu-id="de3be-124">Run hello custom script on hello VM instances that were deployed before hello extension was applied toohello scale set.</span></span> |
| [<span data-ttu-id="de3be-125">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="de3be-125">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="de3be-126">向上擴充 hello 標尺加入多個 VM 執行個體來設定。</span><span class="sxs-lookup"><span data-stu-id="de3be-126">Scale up hello scale set by adding more VM instances.</span></span> <span data-ttu-id="de3be-127">這些執行 hello 自訂指令碼，在部署時。</span><span class="sxs-lookup"><span data-stu-id="de3be-127">hello custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="de3be-128">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="de3be-128">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="de3be-129">取得 hello 的 hello hello 範例所建立的 Vm 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="de3be-129">Get hello IP addresses of hello VMs created by hello sample.</span></span> |
| [<span data-ttu-id="de3be-130">az network lb show</span><span class="sxs-lookup"><span data-stu-id="de3be-130">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="de3be-131">取得 hello 前端及後端 hello 負載平衡器使用的通訊埠。</span><span class="sxs-lookup"><span data-stu-id="de3be-131">Get hello frontend and backend ports used by hello load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="de3be-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="de3be-132">Next steps</span></span>

<span data-ttu-id="de3be-133">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="de3be-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="de3be-134">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="de3be-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
