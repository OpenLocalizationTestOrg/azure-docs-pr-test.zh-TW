---
title: "CLI 指令碼範例的批次執行作業 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: f73a7cb341e550fd1c92f92201e20b27fa20d238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="running-jobs-on-azure-batch-with-azure-cli"></a><span data-ttu-id="81913-103">在 Azure Batch 上使用 Azure CLI 執行工作</span><span class="sxs-lookup"><span data-stu-id="81913-103">Running jobs on Azure Batch with Azure CLI</span></span>

<span data-ttu-id="81913-104">此指令碼建立批次作業，並將一系列的工作 toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="81913-104">This script creates a Batch job and adds a series of tasks toohello job.</span></span> <span data-ttu-id="81913-105">它也會示範如何 toomonitor 的作業，且其工作。</span><span class="sxs-lookup"><span data-stu-id="81913-105">It also demonstrates how toomonitor a job and its tasks.</span></span> <span data-ttu-id="81913-106">最後，它會顯示如何 tooquery hello 批次服務有效率地 hello 作業 」 工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="81913-106">Finally, it shows how tooquery hello Batch service efficiently for information about hello job's tasks.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="81913-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="81913-107">Prerequisites</span></span>

- <span data-ttu-id="81913-108">安裝 hello Azure CLI 使用 hello 中提供的 hello 指示[Azure CLI 安裝指南](https://docs.microsoft.com/cli/azure/install-azure-cli)，如果您有不這麼做。</span><span class="sxs-lookup"><span data-stu-id="81913-108">Install hello Azure CLI using hello instructions provided in hello [Azure CLI installation guide](https://docs.microsoft.com/cli/azure/install-azure-cli), if you have not already done so.</span></span>
- <span data-ttu-id="81913-109">建立 Batch 帳戶 (如果您還沒有帳戶的話)。</span><span class="sxs-lookup"><span data-stu-id="81913-109">Create a Batch account if you don't already have one.</span></span> <span data-ttu-id="81913-110">請參閱[建立 Batch 帳戶以 hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account)建立帳戶的範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="81913-110">See [Create a Batch account with hello Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-create-account) for a sample script that creates an account.</span></span>
- <span data-ttu-id="81913-111">如果您尚未尚未這麼做，請設定應用程式 toorun，從啟動工作。</span><span class="sxs-lookup"><span data-stu-id="81913-111">Configure an application toorun from a start task if you haven't yet done so.</span></span> <span data-ttu-id="81913-112">請參閱[加入應用程式 tooAzure 批次使用 Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application)所建立的應用程式，並上傳應用程式封裝 tooAzure 的範例指令碼。</span><span class="sxs-lookup"><span data-stu-id="81913-112">See [Adding applications tooAzure Batch with Azure CLI](https://docs.microsoft.com/azure/batch/scripts/batch-cli-sample-add-application) for a sample script that creates an application and uploads an application package tooAzure.</span></span>
- <span data-ttu-id="81913-113">設定哪些 hello 將執行作業的集區。</span><span class="sxs-lookup"><span data-stu-id="81913-113">Configure a pool on which hello job will run.</span></span> <span data-ttu-id="81913-114">如需指令碼範例以使用雲端服務組態或虛擬機器組態來建立集區，請參閱[使用 Azure CLI 管理 Azure Batch 集區](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool)。</span><span class="sxs-lookup"><span data-stu-id="81913-114">See [Managing Azure Batch pools with Azure CLI](https://docs.microsoft.com/azure/batch/batch-cli-sample-manage-pool) for a sample script that creates a pool with either a Cloud Service Configuration or a Virtual Machine Configuration.</span></span>

## <a name="sample-script"></a><span data-ttu-id="81913-115">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="81913-115">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/batch/run-job/run-job.sh "Run Job")]

## <a name="clean-up-job"></a><span data-ttu-id="81913-116">清除工作</span><span class="sxs-lookup"><span data-stu-id="81913-116">Clean up job</span></span>

<span data-ttu-id="81913-117">執行 hello 上面的範例指令碼之後，執行下列命令 tooremove hello 的工作及所有的工作。</span><span class="sxs-lookup"><span data-stu-id="81913-117">After you run hello above sample script, run hello following command tooremove the job and all of its tasks.</span></span> <span data-ttu-id="81913-118">請注意，hello 集區必須另外刪除 toobe。</span><span class="sxs-lookup"><span data-stu-id="81913-118">Note that hello pool will need toobe deleted separately.</span></span> <span data-ttu-id="81913-119">如需建立和刪除集區的詳細資訊，請參閱[使用 Azure CLI 管理 Azure Batch 集區](./batch-cli-sample-manage-pool.md)。</span><span class="sxs-lookup"><span data-stu-id="81913-119">See [Managing Azure Batch pools with Azure CLI](./batch-cli-sample-manage-pool.md) for more information on creating and deleting pools.</span></span>

```azurecli
az batch job delete --job-id myjob
```

## <a name="script-explanation"></a><span data-ttu-id="81913-120">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="81913-120">Script explanation</span></span>

<span data-ttu-id="81913-121">此指令碼會使用下列命令 toocreate hello 批次工作和工作。</span><span class="sxs-lookup"><span data-stu-id="81913-121">This script uses hello following commands toocreate a Batch job and tasks.</span></span> <span data-ttu-id="81913-122">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="81913-122">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="81913-123">命令</span><span class="sxs-lookup"><span data-stu-id="81913-123">Command</span></span> | <span data-ttu-id="81913-124">注意事項</span><span class="sxs-lookup"><span data-stu-id="81913-124">Notes</span></span> |
|---|---|
| [<span data-ttu-id="81913-125">az batch account login</span><span class="sxs-lookup"><span data-stu-id="81913-125">az batch account login</span></span>](https://docs.microsoft.com/cli/azure/batch/account#login) | <span data-ttu-id="81913-126">對 Batch 帳戶進行驗證。</span><span class="sxs-lookup"><span data-stu-id="81913-126">Authenticate against a Batch account.</span></span>  |
| [<span data-ttu-id="81913-127">az batch job create</span><span class="sxs-lookup"><span data-stu-id="81913-127">az batch job create</span></span>](https://docs.microsoft.com/cli/azure/batch/job#create) | <span data-ttu-id="81913-128">建立 Batch 工作。</span><span class="sxs-lookup"><span data-stu-id="81913-128">Creates a Batch job.</span></span>  |
| [<span data-ttu-id="81913-129">az batch job set</span><span class="sxs-lookup"><span data-stu-id="81913-129">az batch job set</span></span>](https://docs.microsoft.com/cli/azure/batch/job#set) | <span data-ttu-id="81913-130">更新 Batch 工作的屬性。</span><span class="sxs-lookup"><span data-stu-id="81913-130">Updates properties of a Batch job.</span></span>  |
| [<span data-ttu-id="81913-131">az batch job show</span><span class="sxs-lookup"><span data-stu-id="81913-131">az batch job show</span></span>](https://docs.microsoft.com/cli/azure/batch/job#show) | <span data-ttu-id="81913-132">擷取指定的 Batch 工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="81913-132">Retrieves details of a specified Batch job.</span></span>  |
| [<span data-ttu-id="81913-133">az batch task create</span><span class="sxs-lookup"><span data-stu-id="81913-133">az batch task create</span></span>](https://docs.microsoft.com/cli/azure/batch/task#create) | <span data-ttu-id="81913-134">新增工作 toohello 指定批次作業。</span><span class="sxs-lookup"><span data-stu-id="81913-134">Adds a task toohello specified Batch job.</span></span>  |
| [<span data-ttu-id="81913-135">az batch task show</span><span class="sxs-lookup"><span data-stu-id="81913-135">az batch task show</span></span>](https://docs.microsoft.com/cli/azure/batch/task#show) | <span data-ttu-id="81913-136">擷取 hello hello 工作詳細資料指定批次作業。</span><span class="sxs-lookup"><span data-stu-id="81913-136">Retrieves hello details of a task from hello specified Batch job.</span></span>  |
| [<span data-ttu-id="81913-137">az batch task list</span><span class="sxs-lookup"><span data-stu-id="81913-137">az batch task list</span></span>](https://docs.microsoft.com/cli/azure/batch/task#list) | <span data-ttu-id="81913-138">列出 hello 與 hello 指定作業相關聯的工作。</span><span class="sxs-lookup"><span data-stu-id="81913-138">Lists hello tasks associated with hello specified job.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="81913-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="81913-139">Next steps</span></span>

<span data-ttu-id="81913-140">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="81913-140">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="81913-141">其他批次 CLI 指令碼範例可以在 hello [Azure 批次 CLI 文件](../batch-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="81913-141">Additional Batch CLI script samples can be found in hello [Azure Batch CLI documentation](../batch-cli-samples.md).</span></span>
