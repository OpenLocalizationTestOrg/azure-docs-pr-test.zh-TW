---
title: "aaaPersist 作業和工作輸出 hello 檔案慣例程式庫的儲存體 tooAzure for.NET-Azure 批次 |Microsoft 文件"
description: "了解如何 toouse.NET toopersist 批次工作的 Azure 批次檔慣例文件庫和工作輸出 tooAzure 存放裝置和檢視 hello 保存 hello Azure 入口網站中的輸出。"
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
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="33621-103">保存工作和工作資料 tooAzure 儲存體與 hello.NET toopersist 的批次檔慣例文件庫</span><span class="sxs-lookup"><span data-stu-id="33621-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="33621-104">其中一種方式 toopersist 工作資料為 toouse hello[適用於.NET 的 Azure 批次檔慣例程式庫][nuget_package]。</span><span class="sxs-lookup"><span data-stu-id="33621-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="33621-105">hello 檔案慣例程式庫會簡化 hello 程序儲存工作輸出的資料 tooAzure 儲存和擷取。</span><span class="sxs-lookup"><span data-stu-id="33621-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="33621-106">您可以使用工作和用戶端程式碼中的 hello 檔案慣例文件庫&mdash;保存檔案，工作的程式碼和用戶端程式碼 toolist，並將其擷取。</span><span class="sxs-lookup"><span data-stu-id="33621-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="33621-107">工作程式碼也可以使用 hello 庫 tooretrieve hello 輸出上游的工作，例如[工作相依性](batch-task-dependencies.md)案例。</span><span class="sxs-lookup"><span data-stu-id="33621-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="33621-108">tooretrieve 輸出與 hello 檔案慣例媒體櫃的檔案，您可以找到 hello 檔案指定的工作或工作識別碼的用途中列出它們。</span><span class="sxs-lookup"><span data-stu-id="33621-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="33621-109">您不需要 tooknow hello 名稱或 hello 檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="33621-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="33621-110">例如，您可以用於 hello 檔案慣例文件庫 toolist 所有中繼檔案指定的工作，或取得給定作業的預覽檔案。</span><span class="sxs-lookup"><span data-stu-id="33621-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="33621-111">從 2017年-05-01 版開始，hello 批次服務應用程式開發介面支援保存的輸出資料 tooAzure 儲存體工作和使用 hello 虛擬機器組態建立的集區上執行的作業管理員工作。</span><span class="sxs-lookup"><span data-stu-id="33621-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="33621-112">hello 批次服務 API 提供簡單的方式 toopersist hello 程式碼所建立的工作，並做為替代 toohello 檔案慣例的文件庫中的輸出。</span><span class="sxs-lookup"><span data-stu-id="33621-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="33621-113">您可以修改批次用戶端應用程式 toopersist 輸出，而不需要您的工作正在執行的 tooupdate hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="33621-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="33621-114">如需詳細資訊，請參閱[保存以 hello 批次服務應用程式開發介面的工作資料 tooAzure 儲存體](batch-task-output-files.md)。</span><span class="sxs-lookup"><span data-stu-id="33621-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="33621-115">何時使用 hello 檔案慣例庫 toopersist 工作輸出？</span><span class="sxs-lookup"><span data-stu-id="33621-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="33621-116">Azure 批次提供多個單向 toopersist 工作輸出。</span><span class="sxs-lookup"><span data-stu-id="33621-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="33621-117">hello 檔案慣例是最適合的 toothese 案例：</span><span class="sxs-lookup"><span data-stu-id="33621-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="33621-118">您可以輕鬆地修改 hello hello 應用程式確認您的工作正在執行 toopersist 檔案使用 hello 檔案慣例程式庫的程式碼。</span><span class="sxs-lookup"><span data-stu-id="33621-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="33621-119">Hello 工作仍在執行時，您會想 toostream 資料 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="33621-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="33621-120">您想要從以 hello 雲端服務組態或 hello 虛擬機器組態建立的集區的 toopersist 資料。</span><span class="sxs-lookup"><span data-stu-id="33621-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="33621-121">用戶端應用程式或其他工作在 hello 作業需求 toolocate 和下載工作輸出檔依識別碼或依用途。</span><span class="sxs-lookup"><span data-stu-id="33621-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="33621-122">您想 tooview hello Azure 入口網站中的工作輸出。</span><span class="sxs-lookup"><span data-stu-id="33621-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="33621-123">如果您的案例與以上所列不同，您可能需要 tooconsider 不同的方法。</span><span class="sxs-lookup"><span data-stu-id="33621-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="33621-124">如需保存的工作輸出的其他選項的詳細資訊，請參閱[保存作業和工作輸出 tooAzure 儲存體](batch-task-output.md)。</span><span class="sxs-lookup"><span data-stu-id="33621-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="33621-125">什麼是標準的批次檔慣例 hello？</span><span class="sxs-lookup"><span data-stu-id="33621-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="33621-126">hello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)hello 目的地容器和 blob 路徑 toowhich 輸出檔案會寫入提供的命名配置。</span><span class="sxs-lookup"><span data-stu-id="33621-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="33621-127">檔案保存的 tooAzure 遵守 toohello 檔案慣例標準的儲存體都會自動供 hello Azure 入口網站中的檢視。</span><span class="sxs-lookup"><span data-stu-id="33621-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="33621-128">hello 入口網站可感知 hello 命名慣例，而且因此可以顯示遵守 tooit 的檔案。</span><span class="sxs-lookup"><span data-stu-id="33621-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="33621-129">適用於.NET 的 hello 檔案慣例程式庫會自動命名您的儲存體容器和工作的輸出檔案根據 toohello 標準檔案慣例。</span><span class="sxs-lookup"><span data-stu-id="33621-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="33621-130">hello 檔案慣例程式庫也會提供 Azure 儲存體中的方法 tooquery 輸出檔案根據 toojob ID、 工作識別碼或用途。</span><span class="sxs-lookup"><span data-stu-id="33621-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="33621-131">如果您正在開發以.NET 以外的語言，您可以實作 hello 檔案慣例標準自己應用程式中。</span><span class="sxs-lookup"><span data-stu-id="33621-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="33621-132">如需詳細資訊，請參閱[關於 hello 批次檔慣例標準](batch-task-output.md#about-the-batch-file-conventions-standard)。</span><span class="sxs-lookup"><span data-stu-id="33621-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="33621-133">連結的 Azure 儲存體帳戶 tooyour 批次帳戶</span><span class="sxs-lookup"><span data-stu-id="33621-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="33621-134">toopersist 輸出資料 tooAzure 使用 hello 檔案慣例程式庫的儲存體，您必須先連結的 Azure 儲存體帳戶 tooyour Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="33621-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="33621-135">如果您尚未這樣做，批次帳戶的儲存體帳戶 tooyour 使用連結 hello [Azure 入口網站](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="33621-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="33621-136">瀏覽 tooyour hello Azure 入口網站中的批次帳戶。</span><span class="sxs-lookup"><span data-stu-id="33621-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="33621-137">在 [設定] 下，選取 [儲存體帳戶]。</span><span class="sxs-lookup"><span data-stu-id="33621-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="33621-138">如果您還沒有與您的 Batch 帳戶相關聯的儲存體帳戶，請按一下 [儲存體帳戶 (無)]。</span><span class="sxs-lookup"><span data-stu-id="33621-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="33621-139">從訂用帳戶的 hello 清單中選取的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="33621-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="33621-140">為了達到最佳效能，使用 Azure 儲存體帳戶中 hello，正在您的工作與 hello 批次帳戶相同的區域。</span><span class="sxs-lookup"><span data-stu-id="33621-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="33621-141">保存輸出資料</span><span class="sxs-lookup"><span data-stu-id="33621-141">Persist output data</span></span>

<span data-ttu-id="33621-142">toopersist 作業和工作使用 hello 檔案慣例程式庫輸出的資料，請建立容器，在 Azure 儲存體，然後儲存 hello 輸出 toohello 容器。</span><span class="sxs-lookup"><span data-stu-id="33621-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="33621-143">使用 hello[適用於.NET 的 Azure 儲存體用戶端程式庫](https://www.nuget.org/packages/WindowsAzure.Storage)您工作的程式碼 tooupload hello 工作輸出 toohello 容器中。</span><span class="sxs-lookup"><span data-stu-id="33621-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="33621-144">如需在 Azure 儲存體中使用容器和 Blob 的詳細資訊，請參閱[以 .NET 開始使用 Azure Blob 儲存體](../storage/blobs/storage-dotnet-how-to-use-blobs.md)。</span><span class="sxs-lookup"><span data-stu-id="33621-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="33621-145">與程式庫會儲存在 hello 檔案慣例一起保存的所有作業和工作的輸出 hello 相同的容器。</span><span class="sxs-lookup"><span data-stu-id="33621-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="33621-146">如果大量的工作嘗試 toopersist 使用位於檔案 hello 相同時間[儲存體節流限制](../storage/common/storage-performance-checklist.md#blobs)可能會強制執行。</span><span class="sxs-lookup"><span data-stu-id="33621-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="33621-147">建立儲存體容器</span><span class="sxs-lookup"><span data-stu-id="33621-147">Create storage container</span></span>

<span data-ttu-id="33621-148">toopersist 工作輸出 tooAzure 儲存體，先建立容器，藉由呼叫[CloudJob][net_cloudjob]。[PrepareOutputStorageAsync][net_prepareoutputasync]。</span><span class="sxs-lookup"><span data-stu-id="33621-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="33621-149">這個擴充方法會採用 [CloudStorageAccount][net_cloudstorageaccount] 物件作為參數。</span><span class="sxs-lookup"><span data-stu-id="33621-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="33621-150">它會建立具名相應 toohello 檔案慣例標準，使其內容是可探索的 hello hello 本文稍後所述的 Azure 入口網站與 hello 擷取方法的容器。</span><span class="sxs-lookup"><span data-stu-id="33621-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="33621-151">您通常將 hello 程式碼 toocreate 容器放在用戶端應用程式&mdash;hello 建立您的集區、 工作和工作的應用程式。</span><span class="sxs-lookup"><span data-stu-id="33621-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="33621-152">儲存工作輸出</span><span class="sxs-lookup"><span data-stu-id="33621-152">Store task outputs</span></span>

<span data-ttu-id="33621-153">既然您已備妥在 Azure 儲存體容器，工作可以使用將儲存輸出 toohello 容器 hello [TaskOutputStorage] [ net_taskoutputstorage] hello 檔案慣例文件庫中找到的類別。</span><span class="sxs-lookup"><span data-stu-id="33621-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="33621-154">在您工作的程式碼，先建立[TaskOutputStorage] [ net_taskoutputstorage]物件，然後 hello 工作已完成其工作，當呼叫 hello [TaskOutputStorage] [ net_taskoutputstorage].[SaveAsync] [ net_saveasync]方法 toosave 其輸出 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="33621-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="33621-155">hello `kind` hello 參數[TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx)。[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx)方法來分類 hello 保存檔案。</span><span class="sxs-lookup"><span data-stu-id="33621-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="33621-156">有四個預先定義的 [TaskOutputKind][net_taskoutputkind] 類型：`TaskOutput`、`TaskPreview`、`TaskLog` 和 `TaskIntermediate.`。您也可以定義輸出的自訂類別。</span><span class="sxs-lookup"><span data-stu-id="33621-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="33621-157">這些輸出類型可讓您 toospecify 哪種類型的輸出 toolist，當您稍後查詢 hello 批次中保存指定工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="33621-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="33621-158">換句話說，當您列出 hello 輸出工作，您可以篩選 hello 清單的某個 hello 輸出類型。</span><span class="sxs-lookup"><span data-stu-id="33621-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="33621-159">例如，"給我 hello*預覽*工作輸出*109*。 」</span><span class="sxs-lookup"><span data-stu-id="33621-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="33621-160">需列出和擷取輸出的詳細資訊會出現在[擷取輸出](#retrieve-output)hello 文件中的更新版本。</span><span class="sxs-lookup"><span data-stu-id="33621-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="33621-161">hello 輸出種類也會決定在 hello Azure 入口網站特定的檔案出現的位置： *TaskOutput*-分類的檔案會出現在**工作輸出檔**，和*TaskLog*檔案會出現在**工作記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="33621-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="33621-162">儲存工作輸出</span><span class="sxs-lookup"><span data-stu-id="33621-162">Store job outputs</span></span>

<span data-ttu-id="33621-163">此外 toostoring 工作輸出，您就可以儲存 hello 整項作業相關聯的輸出。</span><span class="sxs-lookup"><span data-stu-id="33621-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="33621-164">比方說，在 hello 合併工作的影片轉譯作業中，您可能會完整呈現的 hello 影片保留做為工作輸出。</span><span class="sxs-lookup"><span data-stu-id="33621-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="33621-165">您的工作完成時，用戶端應用程式可以列出和擷取 hello hello 工作的輸出，並不需要 tooquery hello 個別工作。</span><span class="sxs-lookup"><span data-stu-id="33621-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="33621-166">儲存工作輸出呼叫 hello [JobOutputStorage][net_joboutputstorage]。[SaveAsync] [ net_joboutputstorage_saveasync]方法，並指定 hello [JobOutputKind] [ net_joboutputkind]和檔案名稱：</span><span class="sxs-lookup"><span data-stu-id="33621-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="33621-167">如同 hello **TaskOutputKind**類型為工作輸出，您可以使用 hello [JobOutputKind] [ net_joboutputkind]類型 toocategorize 工作的保存檔案。</span><span class="sxs-lookup"><span data-stu-id="33621-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="33621-168">這個參數可讓您 toolater （清單） 的輸出特定類型的查詢。</span><span class="sxs-lookup"><span data-stu-id="33621-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="33621-169">hello **JobOutputKind**類型包含輸出和預覽類別，並支援建立自訂的類別。</span><span class="sxs-lookup"><span data-stu-id="33621-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="33621-170">儲存工作記錄檔</span><span class="sxs-lookup"><span data-stu-id="33621-170">Store task logs</span></span>

<span data-ttu-id="33621-171">此外 toopersisting 檔案 toodurable 儲存體時的工作或作業完成，您可能需要 toopersist 檔案 hello 工作執行期間更新&mdash;記錄檔或`stdout.txt`和`stderr.txt`，例如。</span><span class="sxs-lookup"><span data-stu-id="33621-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="33621-172">基於此目的，hello Azure 批次檔慣例程式庫提供 hello [TaskOutputStorage][net_taskoutputstorage]。[SaveTrackedAsync] [ net_savetrackedasync]方法。</span><span class="sxs-lookup"><span data-stu-id="33621-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="33621-173">與[SaveTrackedAsync][net_savetrackedasync]，您可以追蹤 hello 節點 （在您指定的間隔內） 上的更新 tooa 檔案並保存這些更新 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="33621-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="33621-174">在下列程式碼片段的 hello，我們使用[SaveTrackedAsync] [ net_savetrackedasync] tooupdate`stdout.txt`在 Azure 儲存體 hello hello 工作執行期間每 15 秒：</span><span class="sxs-lookup"><span data-stu-id="33621-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="33621-175">hello 標記為註解區段`Code tooprocess data and produce output file(s)`是 hello 通常會執行您的工作的程式碼的預留位置。</span><span class="sxs-lookup"><span data-stu-id="33621-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="33621-176">例如，您可能有程式碼會從 Azure 儲存體下載資料，並對這些資料執行轉換或計算。</span><span class="sxs-lookup"><span data-stu-id="33621-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="33621-177">hello 很重要的一部分此程式碼片段會示範如何將包裝在這類程式碼`using`區塊 tooperiodically 更新的檔案[SaveTrackedAsync][net_savetrackedasync]。</span><span class="sxs-lookup"><span data-stu-id="33621-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="33621-178">hello 節點代理程式是 hello 集區中的每個節點上執行，並提供 hello 節點與 hello 批次服務之間的 hello 命令控制項介面的程式。</span><span class="sxs-lookup"><span data-stu-id="33621-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="33621-179">hello`Task.Delay`呼叫是這個 hello 結尾需要`using`hello 節點代理程式的區塊 tooensure 出 hello 節點上 toohello stdout.txt 檔案含有標準時間 tooflush hello 內容。</span><span class="sxs-lookup"><span data-stu-id="33621-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="33621-180">沒有這項延遲，就可能 toomiss hello 輸出的最後幾秒。</span><span class="sxs-lookup"><span data-stu-id="33621-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="33621-181">此延遲可能並非所有檔案都需要。</span><span class="sxs-lookup"><span data-stu-id="33621-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="33621-182">當您啟用檔案與追蹤**SaveTrackedAsync**，則只*附加*toohello 追蹤的檔案會保存的 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="33621-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="33621-183">使用這個方法只可以用於追蹤非輪替記錄檔或其他檔案寫入 toowith 附加 hello 檔案作業 toohello 結尾。</span><span class="sxs-lookup"><span data-stu-id="33621-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="33621-184">擷取輸出資料</span><span class="sxs-lookup"><span data-stu-id="33621-184">Retrieve output data</span></span>

<span data-ttu-id="33621-185">當您擷取保存的輸出使用 hello Azure 批次檔慣例程式庫時，您在進行工作和工作中心的方式。</span><span class="sxs-lookup"><span data-stu-id="33621-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="33621-186">您可以要求 hello 輸出指定的工作或作業而不需要 tooknow 它在 Azure 儲存體或甚至是其檔案名稱中的路徑。</span><span class="sxs-lookup"><span data-stu-id="33621-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="33621-187">相反地，您可以依據工作或作業識別碼要求輸出檔案。</span><span class="sxs-lookup"><span data-stu-id="33621-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="33621-188">hello 下列程式碼片段逐一查看作業的工作會列印 hello hello 工作的輸出檔的一些資訊，然後從儲存體下載檔案。</span><span class="sxs-lookup"><span data-stu-id="33621-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

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

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="33621-189">Hello Azure 入口網站中檢視輸出檔</span><span class="sxs-lookup"><span data-stu-id="33621-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="33621-190">hello Azure 入口網站會顯示工作輸出的檔案和記錄都會保存的 tooa 連結的 Azure 儲存體帳戶使用 hello[批次檔慣例標準](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions)。</span><span class="sxs-lookup"><span data-stu-id="33621-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="33621-191">您可以實作這些慣例自行在 hello 您選擇的語言，或您可以使用.NET 應用程式中的 hello 檔案慣例程式庫。</span><span class="sxs-lookup"><span data-stu-id="33621-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="33621-192">tooenable hello 顯示 hello 入口網站中的輸出檔案，您必須滿足下列需求的 hello:</span><span class="sxs-lookup"><span data-stu-id="33621-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="33621-193">[Azure 儲存體帳戶連結](#requirement-linked-storage-account)tooyour Batch 帳戶。</span><span class="sxs-lookup"><span data-stu-id="33621-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="33621-194">保存輸出時，請遵守 toohello 預先定義的命名慣例，儲存體容器和檔案。</span><span class="sxs-lookup"><span data-stu-id="33621-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="33621-195">您可以在 hello 檔案慣例文件庫中找到的這些慣例的 hello 定義[讀我檔案][github_file_conventions_readme]。</span><span class="sxs-lookup"><span data-stu-id="33621-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="33621-196">如果您使用 hello [Azure 批次檔慣例][ nuget_package]文件庫 toopersist 您輸出，您的檔案會保存根據 toohello 標準檔案慣例。</span><span class="sxs-lookup"><span data-stu-id="33621-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="33621-197">tooview 工作輸出檔，並登入 hello Azure 入口網站，瀏覽您感興趣，其輸出 continuación，elija toohello 工作**儲存輸出檔案**或**儲存記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="33621-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="33621-198">下圖顯示 hello**儲存輸出檔案**識別碼為"007"hello 工作：</span><span class="sxs-lookup"><span data-stu-id="33621-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="33621-199">![工作輸出 刀鋒視窗中 hello Azure 入口網站][2]</span><span class="sxs-lookup"><span data-stu-id="33621-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="33621-200">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="33621-200">Code sample</span></span>

<span data-ttu-id="33621-201">hello [PersistOutputs] [ github_persistoutputs]範例專案是其中一個 hello [Azure 批次程式碼範例][ github_samples] GitHub 上。</span><span class="sxs-lookup"><span data-stu-id="33621-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="33621-202">這個 Visual Studio 方案會示範如何 toouse hello Azure 批次檔慣例的文件庫 toopersist 工作輸出 toodurable 儲存體。</span><span class="sxs-lookup"><span data-stu-id="33621-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="33621-203">toorun hello 範例，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="33621-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="33621-204">在開啟 hello 專案**2015年或更新版本的 Visual Studio**。</span><span class="sxs-lookup"><span data-stu-id="33621-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="33621-205">新增您的批次和儲存體**帳戶認證**太**AccountSettings.settings** hello Microsoft.Azure.Batch.Samples.Common 專案中。</span><span class="sxs-lookup"><span data-stu-id="33621-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="33621-206">**建置**（但不是會執行） hello 方案。</span><span class="sxs-lookup"><span data-stu-id="33621-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="33621-207">如果出現提示，請還原任何 NuGet 封裝。</span><span class="sxs-lookup"><span data-stu-id="33621-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="33621-208">使用 hello Azure 入口網站 tooupload[應用程式封裝](batch-application-packages.md)如**PersistOutputsTask**。</span><span class="sxs-lookup"><span data-stu-id="33621-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="33621-209">包含 hello `PersistOutputsTask.exe` hello.zip 套件中，設定 hello 應用程式識別碼及其相依組件太"PersistOutputsTask 」，以及 hello 應用程式封裝的版本太"1.0 的"。</span><span class="sxs-lookup"><span data-stu-id="33621-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="33621-210">**啟動**（執行） 的 hello **PersistOutputs**專案。</span><span class="sxs-lookup"><span data-stu-id="33621-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="33621-211">當提示的 toochoose hello 持續性技術 toouse 執行 hello 範例中，輸入**1** toorun hello 範例使用 hello 檔案慣例庫 toopersist 工作輸出。</span><span class="sxs-lookup"><span data-stu-id="33621-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="33621-212">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33621-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="33621-213">取得 hello 批次檔慣例 library for.NET</span><span class="sxs-lookup"><span data-stu-id="33621-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="33621-214">hello 批次檔慣例 library for.NET 是用於[NuGet][nuget_package]。</span><span class="sxs-lookup"><span data-stu-id="33621-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="33621-215">hello 程式庫會擴充 hello [CloudJob] [ net_cloudjob]和[CloudTask] [ net_cloudtask]類別的新方法。</span><span class="sxs-lookup"><span data-stu-id="33621-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="33621-216">另請參閱 hello[參考文件](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files)hello 檔案慣例程式庫。</span><span class="sxs-lookup"><span data-stu-id="33621-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="33621-217">hello[原始程式碼][ github_file_conventions] hello 檔案慣例程式庫會提供在 GitHub 上 hello Microsoft Azure SDK for.NET 的儲存機制。</span><span class="sxs-lookup"><span data-stu-id="33621-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="33621-218">探索保存輸出資料的其他方法</span><span class="sxs-lookup"><span data-stu-id="33621-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="33621-219">請參閱[保存作業和工作輸出 tooAzure 儲存體](batch-task-output.md)保存的工作和作業資料的概觀。</span><span class="sxs-lookup"><span data-stu-id="33621-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="33621-220">請參閱[保存以 hello 批次服務應用程式開發介面的工作資料 tooAzure 儲存體](batch-task-output-files.md)toolearn toouse hello 批次服務 API toopersist 資料的輸出。</span><span class="sxs-lookup"><span data-stu-id="33621-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

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
[2]: ./media/batch-task-output/task-output-02.png "工作輸出 刀鋒視窗中 hello Azure 入口網站"
