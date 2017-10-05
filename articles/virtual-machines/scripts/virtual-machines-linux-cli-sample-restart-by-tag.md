---
title: "Azure CLI 指令碼範例 - 重新啟動 VM | Microsoft Docs"
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
ms.openlocfilehash: 4d0fe95287c91a4b656904f9007ceaaf866e155f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="restart-vms"></a><span data-ttu-id="0dc78-103">重新啟動 VM</span><span class="sxs-lookup"><span data-stu-id="0dc78-103">Restart VMs</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

<span data-ttu-id="0dc78-104">這個範例顯示取得一些 VM 並加以重新啟動的幾種方式。</span><span class="sxs-lookup"><span data-stu-id="0dc78-104">This sample shows a couple of ways to get some VMs and restart them.</span></span>

<span data-ttu-id="0dc78-105">第一種方式可重新啟動資源群組中的所有 VM。</span><span class="sxs-lookup"><span data-stu-id="0dc78-105">The first restarts all the VMs in the resource group.</span></span>

```bash
az vm restart --ids $(az vm list --resource-group myResourceGroup --query "[].id" -o tsv)
```

<span data-ttu-id="0dc78-106">第二種方式可使用 `az resouce list` 取得已標記的 VM 並篩選至屬於 VM 的資源，然後重新啟動這些 VM。</span><span class="sxs-lookup"><span data-stu-id="0dc78-106">The second gets the tagged VMs using `az resouce list` and filters to the resources that are VMs, and restarts those VMs.</span></span>

```bash
az vm restart --ids $(az resource list --tag "restart-tag" --query "[?type=='Microsoft.Compute/virtualMachines'].id" -o tsv)
```

<span data-ttu-id="0dc78-107">這個範例適用於 Bash 殼層。</span><span class="sxs-lookup"><span data-stu-id="0dc78-107">This sample works in a Bash shell.</span></span> <span data-ttu-id="0dc78-108">如需在 Windows 用戶端上執行 Azure CLI 指令碼的選項，請參閱[在 Windows 中執行 Azure CLI](../windows/cli-options.md)。</span><span class="sxs-lookup"><span data-stu-id="0dc78-108">For options on running Azure CLI scripts on Windows client, see [Running the Azure CLI in Windows](../windows/cli-options.md).</span></span>


## <a name="sample-script"></a><span data-ttu-id="0dc78-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="0dc78-109">Sample script</span></span>

<span data-ttu-id="0dc78-110">此範例有三個指令碼。</span><span class="sxs-lookup"><span data-stu-id="0dc78-110">The sample has three scripts.</span></span>
<span data-ttu-id="0dc78-111">第一個指令碼會佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0dc78-111">The first one provisions the virtual machines.</span></span>
<span data-ttu-id="0dc78-112">它會使用不等待選項，因此命令會傳回，而不會在每個 VM 上等待佈建。</span><span class="sxs-lookup"><span data-stu-id="0dc78-112">It uses the no-wait option so the command returns without waiting on each VM to be provisioned.</span></span>
<span data-ttu-id="0dc78-113">第二個指令碼會等待 VM 完整佈建。</span><span class="sxs-lookup"><span data-stu-id="0dc78-113">The second waits for the VMs to be fully provisioned.</span></span>
<span data-ttu-id="0dc78-114">第三個指令碼會重新啟動所有已佈建的 VM，然後只重新啟動已標記的 VM。</span><span class="sxs-lookup"><span data-stu-id="0dc78-114">The third script restarts all the VMs that were provisioned, and then just the tagged VMs.</span></span>

### <a name="provision-the-vms"></a><span data-ttu-id="0dc78-115">佈建 VM</span><span class="sxs-lookup"><span data-stu-id="0dc78-115">Provision the VMs</span></span>

<span data-ttu-id="0dc78-116">此指令碼會建立資源群組，然後建立三部要重新啟動的 VM。</span><span class="sxs-lookup"><span data-stu-id="0dc78-116">This script creates a resource group and then it creates three VMs to restart.</span></span>
<span data-ttu-id="0dc78-117">其中兩部已加上標記。</span><span class="sxs-lookup"><span data-stu-id="0dc78-117">Two of them are tagged.</span></span>

<span data-ttu-id="0dc78-118">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "佈建 VM")]</span><span class="sxs-lookup"><span data-stu-id="0dc78-118">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/provision.sh "Provision the VMs")]</span></span>

### <a name="wait"></a><span data-ttu-id="0dc78-119">等候</span><span class="sxs-lookup"><span data-stu-id="0dc78-119">Wait</span></span>

<span data-ttu-id="0dc78-120">此指令碼會每 20 秒檢查一次佈建狀態，直到三部 VM 都已佈建，或其中一部佈建失敗為止。</span><span class="sxs-lookup"><span data-stu-id="0dc78-120">This script checks on the provisioning status every 20 seconds until all three VMs are provisioned, or one of them fails to provision.</span></span>

<span data-ttu-id="0dc78-121">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "等待 VM 進行佈建")]</span><span class="sxs-lookup"><span data-stu-id="0dc78-121">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/wait.sh "Wait for the VMs to be provisioned")]</span></span>

### <a name="restart-the-vms"></a><span data-ttu-id="0dc78-122">重新啟動 VM</span><span class="sxs-lookup"><span data-stu-id="0dc78-122">Restart the VMs</span></span>

<span data-ttu-id="0dc78-123">此指令碼重新啟動資源群組中的所有 VM，然後只重新啟動已標記的 VM。</span><span class="sxs-lookup"><span data-stu-id="0dc78-123">This script restarts all the VMs in the resource group, and then it restarts just the tagged VMs.</span></span>

<span data-ttu-id="0dc78-124">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "依標記重新啟動 VM")]</span><span class="sxs-lookup"><span data-stu-id="0dc78-124">[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/restart-by-tag/restart.sh "Restart VMs by tag")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="0dc78-125">清除部署</span><span class="sxs-lookup"><span data-stu-id="0dc78-125">Clean up deployment</span></span> 

<span data-ttu-id="0dc78-126">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、VM 和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="0dc78-126">After the script sample has been run, the following command can be used to remove the resource groups, VMs, and all related resources.</span></span>

```azurecli-interactive 
az group delete -n myResourceGroup --no-wait --yes
```

## <a name="script-explanation"></a><span data-ttu-id="0dc78-127">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="0dc78-127">Script explanation</span></span>

<span data-ttu-id="0dc78-128">此指令碼使用下列命令來建立資源群組、虛擬機器、可用性設定組、負載平衡器和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="0dc78-128">This script uses the following commands to create a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="0dc78-129">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="0dc78-129">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="0dc78-130">命令</span><span class="sxs-lookup"><span data-stu-id="0dc78-130">Command</span></span> | <span data-ttu-id="0dc78-131">注意事項</span><span class="sxs-lookup"><span data-stu-id="0dc78-131">Notes</span></span> |
|---|---|
| [<span data-ttu-id="0dc78-132">az group create</span><span class="sxs-lookup"><span data-stu-id="0dc78-132">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="0dc78-133">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="0dc78-133">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="0dc78-134">az vm create</span><span class="sxs-lookup"><span data-stu-id="0dc78-134">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | <span data-ttu-id="0dc78-135">建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="0dc78-135">Creates the virtual machines.</span></span>  |
| [<span data-ttu-id="0dc78-136">az vm list</span><span class="sxs-lookup"><span data-stu-id="0dc78-136">az vm list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="0dc78-137">與 `--query` 搭配使用，確保在重新啟動 VM 之前先加以佈建，然後取得 VM 識別碼加以重新啟動。</span><span class="sxs-lookup"><span data-stu-id="0dc78-137">Used with `--query` to ensure the VMs are provisioned before restarting them, and then to get the IDs of the VMs to restart them.</span></span> |
| [<span data-ttu-id="0dc78-138">az resource list</span><span class="sxs-lookup"><span data-stu-id="0dc78-138">az resource list</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="0dc78-139">與 `--query` 搭配使用，使用標籤取得 VM 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="0dc78-139">Used with `--query` to get the IDs of the VMs using the tag.</span></span> |
| [<span data-ttu-id="0dc78-140">az vm restart</span><span class="sxs-lookup"><span data-stu-id="0dc78-140">az vm restart</span></span>](https://docs.microsoft.com/cli/azure/vm#list) | <span data-ttu-id="0dc78-141">重新啟動 VM。</span><span class="sxs-lookup"><span data-stu-id="0dc78-141">Restarts the VMs.</span></span> |
| [<span data-ttu-id="0dc78-142">az group delete</span><span class="sxs-lookup"><span data-stu-id="0dc78-142">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="0dc78-143">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="0dc78-143">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0dc78-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0dc78-144">Next steps</span></span>

<span data-ttu-id="0dc78-145">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="0dc78-145">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="0dc78-146">您可以在 [Azure Linux VM 文件](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)中找到其他的虛擬機器 CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="0dc78-146">Additional virtual machine CLI script samples can be found in the [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
