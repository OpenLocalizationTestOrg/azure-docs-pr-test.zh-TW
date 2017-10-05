---
title: "建立用來準備作業的工作並對計算節點完成作業 - Azure Batch | Microsoft Docs"
description: "使用作業層級準備工作以減少傳輸到 Azure Batch 計算節點的資料，並在作業完成時解除工作以清理節點。"
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
ms.openlocfilehash: 6a2525c02ce7bd3969469d2e28a5fccc948f89b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="4bd64-103">在 Batch 計算節點上執行作業準備和作業解除工作</span><span class="sxs-lookup"><span data-stu-id="4bd64-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="4bd64-104">Azure Batch 作業在執行其工作之前，通常需要經過某種形式的設定，並需要在其工作完成時進行後置作業維護。</span><span class="sxs-lookup"><span data-stu-id="4bd64-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="4bd64-105">您可能需要將常見的工作輸入資料下載到計算節點，或在作業完成後，將工作輸出資料上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="4bd64-105">You might need to download common task input data to your compute nodes, or upload task output data to Azure Storage after the job completes.</span></span> <span data-ttu-id="4bd64-106">您可以使用**作業準備**和**作業解除**工作來執行這些操作。</span><span class="sxs-lookup"><span data-stu-id="4bd64-106">You can use **job preparation** and **job release** tasks to perform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="4bd64-107">什麼是作業準備和作業解除工作？</span><span class="sxs-lookup"><span data-stu-id="4bd64-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="4bd64-108">在作業的工作執行之前，會在排定執行至少一個工作的所有計算節點上執行作業準備工作。</span><span class="sxs-lookup"><span data-stu-id="4bd64-108">Before a job's tasks run, the job preparation task runs on all compute nodes scheduled to run at least one task.</span></span> <span data-ttu-id="4bd64-109">作業一旦完成，作業解除工作會在集區中的每個節點上執行，集區至少會執行一項工作。</span><span class="sxs-lookup"><span data-stu-id="4bd64-109">Once the job is completed, the job release task runs on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="4bd64-110">如同一般的 Batch 工作，您可以指定要在作業準備或作業解除工作執行時叫用的命令列。</span><span class="sxs-lookup"><span data-stu-id="4bd64-110">As with normal Batch tasks, you can specify a command line to be invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="4bd64-111">作業準備和作業解除工作會提供熟悉的 Batch 工作功能，例如檔案下載 ([資源檔][net_job_prep_resourcefiles])、提升權限的執行、自訂環境變數、最大執行持續時間、重試計數和檔案保留時間。</span><span class="sxs-lookup"><span data-stu-id="4bd64-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="4bd64-112">在接下來幾節中，您將了解如何使用在 [Batch .NET][api_net] 程式庫中找到的 [JobPreparationTask][net_job_prep] 和 [JobReleaseTask][net_job_release] 類別。</span><span class="sxs-lookup"><span data-stu-id="4bd64-112">In the following sections, you'll learn how to use the [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in the [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="4bd64-113">作業準備和作業解除工作在「共用集區」環境中特別有用；在這種環境中，計算節點的集區會在作業執行之間保存，並由許多作業使用。</span><span class="sxs-lookup"><span data-stu-id="4bd64-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-to-use-job-preparation-and-release-tasks"></a><span data-ttu-id="4bd64-114">使用作業準備和作業解除工作的時機</span><span class="sxs-lookup"><span data-stu-id="4bd64-114">When to use job preparation and release tasks</span></span>
<span data-ttu-id="4bd64-115">作業準備和作業解除工作適用於下列情況︰</span><span class="sxs-lookup"><span data-stu-id="4bd64-115">Job preparation and job release tasks are a good fit for the following situations:</span></span>

<span data-ttu-id="4bd64-116">**下載常見的工作資料**</span><span class="sxs-lookup"><span data-stu-id="4bd64-116">**Download common task data**</span></span>

<span data-ttu-id="4bd64-117">Batch 作業通常需要一組常用的資料做為作業工作的輸入。</span><span class="sxs-lookup"><span data-stu-id="4bd64-117">Batch jobs often require a common set of data as input for the job's tasks.</span></span> <span data-ttu-id="4bd64-118">例如，在每日風險分析計算中，市場資料是作業專屬的，也是作業中所有工作通用的。</span><span class="sxs-lookup"><span data-stu-id="4bd64-118">For example, in daily risk analysis calculations, market data is job-specific, yet common to all tasks in the job.</span></span> <span data-ttu-id="4bd64-119">這個市場資料 (通常是幾個 GB 的大小) 應該只下載到各個計算節點一次，讓在節點上執行的任何工作可以使用它。</span><span class="sxs-lookup"><span data-stu-id="4bd64-119">This market data, often several gigabytes in size, should be downloaded to each compute node only once so that any task that runs on the node can use it.</span></span> <span data-ttu-id="4bd64-120">在作業的其他工作執行之前使用 **作業準備工作** 將此資料下載到每個節點。</span><span class="sxs-lookup"><span data-stu-id="4bd64-120">Use a **job preparation task** to download this data to each node before the execution of the job's other tasks.</span></span>

<span data-ttu-id="4bd64-121">**刪除作業和工作的輸出**</span><span class="sxs-lookup"><span data-stu-id="4bd64-121">**Delete job and task output**</span></span>

<span data-ttu-id="4bd64-122">在「共用集區」環境中，作業之間的集區計算節點並未解除委任，因此您可能需要刪除執行之間的作業資料。</span><span class="sxs-lookup"><span data-stu-id="4bd64-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need to delete job data between runs.</span></span> <span data-ttu-id="4bd64-123">您可能需要保留節點上的磁碟空間，或符合組織的安全性原則。</span><span class="sxs-lookup"><span data-stu-id="4bd64-123">You might need to conserve disk space on the nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="4bd64-124">使用 **作業解除工作** 可刪除作業準備工作所下載的資料或在工作執行期間產生的資料。</span><span class="sxs-lookup"><span data-stu-id="4bd64-124">Use a **job release task** to delete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="4bd64-125">**記錄保留**</span><span class="sxs-lookup"><span data-stu-id="4bd64-125">**Log retention**</span></span>

<span data-ttu-id="4bd64-126">您可能想要保留一份工作產生的記錄檔，或失敗應用程式所產生的損毀傾印檔案。</span><span class="sxs-lookup"><span data-stu-id="4bd64-126">You might want to keep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="4bd64-127">在這類情況下使用**作業解除工作**，將此資料壓縮並上傳至 [Azure 儲存體][azure_storage]帳戶。</span><span class="sxs-lookup"><span data-stu-id="4bd64-127">Use a **job release task** in such cases to compress and upload this data to an [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="4bd64-128">另一個可保存記錄以及其他作業和工作輸出資料的方法是使用 [Azure Batch 檔案慣例](batch-task-output.md) 庫。</span><span class="sxs-lookup"><span data-stu-id="4bd64-128">Another way to persist logs and other job and task output data is to use the [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="4bd64-129">作業準備工作</span><span class="sxs-lookup"><span data-stu-id="4bd64-129">Job preparation task</span></span>
<span data-ttu-id="4bd64-130">執行作業的工作之前，Batch 會在排定執行工作的每個計算節點上執行作業準備工作。</span><span class="sxs-lookup"><span data-stu-id="4bd64-130">Before execution of a job's tasks, Batch executes the job preparation task on each compute node that is scheduled to run a task.</span></span> <span data-ttu-id="4bd64-131">依預設，Batch 服務會等作業準備工作完成，才執行節點上排定的工作。</span><span class="sxs-lookup"><span data-stu-id="4bd64-131">By default, the Batch service waits for the job preparation task to be completed before running the tasks scheduled to execute on the node.</span></span> <span data-ttu-id="4bd64-132">不過，您可以設定服務不要等待。</span><span class="sxs-lookup"><span data-stu-id="4bd64-132">However, you can configure the service not to wait.</span></span> <span data-ttu-id="4bd64-133">如果節點重新啟動，作業準備工作會再次執行，但您也可以停用此行為。</span><span class="sxs-lookup"><span data-stu-id="4bd64-133">If the node restarts, the job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="4bd64-134">作業準備工作只會在排定執行工作的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="4bd64-134">The job preparation task is executed only on nodes that are scheduled to run a task.</span></span> <span data-ttu-id="4bd64-135">這可避免未指派工作的節點執行不必要的準備工作。</span><span class="sxs-lookup"><span data-stu-id="4bd64-135">This prevents the unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="4bd64-136">這種情況會發生在當作業的工作數目小於集區中的節點數目時。</span><span class="sxs-lookup"><span data-stu-id="4bd64-136">This can occur when the number of tasks for a job is less than the number of nodes in a pool.</span></span> <span data-ttu-id="4bd64-137">此外，也適用於已啟用 [並行工作執行](batch-parallel-node-tasks.md) 時，而如果作業計數小於可能的並行工作總數，則會讓一些節點閒置。</span><span class="sxs-lookup"><span data-stu-id="4bd64-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if the task count is lower than the total possible concurrent tasks.</span></span> <span data-ttu-id="4bd64-138">藉由不在閒置的節點上執行作業準備工作，您在資料傳輸費用上可以花費更少金錢。</span><span class="sxs-lookup"><span data-stu-id="4bd64-138">By not running the job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="4bd64-139">[JobPreparationTask][net_job_prep_cloudjob] 與 [CloudPool.StartTask][pool_starttask] 的不同之處在於，JobPreparationTask 在每個作業開始時執行，而 StartTask 只在計算節點第一次加入集區或重新啟動時執行。</span><span class="sxs-lookup"><span data-stu-id="4bd64-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at the start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="4bd64-140">作業解除工作</span><span class="sxs-lookup"><span data-stu-id="4bd64-140">Job release task</span></span>
<span data-ttu-id="4bd64-141">作業一旦標示為完成，作業解除工作會在集區中的每個節點上執行，集區至少會執行一項工作。</span><span class="sxs-lookup"><span data-stu-id="4bd64-141">Once a job is marked as completed, the job release task is executed on each node in the pool that executed at least one task.</span></span> <span data-ttu-id="4bd64-142">透過發出終止要求將工作標示為完成。</span><span class="sxs-lookup"><span data-stu-id="4bd64-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="4bd64-143">然後 Batch 服務會將作業狀態設定為「正在終止」，終止與作業相關聯的任何作用中或執行中工作，並執行作業解除工作。</span><span class="sxs-lookup"><span data-stu-id="4bd64-143">The Batch service then sets the job state to *terminating*, terminates any active or running tasks associated with the job, and runs the job release task.</span></span> <span data-ttu-id="4bd64-144">作業接著會進入「已完成」狀態。</span><span class="sxs-lookup"><span data-stu-id="4bd64-144">The job then moves to the *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="4bd64-145">工作刪除也會執行工作解除任務。</span><span class="sxs-lookup"><span data-stu-id="4bd64-145">Job deletion also executes the job release task.</span></span> <span data-ttu-id="4bd64-146">不過，如果先前已終止作業，當後來刪除該作業時，解除工作不會執行第二次。</span><span class="sxs-lookup"><span data-stu-id="4bd64-146">However, if a job has already been terminated, the release task is not run a second time if the job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="4bd64-147">使用 Batch .NET 進行作業準備和作業解除工作</span><span class="sxs-lookup"><span data-stu-id="4bd64-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="4bd64-148">若要使用作業準備工作，請將 [JobPreparationTask][net_job_prep] 物件指派給作業的 [CloudJob.JobPreparationTask][net_job_prep_cloudjob] 屬性。</span><span class="sxs-lookup"><span data-stu-id="4bd64-148">To use a job preparation task, assign a [JobPreparationTask][net_job_prep] object to your job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="4bd64-149">同樣地，初始化 [JobReleaseTask][net_job_release] 並將它指派給作業的 [CloudJob.JobReleaseTask][net_job_prep_cloudjob] 屬性即可設定作業的解除任務。</span><span class="sxs-lookup"><span data-stu-id="4bd64-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it to your job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property to set the job's release task.</span></span>

<span data-ttu-id="4bd64-150">在此程式碼片段中，`myBatchClient` 是 [BatchClient][net_batch_client] 的執行個體，而 `myPool` 是 Batch 帳戶內的現有集區。</span><span class="sxs-lookup"><span data-stu-id="4bd64-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within the Batch account.</span></span>

```csharp
// Create the CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify the command lines for the job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign the job preparation task to the job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign the job release task to the job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

<span data-ttu-id="4bd64-151">如先前所述，終止或刪除作業時會執行解除任務。</span><span class="sxs-lookup"><span data-stu-id="4bd64-151">As mentioned earlier, the release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="4bd64-152">使用 [JobOperations.TerminateJobAsync][net_job_terminate] 終止作業。</span><span class="sxs-lookup"><span data-stu-id="4bd64-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="4bd64-153">使用 [JobOperations.DeleteJobAsync][net_job_delete] 刪除作業。</span><span class="sxs-lookup"><span data-stu-id="4bd64-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="4bd64-154">您通常會在作業的工作完成時或達到定義之逾時時終止或刪除作業。</span><span class="sxs-lookup"><span data-stu-id="4bd64-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate the job to mark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="4bd64-155">GitHub 上的程式碼範例</span><span class="sxs-lookup"><span data-stu-id="4bd64-155">Code sample on GitHub</span></span>
<span data-ttu-id="4bd64-156">若要了解作業準備和作業解除工作的運作，請查看 GitHub 上的 [JobPrepRelease][job_prep_release_sample] 範例專案。</span><span class="sxs-lookup"><span data-stu-id="4bd64-156">To see job preparation and release tasks in action, check out the [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="4bd64-157">此主控台應用程式會做這些事：</span><span class="sxs-lookup"><span data-stu-id="4bd64-157">This console application does the following:</span></span>

1. <span data-ttu-id="4bd64-158">建立包含兩個「小」節點的集區。</span><span class="sxs-lookup"><span data-stu-id="4bd64-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="4bd64-159">建立具有作業準備、解除和標準工作的作業。</span><span class="sxs-lookup"><span data-stu-id="4bd64-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="4bd64-160">執行作業準備工作，將節點識別碼第一次寫入節點的「共用」目錄的文字檔中。</span><span class="sxs-lookup"><span data-stu-id="4bd64-160">Runs the job preparation task, which first writes the node ID to a text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="4bd64-161">在每個節點上執行工作，將其工作識別碼寫入同一文字檔案中。</span><span class="sxs-lookup"><span data-stu-id="4bd64-161">Runs a task on each node that writes its task ID to the same text file.</span></span>
5. <span data-ttu-id="4bd64-162">一旦完成所有工作 (或達到逾時)，會列印每個節點的文字檔案的內容到主控台。</span><span class="sxs-lookup"><span data-stu-id="4bd64-162">Once all tasks are completed (or the timeout is reached), prints the contents of each node's text file to the console.</span></span>
6. <span data-ttu-id="4bd64-163">在作業完成時，執行作業解除工作會將該檔案從節點中刪除。</span><span class="sxs-lookup"><span data-stu-id="4bd64-163">When the job is completed, runs the job release task to delete the file from the node.</span></span>
7. <span data-ttu-id="4bd64-164">列印執行作業準備和解除工作的每個節點上這些工作的結束代碼。</span><span class="sxs-lookup"><span data-stu-id="4bd64-164">Prints the exit codes of the job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="4bd64-165">暫停執行以允許確認刪除作業和/或集區。</span><span class="sxs-lookup"><span data-stu-id="4bd64-165">Pauses execution to allow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="4bd64-166">範例應用程式的輸出類似這樣：</span><span class="sxs-lookup"><span data-stu-id="4bd64-166">Output from the sample application is similar to the following:</span></span>

```
Attempting to create pool: JobPrepReleaseSamplePool
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

Waiting for job JobPrepReleaseSampleJob to reach state Completed
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

Sample complete, hit ENTER to exit...
```

> [!NOTE]
> <span data-ttu-id="4bd64-167">因為新集區中各個節點的建立和啟動時間並不一樣 (某些節點比其他節點還早做好工作準備)，您可能會看到不同的輸出。</span><span class="sxs-lookup"><span data-stu-id="4bd64-167">Due to the variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="4bd64-168">具體而言，因為工作會快速完成，集區的某個節點可能會執行作業的所有工作。</span><span class="sxs-lookup"><span data-stu-id="4bd64-168">Specifically, because the tasks complete quickly, one of the pool's nodes may execute all of the job's tasks.</span></span> <span data-ttu-id="4bd64-169">如果發生這種情況，您會發現未執行任何工作的節點不會有作業準備和作業解除工作存在。</span><span class="sxs-lookup"><span data-stu-id="4bd64-169">If this occurs, you will notice that the job prep and release tasks do not exist for the node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-the-azure-portal"></a><span data-ttu-id="4bd64-170">在 Azure 入口網站中檢查作業準備和作業解除工作</span><span class="sxs-lookup"><span data-stu-id="4bd64-170">Inspect job preparation and release tasks in the Azure portal</span></span>
<span data-ttu-id="4bd64-171">當您執行範例應用程式時，您可以使用 [Azure 入口網站][portal]檢視作業和其工作的屬性，或甚至下載作業的工作修改過的共用文字檔案。</span><span class="sxs-lookup"><span data-stu-id="4bd64-171">When you run the sample application, you can use the [Azure portal][portal] to view the properties of the job and its tasks, or even download the shared text file that is modified by the job's tasks.</span></span>

<span data-ttu-id="4bd64-172">下面的螢幕擷取畫面顯示在執行範例應用程式之後，Azure 入口網站中所出現的 **準備工作刀鋒視窗** 。</span><span class="sxs-lookup"><span data-stu-id="4bd64-172">The screenshot below shows the **Preparation tasks blade** in the Azure portal after a run of the sample application.</span></span> <span data-ttu-id="4bd64-173">在工作完成之後 (但在刪除作業與集區之前) 瀏覽至 JobPrepReleaseSampleJob 屬性，然後按一下 [準備工作] 或 [解除工作] 以檢視其屬性。</span><span class="sxs-lookup"><span data-stu-id="4bd64-173">Navigate to the *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** to view their properties.</span></span>

![Azure 入口網站中的作業準備屬性][1]

## <a name="next-steps"></a><span data-ttu-id="4bd64-175">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4bd64-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="4bd64-176">應用程式封裝</span><span class="sxs-lookup"><span data-stu-id="4bd64-176">Application packages</span></span>
<span data-ttu-id="4bd64-177">除了作業準備工作外，您還可以使用 Batch 的 [應用程式封裝](batch-application-packages.md) 功能來為計算節點做好工作執行準備。</span><span class="sxs-lookup"><span data-stu-id="4bd64-177">In addition to the job preparation task, you can also use the [application packages](batch-application-packages.md) feature of Batch to prepare compute nodes for task execution.</span></span> <span data-ttu-id="4bd64-178">這項功能特別適合用於部署不需要執行安裝程式的應用程式、包含許多 (100 個以上) 檔案的應用程式，或需要嚴格版本控制的應用程式。</span><span class="sxs-lookup"><span data-stu-id="4bd64-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="4bd64-179">安裝應用程式和預備資料</span><span class="sxs-lookup"><span data-stu-id="4bd64-179">Installing applications and staging data</span></span>
<span data-ttu-id="4bd64-180">這篇 MSDN 論壇文章概述幾個方法來讓您的節點做好執行工作的準備︰</span><span class="sxs-lookup"><span data-stu-id="4bd64-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="4bd64-181">[在 Batch 計算節點上安裝應用程式和預備資料][forum_post]</span><span class="sxs-lookup"><span data-stu-id="4bd64-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="4bd64-182">其作者是其中一位 Azure Batch 小組成員，內容在討論數種可供您部署應用程式和資料到計算節點的技巧。</span><span class="sxs-lookup"><span data-stu-id="4bd64-182">Written by one of the Azure Batch team members, it discusses several techniques that you can use to deploy applications and data to compute nodes.</span></span>

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
