---
title: "aaaAzure 批次在 hello 雲端執行大規模的平行運算解決方案 |Microsoft 文件"
description: "了解如何使用 hello Azure 批次服務針對大規模的平行和 HPC 工作負載"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: 93e37d44-7585-495e-8491-312ed584ab79
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/05/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: acc52e46330c465f81951441d9067371098cf63a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a><span data-ttu-id="0d1f5-103">使用 Batch 執行本質平行的工作負載</span><span class="sxs-lookup"><span data-stu-id="0d1f5-103">Run intrinsically parallel workloads with Batch</span></span>

<span data-ttu-id="0d1f5-104">Azure 批次是 hello 雲端中有效率地執行大規模平行和高效能運算 (HPC) 應用程式的平台服務。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-104">Azure Batch is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in hello cloud.</span></span> <span data-ttu-id="0d1f5-105">Azure 批次排程需要大量計算工作 toorun 上受管理的虛擬機器的集合，並可自動調整計算資源 toomeet hello 需求的工作。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-105">Azure Batch schedules compute-intensive work toorun on a managed collection of virtual machines, and can automatically scale compute resources toomeet hello needs of your jobs.</span></span>

<span data-ttu-id="0d1f5-106">透過 Azure 批次中，您可以輕鬆地定義 Azure 計算資源 tooexecute 應用程式以平行方式，而是在標尺。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-106">With Azure Batch, you can easily define Azure compute resources tooexecute your applications in parallel, and at scale.</span></span> <span data-ttu-id="0d1f5-107">沒有任何需要 toomanually 建立、 設定和管理 HPC 叢集、 個別的虛擬機器、 虛擬網路或複雜的工作和工作排程基礎結構。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-107">There's no need toomanually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span> <span data-ttu-id="0d1f5-108">Azure Batch 會為您自動執行或簡化這些工作。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-108">Azure Batch automates or simplifies these tasks for you.</span></span>

## <a name="use-cases-for-batch"></a><span data-ttu-id="0d1f5-109">Batch 的使用案例</span><span class="sxs-lookup"><span data-stu-id="0d1f5-109">Use cases for Batch</span></span>
<span data-ttu-id="0d1f5-110">Batch 是一項受管理的 Azure 服務，可用於批次處理或批次運算 -- 執行大量的類似工作以得到期望的結果。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-110">Batch is a managed Azure service that is used for *batch processing* or *batch computing*--running a large volume of similar tasks for a desired result.</span></span> <span data-ttu-id="0d1f5-111">定期處理、轉換和分析大量資料的組織最常使用批次運算。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-111">Batch computing is most commonly used by organizations that regularly process, transform, and analyze large volumes of data.</span></span>

<span data-ttu-id="0d1f5-112">Batch 很適合處理本質平行 (也稱為「超簡單平行」) 的應用程式和工作負載。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-112">Batch works well with intrinsically parallel (also known as "embarrassingly parallel") applications and workloads.</span></span> <span data-ttu-id="0d1f5-113">本質上平行的工作負載可輕易分割成多個工作，以在多部電腦上同時執行。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-113">Intrinsically parallel workloads are those that are easily split into multiple tasks that perform work simultaneously on many computers.</span></span>

![平行工作][1]<br/>

<span data-ttu-id="0d1f5-115">常見使用這項技術處理的一些工作負載範例如下：</span><span class="sxs-lookup"><span data-stu-id="0d1f5-115">Some examples of workloads that are commonly processed using this technique are:</span></span>

* <span data-ttu-id="0d1f5-116">財務風險模型</span><span class="sxs-lookup"><span data-stu-id="0d1f5-116">Financial risk modeling</span></span>
* <span data-ttu-id="0d1f5-117">氣候和水文資料分析</span><span class="sxs-lookup"><span data-stu-id="0d1f5-117">Climate and hydrology data analysis</span></span>
* <span data-ttu-id="0d1f5-118">影像轉譯、分析和處理</span><span class="sxs-lookup"><span data-stu-id="0d1f5-118">Image rendering, analysis, and processing</span></span>
* <span data-ttu-id="0d1f5-119">媒體編碼及轉碼</span><span class="sxs-lookup"><span data-stu-id="0d1f5-119">Media encoding and transcoding</span></span>
* <span data-ttu-id="0d1f5-120">基因序列分析</span><span class="sxs-lookup"><span data-stu-id="0d1f5-120">Genetic sequence analysis</span></span>
* <span data-ttu-id="0d1f5-121">工程壓力分析</span><span class="sxs-lookup"><span data-stu-id="0d1f5-121">Engineering stress analysis</span></span>
* <span data-ttu-id="0d1f5-122">軟體測試</span><span class="sxs-lookup"><span data-stu-id="0d1f5-122">Software testing</span></span>

<span data-ttu-id="0d1f5-123">批次也可以執行平行計算 hello 結尾減少步驟，並執行更複雜的 HPC 工作負載，例如[訊息傳遞介面 (MPI)](batch-mpi.md)應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-123">Batch can also perform parallel calculations with a reduce step at hello end, and execute more complex HPC workloads such as [Message Passing Interface (MPI)](batch-mpi.md) applications.</span></span>

<span data-ttu-id="0d1f5-124">如需 Batch 與 Azure 中其他 HPC 解決方案選項的比較，請參閱 [Batch 和 HPC 解決方案](batch-hpc-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-124">For a comparison between Batch and other HPC solution options in Azure, see [Batch and HPC solutions](batch-hpc-solutions.md).</span></span>

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a><span data-ttu-id="0d1f5-125">案例：相應放大平行工作負載</span><span class="sxs-lookup"><span data-stu-id="0d1f5-125">Scenario: Scale out a parallel workload</span></span>
<span data-ttu-id="0d1f5-126">使用 hello 批次 Api toointeract 以 hello 批次服務的常見解決方案牽涉到向外延展本質平行工作-例如 hello 轉譯的 3D 場景-的運算節點的集區上的影像。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-126">A common solution that uses hello Batch APIs toointeract with hello Batch service involves scaling out intrinsically parallel work--such as hello rendering of images for 3D scenes--on a pool of compute nodes.</span></span> <span data-ttu-id="0d1f5-127">此集區的計算節點可以是您 「 轉譯伺服陣列 」，提供數十、 數百或甚至數千個核心 tooyour 轉譯工作，例如。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-127">This pool of compute nodes can be your "render farm" that provides tens, hundreds, or even thousands of cores tooyour rendering job, for example.</span></span>

<span data-ttu-id="0d1f5-128">hello 下列圖表顯示常見的批次工作流程，用戶端應用程式或裝載的服務使用批次 toorun 平行的工作負載。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-128">hello following diagram shows a common Batch workflow, with a client application or hosted service using Batch toorun a parallel workload.</span></span>

![Batch 解決方案工作流程][2]

<span data-ttu-id="0d1f5-130">在這個常見的案例中，應用程式或服務來處理 Azure 批次中的運算工作負載上執行下列步驟的 hello:</span><span class="sxs-lookup"><span data-stu-id="0d1f5-130">In this common scenario, your application or service processes a computational workload in Azure Batch by performing hello following steps:</span></span>

1. <span data-ttu-id="0d1f5-131">上傳 hello**輸入檔**和 hello**應用程式**，將會處理這些檔案 tooyour Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-131">Upload hello **input files** and hello **application** that will process those files tooyour Azure Storage account.</span></span> <span data-ttu-id="0d1f5-132">hello 輸入的檔可以是會處理您的應用程式，例如財務模型化資料或視訊檔案 toobe 轉碼任何資料。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-132">hello input files can be any data that your application will process, such as financial modeling data, or video files toobe transcoded.</span></span> <span data-ttu-id="0d1f5-133">hello 應用程式檔案可以用於處理 hello 資料，例如 3D 呈現應用程式或媒體轉碼程式的任何應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-133">hello application files can be any application that is used for processing hello data, such as a 3D rendering application or media transcoder.</span></span>
2. <span data-ttu-id="0d1f5-134">建立批次**集區**的運算節點，在您的 Batch 帳戶-這些節點 hello 的虛擬機器並將執行您的工作。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-134">Create a Batch **pool** of compute nodes in your Batch account--these nodes are hello virtual machines that will execute your tasks.</span></span> <span data-ttu-id="0d1f5-135">您指定屬性，例如 hello[節點大小](../cloud-services/cloud-services-sizes-specs.md)、 其作業系統和 Azure 儲存體中的 hello 應用程式 tooinstall hello 節點加入 hello 集區 （hello 應用程式，您在步驟 1 中上傳） 時的 hello 位置。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-135">You specify properties such as hello [node size](../cloud-services/cloud-services-sizes-specs.md), their operating system, and hello location in Azure Storage of hello application tooinstall when hello nodes join hello pool (hello application that you uploaded in step #1).</span></span> <span data-ttu-id="0d1f5-136">您也可以太設定 hello 集區[自動縮放表單](batch-automatic-scaling.md)回應 toohello 工作負載會產生您的工作中。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-136">You can also configure hello pool too[automatically scale](batch-automatic-scaling.md) in response toohello workload that your tasks generate.</span></span> <span data-ttu-id="0d1f5-137">自動調整動態調整 hello hello 集區中的運算節點數目。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-137">Auto-scaling dynamically adjusts hello number of compute nodes in hello pool.</span></span>
3. <span data-ttu-id="0d1f5-138">建立批次**作業**toorun hello 工作負載的運算節點的 hello 集區上。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-138">Create a Batch **job** toorun hello workload on hello pool of compute nodes.</span></span> <span data-ttu-id="0d1f5-139">當您建立作業時，您需要將它與 Batch 集區建立關聯。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-139">When you create a job, you associate it with a Batch pool.</span></span>
4. <span data-ttu-id="0d1f5-140">新增**工作**toohello 作業。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-140">Add **tasks** toohello job.</span></span> <span data-ttu-id="0d1f5-141">當您新增工作 tooa 作業時，hello 批次服務會自動排程 hello hello 集區中的 hello 計算節點上執行的工作。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-141">When you add tasks tooa job, hello Batch service automatically schedules hello tasks for execution on hello compute nodes in hello pool.</span></span> <span data-ttu-id="0d1f5-142">每項工作會使用您上傳 tooprocess hello 輸入的檔的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-142">Each task uses hello application that you uploaded tooprocess hello input files.</span></span>
   
   * <span data-ttu-id="0d1f5-143">4a.</span><span class="sxs-lookup"><span data-stu-id="0d1f5-143">4a.</span></span> <span data-ttu-id="0d1f5-144">工作會執行之前，它可以下載它是指派給 tooprocess toohello 計算節點的 hello 資料 （hello 輸入檔案）。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-144">Before a task executes, it can download hello data (hello input files) that it is tooprocess toohello compute node it is assigned to.</span></span> <span data-ttu-id="0d1f5-145">如果 hello 應用程式未安裝 hello 節點上 （請參閱步驟 2），它可以在這裡下載改為。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-145">If hello application has not already been installed on hello node (see step #2), it can be downloaded here instead.</span></span> <span data-ttu-id="0d1f5-146">Hello 下載完成時，會在其指派的節點上執行 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-146">When hello downloads are complete, hello tasks execute on their assigned nodes.</span></span>
5. <span data-ttu-id="0d1f5-147">Hello 工作執行時，您可以查詢 hello 工作和其工作批次 toomonitor hello 進度。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-147">As hello tasks run, you can query Batch toomonitor hello progress of hello job and its tasks.</span></span> <span data-ttu-id="0d1f5-148">用戶端應用程式或服務透過 HTTPS 通訊以 hello 批次服務。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-148">Your client application or service communicates with hello Batch service over HTTPS.</span></span> <span data-ttu-id="0d1f5-149">因為您可能會監視數千個數千個計算節點上執行的工作，請務必太[有效率地查詢 hello 批次服務](batch-efficient-list-queries.md)。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-149">Because you may be monitoring thousands of tasks running on thousands of compute nodes, be sure too[query hello Batch service efficiently](batch-efficient-list-queries.md).</span></span>
6. <span data-ttu-id="0d1f5-150">當 hello 工作完成時，他們可以上傳其結果資料 tooAzure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-150">As hello tasks complete, they can upload their result data tooAzure Storage.</span></span> <span data-ttu-id="0d1f5-151">您也可以直接從 hello 計算節點上的檔案系統擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-151">You can also retrieve files directly from hello file system on a compute node.</span></span>
7. <span data-ttu-id="0d1f5-152">當您的監視偵測到您的工作中的 hello 工作都完成後時，用戶端應用程式或服務可以下載 hello 做進一步處理或評估的輸出資料。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-152">When your monitoring detects that hello tasks in your job have completed, your client application or service can download hello output data for further processing or evaluation.</span></span>

<span data-ttu-id="0d1f5-153">請記住，這是其中一個方法 toouse 批次，以及這個案例說明僅提供少數可用的功能。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-153">Keep in mind this is just one way toouse Batch, and this scenario describes only a few of its available features.</span></span> <span data-ttu-id="0d1f5-154">例如，您可以執行[多項工作的平行](batch-parallel-node-tasks.md)上每個計算節點，而且您可以使用[作業準備與完成工作](batch-job-prep-release.md)tooprepare hello 節點為您的工作，然後清除之後。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-154">For example, you can execute [multiple tasks in parallel](batch-parallel-node-tasks.md) on each compute node, and you can use [job preparation and completion tasks](batch-job-prep-release.md) tooprepare hello nodes for your jobs, then clean up afterward.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0d1f5-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0d1f5-155">Next steps</span></span>
<span data-ttu-id="0d1f5-156">現在您擁有 hello 批次服務的高階概觀，它是時間 toodig 更深入 toolearn 您可以如何使用它 tooprocess 需要大量計算的平行工作負載。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-156">Now that you have a high-level overview of hello Batch service, it's time toodig deeper toolearn how you can use it tooprocess your compute-intensive parallel workloads.</span></span>

* <span data-ttu-id="0d1f5-157">讀取 hello[批次功能概觀，讓開發人員](batch-api-basics.md)，任何人準備 toouse 批次的重要資訊。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-157">Read hello [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing toouse Batch.</span></span> <span data-ttu-id="0d1f5-158">hello 發行項包含許多建置批次應用程式時，可以使用的 API 功能的批次服務資源集區、 節點、 工作和工作和 hello，如需詳細的資訊。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-158">hello article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and hello many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="0d1f5-159">深入了解 hello[批次應用程式開發介面和工具](batch-apis-tools.md)可用來建置批次的解決方案。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-159">Learn about hello [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
* <span data-ttu-id="0d1f5-160">[開始使用 hello Azure Batch library for.NET](batch-dotnet-get-started.md) toolearn 如何 toouse C# 和 hello 批次.NET 程式庫 tooexecute 簡單的工作負載使用常見的批次工作流程。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-160">[Get started with hello Azure Batch library for .NET](batch-dotnet-get-started.md) toolearn how toouse C# and hello Batch .NET library tooexecute a simple workload using a common Batch workflow.</span></span> <span data-ttu-id="0d1f5-161">這篇文章應為其中一個您同時學習如何 toouse hello 批次服務的第一個停止。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-161">This article should be one of your first stops while learning how toouse hello Batch service.</span></span> <span data-ttu-id="0d1f5-162">另外還有[Python 版本](batch-python-tutorial.md)hello 教學課程。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-162">There is also a [Python version](batch-python-tutorial.md) of hello tutorial.</span></span>
* <span data-ttu-id="0d1f5-163">下載 hello[程式碼範例在 GitHub 上的][ github_samples] toosee C# 和 Python 與批次 tooschedule 和程序範例工作負載可以互動方式。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-163">Download hello [code samples on GitHub][github_samples] toosee how both C# and Python can interface with Batch tooschedule and process sample workloads.</span></span>
* <span data-ttu-id="0d1f5-164">簽出 hello[批次學習路徑][ learning_path] tooget hello 資源可用 tooyou 您了解學習 toowork 與批次。</span><span class="sxs-lookup"><span data-stu-id="0d1f5-164">Check out hello [Batch Learning Path][learning_path] tooget an idea of hello resources available tooyou as you learn toowork with Batch.</span></span>


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
