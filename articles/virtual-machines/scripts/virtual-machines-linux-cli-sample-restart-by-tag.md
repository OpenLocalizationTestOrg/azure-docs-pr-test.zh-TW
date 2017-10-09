---
title: "aaaAzure CLI 指令碼範例-重新啟動 Vm |Microsoft 文件"
description: "Azure CLI 指令碼範例 - 依標記和識別碼重新啟動 VM"
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
ms.date: 03/01/2017
ms.author: allclark
ms.custom: mvc
ms.openlocfilehash: a1ae07bd1d2be906553bef817385a4a333a10eca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="restart-vms"></a><span data-ttu-id="12111-103">重新啟動 VM</span><span class="sxs-lookup"><span data-stu-id="12111-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="12111-104">這個範例示範幾個方式 tooget 一些 Vm，然後重新啟動它們。</span><span class="sxs-lookup"><span data-stu-id="12111-104">This sample shows a couple of ways tooget some VMs and restart them.</span></span>

<span data-ttu-id="12111-105">hello 第一次重新啟動 hello 資源群組中的所有 hello Vm。</span><span class="sxs-lookup"><span data-stu-id="12111-105">hello first restarts all hello VMs in hello resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="12111-106">hello 第二個取得 hello 標記 Vm 使用`az resouce list`和篩選 toohello 資源的 Vm，並重新啟動這些 Vm。</span><span class="sxs-lookup"><span data-stu-id="12111-106">hello second gets hello tagged VMs using `az resouce list` and filters toohello resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="12111-107">這個範例適用於 Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="12111-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="12111-108">在 Windows 用戶端上執行 Azure CLI 指令碼選項，請參閱[Windows 中執行 hello Azure CLI](../windows/cli-options.md)。</span><span class="sxs-lookup"><span data-stu-id="12111-108">For options on running Azure CLI scripts on Windows client, see [Running hello Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="12111-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="12111-109">Sample script</span></span>

<span data-ttu-id="12111-110">hello 範例具備三個指令碼。</span><span class="sxs-lookup"><span data-stu-id="12111-110">hello sample has three scripts.</span></span>
<span data-ttu-id="12111-111">hello 第一個佈建 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="12111-111">hello first one provisions hello virtual machines.</span></span>
<span data-ttu-id="12111-112">因此 hello 命令會傳回而不會等到上佈建每個 VM toobe，它會使用 hello 否等候選項。</span><span class="sxs-lookup"><span data-stu-id="12111-112">It uses hello no-wait option so hello command returns without waiting on each VM toobe provisioned.</span></span>
<span data-ttu-id="12111-113">hello 第二個等候 hello Vm toobe 完整佈建。</span><span class="sxs-lookup"><span data-stu-id="12111-113">hello second waits for hello VMs toobe fully provisioned.</span></span>
<span data-ttu-id="12111-114">hello 第三個指令碼會重新啟動所有的 hello Vm 已佈建，然後只 hello 標記 Vm。</span><span class="sxs-lookup"><span data-stu-id="12111-114">hello third script restarts all hello VMs that were provisioned, and then just hello tagged VMs.</span></span>

### <a name="provision-hello-vms"></a><span data-ttu-id="12111-115">佈建 Vm hello</span><span class="sxs-lookup"><span data-stu-id="12111-115">Provision hello VMs</span></span>

<span data-ttu-id="12111-116">此指令碼會建立資源群組，然後再建立三個 Vm toorestart。</span><span class="sxs-lookup"><span data-stu-id="12111-116">This script creates a resource group and then it creates three VMs toorestart.</span></span>
<span data-ttu-id="12111-117">其中兩部已加上標記。</span><span class="sxs-lookup"><span data-stu-id="12111-117">Two of them are tagged.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision hello VMs")]

### <a name="wait"></a><span data-ttu-id="12111-118">等候</span><span class="sxs-lookup"><span data-stu-id="12111-118">Wait</span></span>

<span data-ttu-id="12111-119">此指令碼會檢查在 hello 每 20 秒，直到所有的三個 Vm 會佈建，或其中一個失敗 tooprovision 佈建狀態。</span><span class="sxs-lookup"><span data-stu-id="12111-119">This script checks on hello provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails tooprovision.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for hello VMs toobe provisioned")]

### <a name="restart-hello-vms"></a><span data-ttu-id="12111-120">重新啟動 Vm hello</span><span class="sxs-lookup"><span data-stu-id="12111-120">Restart hello VMs</span></span>

<span data-ttu-id="12111-121">此指令碼以 hello 資源群組，重新啟動所有 hello Vm，然後重新都啟動只 hello 標記 Vm。</span><span class="sxs-lookup"><span data-stu-id="12111-121">This script restarts all hello VMs in hello resource group, and then it restarts just hello tagged VMs.</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]

## <a name="clean-up-deployment"></a><span data-ttu-id="12111-122">清除部署</span><span class="sxs-lookup"><span data-stu-id="12111-122">Clean up deployment</span></span> 

<span data-ttu-id="12111-123">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組，Vm 和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="12111-123">After hello script sample has been run, hello following command can be used tooremove hello resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="12111-124">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="12111-124">Script explanation</span></span>

<span data-ttu-id="12111-125">此指令碼會使用下列命令 toocreate 資源群組、 虛擬機器、 可用性設定組中，負載平衡器和所有相關的資源的 hello。</span><span class="sxs-lookup"><span data-stu-id="12111-125">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="12111-126">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="12111-126">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="12111-127">命令</span><span class="sxs-lookup"><span data-stu-id="12111-127">Command</span></span> | <span data-ttu-id="12111-128">注意事項</span><span class="sxs-lookup"><span data-stu-id="12111-128">Notes</span></span> |
|---|---|
| [<span data-ttu-id="12111-129">az group create</span><span class="sxs-lookup"><span data-stu-id="12111-129">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="12111-130">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="12111-130">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="12111-131">az vm create</span><span class="sxs-lookup"><span data-stu-id="12111-131">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="12111-132">建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="12111-132">Creates hello virtual machines.</span></span>  |
| [<span data-ttu-id="12111-133">az vm list</span><span class="sxs-lookup"><span data-stu-id="12111-133">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="12111-134">搭配`--query`tooensure hello Vm 佈建後再重新啟動，並再 tooget hello 識別碼 hello Vm toorestart 它們。</span><span class="sxs-lookup"><span data-stu-id="12111-134">Used with `--query` tooensure hello VMs are provisioned before restarting them, and then tooget hello IDs of hello VMs toorestart them.</span></span> |
| [<span data-ttu-id="12111-135">az resource list</span><span class="sxs-lookup"><span data-stu-id="12111-135">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="12111-136">搭配`--query`tooget hello hello Vm 使用 hello 標記的識別碼。</span><span class="sxs-lookup"><span data-stu-id="12111-136">Used with `--query` tooget hello IDs of hello VMs using hello tag.</span></span> |
| [<span data-ttu-id="12111-137">az vm restart</span><span class="sxs-lookup"><span data-stu-id="12111-137">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="12111-138">Hello Vm 會重新啟動。</span><span class="sxs-lookup"><span data-stu-id="12111-138">Restarts hello VMs.</span></span> |
| [<span data-ttu-id="12111-139">az group delete</span><span class="sxs-lookup"><span data-stu-id="12111-139">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="12111-140">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="12111-140">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="12111-141">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12111-141">Next steps</span></span>

<span data-ttu-id="12111-142">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="12111-142">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="12111-143">您可以找到額外的虛擬機器 CLI 指令碼範例在 hello [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="12111-143">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
