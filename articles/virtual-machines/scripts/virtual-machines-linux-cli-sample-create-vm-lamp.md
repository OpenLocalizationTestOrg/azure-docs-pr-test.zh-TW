---
title: "Azure CLI 指令碼範例 - 在負載平衡虛擬機器擴展集中部署 LAMP 堆疊 | Microsoft Docs"
description: "使用自訂指令碼擴充功能，在 Azure 上的負載平衡虛擬機器擴展集中部署 LAMP 堆疊。"
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
ms.openlocfilehash: 4007e8c85c0ff24bf5030881eac666582714eae3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-the-lamp-stack-in-a-load-balanced-virtual-machine-scale-set"></a><span data-ttu-id="930db-103">在負載平衡虛擬機器擴展集中部署 LAMP 堆疊</span><span class="sxs-lookup"><span data-stu-id="930db-103">Deploy the LAMP stack in a load-balanced virtual machine scale set</span></span>

<span data-ttu-id="930db-104">這個範例會建立虛擬機器擴展集，並且套用執行自訂指令碼的擴充功能，在擴展集的每部虛擬機器上部署 LAMP 堆疊。</span><span class="sxs-lookup"><span data-stu-id="930db-104">This example creates a virtual machine scale set and applies an extension that runs a custom script to deploy the LAMP stack on each virtual machine in the scale set.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="930db-105">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="930db-105">Sample script</span></span>

<span data-ttu-id="930db-106">[!code-azurecli-interactive[主要](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "建立具有 LAMP 堆疊的虛擬機器擴展集")]</span><span class="sxs-lookup"><span data-stu-id="930db-106">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/build-stack.sh "Create virtual machine scale set with LAMP stack")]</span></span>

## <a name="connect"></a><span data-ttu-id="930db-107">連線</span><span class="sxs-lookup"><span data-stu-id="930db-107">Connect</span></span>

<span data-ttu-id="930db-108">使用下列程式碼，以了解如何連線至您的 VM 和您的擴展集。</span><span class="sxs-lookup"><span data-stu-id="930db-108">Use this code to see how to connect to your VMs and your scale set.</span></span>

<span data-ttu-id="930db-109">[!code-azurecli[主要](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "存取虛擬機器擴展集")]</span><span class="sxs-lookup"><span data-stu-id="930db-109">[!code-azurecli[main](../../../cli_scripts/virtual-machine/create-scaleset-php-ansible/how-to-access.sh "Access the virtual machine scale set")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="930db-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="930db-110">Clean up deployment</span></span> 

<span data-ttu-id="930db-111">執行下列命令來移除資源群組、擴展集和 VM，以及所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="930db-111">Run the following command to remove the resource group, the scale set and VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="930db-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="930db-112">Script explanation</span></span>

<span data-ttu-id="930db-113">此指令碼使用下列命令來建立資源群組、虛擬機器、可用性設定組、負載平衡器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="930db-113">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="930db-114">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="930db-114">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="930db-115">命令</span><span class="sxs-lookup"><span data-stu-id="930db-115">Command</span></span> | <span data-ttu-id="930db-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="930db-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="930db-117">az group create</span><span class="sxs-lookup"><span data-stu-id="930db-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="930db-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="930db-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="930db-119">az vmss create</span><span class="sxs-lookup"><span data-stu-id="930db-119">az vmss create</span></span>](https://docs.microsoft.com/cli/azure/vmss#create) | <span data-ttu-id="930db-120">建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="930db-120">Creates a virtual machine scale set</span></span> |
| [<span data-ttu-id="930db-121">az network lb rule create</span><span class="sxs-lookup"><span data-stu-id="930db-121">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="930db-122">新增負載平衡端點</span><span class="sxs-lookup"><span data-stu-id="930db-122">Add a load-balanced endpoint</span></span> |
| [<span data-ttu-id="930db-123">az vmss extension set</span><span class="sxs-lookup"><span data-stu-id="930db-123">az vmss extension set</span></span>](https://docs.microsoft.com/cli/azure/vmss/extension#set) | <span data-ttu-id="930db-124">建立擴充功能，該擴充功能在 VM 部署上執行自訂指令碼</span><span class="sxs-lookup"><span data-stu-id="930db-124">Create the extension that runs the custom script on deployment of a VM</span></span> |
| [<span data-ttu-id="930db-125">az vmss update-instances</span><span class="sxs-lookup"><span data-stu-id="930db-125">az vmss update-instances</span></span>](https://docs.microsoft.com/cli/azure/vmss#update-instances) | <span data-ttu-id="930db-126">在 VM 執行個體上執行自訂指令碼，該執行個體是在擴充功能套用至擴展集之前部署的。</span><span class="sxs-lookup"><span data-stu-id="930db-126">Run the custom script on the VM instances that were deployed before the extension was applied to the scale set.</span></span> |
| [<span data-ttu-id="930db-127">az vmss scale</span><span class="sxs-lookup"><span data-stu-id="930db-127">az vmss scale</span></span>](https://docs.microsoft.com/cli/azure/vmss#scale) | <span data-ttu-id="930db-128">藉由新增更多 VM 執行個體以相應增加擴展集。</span><span class="sxs-lookup"><span data-stu-id="930db-128">Scale up the scale set by adding more VM instances.</span></span> <span data-ttu-id="930db-129">當這些執行個體部署時，自訂指令碼會在上面執行。</span><span class="sxs-lookup"><span data-stu-id="930db-129">The custom script is run on these when they are deployed.</span></span> |
| [<span data-ttu-id="930db-130">az network public-ip list</span><span class="sxs-lookup"><span data-stu-id="930db-130">az network public-ip list</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#list) | <span data-ttu-id="930db-131">取得範例建立之 VM 的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="930db-131">Get the IP addresses of the VMs created by the sample.</span></span> |
| [<span data-ttu-id="930db-132">az network lb show</span><span class="sxs-lookup"><span data-stu-id="930db-132">az network lb show</span></span>](https://docs.microsoft.com/cli/azure/network/lb#show) | <span data-ttu-id="930db-133">取得由負載平衡器使用的前端和後端連接埠。</span><span class="sxs-lookup"><span data-stu-id="930db-133">Get the frontend and backend ports used by the load balancer.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="930db-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="930db-134">Next steps</span></span>

<span data-ttu-id="930db-135">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="930db-135">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="930db-136">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="930db-136">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
