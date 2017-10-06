---
title: "aaaAzure CLI 指令碼範例的批次中的 管理集區 |Microsoft 文件"
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
ms.openlocfilehash: 6c9ca9515565aff42752231a080943be8e4c810b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="managing-azure-batch-pools-with-azure-cli"></a><span data-ttu-id="be5b7-103">使用 Azure CLI 管理 Azure Batch 集區</span><span class="sxs-lookup"><span data-stu-id="be5b7-103">Managing Azure Batch pools with Azure CLI</span></span>

<span data-ttu-id="be5b7-104">這些指令碼示範一些可用的 hello Azure CLI toocreate hello 工具和管理集區的 hello Azure 批次服務中的運算節點。</span><span class="sxs-lookup"><span data-stu-id="be5b7-104">These script demonstrates some of hello tools available in hello Azure CLI toocreate and manage pools of compute nodes in hello Azure Batch service.</span></span>

> [!NOTE]
> <span data-ttu-id="be5b7-105">在此範例中的 hello 命令會建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="be5b7-105">hello commands in this sample create Azure virtual machines.</span></span> <span data-ttu-id="be5b7-106">執行中 Vm 會累算費用 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="be5b7-106">Running VMs will accrue charges tooyour account.</span></span> <span data-ttu-id="be5b7-107">toominimize 費用，刪除 hello Vm 一旦您完成時執行的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="be5b7-107">toominimize these charges, delete hello VMs once you're done running hello sample.</span></span> <span data-ttu-id="be5b7-108">請參閱[清除集區](#clean-up-pools)。</span><span class="sxs-lookup"><span data-stu-id="be5b7-108">See [Clean up pools](#clean-up-pools).</span></span>

<span data-ttu-id="be5b7-109">有兩種方式可以設定 Batch 集區，即使用雲端服務組態 (僅限 Windows) 或虛擬機器組態 (Windows 和 Linux)。</span><span class="sxs-lookup"><span data-stu-id="be5b7-109">Batch pools can be configured in two ways, either with a Cloud Services configuration (Windows only), or a Virtual Machine configuration (Windows and Linux).</span></span> <span data-ttu-id="be5b7-110">下列的 hello 範例指令碼會顯示 toocreate 這兩種設定使用的集區。</span><span class="sxs-lookup"><span data-stu-id="be5b7-110">hello sample scripts below show how toocreate pools with both configurations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be5b7-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="be5b7-111">Prerequisites</span></span>

- <span data-ttu-id="be5b7-112">安裝 hello Azure CLI 使用 hello 中提供的 hello 指示[Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)，如果您有不這麼做。</span><span class="sxs-lookup"><span data-stu-id="be5b7-112">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="be5b7-113">建立 Batch 帳戶 (如果您還沒有帳戶的話)。</span><span class="sxs-lookup"><span data-stu-id="be5b7-113">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="be5b7-114">請參閱[建立 Batch 帳戶以 hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)建立帳戶的範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="be5b7-114">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="be5b7-115">如果您尚未尚未這麼做，請設定應用程式 toorun，從啟動工作。</span><span class="sxs-lookup"><span data-stu-id="be5b7-115">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="be5b7-116">請參閱[加入應用程式 tooAzure 批次使用 Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application)所建立的應用程式，並上傳應用程式封裝 tooAzure 的範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="be5b7-116">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>

## <a name="pool-with-cloud-service-configuration-sample-script"></a><span data-ttu-id="be5b7-117">使用雲端服務組態範例指令碼的集區</span><span class="sxs-lookup"><span data-stu-id="be5b7-117">Pool with cloud service configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-windows.sh "Manage Cloud Services Pools")]

## <a name="pool-with-virtual-machine-configuration-sample-script"></a><span data-ttu-id="be5b7-118">使用虛擬機器組態範例指令碼的集區</span><span class="sxs-lookup"><span data-stu-id="be5b7-118">Pool with virtual machine configuration sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/manage-pool/manage-pool-linux.sh "Manage Virtual Machine Pools")]

## <a name="clean-up-pools"></a><span data-ttu-id="be5b7-119">清除集區</span><span class="sxs-lookup"><span data-stu-id="be5b7-119">Clean up pools</span></span>

<span data-ttu-id="be5b7-120">執行上述範例指令碼的 hello 之後，執行下列命令 toodelete hello 集區的 hello。</span><span class="sxs-lookup"><span data-stu-id="be5b7-120">After you run hello above sample script, run hello following command toodelete hello pools.</span></span>
```azurecli
az batch pool delete --pool-id mypool-windows
az batch pool delete --pool-id mypool-linux
```

## <a name="script-explanation"></a><span data-ttu-id="be5b7-121">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="be5b7-121">Script explanation</span></span>

<span data-ttu-id="be5b7-122">此指令碼會使用下列命令 toocreate hello 和操作批次集區。</span><span class="sxs-lookup"><span data-stu-id="be5b7-122">This script uses hello following commands toocreate and manipulate Batch pools.</span></span>
<span data-ttu-id="be5b7-123">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="be5b7-123">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="be5b7-124">命令</span><span class="sxs-lookup"><span data-stu-id="be5b7-124">Command</span></span> | <span data-ttu-id="be5b7-125">注意事項</span><span class="sxs-lookup"><span data-stu-id="be5b7-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="be5b7-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="be5b7-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="be5b7-127">對 Batch 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="be5b7-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="be5b7-128">az batch application summary list</span><span class="sxs-lookup"><span data-stu-id="be5b7-128">az batch application summary list</span></span>](https://docs.microsoft.com/cli/azure/batch/application/summary#list) | <span data-ttu-id="be5b7-129">列出可用的應用程式 hello hello 批次帳戶中。</span><span class="sxs-lookup"><span data-stu-id="be5b7-129">List hello available applications in hello Batch account.</span></span>  |
| [<span data-ttu-id="be5b7-130">az batch pool create</span><span class="sxs-lookup"><span data-stu-id="be5b7-130">az batch pool create</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#create) | <span data-ttu-id="be5b7-131">建立 VM 集區。</span><span class="sxs-lookup"><span data-stu-id="be5b7-131">Create a pool of VMs.</span></span>  |
| [<span data-ttu-id="be5b7-132">az batch pool set</span><span class="sxs-lookup"><span data-stu-id="be5b7-132">az batch pool set</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#set) | <span data-ttu-id="be5b7-133">更新集區的屬性。</span><span class="sxs-lookup"><span data-stu-id="be5b7-133">Update properties of a pool.</span></span>  |
| [<span data-ttu-id="be5b7-134">az batch pool node-agent-skus list</span><span class="sxs-lookup"><span data-stu-id="be5b7-134">az batch pool node-agent-skus list</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/node-agent-skus#list) | <span data-ttu-id="be5b7-135">列出可用的節點代理程式 SKU 和映像資訊。</span><span class="sxs-lookup"><span data-stu-id="be5b7-135">List available node agent SKUs and image information.</span></span>  |
| [<span data-ttu-id="be5b7-136">az batch pool resize</span><span class="sxs-lookup"><span data-stu-id="be5b7-136">az batch pool resize</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#resize) | <span data-ttu-id="be5b7-137">集區指定的執行中 hello Vm 的調整大小 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="be5b7-137">Resize hello number of running VMs in hello specified pool.</span></span>  |
| [<span data-ttu-id="be5b7-138">az batch pool show</span><span class="sxs-lookup"><span data-stu-id="be5b7-138">az batch pool show</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#show) | <span data-ttu-id="be5b7-139">顯示 hello 屬性集區。</span><span class="sxs-lookup"><span data-stu-id="be5b7-139">Display hello properties of a pool.</span></span>  |
| [<span data-ttu-id="be5b7-140">az batch pool delete</span><span class="sxs-lookup"><span data-stu-id="be5b7-140">az batch pool delete</span></span>](https://docs.microsoft.com/cli/azure/batch/pool#delete) | <span data-ttu-id="be5b7-141">刪除指定的 hello 集區。</span><span class="sxs-lookup"><span data-stu-id="be5b7-141">Delete hello specified pool.</span></span>  |
| [<span data-ttu-id="be5b7-142">az batch pool autoscale enable</span><span class="sxs-lookup"><span data-stu-id="be5b7-142">az batch pool autoscale enable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#enable) | <span data-ttu-id="be5b7-143">在集區啟用自動調整規模並套用公式。</span><span class="sxs-lookup"><span data-stu-id="be5b7-143">Enable auto-scaling on a pool and apply a formula.</span></span>  |
| [<span data-ttu-id="be5b7-144">az batch pool autoscale disable</span><span class="sxs-lookup"><span data-stu-id="be5b7-144">az batch pool autoscale disable</span></span>](https://docs.microsoft.com/cli/azure/batch/pool/autoscale#disable) | <span data-ttu-id="be5b7-145">在集區停用自動調整規模。</span><span class="sxs-lookup"><span data-stu-id="be5b7-145">Disable auto-scaling on a pool.</span></span>  |
| [<span data-ttu-id="be5b7-146">az batch node list</span><span class="sxs-lookup"><span data-stu-id="be5b7-146">az batch node list</span></span>](https://docs.microsoft.com/cli/azure/batch/node#list) | <span data-ttu-id="be5b7-147">列出所有在 hello hello 計算節點指定集區。</span><span class="sxs-lookup"><span data-stu-id="be5b7-147">List all hello compute node in hello specified pool.</span></span>  |
| [<span data-ttu-id="be5b7-148">az batch node reboot</span><span class="sxs-lookup"><span data-stu-id="be5b7-148">az batch node reboot</span></span>](https://docs.microsoft.com/cli/azure/batch/node#reboot) | <span data-ttu-id="be5b7-149">重新啟動 hello 指定的運算節點。</span><span class="sxs-lookup"><span data-stu-id="be5b7-149">Reboot hello specified compute node.</span></span>  |
| [<span data-ttu-id="be5b7-150">az batch node delete</span><span class="sxs-lookup"><span data-stu-id="be5b7-150">az batch node delete</span></span>](https://docs.microsoft.com/cli/azure/batch/node#delete) | <span data-ttu-id="be5b7-151">刪除列出的 hello 節點從 hello 指定集區。</span><span class="sxs-lookup"><span data-stu-id="be5b7-151">Delete hello listed nodes from hello specified pool.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="be5b7-152">後續步驟</span><span class="sxs-lookup"><span data-stu-id="be5b7-152">Next steps</span></span>

<span data-ttu-id="be5b7-153">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="be5b7-153">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="be5b7-154">其他批次 CLI 指令碼範例可以在 hello [Azure 批次 CLI 文件](../batch-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="be5b7-154">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>

