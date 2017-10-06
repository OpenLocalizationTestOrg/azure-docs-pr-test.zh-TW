---
title: "aaaCreate 工作 tooprepare 工作和計算節點-Azure 批次上完成的工作 |Microsoft 文件"
description: "使用工作層級的準備工作 toominimize 資料傳輸 tooAzure 批次計算節點，並釋放節點清除在作業完成的工作。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="9c10d-103">在 Batch 計算節點上執行作業準備和作業解除工作</span><span class="sxs-lookup"><span data-stu-id="9c10d-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="9c10d-104">Azure Batch 作業在執行其工作之前，通常需要經過某種形式的設定，並需要在其工作完成時進行後置作業維護。</span><span class="sxs-lookup"><span data-stu-id="9c10d-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="9c10d-105">您可能需要 toodownload 常見工作的輸入的資料 tooyour 計算節點，或 hello 作業完成之後，請上傳工作的輸出資料 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="9c10d-105">You might need toodownload common task input data tooyour compute nodes, or upload task output data tooAzure Storage after hello job completes.</span></span> <span data-ttu-id="9c10d-106">您可以使用**作業準備**和**作業發行**工作 tooperform 這些作業。</span><span class="sxs-lookup"><span data-stu-id="9c10d-106">You can use **job preparation** and **job release** tasks tooperform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="9c10d-107">什麼是作業準備和作業解除工作？</span><span class="sxs-lookup"><span data-stu-id="9c10d-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="9c10d-108">執行作業的工作之前，hello 作業準備工作上執行所有計算節點排程 toorun 至少一個工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-108">Before a job's tasks run, hello job preparation task runs on all compute nodes scheduled toorun at least one task.</span></span> <span data-ttu-id="9c10d-109">Hello 作業完成後，hello 作業解除工作會執行至少一個工作的 hello 集區中的每個節點上執行。</span><span class="sxs-lookup"><span data-stu-id="9c10d-109">Once hello job is completed, hello job release task runs on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="9c10d-110">如同一般的批次工作，您可以指定作業準備時叫用命令列 toobe 或發行工作執行。</span><span class="sxs-lookup"><span data-stu-id="9c10d-110">As with normal Batch tasks, you can specify a command line toobe invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="9c10d-111">作業準備和作業解除工作會提供熟悉的 Batch 工作功能，例如檔案下載 ([資源檔][net_job_prep_resourcefiles])、提升權限的執行、自訂環境變數、最大執行持續時間、重試計數和檔案保留時間。</span><span class="sxs-lookup"><span data-stu-id="9c10d-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="9c10d-112">在下列各節的 hello，您將學習如何 toouse hello [JobPreparationTask] [ net_job_prep]和[JobReleaseTask] [ net_job_release] hello 中找到類別[批次.NET] [ api_net]程式庫。</span><span class="sxs-lookup"><span data-stu-id="9c10d-112">In hello following sections, you'll learn how toouse hello [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in hello [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="9c10d-113">作業準備和作業解除工作在「共用集區」環境中特別有用；在這種環境中，計算節點的集區會在作業執行之間保存，並由許多作業使用。</span><span class="sxs-lookup"><span data-stu-id="9c10d-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a><span data-ttu-id="9c10d-114">當 toouse 作業準備工作，並釋放工作</span><span class="sxs-lookup"><span data-stu-id="9c10d-114">When toouse job preparation and release tasks</span></span>
<span data-ttu-id="9c10d-115">作業準備及作業版本 」 工作是適合 hello 下列情況：</span><span class="sxs-lookup"><span data-stu-id="9c10d-115">Job preparation and job release tasks are a good fit for hello following situations:</span></span>

<span data-ttu-id="9c10d-116">**下載常見的工作資料**</span><span class="sxs-lookup"><span data-stu-id="9c10d-116">**Download common task data**</span></span>

<span data-ttu-id="9c10d-117">批次作業通常需要一組常用的資料，做為輸入 hello 作業的工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-117">Batch jobs often require a common set of data as input for hello job's tasks.</span></span> <span data-ttu-id="9c10d-118">例如，在每日的風險分析計算市場資料是 hello 作業中的工作特有的但常見 tooall 工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-118">For example, in daily risk analysis calculations, market data is job-specific, yet common tooall tasks in hello job.</span></span> <span data-ttu-id="9c10d-119">此市場資料時，通常有幾個 gb 的大小，應該下載的 tooeach 計算節點一次以便在 hello 節點執行任何工作可以使用它。</span><span class="sxs-lookup"><span data-stu-id="9c10d-119">This market data, often several gigabytes in size, should be downloaded tooeach compute node only once so that any task that runs on hello node can use it.</span></span> <span data-ttu-id="9c10d-120">使用**作業準備工作**toodownload 這個資料 tooeach 節點之前 hello hello 工作執行的其他工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-120">Use a **job preparation task** toodownload this data tooeach node before hello execution of hello job's other tasks.</span></span>

<span data-ttu-id="9c10d-121">**刪除作業和工作的輸出**</span><span class="sxs-lookup"><span data-stu-id="9c10d-121">**Delete job and task output**</span></span>

<span data-ttu-id="9c10d-122">在 「 共用集區 」 環境中，其中的集區計算節點不是已解除任務工作之間，您可能需要執行之間的 toodelete 作業資料。</span><span class="sxs-lookup"><span data-stu-id="9c10d-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need toodelete job data between runs.</span></span> <span data-ttu-id="9c10d-123">您可能需要 tooconserve hello 節點上的磁碟空間或符合您的組織安全性原則。</span><span class="sxs-lookup"><span data-stu-id="9c10d-123">You might need tooconserve disk space on hello nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="9c10d-124">使用**作業解除工作**所下載的作業準備工作，或期間所產生的 toodelete 資料工作執行。</span><span class="sxs-lookup"><span data-stu-id="9c10d-124">Use a **job release task** toodelete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="9c10d-125">**記錄保留**</span><span class="sxs-lookup"><span data-stu-id="9c10d-125">**Log retention**</span></span>

<span data-ttu-id="9c10d-126">您可能想 tookeep 記錄檔，產生您的工作或可能是損毀傾印檔案可能會產生失敗的應用程式的複本。</span><span class="sxs-lookup"><span data-stu-id="9c10d-126">You might want tookeep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="9c10d-127">使用**作業解除工作**中這類情況下 toocompress 並上傳此資料 tooan [Azure 儲存體][ azure_storage]帳戶。</span><span class="sxs-lookup"><span data-stu-id="9c10d-127">Use a **job release task** in such cases toocompress and upload this data tooan [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="9c10d-128">另一個方式 toopersist 記錄檔及其他作業和工作輸出資料為 toouse hello [Azure 批次檔慣例](batch-task-output.md)程式庫。</span><span class="sxs-lookup"><span data-stu-id="9c10d-128">Another way toopersist logs and other job and task output data is toouse hello [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="9c10d-129">作業準備工作</span><span class="sxs-lookup"><span data-stu-id="9c10d-129">Job preparation task</span></span>
<span data-ttu-id="9c10d-130">之前執行作業的工作時，批次會執行 hello 作業準備工作會排定的 toorun 工作每個計算節點上。</span><span class="sxs-lookup"><span data-stu-id="9c10d-130">Before execution of a job's tasks, Batch executes hello job preparation task on each compute node that is scheduled toorun a task.</span></span> <span data-ttu-id="9c10d-131">根據預設，hello 批次服務會等到 hello 作業準備工作 toobe hello 節點上執行 hello 工作排程的 tooexecute 之前完成。</span><span class="sxs-lookup"><span data-stu-id="9c10d-131">By default, hello Batch service waits for hello job preparation task toobe completed before running hello tasks scheduled tooexecute on hello node.</span></span> <span data-ttu-id="9c10d-132">不過，您可以設定 hello 服務不 toowait。</span><span class="sxs-lookup"><span data-stu-id="9c10d-132">However, you can configure hello service not toowait.</span></span> <span data-ttu-id="9c10d-133">如果 hello 節點重新啟動，hello 作業準備工作會執行一次，但您也可以停用此行為。</span><span class="sxs-lookup"><span data-stu-id="9c10d-133">If hello node restarts, hello job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="9c10d-134">只有在排程的 toorun 工作的節點上執行 hello 作業準備工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-134">hello job preparation task is executed only on nodes that are scheduled toorun a task.</span></span> <span data-ttu-id="9c10d-135">如果節點未指派工作，這可防止 hello 不需要執行的準備工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-135">This prevents hello unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="9c10d-136">發生這個問題 hello 作業的工作數目小於 hello 集區中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="9c10d-136">This can occur when hello number of tasks for a job is less than hello number of nodes in a pool.</span></span> <span data-ttu-id="9c10d-137">它也適用於當[並行工作執行](batch-parallel-node-tasks.md)已啟用，讓某些節點閒置如果 hello 工作計數低於 hello 總可能並行的工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if hello task count is lower than hello total possible concurrent tasks.</span></span> <span data-ttu-id="9c10d-138">由閒置的節點未執行 hello 作業準備工作，您可以在資料傳輸費用花成本較低。</span><span class="sxs-lookup"><span data-stu-id="9c10d-138">By not running hello job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="9c10d-139">[JobPreparationTask] [ net_job_prep_cloudjob]不同於[CloudPool.StartTask] [ pool_starttask] ，而執行的每個工作中，hello 開頭 JobPreparationTask StartTask只有當運算節點第一次加入集區會執行或重新啟動。</span><span class="sxs-lookup"><span data-stu-id="9c10d-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at hello start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="9c10d-140">作業解除工作</span><span class="sxs-lookup"><span data-stu-id="9c10d-140">Job release task</span></span>
<span data-ttu-id="9c10d-141">一旦作業標示為已完成，hello 作業解除工作被執行至少一個工作的 hello 集區中的每個節點上執行。</span><span class="sxs-lookup"><span data-stu-id="9c10d-141">Once a job is marked as completed, hello job release task is executed on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="9c10d-142">透過發出終止要求將工作標示為完成。</span><span class="sxs-lookup"><span data-stu-id="9c10d-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="9c10d-143">hello 批次服務，然後設定太 hello 工作狀態*終止*、 終止與 hello 工作相關聯的任何作用中或執行工作，並執行 hello 作業解除工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-143">hello Batch service then sets hello job state too*terminating*, terminates any active or running tasks associated with hello job, and runs hello job release task.</span></span> <span data-ttu-id="9c10d-144">hello 作業接著將移 toohello*完成*狀態。</span><span class="sxs-lookup"><span data-stu-id="9c10d-144">hello job then moves toohello *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="9c10d-145">刪除作業也會執行 hello 作業解除工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-145">Job deletion also executes hello job release task.</span></span> <span data-ttu-id="9c10d-146">不過，已終止工作，hello 解除工作會執行第二次，如果稍後刪除 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="9c10d-146">However, if a job has already been terminated, hello release task is not run a second time if hello job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="9c10d-147">使用 Batch .NET 進行作業準備和作業解除工作</span><span class="sxs-lookup"><span data-stu-id="9c10d-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="9c10d-148">toouse 作業準備工作，指派[JobPreparationTask] [ net_job_prep]物件 tooyour 作業的[CloudJob.JobPreparationTask] [ net_job_prep_cloudjob]屬性.</span><span class="sxs-lookup"><span data-stu-id="9c10d-148">toouse a job preparation task, assign a [JobPreparationTask][net_job_prep] object tooyour job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="9c10d-149">同樣地，初始化[JobReleaseTask] [ net_job_release]並將它指派 tooyour 作業[CloudJob.JobReleaseTask] [ net_job_prep_cloudjob]屬性 tooset hello作業解除工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it tooyour job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property tooset hello job's release task.</span></span>

<span data-ttu-id="9c10d-150">在此程式碼片段中，`myBatchClient`的執行個體[BatchClient][net_batch_client]，和`myPool`是 hello 批次帳戶中現有的集區。</span><span class="sxs-lookup"><span data-stu-id="9c10d-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within hello Batch account.</span></span>

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="9c10d-151">如先前所述，hello 解除工作會執行作業已終止或已刪除。</span><span class="sxs-lookup"><span data-stu-id="9c10d-151">As mentioned earlier, hello release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="9c10d-152">使用 [JobOperations.TerminateJobAsync][net_job_terminate] 終止作業。</span><span class="sxs-lookup"><span data-stu-id="9c10d-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="9c10d-153">使用 [JobOperations.DeleteJobAsync][net_job_delete] 刪除作業。</span><span class="sxs-lookup"><span data-stu-id="9c10d-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="9c10d-154">您通常會在作業的工作完成時或達到定義之逾時時終止或刪除作業。</span><span class="sxs-lookup"><span data-stu-id="9c10d-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="9c10d-155">GitHub 上的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="9c10d-155">Code sample on GitHub</span></span>
<span data-ttu-id="9c10d-156">toosee 作業準備和發佈工作的動作，請參閱 hello [JobPrepRelease] [ job_prep_release_sample] GitHub 上的範例專案。</span><span class="sxs-lookup"><span data-stu-id="9c10d-156">toosee job preparation and release tasks in action, check out hello [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="9c10d-157">此主控台應用程式沒有 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="9c10d-157">This console application does hello following:</span></span>

1. <span data-ttu-id="9c10d-158">建立包含兩個「小」節點的集區。</span><span class="sxs-lookup"><span data-stu-id="9c10d-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="9c10d-159">建立具有作業準備、解除和標準工作的作業。</span><span class="sxs-lookup"><span data-stu-id="9c10d-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="9c10d-160">執行 hello 作業準備工作，先將 hello 節點識別碼 tooa 文字檔寫入節點的 「 共用 」 目錄中。</span><span class="sxs-lookup"><span data-stu-id="9c10d-160">Runs hello job preparation task, which first writes hello node ID tooa text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="9c10d-161">寫入其工作識別碼 toohello 每個節點上執行的工作相同的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="9c10d-161">Runs a task on each node that writes its task ID toohello same text file.</span></span>
5. <span data-ttu-id="9c10d-162">一旦完成所有工作 （或達到 hello 逾時），會列印每個節點的文字檔案 toohello 主控台 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="9c10d-162">Once all tasks are completed (or hello timeout is reached), prints hello contents of each node's text file toohello console.</span></span>
6. <span data-ttu-id="9c10d-163">Hello 作業完成時，會執行 hello 作業發行工作 toodelete hello 檔案從 hello 節點。</span><span class="sxs-lookup"><span data-stu-id="9c10d-163">When hello job is completed, runs hello job release task toodelete hello file from hello node.</span></span>
7. <span data-ttu-id="9c10d-164">列印 hello 結束代碼的 hello 作業準備工作，並釋放每個節點執行所在的工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-164">Prints hello exit codes of hello job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="9c10d-165">暫停執行的作業和/或集區刪除的 tooallow 確認。</span><span class="sxs-lookup"><span data-stu-id="9c10d-165">Pauses execution tooallow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="9c10d-166">Hello 範例應用程式的輸出是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="9c10d-166">Output from hello sample application is similar toohello following:</span></span>

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> <span data-ttu-id="9c10d-167">由於 toohello 變數建立和開始時間 （有些節點已做好之前其他工作） 的新集區中的節點，您可能會看到不同的輸出。</span><span class="sxs-lookup"><span data-stu-id="9c10d-167">Due toohello variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="9c10d-168">具體來說，hello 工作快速完成，因為其中 hello 集區的節點可能會執行所有 hello 作業的工作。</span><span class="sxs-lookup"><span data-stu-id="9c10d-168">Specifically, because hello tasks complete quickly, one of hello pool's nodes may execute all of hello job's tasks.</span></span> <span data-ttu-id="9c10d-169">如果發生這種情況，您會發現該 hello 作業準備與發行工作不執行的任何工作的 hello 節點不存在。</span><span class="sxs-lookup"><span data-stu-id="9c10d-169">If this occurs, you will notice that hello job prep and release tasks do not exist for hello node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a><span data-ttu-id="9c10d-170">檢查作業準備及 hello Azure 入口網站中的發行工作</span><span class="sxs-lookup"><span data-stu-id="9c10d-170">Inspect job preparation and release tasks in hello Azure portal</span></span>
<span data-ttu-id="9c10d-171">當您執行 hello 範例應用程式時，您可以使用 hello [Azure 入口網站][ portal] tooview hello hello 作業屬性及其工作，或甚至下載 hello 作業 」 工作來修改的 hello 共用的文字檔案。</span><span class="sxs-lookup"><span data-stu-id="9c10d-171">When you run hello sample application, you can use hello [Azure portal][portal] tooview hello properties of hello job and its tasks, or even download hello shared text file that is modified by hello job's tasks.</span></span>

<span data-ttu-id="9c10d-172">hello 以下螢幕擷取畫面顯示 hello**準備工作 刀鋒視窗**hello hello 範例應用程式執行之後的 Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="9c10d-172">hello screenshot below shows hello **Preparation tasks blade** in hello Azure portal after a run of hello sample application.</span></span> <span data-ttu-id="9c10d-173">瀏覽 toohello *JobPrepReleaseSampleJob*屬性您的工作完成後 （但在刪除您的工作與集區之前），按一下 **準備工作**或**釋放工作** tooview 及其屬性。</span><span class="sxs-lookup"><span data-stu-id="9c10d-173">Navigate toohello *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** tooview their properties.</span></span>

![Azure 入口網站中的作業準備屬性][1]

## <a name="next-steps"></a><span data-ttu-id="9c10d-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c10d-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="9c10d-176">應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="9c10d-176">Application packages</span></span>
<span data-ttu-id="9c10d-177">在加法 toohello 作業準備工作，您也可以使用 hello[應用程式封裝](batch-application-packages.md)的批次 tooprepare 功能的計算執行工作的節點。</span><span class="sxs-lookup"><span data-stu-id="9c10d-177">In addition toohello job preparation task, you can also use hello [application packages](batch-application-packages.md) feature of Batch tooprepare compute nodes for task execution.</span></span> <span data-ttu-id="9c10d-178">這項功能特別適合用於部署不需要執行安裝程式的應用程式、包含許多 (100 個以上) 檔案的應用程式，或需要嚴格版本控制的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9c10d-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="9c10d-179">安裝應用程式和預備資料</span><span class="sxs-lookup"><span data-stu-id="9c10d-179">Installing applications and staging data</span></span>
<span data-ttu-id="9c10d-180">這篇 MSDN 論壇文章概述幾個方法來讓您的節點做好執行工作的準備︰</span><span class="sxs-lookup"><span data-stu-id="9c10d-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="9c10d-181">[在 Batch 計算節點上安裝應用程式和預備資料][forum_post]</span><span class="sxs-lookup"><span data-stu-id="9c10d-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="9c10d-182">它其中寫入 hello Azure 批次小組成員，討論您可以使用 toodeploy 應用程式和資料 toocompute 節點的數種技術。</span><span class="sxs-lookup"><span data-stu-id="9c10d-182">Written by one of hello Azure Batch team members, it discusses several techniques that you can use toodeploy applications and data toocompute nodes.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
