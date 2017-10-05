---
title: "Azure CLI 指令碼範例 - 使用 Batch 執行工作 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 使用 Batch 執行工作"
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
ms.openlocfilehash: 5fe1e3595d9459e60b2fd54d6f17f6822731f453
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="e5a23-103">在 Azure Batch 上使用 Azure CLI 執行工作</span><span class="sxs-lookup"><span data-stu-id="e5a23-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="e5a23-104">此指令碼會建立 Batch 工作，並將一系列作業加入至工作。</span><span class="sxs-lookup"><span data-stu-id="e5a23-104">This script creates a Batch job and adds a series of tasks to the job.</span></span> <span data-ttu-id="e5a23-105">它也示範如何監視工作和其作業。</span><span class="sxs-lookup"><span data-stu-id="e5a23-105">It also demonstrates how to monitor a job and its tasks.</span></span> <span data-ttu-id="e5a23-106">最後，它會示範如何有效率地查詢 Batch 服務，以取得作業工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e5a23-106">Finally, it shows how to query the Batch service efficiently for information about the job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e5a23-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="e5a23-107">Prerequisites</span></span>

- <span data-ttu-id="e5a23-108">如果您尚未安裝 Azure CLI，請使用 [Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)中所提供的指示來安裝 Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="e5a23-108">Install the Azure CLI using the instructions provided in the [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="e5a23-109">建立 Batch 帳戶 (如果您還沒有帳戶的話)。</span><span class="sxs-lookup"><span data-stu-id="e5a23-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="e5a23-110">如需用以建立帳戶的指令碼範例，請參閱[使用 Azure CLI 建立 Batch 帳戶](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)。</span><span class="sxs-lookup"><span data-stu-id="e5a23-110">See [Create a Batch account with the Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="e5a23-111">將應用程式設定為從啟動工作來執行 (如果您尚未設定)。</span><span class="sxs-lookup"><span data-stu-id="e5a23-111">Configure an application to run from a start task if you haven't yet done so.</span></span> <span data-ttu-id="e5a23-112">如需指令碼範例以建立應用程式並將應用程式套件上傳至 Azure，請參閱[使用 Azure CLI 將應用程式新增至 Azure Batch](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application)。</span><span class="sxs-lookup"><span data-stu-id="e5a23-112">See [Adding applications to Azure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package to Azure.</span></span>
- <span data-ttu-id="e5a23-113">設定用來執行作業的集區。</span><span class="sxs-lookup"><span data-stu-id="e5a23-113">Configure a pool on which the job will run.</span></span> <span data-ttu-id="e5a23-114">如需指令碼範例以使用雲端服務組態或虛擬機器組態來建立集區，請參閱[使用 Azure CLI 管理 Azure Batch 集區](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool)。</span><span class="sxs-lookup"><span data-stu-id="e5a23-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="e5a23-115">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="e5a23-115">Sample script</span></span>

<span data-ttu-id="e5a23-116">[!code-azurecli[主要](../../../cli_scripts/batch/run-job/run-job.sh "執行工作")]</span><span class="sxs-lookup"><span data-stu-id="e5a23-116">[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]</span></span>

## <a name="clean-up-job"></a><span data-ttu-id="e5a23-117">清除工作</span><span class="sxs-lookup"><span data-stu-id="e5a23-117">Clean up job</span></span>

<span data-ttu-id="e5a23-118">執行上述範例指令碼之後，請執行下列命令以移除工作和其所有作業。</span><span class="sxs-lookup"><span data-stu-id="e5a23-118">After you run the above sample script, run the following command to remove the job and all of its tasks.</span></span> <span data-ttu-id="e5a23-119">請注意，您必須另外刪除集區。</span><span class="sxs-lookup"><span data-stu-id="e5a23-119">Note that the pool will need to be deleted separately.</span></span> <span data-ttu-id="e5a23-120">如需建立和刪除集區的詳細資訊，請參閱[使用 Azure CLI 管理 Azure Batch 集區](./batch-cli-sample-manage-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="e5a23-120">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="e5a23-121">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="e5a23-121">Script explanation</span></span>

<span data-ttu-id="e5a23-122">此指令碼使用下列命令來建立 Batch 工作和作業。</span><span class="sxs-lookup"><span data-stu-id="e5a23-122">This script uses the following commands to create a Batch job and tasks.</span></span> <span data-ttu-id="e5a23-123">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="e5a23-123">Each command in the table links to command-specific documentation.</span></span>

| <span data-ttu-id="e5a23-124">命令</span><span class="sxs-lookup"><span data-stu-id="e5a23-124">Command</span></span> | <span data-ttu-id="e5a23-125">注意事項</span><span class="sxs-lookup"><span data-stu-id="e5a23-125">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e5a23-126">az batch account login</span><span class="sxs-lookup"><span data-stu-id="e5a23-126">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="e5a23-127">對 Batch 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="e5a23-127">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="e5a23-128">az batch job create</span><span class="sxs-lookup"><span data-stu-id="e5a23-128">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="e5a23-129">建立 Batch 工作。</span><span class="sxs-lookup"><span data-stu-id="e5a23-129">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="e5a23-130">az batch job set</span><span class="sxs-lookup"><span data-stu-id="e5a23-130">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="e5a23-131">更新 Batch 工作的屬性。</span><span class="sxs-lookup"><span data-stu-id="e5a23-131">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="e5a23-132">az batch job show</span><span class="sxs-lookup"><span data-stu-id="e5a23-132">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="e5a23-133">擷取指定的 Batch 工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e5a23-133">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="e5a23-134">az batch task create</span><span class="sxs-lookup"><span data-stu-id="e5a23-134">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="e5a23-135">將作業加入至指定的 Batch 工作。</span><span class="sxs-lookup"><span data-stu-id="e5a23-135">Adds a task to the specified Batch job.</span></span>  |
| [<span data-ttu-id="e5a23-136">az batch task show</span><span class="sxs-lookup"><span data-stu-id="e5a23-136">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="e5a23-137">從指定的 Batch 工作擷取作業的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="e5a23-137">Retrieves the details of a task from the specified Batch job.</span></span>  |
| [<span data-ttu-id="e5a23-138">az batch task list</span><span class="sxs-lookup"><span data-stu-id="e5a23-138">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="e5a23-139">列出指定作業的相關工作。</span><span class="sxs-lookup"><span data-stu-id="e5a23-139">Lists the tasks associated with the specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="e5a23-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e5a23-140">Next steps</span></span>

<span data-ttu-id="e5a23-141">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="e5a23-141">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e5a23-142">您可以在 [Azure Batch CLI 文件](../batch-cli-samples.md)中找到其他的 Batch CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="e5a23-142">Additional Batch CLI script samples can be found in the [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
