---
title: "使用適用於 .NET 的檔案慣例程式庫將作業和工作輸出保存到 Azure 儲存體 - Azure Batch | Microsoft Docs"
description: "了解如何使用適用於 .NET 的 Azure Batch 檔案慣例程式庫，將 Batch 工作和作業輸出保存到 Azure 儲存體，並在 Azure 入口網站檢視保存的輸出。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a9de327c20463469bc91d9720aa17333a36f919e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="persist-job-and-task-data-to-azure-storage-with-the-batch-file-conventions-library-for-net-to-persist"></a><span data-ttu-id="a3b57-103">使用適用於 .NET 的 Batch 檔案慣例程式庫將作業和工作輸出保存到 Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="a3b57-103">Persist job and task data to Azure Storage with the Batch File Conventions library for .NET to persist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="a3b57-104">保存工作資料的其中一個方法是使用[適用於 .NET 的 Azure Batch 檔案慣例程式庫][nuget_package]。</span><span class="sxs-lookup"><span data-stu-id="a3b57-104">One way to persist task data is to use the [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="a3b57-105">檔案慣例程式庫會簡化將工作輸出資料儲存至 Azure 儲存體並且擷取它的程序。</span><span class="sxs-lookup"><span data-stu-id="a3b57-105">The File Conventions library simplifies the process of storing task output data to Azure Storage and retrieving it.</span></span> <span data-ttu-id="a3b57-106">您可以將檔案慣例程式庫用於工作和用戶端程式碼 &mdash; 在工作程式碼中用來保存檔案，以及在用戶端程式碼中用來列出和擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-106">You can use the File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code to list and retrieve them.</span></span> <span data-ttu-id="a3b57-107">您的工作程式碼也可以將程式庫用於擷取上游工作的輸出，例如[工作相依性](batch-task-dependencies.md)案例。</span><span class="sxs-lookup"><span data-stu-id="a3b57-107">Your task code can also use the library to retrieve the output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="a3b57-108">若要使用檔案慣例程式庫擷取輸出檔案，您可以藉由依據識別碼和用途列出它們，找到指定作業或工作的檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-108">To retrieve output files with the File Conventions library, you can locate the files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="a3b57-109">您不需要知道檔案的名稱或位置。</span><span class="sxs-lookup"><span data-stu-id="a3b57-109">You don't need to know the names or locations of the files.</span></span> <span data-ttu-id="a3b57-110">例如，您可以使用檔案慣例程式庫以列出指定工作的所有中繼檔案，或取得指定作業的預覽檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-110">For example, you can use the File Conventions library to list all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="a3b57-111">從 2017-05-01 版開始，Batch 服務 API 針對使用虛擬機器設定建立，在集區上執行的工作和作業管理員工作，支援將輸出資料保存到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a3b57-111">Starting with version 2017-05-01, the Batch service API supports persisting output data to Azure Storage for tasks and job manager tasks that run on pools created with the virtual machine configuration.</span></span> <span data-ttu-id="a3b57-112">Batch 服務 API 提供簡單的方式來保存程式碼內的輸出，該程式碼會建立工作，並且作為檔案慣例程式庫的替代方案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-112">The Batch service API provides a simple way to persist output from within the code that creates a task and serves as an alternative to the File Conventions library.</span></span> <span data-ttu-id="a3b57-113">您可以修改 Batch 用戶端應用程式以保存輸出，而不需要更新您的工作正在執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3b57-113">You can modify your Batch client applications to persist output without needing to update the application that your task is running.</span></span> <span data-ttu-id="a3b57-114">如需詳細資訊，請參閱[使用 Batch 服務 API 將工作資料保存到 Azure 儲存體](batch-task-output-files.md)。</span><span class="sxs-lookup"><span data-stu-id="a3b57-114">For more information, see [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-the-file-conventions-library-to-persist-task-output"></a><span data-ttu-id="a3b57-115">使用檔案慣例程式庫保存工作輸出的時機？</span><span class="sxs-lookup"><span data-stu-id="a3b57-115">When do I use the File Conventions library to persist task output?</span></span>

<span data-ttu-id="a3b57-116">Azure Batch 提供多個方法來保存工作輸出。</span><span class="sxs-lookup"><span data-stu-id="a3b57-116">Azure Batch provides more than one way to persist task output.</span></span> <span data-ttu-id="a3b57-117">檔案慣例最適合這些案例：</span><span class="sxs-lookup"><span data-stu-id="a3b57-117">The File Conventions is best suited to these scenarios:</span></span>

- <span data-ttu-id="a3b57-118">您可以輕鬆地修改您的工作正在執行的應用程式程式碼，使用檔案慣例程式庫來保存檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-118">You can easily modify the code for the application that your task is running to persist files using the File Conventions library.</span></span>
- <span data-ttu-id="a3b57-119">您在工作還在執行時，想要將資料串流至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a3b57-119">You want to stream data to Azure Storage while the task is still running.</span></span>
- <span data-ttu-id="a3b57-120">您想要保存的資料是在使用雲端服務設定或虛擬機器設定建立的集區中。</span><span class="sxs-lookup"><span data-stu-id="a3b57-120">You want to persist data from pools created with either the cloud service configuration or the virtual machine configuration.</span></span>
- <span data-ttu-id="a3b57-121">用戶端應用程式或作業中的其他工作必須依識別碼或依用途來尋找及下載工作輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-121">Your client application or other tasks in the job needs to locate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="a3b57-122">您想要在 Azure 入口網站中檢視工作輸出。</span><span class="sxs-lookup"><span data-stu-id="a3b57-122">You want to view task output in the Azure portal.</span></span>

<span data-ttu-id="a3b57-123">如果您的情節與以上所列不同，可能需要考慮不同的方法。</span><span class="sxs-lookup"><span data-stu-id="a3b57-123">If your scenario differs from those listed above, you may need to consider a different approach.</span></span> <span data-ttu-id="a3b57-124">如需保存工作輸出之其他選項的詳細資訊，請參閱[將作業和工作輸出保存到 Azure 儲存體](batch-task-output.md)。</span><span class="sxs-lookup"><span data-stu-id="a3b57-124">For more information on other options for persisting task output, see [Persist job and task output to Azure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-the-batch-file-conventions-standard"></a><span data-ttu-id="a3b57-125">Batch 檔案慣例標準是什麼？</span><span class="sxs-lookup"><span data-stu-id="a3b57-125">What is the Batch File Conventions standard?</span></span>

<span data-ttu-id="a3b57-126">[Batch 檔案慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)提供目的地容器的命名配置，以及寫入輸出檔案的 blob 路徑。</span><span class="sxs-lookup"><span data-stu-id="a3b57-126">The [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for the destination containers and blob paths to which your output files are written.</span></span> <span data-ttu-id="a3b57-127">保存到 Azure 儲存體 (符合檔案慣例標準) 的檔案會自動可在 Azure 入口網站中檢視。</span><span class="sxs-lookup"><span data-stu-id="a3b57-127">Files persisted to Azure Storage that adhere to the File Conventions standard are automatically available for viewing in the Azure portal.</span></span> <span data-ttu-id="a3b57-128">入口網站知道命名慣例，因此可以顯示符合它的檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-128">The portal is aware of the naming convention and so can display files that adhere to it.</span></span>

<span data-ttu-id="a3b57-129">適用於 .NET 的檔案慣例程式庫會根據檔案慣例標準，自動命名您的儲存體容器和工作輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-129">The File Conventions library for .NET automatically names your storage containers and task output files according to the File Conventions standard.</span></span> <span data-ttu-id="a3b57-130">檔案慣例程式庫也提供方法來根據作業識別碼、工作識別碼或目的，在 Azure 儲存體中查詢輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-130">The File Conventions library also provides methods to query output files in Azure Storage according to job ID, task ID, or purpose.</span></span>   

<span data-ttu-id="a3b57-131">如果您要使用 .NET 以外的語言進行開發，可以在您的應用程式中自行實作檔案慣例標準。</span><span class="sxs-lookup"><span data-stu-id="a3b57-131">If you are developing with a language other than .NET, you can implement the File Conventions standard yourself in your application.</span></span> <span data-ttu-id="a3b57-132">如需詳細資訊，請參閱[關於 Batch 檔案慣例標準](batch-task-output.md#about-the-batch-file-conventions-standard)。</span><span class="sxs-lookup"><span data-stu-id="a3b57-132">For more information, see [About the Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-to-your-batch-account"></a><span data-ttu-id="a3b57-133">將 Azure 儲存體帳戶連結到您的 Batch 帳戶</span><span class="sxs-lookup"><span data-stu-id="a3b57-133">Link an Azure Storage account to your Batch account</span></span>

<span data-ttu-id="a3b57-134">若要使用檔案慣例程式庫將輸出資料保存到 Azure 儲存體，您必須先將 Azure 儲存體帳戶連結到您的 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3b57-134">To persist output data to Azure Storage using the File Conventions library, you must first link an Azure Storage account to your Batch account.</span></span> <span data-ttu-id="a3b57-135">如果您尚未這麼做，請使用 [Azure 入口網站](https://portal.azure.com)將儲存體帳戶連結到您的 Batch 帳戶：</span><span class="sxs-lookup"><span data-stu-id="a3b57-135">If you haven't done so already, link a Storage account to your Batch account by using the [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="a3b57-136">在 Azure 入口網站中瀏覽至您的 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3b57-136">Navigate to your Batch account in the Azure portal.</span></span> 
2. <span data-ttu-id="a3b57-137">在 [設定] 下，選取 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="a3b57-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="a3b57-138">如果您還沒有與您的 Batch 帳戶相關聯的儲存體帳戶，請按一下 [儲存體帳戶 (無)]。</span><span class="sxs-lookup"><span data-stu-id="a3b57-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="a3b57-139">從訂用帳戶清單中選取儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3b57-139">Select a Storage account from the list for your subscription.</span></span> <span data-ttu-id="a3b57-140">為了達到最佳效能，使用位於與您執行工作所在之 Batch 帳戶相同區域的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3b57-140">For best performance, use an Azure Storage account that is in the same region as the Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="a3b57-141">保存輸出資料</span><span class="sxs-lookup"><span data-stu-id="a3b57-141">Persist output data</span></span>

<span data-ttu-id="a3b57-142">若要使用檔案慣例程式庫保存作業和工作輸出資料，請在 Azure 儲存體中建立容器，然後將輸出儲存至容器。</span><span class="sxs-lookup"><span data-stu-id="a3b57-142">To persist job and task output data with the File Conventions library, create a container in Azure Storage, then save the output to the container.</span></span> <span data-ttu-id="a3b57-143">在您的工作程式碼中使用[適用於 .NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)，將工作輸出上傳到容器中。</span><span class="sxs-lookup"><span data-stu-id="a3b57-143">Use the [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code to upload the task output to the container.</span></span> 

<span data-ttu-id="a3b57-144">如需在 Azure 儲存體中使用容器和 Blob 的詳細資訊，請參閱[以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="a3b57-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="a3b57-145">使用檔案慣例程式庫保存的所有作業和工作輸出，都會儲存在相同容器中。</span><span class="sxs-lookup"><span data-stu-id="a3b57-145">All job and task outputs persisted with the File Conventions library are stored in the same container.</span></span> <span data-ttu-id="a3b57-146">如果大量工作同時嘗試保存檔案，可能會強制執行[儲存體節流限制](../storage/common/storage-performance-checklist.md#blobs)。</span><span class="sxs-lookup"><span data-stu-id="a3b57-146">If a large number of tasks try to persist files at the same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="a3b57-147">建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="a3b57-147">Create storage container</span></span>

<span data-ttu-id="a3b57-148">若要將工作輸出保存到 Azure 儲存體，先建立一個名為 [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync] 的容器。</span><span class="sxs-lookup"><span data-stu-id="a3b57-148">To persist task output to Azure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="a3b57-149">這個擴充方法會採用 [CloudStorageAccount][net_cloudstorageaccount] 物件作為參數。</span><span class="sxs-lookup"><span data-stu-id="a3b57-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="a3b57-150">它會建立容器，容器名稱是根據檔案慣例標準，使其內容可以由 Azure 入口網站和本文稍後討論的擷取方法進行探索。</span><span class="sxs-lookup"><span data-stu-id="a3b57-150">It creates a container named according to the File Conventions standard,so that its contents are discoverable by the Azure portal and the retrieval methods discussed later in the article.</span></span>

<span data-ttu-id="a3b57-151">您通常會放置此程式碼以在用戶端應用程式中建立容器 &mdash; 也就是建立您的集區、作業及工作的應用程式。</span><span class="sxs-lookup"><span data-stu-id="a3b57-151">You typically place the code to create a container in your client application &mdash; the application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference to the linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create the blob storage container for the outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="a3b57-152">儲存工作輸出</span><span class="sxs-lookup"><span data-stu-id="a3b57-152">Store task outputs</span></span>

<span data-ttu-id="a3b57-153">當您在 Azure 儲存體中備妥容器之後，工作便可以使用檔案慣例程式庫中的 [TaskOutputStorage][net_taskoutputstorage] 類別來將輸出儲存到容器。</span><span class="sxs-lookup"><span data-stu-id="a3b57-153">Now that you've prepared a container in Azure Storage, tasks can save output to the container by using the [TaskOutputStorage][net_taskoutputstorage] class found in the File Conventions library.</span></span>

<span data-ttu-id="a3b57-154">在您的工作程式碼中，先建立一個 [TaskOutputStorage][net_taskoutputstorage] 物件，然後在工作完成時呼叫 [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] 方法，以將其輸出儲存到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a3b57-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when the task has completed its work, call the [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method to save its output to Azure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code to process data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="a3b57-155">[TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) 方法的 `kind` 參數會分類保存的檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-155">The `kind` parameter of the [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes the persisted files.</span></span> <span data-ttu-id="a3b57-156">有四個預先定義的 [TaskOutputKind][net_taskoutputkind] 類型：`TaskOutput`、`TaskPreview`、`TaskLog` 和 `TaskIntermediate.`。您也可以定義輸出的自訂類別。</span><span class="sxs-lookup"><span data-stu-id="a3b57-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="a3b57-157">這些輸出類型可供您在稍後針對特定工作的保存輸出查詢 Batch 時，指定要列出的輸出類型。</span><span class="sxs-lookup"><span data-stu-id="a3b57-157">These output types allow you to specify which type of outputs to list when you later query Batch for the persisted outputs of a given task.</span></span> <span data-ttu-id="a3b57-158">換句話說，當您列出某個工作的輸出時，可以根據其中一個輸出類型來篩選清單。</span><span class="sxs-lookup"><span data-stu-id="a3b57-158">In other words, when you list the outputs for a task, you can filter the list on one of the output types.</span></span> <span data-ttu-id="a3b57-159">例如，「給我工作 *109* 的 *preview* 輸出」。</span><span class="sxs-lookup"><span data-stu-id="a3b57-159">For example, "Give me the *preview* output for task *109*."</span></span> <span data-ttu-id="a3b57-160">本文稍後的 [擷取輸出](#retrieve-output) 會提供列出和擷取輸出的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="a3b57-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in the article.</span></span>

> [!TIP]
> <span data-ttu-id="a3b57-161">輸出類型也會決定特定檔案出現在 Azure 入口網站的位置：TaskOutput 類別的檔案會出現在 [工作輸出檔案] 底下，而 TaskLog 檔案會出現在 [工作記錄] 底下。</span><span class="sxs-lookup"><span data-stu-id="a3b57-161">The output kind also determines where in the Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="a3b57-162">儲存工作輸出</span><span class="sxs-lookup"><span data-stu-id="a3b57-162">Store job outputs</span></span>

<span data-ttu-id="a3b57-163">除了儲存工作輸出，您也可以儲存和整個作業相關聯的輸出。</span><span class="sxs-lookup"><span data-stu-id="a3b57-163">In addition to storing task outputs, you can store the outputs associated with an entire job.</span></span> <span data-ttu-id="a3b57-164">例如，在影片轉譯作業的合併工作中，您可以將完整轉譯的影片以作業輸出的形式保存。</span><span class="sxs-lookup"><span data-stu-id="a3b57-164">For example, in the merge task of a movie rendering job, you could persist the fully rendered movie as a job output.</span></span> <span data-ttu-id="a3b57-165">當您的作業完成時，用戶端應用程式即可列出並擷取該作業的輸出，而不需要查詢個別的工作。</span><span class="sxs-lookup"><span data-stu-id="a3b57-165">When your job is completed, your client application can list and retrieve the outputs for the job, and does not need to query the individual tasks.</span></span>

<span data-ttu-id="a3b57-166">呼叫 [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] 方法，並指定 [JobOutputKind][net_joboutputkind] 和檔案名稱以儲存作業輸出：</span><span class="sxs-lookup"><span data-stu-id="a3b57-166">Store job output by calling the [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify the [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="a3b57-167">如同工作輸出的 **TaskOutputKind** 類型，您會使用 [JobOutputKind][net_joboutputkind] 類型來分類作業的保存檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-167">As with the **TaskOutputKind** type for task outputs, you use the [JobOutputKind][net_joboutputkind] type to categorize a job's persisted files.</span></span> <span data-ttu-id="a3b57-168">此參數可讓您在稍後查詢 (列出) 特定的輸出類型。</span><span class="sxs-lookup"><span data-stu-id="a3b57-168">This parameter allows you to later query for (list) a specific type of output.</span></span> <span data-ttu-id="a3b57-169">**JobOutputKind** 類型包含了輸出和預覽類別，且支援建立自訂類別。</span><span class="sxs-lookup"><span data-stu-id="a3b57-169">The **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="a3b57-170">儲存工作記錄檔</span><span class="sxs-lookup"><span data-stu-id="a3b57-170">Store task logs</span></span>

<span data-ttu-id="a3b57-171">除了在工作或作業完成時將檔案保存到永久性儲存體之外，您可能也會需要保存在工作執行期間更新的檔案 &mdash; 例如記錄檔或 `stdout.txt` 和 `stderr.txt`。</span><span class="sxs-lookup"><span data-stu-id="a3b57-171">In addition to persisting a file to durable storage when a task or job completes, you may need to persist files that are updated during the execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="a3b57-172">針對此目的，Azure Batch 檔案慣例庫會提供 [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] 方法。</span><span class="sxs-lookup"><span data-stu-id="a3b57-172">For this purpose, the Azure Batch File Conventions library provides the [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="a3b57-173">透過 [SaveTrackedAsync][net_savetrackedasync]，您可以追蹤節點上檔案的更新 (依照您指定的時間間隔)，並將這些更新保存到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a3b57-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates to a file on the node (at an interval that you specify) and persist those updates to Azure Storage.</span></span>

<span data-ttu-id="a3b57-174">在下列程式碼片段中，我們使用 [SaveTrackedAsync][net_savetrackedasync]，於工作執行期間每 15 秒更新一次 Azure 儲存體中的 `stdout.txt`：</span><span class="sxs-lookup"><span data-stu-id="a3b57-174">In the following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] to update `stdout.txt` in Azure Storage every 15 seconds during the execution of the task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// The primary task logic is wrapped in a using statement that sends updates to
// the stdout.txt blob in Storage every 15 seconds while the task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code to process data and produce output file(s) */

    // We are tracking the disk file to save our standard output, but the
    // node agent may take up to 3 seconds to flush the stdout stream to
    // disk. So give the file a moment to catch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="a3b57-175">加上註解的區段 `Code to process data and produce output file(s)` 是您的工作正常會執行的程式碼預留位置。</span><span class="sxs-lookup"><span data-stu-id="a3b57-175">The commented section `Code to process data and produce output file(s)` is a placeholder for the code that your task would normally perform.</span></span> <span data-ttu-id="a3b57-176">例如，您可能有程式碼會從 Azure 儲存體下載資料，並對這些資料執行轉換或計算。</span><span class="sxs-lookup"><span data-stu-id="a3b57-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="a3b57-177">此程式碼片段的重點，在於示範如何將這樣的程式碼用 `using` 區塊包裝，以透過 [SaveTrackedAsync][net_savetrackedasync] 定期更新檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-177">The important part of this snippet is demonstrating how you can wrap such code in a `using` block to periodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="a3b57-178">節點代理程式是一項程式，會在集區中的每個節點上執行，並在節點與 Batch 服務之間提供命令和控制介面。</span><span class="sxs-lookup"><span data-stu-id="a3b57-178">The node agent is a program that runs on each node in the pool and provides the command-and-control interface between the node and the Batch service.</span></span> <span data-ttu-id="a3b57-179">`Task.Delay` 呼叫在此 `using` 區塊的結尾是必要的，以確保節點代理程式有時間清除節點上 stdout.txt 檔案的標準內容。</span><span class="sxs-lookup"><span data-stu-id="a3b57-179">The `Task.Delay` call is required at the end of this `using` block to ensure that the node agent has time to flush the contents of standard out to the stdout.txt file on the node.</span></span> <span data-ttu-id="a3b57-180">若沒有此延遲，就可能會遺漏輸出的最後幾秒。</span><span class="sxs-lookup"><span data-stu-id="a3b57-180">Without this delay, it is possible to miss the last few seconds of output.</span></span> <span data-ttu-id="a3b57-181">此延遲可能並非所有檔案都需要。</span><span class="sxs-lookup"><span data-stu-id="a3b57-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="a3b57-182">當您使用 **SaveTrackedAsync** 啟用檔案追蹤時，只有附加到追蹤檔案的資料會保存到 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="a3b57-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* to the tracked file are persisted to Azure Storage.</span></span> <span data-ttu-id="a3b57-183">請只將此方法用於追蹤非輪替記錄檔，或其他使用附加作業寫入至結尾的檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-183">Use this method only for tracking non-rotating log files or other files that are written to with append operations to the end of the file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="a3b57-184">擷取輸出資料</span><span class="sxs-lookup"><span data-stu-id="a3b57-184">Retrieve output data</span></span>

<span data-ttu-id="a3b57-185">當您使用 Azure Batch 檔案慣例庫擷取保存的輸出時，您是以工作和作業為主的方式進行。</span><span class="sxs-lookup"><span data-stu-id="a3b57-185">When you retrieve your persisted output using the Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="a3b57-186">您可以要求指定工作或作業的輸出，而不需要知道它在 Azure 儲存體中的位置，甚至連檔案名稱也不需要。</span><span class="sxs-lookup"><span data-stu-id="a3b57-186">You can request the output for given task or job without needing to know its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="a3b57-187">相反地，您可以依據工作或作業識別碼要求輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="a3b57-188">下列程式碼片段會逐一查看作業的工作，並顯示該工作輸出檔案的相關資訊，然後從儲存體下載該工作的檔案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-188">The following code snippet iterates through a job's tasks, prints some information about the output files for the task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-the-azure-portal"></a><span data-ttu-id="a3b57-189">在 Azure 入口網站中檢視輸出檔案</span><span class="sxs-lookup"><span data-stu-id="a3b57-189">View output files in the Azure portal</span></span>

<span data-ttu-id="a3b57-190">Azure 入口網站會顯示使用 [Batch 檔案慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)保存到已連結 Azure 儲存體帳戶的工作輸出檔案和記錄。</span><span class="sxs-lookup"><span data-stu-id="a3b57-190">The Azure portal displays task output files and logs that are persisted to a linked Azure Storage account using the [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="a3b57-191">您可以使用自選的語言實作這些慣例，或是使用 .NET 應用程式中的檔案慣例程式庫。</span><span class="sxs-lookup"><span data-stu-id="a3b57-191">You can implement these conventions yourself in the a language of your choice, or you can use the File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="a3b57-192">若要讓您的輸出檔案顯示在入口網站中，您必須滿足下列需求：</span><span class="sxs-lookup"><span data-stu-id="a3b57-192">To enable the display of your output files in the portal, you must satisfy the following requirements:</span></span>

1. <span data-ttu-id="a3b57-193">[連結 Azure 儲存體帳戶](#requirement-linked-storage-account) 到您的 Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a3b57-193">[Link an Azure Storage account](#requirement-linked-storage-account) to your Batch account.</span></span>
2. <span data-ttu-id="a3b57-194">保存輸出時，依照預先定義的儲存體容器命名與檔案命名慣例。</span><span class="sxs-lookup"><span data-stu-id="a3b57-194">Adhere to the predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="a3b57-195">您可以在檔案慣例程式庫的[讀我檔案][github_file_conventions_readme]中找到這些慣例的定義。</span><span class="sxs-lookup"><span data-stu-id="a3b57-195">You can find the definition of these conventions in the File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="a3b57-196">如果您使用 [Azure Batch 檔案慣例][nuget_package]程式庫來保存您的輸出，您的檔案會根據檔案慣例標準進行保存。</span><span class="sxs-lookup"><span data-stu-id="a3b57-196">If you use the [Azure Batch File Conventions][nuget_package] library to persist your output, your files are persisted according to the File Conventions standard.</span></span>

<span data-ttu-id="a3b57-197">若要在 Azure 入口網站中檢視工作輸出檔案和記錄，請瀏覽到您對其輸出有興趣的工作，然後按一下 [已儲存的輸出檔案] 或 [已儲存的記錄]。</span><span class="sxs-lookup"><span data-stu-id="a3b57-197">To view task output files and logs in the Azure portal, navigate to the task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="a3b57-198">此影像顯示識別碼為 "007" 之工作的 [已儲存的輸出檔案]  ：</span><span class="sxs-lookup"><span data-stu-id="a3b57-198">This image shows the **Saved output files** for the task with ID "007":</span></span>

<span data-ttu-id="a3b57-199">![Azure 入口網站中的 [工作輸出] 刀鋒視窗][2]</span><span class="sxs-lookup"><span data-stu-id="a3b57-199">![Task outputs blade in the Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="a3b57-200">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="a3b57-200">Code sample</span></span>

<span data-ttu-id="a3b57-201">[PersistOutputs][github_persistoutputs] 範例專案是 GitHub 上的其中一個 [Azure Batch 程式碼範例][github_samples]。</span><span class="sxs-lookup"><span data-stu-id="a3b57-201">The [PersistOutputs][github_persistoutputs] sample project is one of the [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="a3b57-202">此 Visual Studio 解決方案示範如何使用 Azure Batch 檔案慣例庫，將工作輸出保存到永久性儲存體。</span><span class="sxs-lookup"><span data-stu-id="a3b57-202">This Visual Studio solution demonstrates how to use the Azure Batch File Conventions library to persist task output to durable storage.</span></span> <span data-ttu-id="a3b57-203">若要執行範例，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="a3b57-203">To run the sample, follow these steps:</span></span>

1. <span data-ttu-id="a3b57-204">在 **Visual Studio 2015 或更新版本**中開啟專案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-204">Open the project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="a3b57-205">將您 Batch 和儲存體的**帳戶認證**新增到 Microsoft.Azure.Batch.Samples.Common 專案中的 **AccountSettings.settings**。</span><span class="sxs-lookup"><span data-stu-id="a3b57-205">Add your Batch and Storage **account credentials** to **AccountSettings.settings** in the Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="a3b57-206"> (但不要執行) 該解決方案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-206">**Build** (but do not run) the solution.</span></span> <span data-ttu-id="a3b57-207">如果出現提示，請還原任何 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="a3b57-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="a3b57-208">使用 Azure 入口網站來為 [PersistOutputsTask](batch-application-packages.md) 上傳 **應用程式封裝**。</span><span class="sxs-lookup"><span data-stu-id="a3b57-208">Use the Azure portal to upload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="a3b57-209">將 `PersistOutputsTask.exe` 及其相依性組件包含在 .zip 封裝中，將應用程式識別碼和應用程式封裝版本分別設為 "PersistOutputsTask" 和 "1.0"。</span><span class="sxs-lookup"><span data-stu-id="a3b57-209">Include the `PersistOutputsTask.exe` and its dependent assemblies in the .zip package, set the application ID to "PersistOutputsTask", and the application package version to "1.0".</span></span>
5. <span data-ttu-id="a3b57-210">**啟動** (執行) **PersistOutputs** 專案。</span><span class="sxs-lookup"><span data-stu-id="a3b57-210">**Start** (run) the **PersistOutputs** project.</span></span>
6. <span data-ttu-id="a3b57-211">當系統提示您選擇要用於執行範例的持續性技術時，輸入 **1** 可使用檔案慣例程式庫保存工作輸出來執行範例。</span><span class="sxs-lookup"><span data-stu-id="a3b57-211">When prompted to choose the persistence technology to use for running the sample, enter **1** to run the sample using the File Conventions library to persist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a3b57-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a3b57-212">Next steps</span></span>

### <a name="get-the-batch-file-conventions-library-for-net"></a><span data-ttu-id="a3b57-213">取得適用於 .NET 的 Batch 檔案慣例程式庫</span><span class="sxs-lookup"><span data-stu-id="a3b57-213">Get the Batch File Conventions library for .NET</span></span>

<span data-ttu-id="a3b57-214">適用於 .NET 的 Batch 檔案慣例程式庫可以在 [NuGet][nuget_package] 取得。</span><span class="sxs-lookup"><span data-stu-id="a3b57-214">The Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="a3b57-215">程式庫會使用新方法擴充 [CloudJob][net_cloudjob] 和 [CloudTask][net_cloudtask] 類別。</span><span class="sxs-lookup"><span data-stu-id="a3b57-215">The library extends the [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="a3b57-216">另請參閱檔案慣例程式庫的[參考文件](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files)。</span><span class="sxs-lookup"><span data-stu-id="a3b57-216">Also see the [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for the File Conventions library.</span></span>

<span data-ttu-id="a3b57-217">檔案慣例程式庫的[原始程式碼][github_file_conventions]可以在 GitHub 上的 Microsoft Azure SDK for .NET 存放庫中取得。</span><span class="sxs-lookup"><span data-stu-id="a3b57-217">The [source code][github_file_conventions] for the File Conventions library is available on GitHub in the Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="a3b57-218">探索保存輸出資料的其他方法</span><span class="sxs-lookup"><span data-stu-id="a3b57-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="a3b57-219">請參閱[將作業和工作輸出保存到 Azure 儲存體](batch-task-output.md)，以取得保存工作和作業資料的概觀。</span><span class="sxs-lookup"><span data-stu-id="a3b57-219">See [Persist job and task output to Azure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="a3b57-220">請參閱[使用 Batch 服務 API 將工作資料保存到 Azure 儲存體](batch-task-output-files.md)，以深入了解如何使用 Batch 服務 API 來保存輸出資料。</span><span class="sxs-lookup"><span data-stu-id="a3b57-220">See [Persist task data to Azure Storage with the Batch service API](batch-task-output-files.md) to learn how to use the Batch service API to persist output data.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "入口網站中的 [已儲存的輸出檔案] 和 [已儲存的記錄檔] 選取器"
[2]: ./media/batch-task-output/task-output-02.png "Azure 入口網站中的 [工作輸出] 刀鋒視窗"
