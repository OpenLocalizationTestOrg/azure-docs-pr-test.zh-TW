---
title: "使用多重執行個體工作執行 MPI 應用程式 - Azure Batch | Microsoft Docs"
description: "了解如何在 Azure Batch 中使用多重執行個體工作類來執行訊息傳遞介面 (MPI) 應用程式。"
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 83e34bd7-a027-4b1b-8314-759384719327
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: 5/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 77d12d6d48b22dfb3e7f09f273dffc11401bb15f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-multi-instance-tasks-to-run-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="1f984-103">在 Batch 中使用多重執行個體工作來執行訊息傳遞介面 (MPI) 應用程式</span><span class="sxs-lookup"><span data-stu-id="1f984-103">Use multi-instance tasks to run Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="1f984-104">多重執行個體工作可讓您在多個計算節點上同時執行 Azure Batch 工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-104">Multi-instance tasks allow you to run an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="1f984-105">這些工作可以在 Batch 中實現高效能運算案例，例如訊息傳遞介面 (MPI) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f984-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="1f984-106">在本文中，您將了解如何使用 [Batch .NET][api_net] 程式庫來執行多重執行個體工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-106">In this article, you learn how to execute multi-instance tasks using the [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="1f984-107">雖然本文中的範例著重於 Batch .NET、MS-MPI 和 Windows 計算節點，不過此處所討論的多重執行個體工作概念也適用於其他平台和技術 (如 Python 和 Linux 節點上的 Intel MPI)。</span><span class="sxs-lookup"><span data-stu-id="1f984-107">While the examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, the multi-instance task concepts discussed here are applicable to other platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="1f984-108">多重執行個體工作概觀</span><span class="sxs-lookup"><span data-stu-id="1f984-108">Multi-instance task overview</span></span>
<span data-ttu-id="1f984-109">在 Batch 中，每個工作通常是在單一計算節點上執行 -- 您將多個工作提交給作業，而 Batch 服務會將每個工作排定在節點上執行。</span><span class="sxs-lookup"><span data-stu-id="1f984-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks to a job, and the Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="1f984-110">不過，藉由設定工作的**多重執行個體設定**，即可告知 Batch 改為建立一個主要工作，以及數個會接著在多個節點上執行的子工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-110">However, by configuring a task's **multi-instance settings**, you tell Batch to instead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="1f984-111">![多重執行個體工作概觀][1]</span><span class="sxs-lookup"><span data-stu-id="1f984-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="1f984-112">將具有多重執行個體設定的工作提交給作業時，Batch 會執行多重執行個體工作特有的幾個步驟：</span><span class="sxs-lookup"><span data-stu-id="1f984-112">When you submit a task with multi-instance settings to a job, Batch performs several steps unique to multi-instance tasks:</span></span>

1. <span data-ttu-id="1f984-113">Batch 服務會根據多重執行個體設定，建立一個**主要**工作和數個**子工作**。</span><span class="sxs-lookup"><span data-stu-id="1f984-113">The Batch service creates one **primary** and several **subtasks** based on the multi-instance settings.</span></span> <span data-ttu-id="1f984-114">工作總數 (主要工作加上所有子工作) 與您在多重執行個體設定中指定的**執行個體** (計算節點) 數目相符。</span><span class="sxs-lookup"><span data-stu-id="1f984-114">The total number of tasks (primary plus all subtasks) matches the number of **instances** (compute nodes) you specify in the multi-instance settings.</span></span>
2. <span data-ttu-id="1f984-115">Batch 能將一個計算節點指定為**主要**節點，然後將主要工作排程在主要節點上執行。</span><span class="sxs-lookup"><span data-stu-id="1f984-115">Batch designates one of the compute nodes as the **master**, and schedules the primary task to execute on the master.</span></span> <span data-ttu-id="1f984-116">它會將子工作排程在配置給多重執行個體工作所剩餘的計算節點上執行，每個節點一個子工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-116">It schedules the subtasks to execute on the remainder of the compute nodes allocated to the multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="1f984-117">主要工作和子工作會下載您在多重執行個體設定中指定的任何**一般資源檔**。</span><span class="sxs-lookup"><span data-stu-id="1f984-117">The primary and all subtasks download any **common resource files** you specify in the multi-instance settings.</span></span>
4. <span data-ttu-id="1f984-118">下載一般資源檔之後，主要工作和子工作會執行您在多重執行個體設定中指定的 **協調命令** 。</span><span class="sxs-lookup"><span data-stu-id="1f984-118">After the common resource files have been downloaded, the primary and subtasks execute the **coordination command** you specify in the multi-instance settings.</span></span> <span data-ttu-id="1f984-119">協調命令通常用來準備執行工作所需的節點。</span><span class="sxs-lookup"><span data-stu-id="1f984-119">The coordination command is typically used to prepare nodes for executing the task.</span></span> <span data-ttu-id="1f984-120">其中包括啟動背景服務 (如 [Microsoft MPI][msmpi_msdn] 的 `smpd.exe`)，以及確認節點已準備好處理節點間的訊息。</span><span class="sxs-lookup"><span data-stu-id="1f984-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that the nodes are ready to process inter-node messages.</span></span>
5. <span data-ttu-id="1f984-121">主要工作及所有子工作順利完成協調命令「之後」，主要工作會在主要節點上執行**應用程式命令**。</span><span class="sxs-lookup"><span data-stu-id="1f984-121">The primary task executes the **application command** on the master node *after* the coordination command has been completed successfully by the primary and all subtasks.</span></span> <span data-ttu-id="1f984-122">應用程式命令是多重執行個體工作自有的命令列，而且只有主要工作能執行。</span><span class="sxs-lookup"><span data-stu-id="1f984-122">The application command is the command line of the multi-instance task itself, and is executed only by the primary task.</span></span> <span data-ttu-id="1f984-123">在 [MS-MPI][msmpi_msdn] 架構的方案中，您會在這裡使用 `mpiexec.exe` 執行已啟用 MPI 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f984-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="1f984-124">雖然「多重執行個體工作」在功能上不同，但不是特殊的工作類型，例如 [StartTask][net_starttask] 或 [JobPreparationTask][net_jobprep]。</span><span class="sxs-lookup"><span data-stu-id="1f984-124">Though it is functionally distinct, the "multi-instance task" is not a unique task type like the [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="1f984-125">多重執行個體工作只是已設定多重執行個體設定的 Standard Batch 工作 (Batch .NET 中的 [CloudTask][net_task])。</span><span class="sxs-lookup"><span data-stu-id="1f984-125">The multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="1f984-126">在本文中，我們將它稱為 **多重執行個體工作**。</span><span class="sxs-lookup"><span data-stu-id="1f984-126">In this article, we refer to this as the **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="1f984-127">多重執行個體工作的需求</span><span class="sxs-lookup"><span data-stu-id="1f984-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="1f984-128">多重執行個體工作需要有**已啟用節點間通訊**和**已停用並行工作執行**的集區。</span><span class="sxs-lookup"><span data-stu-id="1f984-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="1f984-129">若要停用並行工作執行，請將 [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) 屬性設定為 1。</span><span class="sxs-lookup"><span data-stu-id="1f984-129">To disable concurrent task execution, set the [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property to 1.</span></span>

<span data-ttu-id="1f984-130">此程式碼片段會顯示如何使用批次 .NET 程式庫來建立要供多重執行個體工作使用的集區。</span><span class="sxs-lookup"><span data-stu-id="1f984-130">This code snippet shows how to create a pool for multi-instance tasks using the Batch .NET library.</span></span>

```csharp
CloudPool myCloudPool =
    myBatchClient.PoolOperations.CreatePool(
        poolId: "MultiInstanceSamplePool",
        targetDedicatedComputeNodes: 3
        virtualMachineSize: "small",
        cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "4"));

// Multi-instance tasks require inter-node communication, and those nodes
// must run only one task at a time.
myCloudPool.InterComputeNodeCommunicationEnabled = true;
myCloudPool.MaxTasksPerComputeNode = 1;
```

> [!NOTE]
> <span data-ttu-id="1f984-131">如果您嘗試在已停用節點間通訊，或「maxTasksPerNode」  值大於 1 的集區中執行多重執行個體工作，則永遠不會排定工作--它會無限期停留在「作用中」狀態。</span><span class="sxs-lookup"><span data-stu-id="1f984-131">If you try to run a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, the task is never scheduled--it remains indefinitely in the "active" state.</span></span> 
>
> <span data-ttu-id="1f984-132">多重執行個體工作只可以在 2015 年 12 月 14 日後建立之集區中的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="1f984-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-to-install-mpi"></a><span data-ttu-id="1f984-133">使用 StartTask 安裝 MPI</span><span class="sxs-lookup"><span data-stu-id="1f984-133">Use a StartTask to install MPI</span></span>
<span data-ttu-id="1f984-134">若要執行具有多重執行個體工作的 MPI 應用程式，您必須先在集區的計算節點上安裝 MPI 實作 (例如 MS-MPI 或 Intel MPI)。</span><span class="sxs-lookup"><span data-stu-id="1f984-134">To run MPI applications with a multi-instance task, you first need to install an MPI implementation (MS-MPI or Intel MPI, for example) on the compute nodes in the pool.</span></span> <span data-ttu-id="1f984-135">這是使用 [StartTask][net_starttask] 的好時機，每當節點加入集區或重新啟動時，它就會執行。</span><span class="sxs-lookup"><span data-stu-id="1f984-135">This is a good time to use a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="1f984-136">此程式碼片段會建立 StartTask，指定 MS-MPI 安裝套件來做為[資源檔][net_resourcefile]。</span><span class="sxs-lookup"><span data-stu-id="1f984-136">This code snippet creates a StartTask that specifies the MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="1f984-137">資源檔下載至節點後，便會執行啟動工作的命令列。</span><span class="sxs-lookup"><span data-stu-id="1f984-137">The start task's command line is executed after the resource file is downloaded to the node.</span></span> <span data-ttu-id="1f984-138">在此案例中，命令列會執行 MS-MPI 的自動安裝。</span><span class="sxs-lookup"><span data-stu-id="1f984-138">In this case, the command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for the pool which we use for installing MS-MPI on
// the nodes as they join the pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit the fully configured pool to the Batch service to actually create
// the pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="1f984-139">遠端直接記憶體存取 (RDMA)</span><span class="sxs-lookup"><span data-stu-id="1f984-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="1f984-140">當您在 Batch 集區中選擇 [支援 RDMA 大小](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (如 A9 計算節點) 時，MPI 應用程式可以利用 Azure 高效能、低延遲的遠端直接記憶體存取 (RDMA) 網路。</span><span class="sxs-lookup"><span data-stu-id="1f984-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for the compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="1f984-141">在下列文章中尋找指定為「支援 RDMA」的大小︰</span><span class="sxs-lookup"><span data-stu-id="1f984-141">Look for the sizes specified as "RDMA capable" in the following articles:</span></span>

* <span data-ttu-id="1f984-142">**CloudServiceConfiguration** 集區</span><span class="sxs-lookup"><span data-stu-id="1f984-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="1f984-143">[雲端服務的大小](../cloud-services/cloud-services-sizes-specs.md) (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="1f984-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="1f984-144">**VirtualMachineConfiguration** 集區</span><span class="sxs-lookup"><span data-stu-id="1f984-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="1f984-145">[Azure 中的虛擬機器大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="1f984-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="1f984-146">[Azure 中的虛擬機器大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="1f984-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="1f984-147">若要在 [Linux 計算節點](batch-linux-nodes.md)上利用 RDMA，您必須在節點上使用 **Intel MPI**。</span><span class="sxs-lookup"><span data-stu-id="1f984-147">To take advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on the nodes.</span></span> <span data-ttu-id="1f984-148">如需 CloudServiceConfiguration 和 VirtualMachineConfiguration 集區的詳細資訊，請參閱 [Batch 功能概觀](batch-api-basics.md)的＜集區＞一節。</span><span class="sxs-lookup"><span data-stu-id="1f984-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see the Pool section of the [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="1f984-149">使用 Batch .NET 建立多個執行個體工作</span><span class="sxs-lookup"><span data-stu-id="1f984-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="1f984-150">既然我們已討論過集區需求和 MPI 套件安裝，現在讓我們建立多重執行個體工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-150">Now that we've covered the pool requirements and MPI package installation, let's create the multi-instance task.</span></span> <span data-ttu-id="1f984-151">在此片段中，我們會建立標準 [CloudTask][net_task]，然後設定其 [MultiInstanceSettings][net_multiinstance_prop] 屬性。</span><span class="sxs-lookup"><span data-stu-id="1f984-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="1f984-152">如先前所述，多重執行個體工作不是獨特的工作類型，而只是已設定多重執行個體設定的標準 Batch 工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-152">As mentioned earlier, the multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create the multi-instance task. Its command line is the "application command"
// and will be executed *only* by the primary, and only after the primary and
// subtasks execute the CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure the task's MultiInstanceSettings. The CoordinationCommandLine will be executed by
// the primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit the task to the job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on the nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="1f984-153">主要工作和子工作</span><span class="sxs-lookup"><span data-stu-id="1f984-153">Primary task and subtasks</span></span>
<span data-ttu-id="1f984-154">當您建立工作的多重執行個體設定時，您需要指定用來執行工作的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="1f984-154">When you create the multi-instance settings for a task, you specify the number of compute nodes that are to execute the task.</span></span> <span data-ttu-id="1f984-155">當您將工作提交給作業時，Batch 服務會建立一個**主要工作**和足夠的**子工作**，而且合計符合您指定的節點數。</span><span class="sxs-lookup"><span data-stu-id="1f984-155">When you submit the task to a job, the Batch service creates one **primary** task and enough **subtasks** that together match the number of nodes you specified.</span></span>

<span data-ttu-id="1f984-156">系統會指派範圍介於 0 到 *numberOfInstances* - 1 的整數識別碼給這些工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-156">These tasks are assigned an integer id in the range of 0 to *numberOfInstances* - 1.</span></span> <span data-ttu-id="1f984-157">識別碼 0 的工作是主要工作，其他所有識別碼都是子工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-157">The task with id 0 is the primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="1f984-158">比方說，如果您為工作建立下列多重執行個體設定，則主要工作的識別碼為 0，而子工作的識別碼為 1 到 9。</span><span class="sxs-lookup"><span data-stu-id="1f984-158">For example, if you create the following multi-instance settings for a task, the primary task would have an id of 0, and the subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="1f984-159">主要節點</span><span class="sxs-lookup"><span data-stu-id="1f984-159">Master node</span></span>
<span data-ttu-id="1f984-160">當您提交多重執行個體工作時，Batch 服務能將一個計算節點指定為「主要」節點，然後將主要工作排程在主要節點上執行。</span><span class="sxs-lookup"><span data-stu-id="1f984-160">When you submit a multi-instance task, the Batch service designates one of the compute nodes as the "master" node, and schedules the primary task to execute on the master node.</span></span> <span data-ttu-id="1f984-161">它會將子工作排程在配置給多重執行個體工作所剩餘的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="1f984-161">The subtasks are scheduled to execute on the remainder of the nodes allocated to the multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="1f984-162">協調命令</span><span class="sxs-lookup"><span data-stu-id="1f984-162">Coordination command</span></span>
<span data-ttu-id="1f984-163">主要工作和子工作都會執行 **協調命令** 。</span><span class="sxs-lookup"><span data-stu-id="1f984-163">The **coordination command** is executed by both the primary and subtasks.</span></span>

<span data-ttu-id="1f984-164">阻止叫用協調命令 -- 在所有子工作的協調命令順利傳回之前，Batch 不會執行應用程式命令。</span><span class="sxs-lookup"><span data-stu-id="1f984-164">The invocation of the coordination command is blocking--Batch does not execute the application command until the coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="1f984-165">因此，協調命令應該啟動任何所需的背景服務，確認它們已準備好可供使用，然後結束。</span><span class="sxs-lookup"><span data-stu-id="1f984-165">The coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="1f984-166">比方說，在使用 MS-MPI 第 7 版的方案中，此協調命令會在節點上啟動 SMPD 服務，然後結束：</span><span class="sxs-lookup"><span data-stu-id="1f984-166">For example, this coordination command for a solution using MS-MPI version 7 starts the SMPD service on the node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="1f984-167">請注意此協調命令中使用 `start` 。</span><span class="sxs-lookup"><span data-stu-id="1f984-167">Note the use of `start` in this coordination command.</span></span> <span data-ttu-id="1f984-168">這是必要的，因為 `smpd.exe` 應用程式不會在執行後立即傳回。</span><span class="sxs-lookup"><span data-stu-id="1f984-168">This is required because the `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="1f984-169">如果不使用 [start][cmd_start] 命令，此協調命令就不會傳回，因此將阻止執行應用程式命令。</span><span class="sxs-lookup"><span data-stu-id="1f984-169">Without the use of the [start][cmd_start] command, this coordination command would not return, and would therefore block the application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="1f984-170">應用程式命令</span><span class="sxs-lookup"><span data-stu-id="1f984-170">Application command</span></span>
<span data-ttu-id="1f984-171">主要工作及所有子工作完成執行協調命令之後，「只有」 主要工作會執行多重執行個體工作的命令列。</span><span class="sxs-lookup"><span data-stu-id="1f984-171">Once the primary task and all subtasks have finished executing the coordination command, the multi-instance task's command line is executed by the primary task *only*.</span></span> <span data-ttu-id="1f984-172">我們將此命令列稱為 **應用程式命令** ，以便與協調命令有所區別。</span><span class="sxs-lookup"><span data-stu-id="1f984-172">We call this the **application command** to distinguish it from the coordination command.</span></span>

<span data-ttu-id="1f984-173">針對 MS-MPI 應用程式，使用應用程式命令以 `mpiexec.exe`執行已啟用 MPI 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f984-173">For MS-MPI applications, use the application command to execute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="1f984-174">例如，以下是使用 MS-MPI 第 7 版的方案所執行的應用程式命令：</span><span class="sxs-lookup"><span data-stu-id="1f984-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="1f984-175">因為 MS-MPI 的 `mpiexec.exe` 預設會使用 `CCP_NODES` 變數 (請參閱[環境變數](#environment-variables))，上述範例應用程式命令列會排除它。</span><span class="sxs-lookup"><span data-stu-id="1f984-175">Because MS-MPI's `mpiexec.exe` uses the `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) the example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="1f984-176">環境變數</span><span class="sxs-lookup"><span data-stu-id="1f984-176">Environment variables</span></span>
<span data-ttu-id="1f984-177">Batch 會在配置給多重執行個體工作的計算節點上建立幾個多個執行個體工作特有的[環境變數][msdn_env_var]。</span><span class="sxs-lookup"><span data-stu-id="1f984-177">Batch creates several [environment variables][msdn_env_var] specific to multi-instance tasks on the compute nodes allocated to a multi-instance task.</span></span> <span data-ttu-id="1f984-178">您的協調和應用程式命令列可以參考這些環境變數，它們執行的指令碼和程式也可以。</span><span class="sxs-lookup"><span data-stu-id="1f984-178">Your coordination and application command lines can reference these environment variables, as can the scripts and programs they execute.</span></span>

<span data-ttu-id="1f984-179">以下是 Batch 服務為多重執行個體工作所建立的環境變數︰</span><span class="sxs-lookup"><span data-stu-id="1f984-179">The following environment variables are created by the Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="1f984-180">如需這些變數和其他 Batch 計算節點環境變數的完整詳細資料 (包括其內容和可見性)，請參閱[計算節點環境變數][msdn_env_var]。</span><span class="sxs-lookup"><span data-stu-id="1f984-180">For full details on these and the other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="1f984-181">Batch Linux MPI 程式碼範例含有幾個如何使用這些環境變數的範例。</span><span class="sxs-lookup"><span data-stu-id="1f984-181">The Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="1f984-182">[coordination-cmd][coord_cmd_example] Bash 指令碼能從 Azure 儲存體下載一般應用程式和輸入檔案、啟用主要節點上的網路檔案系統 (NFS) 共用，以及將配置給多重執行個體工作的其他節點設定為 NFS 用戶端。</span><span class="sxs-lookup"><span data-stu-id="1f984-182">The [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on the master node, and configures the other nodes allocated to the multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="1f984-183">資源檔</span><span class="sxs-lookup"><span data-stu-id="1f984-183">Resource files</span></span>
<span data-ttu-id="1f984-184">多重執行個體工作需要考量兩組資源檔：「所有」工作 (主要工作和子工作) 下載的**一般資源檔**，以及為多重執行個體工作本身指定的**資源檔** (「只有主要工作」會下載)。</span><span class="sxs-lookup"><span data-stu-id="1f984-184">There are two sets of resource files to consider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and the **resource files** specified for the multi-instance task itself, which *only the primary* task downloads.</span></span>

<span data-ttu-id="1f984-185">您可以在工作的多重執行個體設定中指定一或多個 **一般資源檔** 。</span><span class="sxs-lookup"><span data-stu-id="1f984-185">You can specify one or more **common resource files** in the multi-instance settings for a task.</span></span> <span data-ttu-id="1f984-186">主要工作及所有子工作會從 [Azure 儲存體](../storage/common/storage-introduction.md)，將這些一般資源檔下載到每個節點的**工作共用目錄**。</span><span class="sxs-lookup"><span data-stu-id="1f984-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by the primary and all subtasks.</span></span> <span data-ttu-id="1f984-187">您可以使用 `AZ_BATCH_TASK_SHARED_DIR` 環境變數從應用程式命令和協調命令列存取工作共用目錄。</span><span class="sxs-lookup"><span data-stu-id="1f984-187">You can access the task shared directory from application and coordination command lines by using the `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="1f984-188">每個配置給多重執行個體工作之節點上的 `AZ_BATCH_TASK_SHARED_DIR` 路徑均完全相同，因此您可以讓主要工作和所有子工作共用一個協調命令。</span><span class="sxs-lookup"><span data-stu-id="1f984-188">The `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated to the multi-instance task, thus you can share a single coordination command between the primary and all subtasks.</span></span> <span data-ttu-id="1f984-189">從遠端存取方面來看，Batch 不會「共用」目錄，不過您可以將它當做掛接點或共用點，如同先前有關環境變數的提示所述。</span><span class="sxs-lookup"><span data-stu-id="1f984-189">Batch does not "share" the directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in the tip on environment variables.</span></span>

<span data-ttu-id="1f984-190">依預設，您為多重執行個體工作本身所指定的資源檔會下載到工作的工作目錄 ( `AZ_BATCH_TASK_WORKING_DIR`) 中。</span><span class="sxs-lookup"><span data-stu-id="1f984-190">Resource files that you specify for the multi-instance task itself are downloaded to the task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="1f984-191">如前文所述，相較於一般資源檔，只有主要工作會下載為多重執行個體工作本身所指定的資源檔。</span><span class="sxs-lookup"><span data-stu-id="1f984-191">As mentioned, in contrast to common resource files, only the primary task downloads resource files specified for the  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1f984-192">在命令列中，請一律使用環境變數 `AZ_BATCH_TASK_SHARED_DIR` 和 `AZ_BATCH_TASK_WORKING_DIR` 來參考這些目錄。</span><span class="sxs-lookup"><span data-stu-id="1f984-192">Always use the environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` to refer to these directories in your command lines.</span></span> <span data-ttu-id="1f984-193">請勿嘗試以手動方式建構路徑。</span><span class="sxs-lookup"><span data-stu-id="1f984-193">Do not attempt to construct the paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="1f984-194">工作存留期</span><span class="sxs-lookup"><span data-stu-id="1f984-194">Task lifetime</span></span>
<span data-ttu-id="1f984-195">主要工作的存留期控制整個多重執行個體工作的存留期。</span><span class="sxs-lookup"><span data-stu-id="1f984-195">The lifetime of the primary task controls the lifetime of the entire multi-instance task.</span></span> <span data-ttu-id="1f984-196">當主要工作結束時，所有子工作就會終止。</span><span class="sxs-lookup"><span data-stu-id="1f984-196">When the primary exits, all of the subtasks are terminated.</span></span> <span data-ttu-id="1f984-197">主要工作的結束代碼就是工作的結束代碼，因此在重試用途上用於判斷工作成功或失敗。</span><span class="sxs-lookup"><span data-stu-id="1f984-197">The exit code of the primary is the exit code of the task, and is therefore used to determine the success or failure of the task for retry purposes.</span></span>

<span data-ttu-id="1f984-198">如果任何子工作失敗，比方說結束時傳回碼不是零，則整個多重執行個體工作會失敗。</span><span class="sxs-lookup"><span data-stu-id="1f984-198">If any of the subtasks fail, exiting with a non-zero return code, for example, the entire multi-instance task fails.</span></span> <span data-ttu-id="1f984-199">接著會終止並重試多重執行個體工作，直到觸及重試限制為止。</span><span class="sxs-lookup"><span data-stu-id="1f984-199">The multi-instance task is then terminated and retried, up to its retry limit.</span></span>

<span data-ttu-id="1f984-200">當您刪除多重執行個體工作時，Batch 服務也會刪除主要工作和所有子工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-200">When you delete a multi-instance task, the primary and all subtasks are also deleted by the Batch service.</span></span> <span data-ttu-id="1f984-201">所有子工作目錄及其檔案會從計算節點中刪除，如同在標準工作中一樣。</span><span class="sxs-lookup"><span data-stu-id="1f984-201">All subtask directories and their files are deleted from the compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="1f984-202">多重執行個體工作的 [TaskConstraints][net_taskconstraints] (例如 [MaxTaskRetryCount][net_taskconstraint_maxretry]、[MaxWallClockTime][net_taskconstraint_maxwallclock], 和 [RetentionTime][net_taskconstraint_retention] 屬性) 都視為用於標準工作，並套用至主要工作和所有子工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as the [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply to the primary and all subtasks.</span></span> <span data-ttu-id="1f984-203">不過，如果您在多重執行個體工作新增到作業之後變更 [RetentionTime][net_taskconstraint_retention] 屬性，這項變更只會套用到主要作業。</span><span class="sxs-lookup"><span data-stu-id="1f984-203">However, if you change the [RetentionTime][net_taskconstraint_retention] property after adding the multi-instance task to the job, this change is applied only to the primary task.</span></span> <span data-ttu-id="1f984-204">所有的子工作會繼續使用原始 [RetentionTime][net_taskconstraint_retention]。</span><span class="sxs-lookup"><span data-stu-id="1f984-204">All of the subtasks continue to use the original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="1f984-205">如果最近的工作是多重執行個體工作的一部分，計算節點的最近工作清單會反映子工作的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1f984-205">A compute node's recent task list reflects the id of a subtask if the recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="1f984-206">取得子工作的相關資訊</span><span class="sxs-lookup"><span data-stu-id="1f984-206">Obtain information about subtasks</span></span>
<span data-ttu-id="1f984-207">若要使用 Batch .NET 程式庫取得子工作的詳細資訊，請呼叫 [CloudTask.ListSubtasks][net_task_listsubtasks] 方法。</span><span class="sxs-lookup"><span data-stu-id="1f984-207">To obtain information on subtasks by using the Batch .NET library, call the [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="1f984-208">這個方法會傳回所有子工作的相關資訊，以及已執行工作的計算節點的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1f984-208">This method returns information on all subtasks, and information about the compute node that executed the tasks.</span></span> <span data-ttu-id="1f984-209">您可以根據這項資訊判斷每項子工作的根目錄、集區識別碼、其目前狀態、結束代碼等等。</span><span class="sxs-lookup"><span data-stu-id="1f984-209">From this information, you can determine each subtask's root directory, the pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="1f984-210">您可以使用這項資訊結合 [PoolOperations.GetNodeFile][poolops_getnodefile] 方法，以取得子工作的檔案。</span><span class="sxs-lookup"><span data-stu-id="1f984-210">You can use this information in combination with the [PoolOperations.GetNodeFile][poolops_getnodefile] method to obtain the subtask's files.</span></span> <span data-ttu-id="1f984-211">請注意，這個方法不會傳回主要工作 (識別碼 0) 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1f984-211">Note that this method does not return information for the primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="1f984-212">除非另有指明，否則在多重執行個體 [CloudTask][net_task] 本身執行的 Batch .NET 方法「只會」套用到主要工作。</span><span class="sxs-lookup"><span data-stu-id="1f984-212">Unless otherwise stated, Batch .NET methods that operate on the multi-instance [CloudTask][net_task] itself apply *only* to the primary task.</span></span> <span data-ttu-id="1f984-213">例如，當您在多重執行個體工作上呼叫 [CloudTask.ListNodeFiles][net_task_listnodefiles] 方法時，只會傳回主要工作的檔案。</span><span class="sxs-lookup"><span data-stu-id="1f984-213">For example, when you call the [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only the primary task's files are returned.</span></span>
>
>

<span data-ttu-id="1f984-214">下列程式碼片段示範如何取得子工作資訊，以及從它們執行所在的節點要求檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="1f984-214">The following code snippet shows how to obtain subtask information, as well as request file contents from the nodes on which they executed.</span></span>

```csharp
// Obtain the job and the multi-instance task from the Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain the list of subtasks for the task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over the subtasks and print their stdout and stderr
// output if the subtask has completed
await subtasks.ForEachAsync(async (subtask) =>
{
    Console.WriteLine("subtask: {0}", subtask.Id);
    Console.WriteLine("exit code: {0}", subtask.ExitCode);

    if (subtask.State == SubtaskState.Completed)
    {
        ComputeNode node =
            await batchClient.PoolOperations.GetComputeNodeAsync(subtask.ComputeNodeInformation.PoolId,
                                                                 subtask.ComputeNodeInformation.ComputeNodeId);

        NodeFile stdOutFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardOutFileName);
        NodeFile stdErrFile = await node.GetNodeFileAsync(subtask.ComputeNodeInformation.TaskRootDirectory + "\\" + Constants.StandardErrorFileName);
        stdOut = await stdOutFile.ReadAsStringAsync();
        stdErr = await stdErrFile.ReadAsStringAsync();

        Console.WriteLine("node: {0}:", node.Id);
        Console.WriteLine("stdout.txt: {0}", stdOut);
        Console.WriteLine("stderr.txt: {0}", stdErr);
    }
    else
    {
        Console.WriteLine("\tSubtask {0} is in state {1}", subtask.Id, subtask.State);
    }
});
```

## <a name="code-sample"></a><span data-ttu-id="1f984-215">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="1f984-215">Code sample</span></span>
<span data-ttu-id="1f984-216">GitHub 上的 [MultiInstanceTasks][github_mpi] 程式碼範例示範如何使用多重執行個體工作在 Batch 計算節點上執行 [MS-MPI][msmpi_msdn] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f984-216">The [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how to use a multi-instance task to run an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="1f984-217">請遵循[準備](#preparation)和[執行](#execution)中的步驟來執行範例。</span><span class="sxs-lookup"><span data-stu-id="1f984-217">Follow the steps in [Preparation](#preparation) and [Execution](#execution) to run the sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="1f984-218">準備工作</span><span class="sxs-lookup"><span data-stu-id="1f984-218">Preparation</span></span>
1. <span data-ttu-id="1f984-219">遵循[如何編譯及執行簡單的 MS-MPI 程式][msmpi_howto]中的前兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="1f984-219">Follow the first two steps in [How to compile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="1f984-220">這可滿足下一個步驟的必要條件。</span><span class="sxs-lookup"><span data-stu-id="1f984-220">This satisfies the prerequesites for the following step.</span></span>
2. <span data-ttu-id="1f984-221">建置 [MPIHelloWorld][helloworld_proj] 範例 MPI 程式的*發行*版本。</span><span class="sxs-lookup"><span data-stu-id="1f984-221">Build a *Release* version of the [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="1f984-222">這是多重執行個體工作將在計算節點上執行的程式。</span><span class="sxs-lookup"><span data-stu-id="1f984-222">This is the program that will be run on compute nodes by the multi-instance task.</span></span>
3. <span data-ttu-id="1f984-223">建立包含 `MPIHelloWorld.exe` (您在步驟 2 所建置) 和 `MSMpiSetup.exe` (您在步驟 1 所下載) 的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="1f984-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="1f984-224">您會在下一個步驟中，將此 zip 檔案上傳為應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="1f984-224">You'll upload this zip file as an application package in the next step.</span></span>
4. <span data-ttu-id="1f984-225">使用 [Azure 入口網站][portal]建立稱為「MPIHelloWorld」的 Batch [應用程式](batch-application-packages.md)，並將您在上一個步驟所建立的 zip 檔案指定為應用程式套件「1.0」版。</span><span class="sxs-lookup"><span data-stu-id="1f984-225">Use the [Azure portal][portal] to create a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify the zip file you created in the previous step as version "1.0" of the application package.</span></span> <span data-ttu-id="1f984-226">如需詳細資訊，請參閱[上傳及管理應用程式](batch-application-packages.md#upload-and-manage-applications)。</span><span class="sxs-lookup"><span data-stu-id="1f984-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="1f984-227">建置 `MPIHelloWorld.exe` 的「發行」版本，以便不需要在應用程式套件中包含任何其他相依項目 (例如，`msvcp140d.dll` 或 `vcruntime140d.dll`)。</span><span class="sxs-lookup"><span data-stu-id="1f984-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have to include any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="1f984-228">執行</span><span class="sxs-lookup"><span data-stu-id="1f984-228">Execution</span></span>
1. <span data-ttu-id="1f984-229">從 GitHub 下載 [azure-batch-samples][github_samples_zip]。</span><span class="sxs-lookup"><span data-stu-id="1f984-229">Download the [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="1f984-230">在 Visual Studio 2015 或更新版本中，開啟 MultiInstanceTasks **方案**。</span><span class="sxs-lookup"><span data-stu-id="1f984-230">Open the MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="1f984-231">`MultiInstanceTasks.sln` 方案檔位於︰</span><span class="sxs-lookup"><span data-stu-id="1f984-231">The `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="1f984-232">在 **Microsoft.Azure.Batch.Samples.Common** 專案的 `AccountSettings.settings` 中輸入 Batch 和儲存體帳戶的認證。</span><span class="sxs-lookup"><span data-stu-id="1f984-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in the **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="1f984-233">**建置並執行** MultiInstanceTasks 方案，以在 Batch 集區的計算節點上執行 MPI 範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="1f984-233">**Build and run** the MultiInstanceTasks solution to execute the MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="1f984-234">*選擇性*︰請先使用 [Azure 入口網站][portal] 或 [Batch 總管][batch_explorer] 檢查範例集區、作業和工作 ("MultiInstanceSamplePool"、"MultiInstanceSampleJob"、"MultiInstanceSampleTask")，然後才刪除資源。</span><span class="sxs-lookup"><span data-stu-id="1f984-234">*Optional*: Use the [Azure portal][portal] or the [Batch Explorer][batch_explorer] to examine the sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete the resources.</span></span>

> [!TIP]
> <span data-ttu-id="1f984-235">如果您沒有 Visual Studio，您可以免費下載 [Visual Studio Community][visual_studio]。</span><span class="sxs-lookup"><span data-stu-id="1f984-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="1f984-236">`MultiInstanceTasks.exe` 的輸出大致如下：</span><span class="sxs-lookup"><span data-stu-id="1f984-236">Output from `MultiInstanceTasks.exe` is similar to the following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] to job [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks to complete...

---- Subtask information ----
subtask: 1
        exit code: 0
        node: tvm-1219235766_3-20161017t162002z
        stdout.txt:
        stderr.txt:
subtask: 2
        exit code: 0
        node: tvm-1219235766_2-20161017t162002z
        stdout.txt:
        stderr.txt:

Delete job? [yes] no: yes
Delete pool? [yes] no: yes

Sample complete, hit ENTER to exit...
```

## <a name="next-steps"></a><span data-ttu-id="1f984-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1f984-237">Next steps</span></span>
* <span data-ttu-id="1f984-238">Microsoft HPC 和 Azure Batch 小組部落格討論 [Azure Batch 上的 Linux MPI 支援][blog_mpi_linux]，其中包含搭配使用 [OpenFOAM][openfoam] 和 Batch 的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="1f984-238">The Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="1f984-239">您可以在 [GitHub][github_mpi] 上找到 OpenFOAM 範例的 Python 程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="1f984-239">You can find Python code samples for the [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="1f984-240">了解如何[建立 Linux 計算節點的集區](batch-linux-nodes.md)以在 Azure Batch MPI 方案中使用。</span><span class="sxs-lookup"><span data-stu-id="1f984-240">Learn how to [create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

[helloworld_proj]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks/MPIHelloWorld

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[batch_explorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[blog_mpi_linux]: https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/
[cmd_start]: https://technet.microsoft.com/library/cc770297.aspx
[coord_cmd_example]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/mpi/data/linux/openfoam/coordination-cmd
[github_mpi]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/MultiInstanceTasks
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[msdn_env_var]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[msmpi_msdn]: https://msdn.microsoft.com/library/bb524831.aspx
[msmpi_sdk]: http://go.microsoft.com/FWLink/p/?LinkID=389556
[msmpi_howto]: http://blogs.technet.com/b/windowshpc/archive/2015/02/02/how-to-compile-and-run-a-simple-ms-mpi-program.aspx
[openfoam]: http://www.openfoam.com/
[visual_studio]: https://www.visualstudio.com/vs/community/

[net_jobprep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_multiinstance_class]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_multiinstance_prop]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.multiinstancesettings.aspx
[net_multiinsance_commonresfiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.commonresourcefiles.aspx
[net_multiinstance_coordcmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.coordinationcommandline.aspx
[net_multiinstance_numinstances]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.numberofinstances.aspx
[net_pool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_pool_create]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.createpool.aspx
[net_pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_resourcefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.resourcefile.aspx
[net_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.aspx
[net_starttask_cmdline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.starttask.commandline.aspx
[net_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_taskconstraints]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.aspx
[net_taskconstraint_maxretry]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxtaskretrycount.aspx
[net_taskconstraint_maxwallclock]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.maxwallclocktime.aspx
[net_taskconstraint_retention]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.taskconstraints.retentiontime.aspx
[net_task_listsubtasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listsubtasks.aspx
[net_task_listnodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[poolops_getnodefile]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.getnodefile.aspx

[portal]: https://portal.azure.com
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx

[1]: ./media/batch-mpi/batch_mpi_01.png "多重執行個體概觀"
