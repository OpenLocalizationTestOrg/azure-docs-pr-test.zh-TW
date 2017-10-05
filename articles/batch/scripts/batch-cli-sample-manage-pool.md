---
title: "Azure CLI 指令碼範例 - 管理 Batch 中的集區 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 管理 Batch 中的集區"
services: batch
documentationcenter: 
author: annatisch
manager: daryls
editor: tysonn
ms.assetid: 
ms.service: batch
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/02/2017
ms.author: antisch
ms.openlocfilehash: 2556b02459886390b803407c5cb828687229a44e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="7b8f3-103">使用 Azure CLI 管理 Azure Batch 集區</span><span class="sxs-lookup"><span data-stu-id="7b8f3-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="7b8f3-104">這些指令碼示範 Azure CLI 中一些可用的工具，用於建立和管理 Azure Batch 服務中的計算節點集區。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-104">These script demonstrates some of the tools available in the Azure CLI to create and manage pools of compute nodes in the Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="7b8f3-105">此範例中的命令會建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-105">The commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="7b8f3-106">執行中的 VM 會累計費用至您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-106">Running VMs will accrue charges to your account.</span></span> <span data-ttu-id="7b8f3-107">若要將這些費用降至最低，請在範例執行完成後隨即刪除 VM。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-107">To minimize these charges, delete the VMs once you're done running the sample.</span></span> <span data-ttu-id="7b8f3-108">請參閱[清除集區](#clean-up-pools)。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="7b8f3-109">有兩種方式可以設定 Batch 集區，即使用雲端服務組態 (僅限 Windows) 或虛擬機器組態 (Windows 和 Linux)。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="7b8f3-110">下列指令碼範例會示範如何使用這兩個組態來建立集區。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-110">The sample scripts below show how to create pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b8f3-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="7b8f3-111">Prerequisites</span></span>

- <span data-ttu-id="7b8f3-112">如果您尚未安裝 Azure CLI，請使用 [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)中所提供的指示來安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-112">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="7b8f3-113">建立 Batch 帳戶 (如果您還沒有帳戶的話)。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="7b8f3-114">如需用以建立帳戶的指令碼範例，請參閱[使用 Azure CLI 建立 Batch 帳戶](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-114">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="7b8f3-115">將應用程式設定為從啟動工作來執行 (如果您尚未設定)。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-115">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="7b8f3-116">如需指令碼範例以建立應用程式並將應用程式套件上傳至 Azure，請參閱[使用 Azure CLI 將應用程式新增至 Azure Batch](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application)。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-116">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="7b8f3-117">使用雲端服務組態範例指令碼的集區</span><span class="sxs-lookup"><span data-stu-id="7b8f3-117">Pool with cloud service configuration sample script</span></span>

<span data-ttu-id="7b8f3-118">[!code-azurecli[主要](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "管理雲端服務集區")]</span><span class="sxs-lookup"><span data-stu-id="7b8f3-118">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]</span></span>

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="7b8f3-119">使用虛擬機器組態範例指令碼的集區</span><span class="sxs-lookup"><span data-stu-id="7b8f3-119">Pool with virtual machine configuration sample script</span></span>

<span data-ttu-id="7b8f3-120">[!code-azurecli[主要](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "管理虛擬機器集區")]</span><span class="sxs-lookup"><span data-stu-id="7b8f3-120">[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]</span></span>

## <a name="clean-up-pools"></a><span data-ttu-id="7b8f3-121">清除集區</span><span class="sxs-lookup"><span data-stu-id="7b8f3-121">Clean up pools</span></span>

<span data-ttu-id="7b8f3-122">執行上述範例指令碼之後，請執行下列命令以刪除集區。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-122">After you run the above sample script, run the following command to delete the pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="7b8f3-123">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="7b8f3-123">Script explanation</span></span>

<span data-ttu-id="7b8f3-124">此指令碼使用下列命令來建立和管理 Batch 集區。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-124">This script uses the following commands to create and manipulate Batch pools.</span></span>
<span data-ttu-id="7b8f3-125">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-125">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="7b8f3-126">命令</span><span class="sxs-lookup"><span data-stu-id="7b8f3-126">Command</span></span> | <span data-ttu-id="7b8f3-127">注意事項</span><span class="sxs-lookup"><span data-stu-id="7b8f3-127">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7b8f3-128">az batch account login</span><span class="sxs-lookup"><span data-stu-id="7b8f3-128">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="7b8f3-129">對 Batch 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-129">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="7b8f3-130">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="7b8f3-130">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="7b8f3-131">列出 Batch 帳戶中可用的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-131">List the available applications in the Batch account.</span></span>  |
| [<span data-ttu-id="7b8f3-132">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="7b8f3-132">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="7b8f3-133">建立 VM 集區。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-133">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="7b8f3-134">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="7b8f3-134">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="7b8f3-135">更新集區的屬性。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-135">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="7b8f3-136">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="7b8f3-136">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="7b8f3-137">列出可用的節點代理程式 SKU 和映像資訊。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-137">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="7b8f3-138">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="7b8f3-138">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="7b8f3-139">調整指定集區的執行中 VM 數大小。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-139">Resize the number of running VMs in the specified pool.</span></span>  |
| [<span data-ttu-id="7b8f3-140">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="7b8f3-140">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="7b8f3-141">顯示集區的屬性。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-141">Display the properties of a pool.</span></span>  |
| [<span data-ttu-id="7b8f3-142">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="7b8f3-142">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="7b8f3-143">刪除指定的集區。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-143">Delete the specified pool.</span></span>  |
| [<span data-ttu-id="7b8f3-144">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="7b8f3-144">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="7b8f3-145">在集區啟用自動調整規模並套用公式。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-145">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="7b8f3-146">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="7b8f3-146">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="7b8f3-147">在集區停用自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-147">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="7b8f3-148">az batch node list</span><span class="sxs-lookup"><span data-stu-id="7b8f3-148">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="7b8f3-149">列出指定集區中的所有計算節點。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-149">List all the compute node in the specified pool.</span></span>  |
| [<span data-ttu-id="7b8f3-150">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="7b8f3-150">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="7b8f3-151">重新啟動指定的計算節點。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-151">Reboot the specified compute node.</span></span>  |
| [<span data-ttu-id="7b8f3-152">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="7b8f3-152">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="7b8f3-153">從指定的集區中刪除列出的節點。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-153">Delete the listed nodes from the specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="7b8f3-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7b8f3-154">Next steps</span></span>

<span data-ttu-id="7b8f3-155">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-155">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="7b8f3-156">您可以在 [Azure Batch CLI 文件](../batch-cli-samples.md)中找到其他的 Batch CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="7b8f3-156">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

