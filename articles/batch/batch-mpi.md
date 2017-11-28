---
title: "aaaUse 多重執行個體工作 toorun MPI 應用程式-Azure 批次 |Microsoft 文件"
description: "了解如何使用 hello 多重執行個體工作 tooexecute 訊息傳遞介面 (MPI) 應用程式輸入 Azure 批次中。"
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
ms.openlocfilehash: b0e3295a6aeb76267c26d5504bcff59de3dc5e22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-multi-instance-tasks-toorun-message-passing-interface-mpi-applications-in-batch"></a><span data-ttu-id="50f30-103">批次中使用多個執行個體工作 toorun 訊息傳遞介面 (MPI) 應用程式</span><span class="sxs-lookup"><span data-stu-id="50f30-103">Use multi-instance tasks toorun Message Passing Interface (MPI) applications in Batch</span></span>

<span data-ttu-id="50f30-104">多個執行個體工作可讓您 toorun Azure 批次工作在多個計算節點上同時。</span><span class="sxs-lookup"><span data-stu-id="50f30-104">Multi-instance tasks allow you toorun an Azure Batch task on multiple compute nodes simultaneously.</span></span> <span data-ttu-id="50f30-105">這些工作可以在 Batch 中實現高效能運算案例，例如訊息傳遞介面 (MPI) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="50f30-105">These tasks enable high performance computing scenarios like Message Passing Interface (MPI) applications in Batch.</span></span> <span data-ttu-id="50f30-106">在本文中，您學會如何使用 tooexecute 多重執行個體工作 hello[批次.NET] [ api_net]程式庫。</span><span class="sxs-lookup"><span data-stu-id="50f30-106">In this article, you learn how tooexecute multi-instance tasks using hello [Batch .NET][api_net] library.</span></span>

> [!NOTE]
> <span data-ttu-id="50f30-107">雖然這篇文章中的 hello 範例著重於批次.NET、 MS-MPI，而 Windows 計算節點，這裡所討論的 hello 多重執行個體工作概念會有適用 tooother 平台和技術 （Python 和 Intel MPI Linux 節點上，例如）。</span><span class="sxs-lookup"><span data-stu-id="50f30-107">While hello examples in this article focus on Batch .NET, MS-MPI, and Windows compute nodes, hello multi-instance task concepts discussed here are applicable tooother platforms and technologies (Python and Intel MPI on Linux nodes, for example).</span></span>
>
>

## <a name="multi-instance-task-overview"></a><span data-ttu-id="50f30-108">多重執行個體工作概觀</span><span class="sxs-lookup"><span data-stu-id="50f30-108">Multi-instance task overview</span></span>
<span data-ttu-id="50f30-109">批次中每項工作通常是在單一計算節點-執行您提交多個工作 tooa 工作，，而 hello 批次服務會排程每個節點上執行的工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-109">In Batch, each task is normally executed on a single compute node--you submit multiple tasks tooa job, and hello Batch service schedules each task for execution on a node.</span></span> <span data-ttu-id="50f30-110">不過，藉由設定工作的**多重執行個體設定**，告訴批次 tooinstead 建立一項主要工作和數個子任務，然後在多個節點上執行。</span><span class="sxs-lookup"><span data-stu-id="50f30-110">However, by configuring a task's **multi-instance settings**, you tell Batch tooinstead create one primary task and several subtasks that are then executed on multiple nodes.</span></span>

<span data-ttu-id="50f30-111">![多重執行個體工作概觀][1]</span><span class="sxs-lookup"><span data-stu-id="50f30-111">![Multi-instance task overview][1]</span></span>

<span data-ttu-id="50f30-112">當您提交多個執行個體設定 tooa 工作的工作時，批次會執行數個步驟的唯一 toomulti 執行個體工作：</span><span class="sxs-lookup"><span data-stu-id="50f30-112">When you submit a task with multi-instance settings tooa job, Batch performs several steps unique toomulti-instance tasks:</span></span>

1. <span data-ttu-id="50f30-113">hello 批次服務會建立一個**主要**和數個**子任務**hello 多重執行個體設定為基礎。</span><span class="sxs-lookup"><span data-stu-id="50f30-113">hello Batch service creates one **primary** and several **subtasks** based on hello multi-instance settings.</span></span> <span data-ttu-id="50f30-114">hello 的總工作數目 （再加上所有子主要） 符合 hello 數目**執行個體**（計算節點） hello 多重執行個體設定所指定的。</span><span class="sxs-lookup"><span data-stu-id="50f30-114">hello total number of tasks (primary plus all subtasks) matches hello number of **instances** (compute nodes) you specify in hello multi-instance settings.</span></span>
2. <span data-ttu-id="50f30-115">批次指定一個 hello 計算節點做為 hello**主要**，並排程 hello hello 主機上的主要工作 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="50f30-115">Batch designates one of hello compute nodes as hello **master**, and schedules hello primary task tooexecute on hello master.</span></span> <span data-ttu-id="50f30-116">它會排程 hello 子任務 tooexecute hello 餘數 hello 計算節點配置的 toohello 多重執行個體 」 工作的一項子工作，每個節點上。</span><span class="sxs-lookup"><span data-stu-id="50f30-116">It schedules hello subtasks tooexecute on hello remainder of hello compute nodes allocated toohello multi-instance task, one subtask per node.</span></span>
3. <span data-ttu-id="50f30-117">主要的 hello 與所有子工作下載任何**通用資源檔**hello 多重執行個體設定所指定的。</span><span class="sxs-lookup"><span data-stu-id="50f30-117">hello primary and all subtasks download any **common resource files** you specify in hello multi-instance settings.</span></span>
4. <span data-ttu-id="50f30-118">已下載 hello 通用資源檔案之後，主要 hello 與子工作執行 hello**協調命令**hello 多重執行個體設定所指定的。</span><span class="sxs-lookup"><span data-stu-id="50f30-118">After hello common resource files have been downloaded, hello primary and subtasks execute hello **coordination command** you specify in hello multi-instance settings.</span></span> <span data-ttu-id="50f30-119">常用的 tooprepare 節點執行 hello 工作 hello 協調命令。</span><span class="sxs-lookup"><span data-stu-id="50f30-119">hello coordination command is typically used tooprepare nodes for executing hello task.</span></span> <span data-ttu-id="50f30-120">這可能包括啟動背景服務 (例如[Microsoft MPI][msmpi_msdn]的`smpd.exe`) 和驗證 hello 節點是否準備好 tooprocess 節點間的訊息。</span><span class="sxs-lookup"><span data-stu-id="50f30-120">This can include starting background services (such as [Microsoft MPI][msmpi_msdn]'s `smpd.exe`) and verifying that hello nodes are ready tooprocess inter-node messages.</span></span>
5. <span data-ttu-id="50f30-121">要執行 hello 主要工作 hello**應用程式命令**hello 主要節點上*之後*hello 協調命令已由主要的 hello 與所有子工作順利完成。</span><span class="sxs-lookup"><span data-stu-id="50f30-121">hello primary task executes hello **application command** on hello master node *after* hello coordination command has been completed successfully by hello primary and all subtasks.</span></span> <span data-ttu-id="50f30-122">hello 應用程式命令 hello 多重執行個體工作本身，hello 命令列，且只有 hello 主要工作執行。</span><span class="sxs-lookup"><span data-stu-id="50f30-122">hello application command is hello command line of hello multi-instance task itself, and is executed only by hello primary task.</span></span> <span data-ttu-id="50f30-123">在 [MS-MPI][msmpi_msdn] 架構的方案中，您會在這裡使用 `mpiexec.exe` 執行已啟用 MPI 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="50f30-123">In an [MS-MPI][msmpi_msdn]-based solution, this is where you execute your MPI-enabled application using `mpiexec.exe`.</span></span>

> [!NOTE]
> <span data-ttu-id="50f30-124">雖然功能不同，但是 hello 「 多個執行個體 」 工作不是唯一的工作類型，例如 hello [StartTask] [ net_starttask]或[JobPreparationTask] [ net_jobprep].</span><span class="sxs-lookup"><span data-stu-id="50f30-124">Though it is functionally distinct, hello "multi-instance task" is not a unique task type like hello [StartTask][net_starttask] or [JobPreparationTask][net_jobprep].</span></span> <span data-ttu-id="50f30-125">hello 多重執行個體工作是只是標準的批次工作 ([CloudTask] [ net_task]在批次.NET) 的多個執行個體尚未設定。</span><span class="sxs-lookup"><span data-stu-id="50f30-125">hello multi-instance task is simply a standard Batch task ([CloudTask][net_task] in Batch .NET) whose multi-instance settings have been configured.</span></span> <span data-ttu-id="50f30-126">我們在本文中，為 hello toothis**多重執行個體工作**。</span><span class="sxs-lookup"><span data-stu-id="50f30-126">In this article, we refer toothis as hello **multi-instance task**.</span></span>
>
>

## <a name="requirements-for-multi-instance-tasks"></a><span data-ttu-id="50f30-127">多重執行個體工作的需求</span><span class="sxs-lookup"><span data-stu-id="50f30-127">Requirements for multi-instance tasks</span></span>
<span data-ttu-id="50f30-128">多重執行個體工作需要有**已啟用節點間通訊**和**已停用並行工作執行**的集區。</span><span class="sxs-lookup"><span data-stu-id="50f30-128">Multi-instance tasks require a pool with **inter-node communication enabled**, and with **concurrent task execution disabled**.</span></span> <span data-ttu-id="50f30-129">toodisable 並行工作執行時，set hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) too1 屬性。</span><span class="sxs-lookup"><span data-stu-id="50f30-129">toodisable concurrent task execution, set hello [CloudPool.MaxTasksPerComputeNode](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudpool#Microsoft_Azure_Batch_CloudPool_MaxTasksPerComputeNode) property too1.</span></span>

<span data-ttu-id="50f30-130">這個程式碼片段會示範 toocreate 多重執行個體的集區工作使用 hello 批次.NET 程式庫。</span><span class="sxs-lookup"><span data-stu-id="50f30-130">This code snippet shows how toocreate a pool for multi-instance tasks using hello Batch .NET library.</span></span>

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
> <span data-ttu-id="50f30-131">如果您嘗試的 toorun 停用多個執行個體中的工作集區的節點間通訊，或使用*maxTasksPerNode*值大於 1 時，永遠不會排程 hello 工作-無限期地保持在 hello 「 作用中 」 狀態。</span><span class="sxs-lookup"><span data-stu-id="50f30-131">If you try toorun a multi-instance task in a pool with internode communication disabled, or with a *maxTasksPerNode* value greater than 1, hello task is never scheduled--it remains indefinitely in hello "active" state.</span></span> 
>
> <span data-ttu-id="50f30-132">多重執行個體工作只可以在 2015 年 12 月 14 日後建立之集區中的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="50f30-132">Multi-instance tasks can execute only on nodes in pools created after 14 December 2015.</span></span>
>
>

### <a name="use-a-starttask-tooinstall-mpi"></a><span data-ttu-id="50f30-133">使用 StartTask tooinstall MPI</span><span class="sxs-lookup"><span data-stu-id="50f30-133">Use a StartTask tooinstall MPI</span></span>
<span data-ttu-id="50f30-134">toorun MPI 應用程式與多重執行個體的工作，您必須先 tooinstall hello 集區中的 hello 計算節點上的 MPI 實作 （MS-MPI 或 Intel MPI，例如）。</span><span class="sxs-lookup"><span data-stu-id="50f30-134">toorun MPI applications with a multi-instance task, you first need tooinstall an MPI implementation (MS-MPI or Intel MPI, for example) on hello compute nodes in hello pool.</span></span> <span data-ttu-id="50f30-135">這是很好的時間 toouse [StartTask][net_starttask]，它會執行時的節點加入集區，或重新啟動。</span><span class="sxs-lookup"><span data-stu-id="50f30-135">This is a good time toouse a [StartTask][net_starttask], which executes whenever a node joins a pool, or is restarted.</span></span> <span data-ttu-id="50f30-136">此程式碼片段會建立指定 hello MS-MPI 安裝程式封裝中的成為 StartTask[資源檔][net_resourcefile]。</span><span class="sxs-lookup"><span data-stu-id="50f30-136">This code snippet creates a StartTask that specifies hello MS-MPI setup package as a [resource file][net_resourcefile].</span></span> <span data-ttu-id="50f30-137">hello 資源檔是下載的 toohello 節點之後，會執行 hello 啟動工作的命令列。</span><span class="sxs-lookup"><span data-stu-id="50f30-137">hello start task's command line is executed after hello resource file is downloaded toohello node.</span></span> <span data-ttu-id="50f30-138">在此情況下，hello 命令列執行 MS-MPI 的自動的安裝。</span><span class="sxs-lookup"><span data-stu-id="50f30-138">In this case, hello command line performs an unattended install of MS-MPI.</span></span>

```csharp
// Create a StartTask for hello pool which we use for installing MS-MPI on
// hello nodes as they join hello pool (or when they are restarted).
StartTask startTask = new StartTask
{
    CommandLine = "cmd /c MSMpiSetup.exe -unattend -force",
    ResourceFiles = new List<ResourceFile> { new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MSMpiSetup.exe", "MSMpiSetup.exe") },
    UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin)),
    WaitForSuccess = true
};
myCloudPool.StartTask = startTask;

// Commit hello fully configured pool toohello Batch service tooactually create
// hello pool and its compute nodes.
await myCloudPool.CommitAsync();
```

### <a name="remote-direct-memory-access-rdma"></a><span data-ttu-id="50f30-139">遠端直接記憶體存取 (RDMA)</span><span class="sxs-lookup"><span data-stu-id="50f30-139">Remote direct memory access (RDMA)</span></span>
<span data-ttu-id="50f30-140">當您選擇[具備 RDMA 功能的大小](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)例如 hello A9 計算節點批次集區中的，您的 MPI 應用程式可以利用 Azure 的高效能、 低延遲的遠端直接記憶體存取 (RDMA) 網路。</span><span class="sxs-lookup"><span data-stu-id="50f30-140">When you choose an [RDMA-capable size](../virtual-machines/windows/sizes-hpc.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) such as A9 for hello compute nodes in your Batch pool, your MPI application can take advantage of Azure's high-performance, low-latency remote direct memory access (RDMA) network.</span></span>

<span data-ttu-id="50f30-141">尋找在 hello 下列發行項指定為 「 具有 RDMA"hello 大小：</span><span class="sxs-lookup"><span data-stu-id="50f30-141">Look for hello sizes specified as "RDMA capable" in hello following articles:</span></span>

* <span data-ttu-id="50f30-142">**CloudServiceConfiguration** 集區</span><span class="sxs-lookup"><span data-stu-id="50f30-142">**CloudServiceConfiguration** pools</span></span>

  * <span data-ttu-id="50f30-143">[雲端服務的大小](../cloud-services/cloud-services-sizes-specs.md) (僅限 Windows)</span><span class="sxs-lookup"><span data-stu-id="50f30-143">[Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md) (Windows only)</span></span>
* <span data-ttu-id="50f30-144">**VirtualMachineConfiguration** 集區</span><span class="sxs-lookup"><span data-stu-id="50f30-144">**VirtualMachineConfiguration** pools</span></span>

  * <span data-ttu-id="50f30-145">[Azure 中的虛擬機器大小](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span><span class="sxs-lookup"><span data-stu-id="50f30-145">[Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux)</span></span>
  * <span data-ttu-id="50f30-146">[Azure 中的虛擬機器大小](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span><span class="sxs-lookup"><span data-stu-id="50f30-146">[Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows)</span></span>

> [!NOTE]
> <span data-ttu-id="50f30-147">上的 RDMA tootake 利用[Linux 計算節點](batch-linux-nodes.md)，您必須使用**Intel MPI** hello 節點上。</span><span class="sxs-lookup"><span data-stu-id="50f30-147">tootake advantage of RDMA on [Linux compute nodes](batch-linux-nodes.md), you must use **Intel MPI** on hello nodes.</span></span> <span data-ttu-id="50f30-148">如需有關 CloudServiceConfiguration 和 VirtualMachineConfiguration 集區的詳細資訊，請參閱 hello 集區 > 一節的 hello[批次功能概觀](batch-api-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="50f30-148">For more information on CloudServiceConfiguration and VirtualMachineConfiguration pools, see hello Pool section of hello [Batch feature overview](batch-api-basics.md).</span></span>
>
>

## <a name="create-a-multi-instance-task-with-batch-net"></a><span data-ttu-id="50f30-149">使用 Batch .NET 建立多個執行個體工作</span><span class="sxs-lookup"><span data-stu-id="50f30-149">Create a multi-instance task with Batch .NET</span></span>
<span data-ttu-id="50f30-150">既然我們已經探討 hello 集區需求和 MPI 套件安裝，讓我們來建立 hello 多重執行個體的工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-150">Now that we've covered hello pool requirements and MPI package installation, let's create hello multi-instance task.</span></span> <span data-ttu-id="50f30-151">在此片段中，我們會建立標準 [CloudTask][net_task]，然後設定其 [MultiInstanceSettings][net_multiinstance_prop] 屬性。</span><span class="sxs-lookup"><span data-stu-id="50f30-151">In this snippet, we create a standard [CloudTask][net_task], then configure its [MultiInstanceSettings][net_multiinstance_prop] property.</span></span> <span data-ttu-id="50f30-152">如先前所述，hello 多重執行個體工作不是不同的工作類型，而多個執行個體設定的標準批次工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-152">As mentioned earlier, hello multi-instance task is not a distinct task type, but a standard Batch task configured with multi-instance settings.</span></span>

```csharp
// Create hello multi-instance task. Its command line is hello "application command"
// and will be executed *only* by hello primary, and only after hello primary and
// subtasks execute hello CoordinationCommandLine.
CloudTask myMultiInstanceTask = new CloudTask(id: "mymultiinstancetask",
    commandline: "cmd /c mpiexec.exe -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe");

// Configure hello task's MultiInstanceSettings. hello CoordinationCommandLine will be executed by
// hello primary and all subtasks.
myMultiInstanceTask.MultiInstanceSettings =
    new MultiInstanceSettings(numberOfNodes) {
    CoordinationCommandLine = @"cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d",
    CommonResourceFiles = new List<ResourceFile> {
    new ResourceFile("https://mystorageaccount.blob.core.windows.net/mycontainer/MyMPIApplication.exe",
                     "MyMPIApplication.exe")
    }
};

// Submit hello task toohello job. Batch will take care of splitting it into subtasks and
// scheduling them for execution on hello nodes.
await myBatchClient.JobOperations.AddTaskAsync("mybatchjob", myMultiInstanceTask);
```

## <a name="primary-task-and-subtasks"></a><span data-ttu-id="50f30-153">主要工作和子工作</span><span class="sxs-lookup"><span data-stu-id="50f30-153">Primary task and subtasks</span></span>
<span data-ttu-id="50f30-154">當您建立 hello 工作的多個執行個體設定時，您會指定 hello tooexecute hello 工作的運算節點數目。</span><span class="sxs-lookup"><span data-stu-id="50f30-154">When you create hello multi-instance settings for a task, you specify hello number of compute nodes that are tooexecute hello task.</span></span> <span data-ttu-id="50f30-155">當您送出 hello 工作 tooa 作業時，hello 批次服務會建立一個**主要**工作以及足以**子任務**一起與相符的 hello 您指定的節點數目。</span><span class="sxs-lookup"><span data-stu-id="50f30-155">When you submit hello task tooa job, hello Batch service creates one **primary** task and enough **subtasks** that together match hello number of nodes you specified.</span></span>

<span data-ttu-id="50f30-156">這些工作會指派整數識別碼 hello 範圍內的 0 太*numberOfInstances* -1。</span><span class="sxs-lookup"><span data-stu-id="50f30-156">These tasks are assigned an integer id in hello range of 0 too*numberOfInstances* - 1.</span></span> <span data-ttu-id="50f30-157">識別碼為 0 的 hello 工作是 hello 主要工作，而所有其他的 id 是子工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-157">hello task with id 0 is hello primary task, and all other ids are subtasks.</span></span> <span data-ttu-id="50f30-158">例如，如果您建立下列工作的多個執行個體設定的 hello，hello 主要工作就會有的識別碼為 0，並 hello 子工作會有 1 到 9 的識別碼。</span><span class="sxs-lookup"><span data-stu-id="50f30-158">For example, if you create hello following multi-instance settings for a task, hello primary task would have an id of 0, and hello subtasks would have ids 1 through 9.</span></span>

```csharp
int numberOfNodes = 10;
myMultiInstanceTask.MultiInstanceSettings = new MultiInstanceSettings(numberOfNodes);
```

### <a name="master-node"></a><span data-ttu-id="50f30-159">主要節點</span><span class="sxs-lookup"><span data-stu-id="50f30-159">Master node</span></span>
<span data-ttu-id="50f30-160">當您提交多個執行個體工作時，hello 批次服務將指定的 hello 其中一個計算節點為 hello 「 主要 」 節點，並排程 hello hello 主要節點上的主要工作 tooexecute。</span><span class="sxs-lookup"><span data-stu-id="50f30-160">When you submit a multi-instance task, hello Batch service designates one of hello compute nodes as hello "master" node, and schedules hello primary task tooexecute on hello master node.</span></span> <span data-ttu-id="50f30-161">hello 子工作會排定的 tooexecute hello 其餘部分的配置 toohello 多重執行個體工作 hello 節點上。</span><span class="sxs-lookup"><span data-stu-id="50f30-161">hello subtasks are scheduled tooexecute on hello remainder of hello nodes allocated toohello multi-instance task.</span></span>

## <a name="coordination-command"></a><span data-ttu-id="50f30-162">協調命令</span><span class="sxs-lookup"><span data-stu-id="50f30-162">Coordination command</span></span>
<span data-ttu-id="50f30-163">hello**協調命令**hello 主要和子工作所執行。</span><span class="sxs-lookup"><span data-stu-id="50f30-163">hello **coordination command** is executed by both hello primary and subtasks.</span></span>

<span data-ttu-id="50f30-164">封鎖的 hello 協調命令的引動過程 hello-批次不會執行 hello 應用程式的命令，直到 hello 協調命令已順利傳回所有子工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-164">hello invocation of hello coordination command is blocking--Batch does not execute hello application command until hello coordination command has returned successfully for all subtasks.</span></span> <span data-ttu-id="50f30-165">因此 hello 協調命令就應該啟動任何所需的背景服務，確定它們是供使用，，然後結束。</span><span class="sxs-lookup"><span data-stu-id="50f30-165">hello coordination command should therefore start any required background services, verify that they are ready for use, and then exit.</span></span> <span data-ttu-id="50f30-166">例如，此解決方案使用 MS-MPI 第 7 版的協調命令 hello 節點上啟動 hello SMPD 服務，然後結束：</span><span class="sxs-lookup"><span data-stu-id="50f30-166">For example, this coordination command for a solution using MS-MPI version 7 starts hello SMPD service on hello node, then exits:</span></span>

```
cmd /c start cmd /c ""%MSMPI_BIN%\smpd.exe"" -d
```

<span data-ttu-id="50f30-167">請注意 hello 使用`start`在此協調命令。</span><span class="sxs-lookup"><span data-stu-id="50f30-167">Note hello use of `start` in this coordination command.</span></span> <span data-ttu-id="50f30-168">這是必要的因為 hello`smpd.exe`應用程式不會在執行後立即傳回。</span><span class="sxs-lookup"><span data-stu-id="50f30-168">This is required because hello `smpd.exe` application does not return immediately after execution.</span></span> <span data-ttu-id="50f30-169">而不需 hello hello 使用[啟動][ cmd_start]命令時，此協調命令就不會傳回，並會因此而封鎖 hello 應用程式命令的執行。</span><span class="sxs-lookup"><span data-stu-id="50f30-169">Without hello use of hello [start][cmd_start] command, this coordination command would not return, and would therefore block hello application command from running.</span></span>

## <a name="application-command"></a><span data-ttu-id="50f30-170">應用程式命令</span><span class="sxs-lookup"><span data-stu-id="50f30-170">Application command</span></span>
<span data-ttu-id="50f30-171">當主要工作就 hello 與所有子工作完成後，執行 hello 協調命令時，hello 主要工作所執行 hello 多重執行個體工作的命令列*只*。</span><span class="sxs-lookup"><span data-stu-id="50f30-171">Once hello primary task and all subtasks have finished executing hello coordination command, hello multi-instance task's command line is executed by hello primary task *only*.</span></span> <span data-ttu-id="50f30-172">我們會呼叫這個 hello**應用程式命令**toodistinguish 從 hello 協調命令。</span><span class="sxs-lookup"><span data-stu-id="50f30-172">We call this hello **application command** toodistinguish it from hello coordination command.</span></span>

<span data-ttu-id="50f30-173">為 MS-MPI 應用程式，使用 hello 應用程式命令 tooexecute MPI 啟用的應用程式與`mpiexec.exe`。</span><span class="sxs-lookup"><span data-stu-id="50f30-173">For MS-MPI applications, use hello application command tooexecute your MPI-enabled application with `mpiexec.exe`.</span></span> <span data-ttu-id="50f30-174">例如，以下是使用 MS-MPI 第 7 版的方案所執行的應用程式命令：</span><span class="sxs-lookup"><span data-stu-id="50f30-174">For example, here is an application command for a solution using MS-MPI version 7:</span></span>

```
cmd /c ""%MSMPI_BIN%\mpiexec.exe"" -c 1 -wdir %AZ_BATCH_TASK_SHARED_DIR% MyMPIApplication.exe
```

> [!NOTE]
> <span data-ttu-id="50f30-175">因為 MS-MPI 的`mpiexec.exe`使用 hello`CCP_NODES`預設變數 (請參閱[環境變數](#environment-variables)) hello 範例上述的應用程式命令列會排除它。</span><span class="sxs-lookup"><span data-stu-id="50f30-175">Because MS-MPI's `mpiexec.exe` uses hello `CCP_NODES` variable by default (see [Environment variables](#environment-variables)) hello example application command line above excludes it.</span></span>
>
>

## <a name="environment-variables"></a><span data-ttu-id="50f30-176">環境變數</span><span class="sxs-lookup"><span data-stu-id="50f30-176">Environment variables</span></span>
<span data-ttu-id="50f30-177">批次建立數個[環境變數][ msdn_env_var] hello 上的特定 toomulti 執行個體工作計算節點配置 tooa 多重執行個體的工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-177">Batch creates several [environment variables][msdn_env_var] specific toomulti-instance tasks on hello compute nodes allocated tooa multi-instance task.</span></span> <span data-ttu-id="50f30-178">您協調和應用程式的命令列可以參考這些環境變數，如指令碼和它們所執行的程式可以 hello。</span><span class="sxs-lookup"><span data-stu-id="50f30-178">Your coordination and application command lines can reference these environment variables, as can hello scripts and programs they execute.</span></span>

<span data-ttu-id="50f30-179">hello 下列環境變數會建立 hello 批次服務用於多個執行個體的工作：</span><span class="sxs-lookup"><span data-stu-id="50f30-179">hello following environment variables are created by hello Batch service for use by multi-instance tasks:</span></span>

* `CCP_NODES`
* `AZ_BATCH_NODE_LIST`
* `AZ_BATCH_HOST_LIST`
* `AZ_BATCH_MASTER_NODE`
* `AZ_BATCH_TASK_SHARED_DIR`
* `AZ_BATCH_IS_CURRENT_NODE_MASTER`

<span data-ttu-id="50f30-180">如需這些完整詳細資料和 hello 其他批次計算節點的環境變數，包括其內容與可見性，請參閱[計算節點環境變數][msdn_env_var]。</span><span class="sxs-lookup"><span data-stu-id="50f30-180">For full details on these and hello other Batch compute node environment variables, including their contents and visibility, see [Compute node environment variables][msdn_env_var].</span></span>

> [!TIP]
> <span data-ttu-id="50f30-181">hello 批次 Linux MPI 程式碼範例包含如何使用這些環境變數的數個範例。</span><span class="sxs-lookup"><span data-stu-id="50f30-181">hello Batch Linux MPI code sample contains an example of how several of these environment variables can be used.</span></span> <span data-ttu-id="50f30-182">hello[協調 cmd] [ coord_cmd_example] Bash 指令碼會從 Azure 儲存體下載常見的應用程式和輸入的檔案，可讓在 hello 主要節點上的網路檔案系統 (NFS) 共用以及設定 hello 其他節點做為 NFS 用戶端配置 toohello 多重執行個體的工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-182">hello [coordination-cmd][coord_cmd_example] Bash script downloads common application and input files from Azure Storage, enables a Network File System (NFS) share on hello master node, and configures hello other nodes allocated toohello multi-instance task as NFS clients.</span></span>
>
>

## <a name="resource-files"></a><span data-ttu-id="50f30-183">資源檔</span><span class="sxs-lookup"><span data-stu-id="50f30-183">Resource files</span></span>
<span data-ttu-id="50f30-184">有兩個集合的多個執行個體工作的資源檔案 tooconsider:**通用資源檔**，*所有*下載工作 (這兩個主要與子工作)，和 hello**資源檔** hello 多重執行個體工作本身，其中指定*只 hello 主要*工作下載項目。</span><span class="sxs-lookup"><span data-stu-id="50f30-184">There are two sets of resource files tooconsider for multi-instance tasks: **common resource files** that *all* tasks download (both primary and subtasks), and hello **resource files** specified for hello multi-instance task itself, which *only hello primary* task downloads.</span></span>

<span data-ttu-id="50f30-185">您可以指定一或多個**通用資源檔**hello 多重執行個體設定的工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-185">You can specify one or more **common resource files** in hello multi-instance settings for a task.</span></span> <span data-ttu-id="50f30-186">從下載這些常見的資源檔[Azure 儲存體](../storage/common/storage-introduction.md)到每個節點的**工作共用的目錄**由主要的 hello 與所有子工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-186">These common resource files are downloaded from [Azure Storage](../storage/common/storage-introduction.md) into each node's **task shared directory** by hello primary and all subtasks.</span></span> <span data-ttu-id="50f30-187">您可以從應用程式及協調命令列存取 hello 工作共用的目錄，使用 hello`AZ_BATCH_TASK_SHARED_DIR`環境變數。</span><span class="sxs-lookup"><span data-stu-id="50f30-187">You can access hello task shared directory from application and coordination command lines by using hello `AZ_BATCH_TASK_SHARED_DIR` environment variable.</span></span> <span data-ttu-id="50f30-188">hello`AZ_BATCH_TASK_SHARED_DIR`路徑上每個節點配置的 toohello 多重執行個體工作相同，因此您可以共用單一協調命令之間主要的 hello 與所有子工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-188">hello `AZ_BATCH_TASK_SHARED_DIR` path is identical on every node allocated toohello multi-instance task, thus you can share a single coordination command between hello primary and all subtasks.</span></span> <span data-ttu-id="50f30-189">批次不會 「 共用 」 hello 目錄中的遠端存取意義上，但是您可以將它當做掛接或共用點，如稍早在 環境變數的 hello 提示中所述。</span><span class="sxs-lookup"><span data-stu-id="50f30-189">Batch does not "share" hello directory in a remote access sense, but you can use it as a mount or share point as mentioned earlier in hello tip on environment variables.</span></span>

<span data-ttu-id="50f30-190">Hello 多重執行個體工作本身會下載的 toohello 工作的工作目錄，為指定的資源檔`AZ_BATCH_TASK_WORKING_DIR`，根據預設。</span><span class="sxs-lookup"><span data-stu-id="50f30-190">Resource files that you specify for hello multi-instance task itself are downloaded toohello task's working directory, `AZ_BATCH_TASK_WORKING_DIR`, by default.</span></span> <span data-ttu-id="50f30-191">如前所述，相較之下 toocommon 資源檔，唯一 hello 主要工作會下載 hello 多重執行個體工作本身為指定的資源檔。</span><span class="sxs-lookup"><span data-stu-id="50f30-191">As mentioned, in contrast toocommon resource files, only hello primary task downloads resource files specified for hello  multi-instance task itself.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="50f30-192">一律使用 hello 環境變數`AZ_BATCH_TASK_SHARED_DIR`和`AZ_BATCH_TASK_WORKING_DIR`toorefer toothese 目錄，在命令列中的。</span><span class="sxs-lookup"><span data-stu-id="50f30-192">Always use hello environment variables `AZ_BATCH_TASK_SHARED_DIR` and `AZ_BATCH_TASK_WORKING_DIR` toorefer toothese directories in your command lines.</span></span> <span data-ttu-id="50f30-193">請勿手動嘗試 tooconstruct hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="50f30-193">Do not attempt tooconstruct hello paths manually.</span></span>
>
>

## <a name="task-lifetime"></a><span data-ttu-id="50f30-194">工作存留期</span><span class="sxs-lookup"><span data-stu-id="50f30-194">Task lifetime</span></span>
<span data-ttu-id="50f30-195">hello 存留期 hello 主要工作控制項 hello 工作的存留期 hello 整個多個執行個體。</span><span class="sxs-lookup"><span data-stu-id="50f30-195">hello lifetime of hello primary task controls hello lifetime of hello entire multi-instance task.</span></span> <span data-ttu-id="50f30-196">Hello 主要當結束時，會終止所有 hello 子任務。</span><span class="sxs-lookup"><span data-stu-id="50f30-196">When hello primary exits, all of hello subtasks are terminated.</span></span> <span data-ttu-id="50f30-197">主要的 hello hello 結束代碼是 hello 的 hello 工作的結束代碼，因此使用的 toodetermine hello 成功或失敗的重試基於 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-197">hello exit code of hello primary is hello exit code of hello task, and is therefore used toodetermine hello success or failure of hello task for retry purposes.</span></span>

<span data-ttu-id="50f30-198">如果任何 hello 子工作失敗，結束使用非零的傳回程式碼，例如 hello 整個多個執行個體工作會失敗。</span><span class="sxs-lookup"><span data-stu-id="50f30-198">If any of hello subtasks fail, exiting with a non-zero return code, for example, hello entire multi-instance task fails.</span></span> <span data-ttu-id="50f30-199">hello 多重執行個體的工作是終止，然後重試，向上 tooits 重試次數上限。</span><span class="sxs-lookup"><span data-stu-id="50f30-199">hello multi-instance task is then terminated and retried, up tooits retry limit.</span></span>

<span data-ttu-id="50f30-200">當您刪除多個執行個體工作時，主要的 hello 與所有子工作會一併刪除的 hello 批次服務。</span><span class="sxs-lookup"><span data-stu-id="50f30-200">When you delete a multi-instance task, hello primary and all subtasks are also deleted by hello Batch service.</span></span> <span data-ttu-id="50f30-201">所有的子工作目錄，並從 hello 計算節點，只適用於標準工作會刪除其檔案。</span><span class="sxs-lookup"><span data-stu-id="50f30-201">All subtask directories and their files are deleted from hello compute nodes, just as for a standard task.</span></span>

<span data-ttu-id="50f30-202">[TaskConstraints] [ net_taskconstraints]多重執行個體的工作，例如 hello [MaxTaskRetryCount][net_taskconstraint_maxretry]， [MaxWallClockTime][ net_taskconstraint_maxwallclock]，和[RetentionTime] [ net_taskconstraint_retention]屬性，系統會接受標準的工作，並套用 toohello 主要與所有子工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-202">[TaskConstraints][net_taskconstraints] for a multi-instance task, such as hello [MaxTaskRetryCount][net_taskconstraint_maxretry], [MaxWallClockTime][net_taskconstraint_maxwallclock], and [RetentionTime][net_taskconstraint_retention] properties, are honored as they are for a standard task, and apply toohello primary and all subtasks.</span></span> <span data-ttu-id="50f30-203">不過，如果您變更 hello [RetentionTime] [ net_taskconstraint_retention]新增 hello 多重執行個體工作 toohello 作業，這項變更後的屬性會套用只有 toohello 主要工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-203">However, if you change hello [RetentionTime][net_taskconstraint_retention] property after adding hello multi-instance task toohello job, this change is applied only toohello primary task.</span></span> <span data-ttu-id="50f30-204">所有 hello 子任務繼續 toouse hello 原始[RetentionTime][net_taskconstraint_retention]。</span><span class="sxs-lookup"><span data-stu-id="50f30-204">All of hello subtasks continue toouse hello original [RetentionTime][net_taskconstraint_retention].</span></span>

<span data-ttu-id="50f30-205">如果 hello 最近的工作是多個執行個體工作的一部分，則計算節點的最近工作清單會反映出 hello 的子工作的識別碼。</span><span class="sxs-lookup"><span data-stu-id="50f30-205">A compute node's recent task list reflects hello id of a subtask if hello recent task was part of a multi-instance task.</span></span>

## <a name="obtain-information-about-subtasks"></a><span data-ttu-id="50f30-206">取得子工作的相關資訊</span><span class="sxs-lookup"><span data-stu-id="50f30-206">Obtain information about subtasks</span></span>
<span data-ttu-id="50f30-207">使用 hello 批次.NET 程式庫，呼叫 hello 子任務的 tooobtain 有關[CloudTask.ListSubtasks] [ net_task_listsubtasks]方法。</span><span class="sxs-lookup"><span data-stu-id="50f30-207">tooobtain information on subtasks by using hello Batch .NET library, call hello [CloudTask.ListSubtasks][net_task_listsubtasks] method.</span></span> <span data-ttu-id="50f30-208">這個方法會傳回資訊上所有的子工作和資訊 hello 計算執行 hello 工作的節點。</span><span class="sxs-lookup"><span data-stu-id="50f30-208">This method returns information on all subtasks, and information about hello compute node that executed hello tasks.</span></span> <span data-ttu-id="50f30-209">這項資訊，您可以判斷每項子工作的根目錄、 hello 集區識別碼，其目前狀態、 結束代碼，等等。</span><span class="sxs-lookup"><span data-stu-id="50f30-209">From this information, you can determine each subtask's root directory, hello pool id, its current state, exit code, and more.</span></span> <span data-ttu-id="50f30-210">您可以使用這項資訊結合 hello [PoolOperations.GetNodeFile] [ poolops_getnodefile]方法 tooobtain hello 子任務的檔案。</span><span class="sxs-lookup"><span data-stu-id="50f30-210">You can use this information in combination with hello [PoolOperations.GetNodeFile][poolops_getnodefile] method tooobtain hello subtask's files.</span></span> <span data-ttu-id="50f30-211">請注意，這個方法不會傳回 hello 主要工作 （識別碼 0） 的資訊。</span><span class="sxs-lookup"><span data-stu-id="50f30-211">Note that this method does not return information for hello primary task (id 0).</span></span>

> [!NOTE]
> <span data-ttu-id="50f30-212">除非另有指明，批次.NET 方法上操作的 hello 多重執行個體[CloudTask] [ net_task]本身套用*只*toohello 主要工作。</span><span class="sxs-lookup"><span data-stu-id="50f30-212">Unless otherwise stated, Batch .NET methods that operate on hello multi-instance [CloudTask][net_task] itself apply *only* toohello primary task.</span></span> <span data-ttu-id="50f30-213">例如，當您呼叫 hello [CloudTask.ListNodeFiles] [ net_task_listnodefiles]多重執行個體工作上的方法，只有 hello 主要工作的檔案會傳回。</span><span class="sxs-lookup"><span data-stu-id="50f30-213">For example, when you call hello [CloudTask.ListNodeFiles][net_task_listnodefiles] method on a multi-instance task, only hello primary task's files are returned.</span></span>
>
>

<span data-ttu-id="50f30-214">hello 下列程式碼片段示範如何 tooobtain 子工作的詳細資訊，以及要求檔案的內容來自 hello 執行所在的節點。</span><span class="sxs-lookup"><span data-stu-id="50f30-214">hello following code snippet shows how tooobtain subtask information, as well as request file contents from hello nodes on which they executed.</span></span>

```csharp
// Obtain hello job and hello multi-instance task from hello Batch service
CloudJob boundJob = batchClient.JobOperations.GetJob("mybatchjob");
CloudTask myMultiInstanceTask = boundJob.GetTask("mymultiinstancetask");

// Now obtain hello list of subtasks for hello task
IPagedEnumerable<SubtaskInformation> subtasks = myMultiInstanceTask.ListSubtasks();

// Asynchronously iterate over hello subtasks and print their stdout and stderr
// output if hello subtask has completed
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

## <a name="code-sample"></a><span data-ttu-id="50f30-215">程式碼範例</span><span class="sxs-lookup"><span data-stu-id="50f30-215">Code sample</span></span>
<span data-ttu-id="50f30-216">hello [MultiInstanceTasks] [ github_mpi] GitHub 上的程式碼範例示範如何 toouse 多重執行個體工作 toorun [MS-MPI] [ msmpi_msdn]批次計算節點上的應用程式。</span><span class="sxs-lookup"><span data-stu-id="50f30-216">hello [MultiInstanceTasks][github_mpi] code sample on GitHub demonstrates how toouse a multi-instance task toorun an [MS-MPI][msmpi_msdn] application on Batch compute nodes.</span></span> <span data-ttu-id="50f30-217">中的 hello 步驟[準備](#preparation)和[執行](#execution)toorun hello 範例。</span><span class="sxs-lookup"><span data-stu-id="50f30-217">Follow hello steps in [Preparation](#preparation) and [Execution](#execution) toorun hello sample.</span></span>

### <a name="preparation"></a><span data-ttu-id="50f30-218">準備工作</span><span class="sxs-lookup"><span data-stu-id="50f30-218">Preparation</span></span>
1. <span data-ttu-id="50f30-219">請依照下列中的 hello 前兩個步驟[如何 toocompile 並執行簡單的 MS-MPI 程式][msmpi_howto]。</span><span class="sxs-lookup"><span data-stu-id="50f30-219">Follow hello first two steps in [How toocompile and run a simple MS-MPI program][msmpi_howto].</span></span> <span data-ttu-id="50f30-220">這可滿足 hello prerequesites hello 遵循的步驟。</span><span class="sxs-lookup"><span data-stu-id="50f30-220">This satisfies hello prerequesites for hello following step.</span></span>
2. <span data-ttu-id="50f30-221">建置*發行*版的 hello [MPIHelloWorld] [ helloworld_proj] MPI 程式範例。</span><span class="sxs-lookup"><span data-stu-id="50f30-221">Build a *Release* version of hello [MPIHelloWorld][helloworld_proj] sample MPI program.</span></span> <span data-ttu-id="50f30-222">這是將 hello 多重執行個體的工作所計算節點執行的 hello 程式。</span><span class="sxs-lookup"><span data-stu-id="50f30-222">This is hello program that will be run on compute nodes by hello multi-instance task.</span></span>
3. <span data-ttu-id="50f30-223">建立包含 `MPIHelloWorld.exe` (您在步驟 2 所建置) 和 `MSMpiSetup.exe` (您在步驟 1 所下載) 的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="50f30-223">Create a zip file containing `MPIHelloWorld.exe` (which you built step 2) and `MSMpiSetup.exe` (which you downloaded step 1).</span></span> <span data-ttu-id="50f30-224">您將為 hello 下一個步驟中的應用程式封裝上傳此 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="50f30-224">You'll upload this zip file as an application package in hello next step.</span></span>
4. <span data-ttu-id="50f30-225">使用 hello [Azure 入口網站][ portal] toocreate 批次[應用程式](batch-application-packages.md)稱為 「 MPIHelloWorld 」，並指定您建立 hello 上一個步驟中，為 「 1.0 」 版的 hello zip 檔案hello 應用程式封裝。</span><span class="sxs-lookup"><span data-stu-id="50f30-225">Use hello [Azure portal][portal] toocreate a Batch [application](batch-application-packages.md) called "MPIHelloWorld", and specify hello zip file you created in hello previous step as version "1.0" of hello application package.</span></span> <span data-ttu-id="50f30-226">如需詳細資訊，請參閱[上傳及管理應用程式](batch-application-packages.md#upload-and-manage-applications)。</span><span class="sxs-lookup"><span data-stu-id="50f30-226">See [Upload and manage applications](batch-application-packages.md#upload-and-manage-applications) for more information.</span></span>

> [!TIP]
> <span data-ttu-id="50f30-227">建置*發行*版本`MPIHelloWorld.exe`，所以您不需要 tooinclude 其他任何相依性 (例如，`msvcp140d.dll`或`vcruntime140d.dll`) 應用程式封裝中。</span><span class="sxs-lookup"><span data-stu-id="50f30-227">Build a *Release* version of `MPIHelloWorld.exe` so that you don't have tooinclude any additional dependencies (for example, `msvcp140d.dll` or `vcruntime140d.dll`) in your application package.</span></span>
>
>

### <a name="execution"></a><span data-ttu-id="50f30-228">執行</span><span class="sxs-lookup"><span data-stu-id="50f30-228">Execution</span></span>
1. <span data-ttu-id="50f30-229">下載 hello [azure 批次範例][ github_samples_zip]從 GitHub。</span><span class="sxs-lookup"><span data-stu-id="50f30-229">Download hello [azure-batch-samples][github_samples_zip] from GitHub.</span></span>
2. <span data-ttu-id="50f30-230">開啟 hello MultiInstanceTasks**方案**在 Visual Studio 2015 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="50f30-230">Open hello MultiInstanceTasks **solution** in Visual Studio 2015 or newer.</span></span> <span data-ttu-id="50f30-231">hello`MultiInstanceTasks.sln`方案檔位於：</span><span class="sxs-lookup"><span data-stu-id="50f30-231">hello `MultiInstanceTasks.sln` solution file is located in:</span></span>

    `azure-batch-samples\CSharp\ArticleProjects\MultiInstanceTasks\`
3. <span data-ttu-id="50f30-232">輸入您的批次和儲存體帳戶認證中`AccountSettings.settings`在 hello **Microsoft.Azure.Batch.Samples.Common**專案。</span><span class="sxs-lookup"><span data-stu-id="50f30-232">Enter your Batch and Storage account credentials in `AccountSettings.settings` in hello **Microsoft.Azure.Batch.Samples.Common** project.</span></span>
4. <span data-ttu-id="50f30-233">**建置並執行**hello MultiInstanceTasks 方案 tooexecute hello MPI 範例應用程式上的計算的批次集區中的節點。</span><span class="sxs-lookup"><span data-stu-id="50f30-233">**Build and run** hello MultiInstanceTasks solution tooexecute hello MPI sample application on compute nodes in a Batch pool.</span></span>
5. <span data-ttu-id="50f30-234">*選擇性*： 使用 hello [Azure 入口網站][ portal]或 hello[批次總管][ batch_explorer] tooexamine hello 範例集區、 工作和之前的工作 （「 MultiInstanceSamplePool"、"MultiInstanceSampleJob"、"MultiInstanceSampleTask"） 刪除 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="50f30-234">*Optional*: Use hello [Azure portal][portal] or hello [Batch Explorer][batch_explorer] tooexamine hello sample pool, job, and task ("MultiInstanceSamplePool", "MultiInstanceSampleJob", "MultiInstanceSampleTask") before you delete hello resources.</span></span>

> [!TIP]
> <span data-ttu-id="50f30-235">如果您沒有 Visual Studio，您可以免費下載 [Visual Studio Community][visual_studio]。</span><span class="sxs-lookup"><span data-stu-id="50f30-235">You can download [Visual Studio Community][visual_studio] for free if you do not have Visual Studio.</span></span>
>
>

<span data-ttu-id="50f30-236">從輸出`MultiInstanceTasks.exe`是類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="50f30-236">Output from `MultiInstanceTasks.exe` is similar toohello following:</span></span>

```
Creating pool [MultiInstanceSamplePool]...
Creating job [MultiInstanceSampleJob]...
Adding task [MultiInstanceSampleTask] toojob [MultiInstanceSampleJob]...
Awaiting task completion, timeout in 00:30:00...

Main task [MultiInstanceSampleTask] is in state [Completed] and ran on compute node [tvm-1219235766_1-20161017t162002z]:
---- stdout.txt ----
Rank 2 received string "Hello world" from Rank 0
Rank 1 received string "Hello world" from Rank 0

---- stderr.txt ----

Main task completed, waiting 00:00:10 for subtasks toocomplete...

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

Sample complete, hit ENTER tooexit...
```

## <a name="next-steps"></a><span data-ttu-id="50f30-237">後續步驟</span><span class="sxs-lookup"><span data-stu-id="50f30-237">Next steps</span></span>
* <span data-ttu-id="50f30-238">hello Microsoft HPC 和 Azure 批次小組部落格討論[適用於 Azure 批次上的 Linux 支援的 MPI][blog_mpi_linux]，並包含有關使用[OpenFOAM] [openfoam]與批次。</span><span class="sxs-lookup"><span data-stu-id="50f30-238">hello Microsoft HPC & Azure Batch Team blog discusses [MPI support for Linux on Azure Batch][blog_mpi_linux], and includes information on using [OpenFOAM][openfoam] with Batch.</span></span> <span data-ttu-id="50f30-239">您可以找到 Python 程式碼範例的 hello [OpenFOAM 範例 GitHub 上的][github_mpi]。</span><span class="sxs-lookup"><span data-stu-id="50f30-239">You can find Python code samples for hello [OpenFOAM example on GitHub][github_mpi].</span></span>
* <span data-ttu-id="50f30-240">了解如何太[建立集區的 Linux 運算節點](batch-linux-nodes.md)Azure 批次 MPI 方案中使用。</span><span class="sxs-lookup"><span data-stu-id="50f30-240">Learn how too[create pools of Linux compute nodes](batch-linux-nodes.md) for use in your Azure Batch MPI solutions.</span></span>

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
