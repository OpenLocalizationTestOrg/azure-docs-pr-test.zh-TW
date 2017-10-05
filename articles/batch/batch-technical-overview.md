---
title: "Azure Batch 在雲端執行大規模的平行運算解決方案 | Microsoft Docs"
description: "了解如何將 Azure Batch 服務用於大規模的平行工作負載和 HPC 工作負載"
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
ms.openlocfilehash: 3bda4859e7ce45f5f7b8df6167e6e9d2cedd5c62
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="run-intrinsically-parallel-workloads-with-batch"></a><span data-ttu-id="271f8-103">使用 Batch 執行本質平行的工作負載</span><span class="sxs-lookup"><span data-stu-id="271f8-103">Run intrinsically parallel workloads with Batch</span></span>

<span data-ttu-id="271f8-104">Azure Batch 是一項平台服務，可用於在雲端有效地執行大規模的平行和高效能運算 (HPC) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="271f8-104">Azure Batch is a platform service for running large-scale parallel and high-performance computing (HPC) applications efficiently in the cloud.</span></span> <span data-ttu-id="271f8-105">Azure Batch 可排程要在一組受管理的虛擬機器上執行的計算密集型工作，而且可以調整計算資源以符合工作的需求。</span><span class="sxs-lookup"><span data-stu-id="271f8-105">Azure Batch schedules compute-intensive work to run on a managed collection of virtual machines, and can automatically scale compute resources to meet the needs of your jobs.</span></span>

<span data-ttu-id="271f8-106">使用 Batch 時，您可以輕鬆定義用來大規模平行執行應用程式的 Azure 計算資源。</span><span class="sxs-lookup"><span data-stu-id="271f8-106">With Azure Batch, you can easily define Azure compute resources to execute your applications in parallel, and at scale.</span></span> <span data-ttu-id="271f8-107">不需要手動建立、設定和管理 HPC 叢集、個別的虛擬機器、虛擬網路或複雜的作業和工作排程基礎結構。</span><span class="sxs-lookup"><span data-stu-id="271f8-107">There's no need to manually create, configure, and manage an HPC cluster, individual virtual machines, virtual networks, or a complex job and task scheduling infrastructure.</span></span> <span data-ttu-id="271f8-108">Azure Batch 會為您自動執行或簡化這些工作。</span><span class="sxs-lookup"><span data-stu-id="271f8-108">Azure Batch automates or simplifies these tasks for you.</span></span>

## <a name="use-cases-for-batch"></a><span data-ttu-id="271f8-109">Batch 的使用案例</span><span class="sxs-lookup"><span data-stu-id="271f8-109">Use cases for Batch</span></span>
<span data-ttu-id="271f8-110">Batch 是一項受管理的 Azure 服務，可用於批次處理或批次運算 -- 執行大量的類似工作以得到期望的結果。</span><span class="sxs-lookup"><span data-stu-id="271f8-110">Batch is a managed Azure service that is used for *batch processing* or *batch computing*--running a large volume of similar tasks for a desired result.</span></span> <span data-ttu-id="271f8-111">定期處理、轉換和分析大量資料的組織最常使用批次運算。</span><span class="sxs-lookup"><span data-stu-id="271f8-111">Batch computing is most commonly used by organizations that regularly process, transform, and analyze large volumes of data.</span></span>

<span data-ttu-id="271f8-112">Batch 很適合處理本質平行 (也稱為「超簡單平行」) 的應用程式和工作負載。</span><span class="sxs-lookup"><span data-stu-id="271f8-112">Batch works well with intrinsically parallel (also known as "embarrassingly parallel") applications and workloads.</span></span> <span data-ttu-id="271f8-113">本質上平行的工作負載可輕易分割成多個工作，以在多部電腦上同時執行。</span><span class="sxs-lookup"><span data-stu-id="271f8-113">Intrinsically parallel workloads are those that are easily split into multiple tasks that perform work simultaneously on many computers.</span></span>

![平行工作][1]<br/>

<span data-ttu-id="271f8-115">常見使用這項技術處理的一些工作負載範例如下：</span><span class="sxs-lookup"><span data-stu-id="271f8-115">Some examples of workloads that are commonly processed using this technique are:</span></span>

* <span data-ttu-id="271f8-116">財務風險模型</span><span class="sxs-lookup"><span data-stu-id="271f8-116">Financial risk modeling</span></span>
* <span data-ttu-id="271f8-117">氣候和水文資料分析</span><span class="sxs-lookup"><span data-stu-id="271f8-117">Climate and hydrology data analysis</span></span>
* <span data-ttu-id="271f8-118">影像轉譯、分析和處理</span><span class="sxs-lookup"><span data-stu-id="271f8-118">Image rendering, analysis, and processing</span></span>
* <span data-ttu-id="271f8-119">媒體編碼及轉碼</span><span class="sxs-lookup"><span data-stu-id="271f8-119">Media encoding and transcoding</span></span>
* <span data-ttu-id="271f8-120">基因序列分析</span><span class="sxs-lookup"><span data-stu-id="271f8-120">Genetic sequence analysis</span></span>
* <span data-ttu-id="271f8-121">工程壓力分析</span><span class="sxs-lookup"><span data-stu-id="271f8-121">Engineering stress analysis</span></span>
* <span data-ttu-id="271f8-122">軟體測試</span><span class="sxs-lookup"><span data-stu-id="271f8-122">Software testing</span></span>

<span data-ttu-id="271f8-123">Batch 也可以執行平行計算 (最後加上歸納步驟)，以及執行其他更複雜的 HPC 工作負載，例如 [訊息傳遞介面 (MPI)](batch-mpi.md) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="271f8-123">Batch can also perform parallel calculations with a reduce step at the end, and execute more complex HPC workloads such as [Message Passing Interface (MPI)](batch-mpi.md) applications.</span></span>

<span data-ttu-id="271f8-124">如需 Batch 與 Azure 中其他 HPC 解決方案選項的比較，請參閱 [Batch 和 HPC 解決方案](batch-hpc-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="271f8-124">For a comparison between Batch and other HPC solution options in Azure, see [Batch and HPC solutions](batch-hpc-solutions.md).</span></span>

[!INCLUDE [batch-pricing-include](../../includes/batch-pricing-include.md)]

## <a name="scenario-scale-out-a-parallel-workload"></a><span data-ttu-id="271f8-125">案例：相應放大平行工作負載</span><span class="sxs-lookup"><span data-stu-id="271f8-125">Scenario: Scale out a parallel workload</span></span>
<span data-ttu-id="271f8-126">使用 Batch API 來與 Batch 服務互動的一個常見案例涉及在一組計算節點上相應放大本質平行工作，例如轉譯 3D 場景的影像。</span><span class="sxs-lookup"><span data-stu-id="271f8-126">A common solution that uses the Batch APIs to interact with the Batch service involves scaling out intrinsically parallel work--such as the rendering of images for 3D scenes--on a pool of compute nodes.</span></span> <span data-ttu-id="271f8-127">例如，這組計算節點可能是您的「轉譯伺服器陣列」，提供數十、數百或甚至數千個核心來呈現作業。</span><span class="sxs-lookup"><span data-stu-id="271f8-127">This pool of compute nodes can be your "render farm" that provides tens, hundreds, or even thousands of cores to your rendering job, for example.</span></span>

<span data-ttu-id="271f8-128">下圖顯示一個常見的 Batch 工作流程，其中有一個用戶端應用程式或託管服務使用 Batch 執行平行工作負載。</span><span class="sxs-lookup"><span data-stu-id="271f8-128">The following diagram shows a common Batch workflow, with a client application or hosted service using Batch to run a parallel workload.</span></span>

![Batch 解決方案工作流程][2]

<span data-ttu-id="271f8-130">在這個常見的案例中，應用程式或服務執行下列步驟，在 Azure Batch 中處理計算工作負載：</span><span class="sxs-lookup"><span data-stu-id="271f8-130">In this common scenario, your application or service processes a computational workload in Azure Batch by performing the following steps:</span></span>

1. <span data-ttu-id="271f8-131">將**輸入檔**和處理這些檔案的**應用程式**上傳到您的 Azure 儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="271f8-131">Upload the **input files** and the **application** that will process those files to your Azure Storage account.</span></span> <span data-ttu-id="271f8-132">輸入檔可以是您的應用程式將會處理的任何資料，例如財務模型化資料或要轉碼的視訊檔案。</span><span class="sxs-lookup"><span data-stu-id="271f8-132">The input files can be any data that your application will process, such as financial modeling data, or video files to be transcoded.</span></span> <span data-ttu-id="271f8-133">應用程式檔案可以是任何用於處理資料的應用程式，例如 3D 轉譯應用程式或媒體轉碼器。</span><span class="sxs-lookup"><span data-stu-id="271f8-133">The application files can be any application that is used for processing the data, such as a 3D rendering application or media transcoder.</span></span>
2. <span data-ttu-id="271f8-134">在 Batch 帳戶中建立計算節點的 Batch **集區** -- 這些節點是將執行工作的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="271f8-134">Create a Batch **pool** of compute nodes in your Batch account--these nodes are the virtual machines that will execute your tasks.</span></span> <span data-ttu-id="271f8-135">您需要指定屬性，例如[節點大小](../cloud-services/cloud-services-sizes-specs.md)、其作業系統，以及節點加入集區時要安裝的應用程式在 Azure 儲存體中的位置 (您在步驟 #1 中上傳的應用程式)。</span><span class="sxs-lookup"><span data-stu-id="271f8-135">You specify properties such as the [node size](../cloud-services/cloud-services-sizes-specs.md), their operating system, and the location in Azure Storage of the application to install when the nodes join the pool (the application that you uploaded in step #1).</span></span> <span data-ttu-id="271f8-136">您也可以設定集區來隨著工作所產生的工作負載而[自動調整](batch-automatic-scaling.md)。</span><span class="sxs-lookup"><span data-stu-id="271f8-136">You can also configure the pool to [automatically scale](batch-automatic-scaling.md) in response to the workload that your tasks generate.</span></span> <span data-ttu-id="271f8-137">自動調整功能可動態調整集區中的計算節點數目。</span><span class="sxs-lookup"><span data-stu-id="271f8-137">Auto-scaling dynamically adjusts the number of compute nodes in the pool.</span></span>
3. <span data-ttu-id="271f8-138">建立 Batch **作業** 以在計算節點集區上執行工作負載。</span><span class="sxs-lookup"><span data-stu-id="271f8-138">Create a Batch **job** to run the workload on the pool of compute nodes.</span></span> <span data-ttu-id="271f8-139">當您建立作業時，您需要將它與 Batch 集區建立關聯。</span><span class="sxs-lookup"><span data-stu-id="271f8-139">When you create a job, you associate it with a Batch pool.</span></span>
4. <span data-ttu-id="271f8-140">將 **工作** 加入至作業。</span><span class="sxs-lookup"><span data-stu-id="271f8-140">Add **tasks** to the job.</span></span> <span data-ttu-id="271f8-141">當您將工作加入至作業時，Batch 服務會自動排程工作在集區中的計算節點上執行。</span><span class="sxs-lookup"><span data-stu-id="271f8-141">When you add tasks to a job, the Batch service automatically schedules the tasks for execution on the compute nodes in the pool.</span></span> <span data-ttu-id="271f8-142">每一項工作會使用您上傳的應用程式來處理輸入檔。</span><span class="sxs-lookup"><span data-stu-id="271f8-142">Each task uses the application that you uploaded to process the input files.</span></span>
   
   * <span data-ttu-id="271f8-143">4a.</span><span class="sxs-lookup"><span data-stu-id="271f8-143">4a.</span></span> <span data-ttu-id="271f8-144">工作執行之前，它可以將它要處理的資料 (輸入檔) 下載至它被指派的計算節點。</span><span class="sxs-lookup"><span data-stu-id="271f8-144">Before a task executes, it can download the data (the input files) that it is to process to the compute node it is assigned to.</span></span> <span data-ttu-id="271f8-145">如果應用程式未安裝在節點上 (請參閱步驟 2#)，您可以從這裡下載它。</span><span class="sxs-lookup"><span data-stu-id="271f8-145">If the application has not already been installed on the node (see step #2), it can be downloaded here instead.</span></span> <span data-ttu-id="271f8-146">下載完成時，工作就會在它被指派的節點上執行。</span><span class="sxs-lookup"><span data-stu-id="271f8-146">When the downloads are complete, the tasks execute on their assigned nodes.</span></span>
5. <span data-ttu-id="271f8-147">工作執行時，您可以查詢 Batch 來監視作業及其工作的進度。</span><span class="sxs-lookup"><span data-stu-id="271f8-147">As the tasks run, you can query Batch to monitor the progress of the job and its tasks.</span></span> <span data-ttu-id="271f8-148">用戶端應用程式或服務可透過 HTTPS 來與 Batch 服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="271f8-148">Your client application or service communicates with the Batch service over HTTPS.</span></span> <span data-ttu-id="271f8-149">因為您可能會監視在數千個計算節點上執行的數千個工作，請務必[有效率地查詢 Batch 服務](batch-efficient-list-queries.md)。</span><span class="sxs-lookup"><span data-stu-id="271f8-149">Because you may be monitoring thousands of tasks running on thousands of compute nodes, be sure to [query the Batch service efficiently](batch-efficient-list-queries.md).</span></span>
6. <span data-ttu-id="271f8-150">當工作完成時，它們可以將其輸出資料上傳至 Azure 儲存體。</span><span class="sxs-lookup"><span data-stu-id="271f8-150">As the tasks complete, they can upload their result data to Azure Storage.</span></span> <span data-ttu-id="271f8-151">您也可以直接從計算節點上的檔案系統擷取檔案。</span><span class="sxs-lookup"><span data-stu-id="271f8-151">You can also retrieve files directly from the file system on a compute node.</span></span>
7. <span data-ttu-id="271f8-152">當您的監視偵測到作業中的工作已完成時，用戶端應用程式或服務可以下載輸出資料來進一步處理或評估。</span><span class="sxs-lookup"><span data-stu-id="271f8-152">When your monitoring detects that the tasks in your job have completed, your client application or service can download the output data for further processing or evaluation.</span></span>

<span data-ttu-id="271f8-153">請記住，這只是使用 Batch 的一種方式，此案例只描述它可用的幾項功能。</span><span class="sxs-lookup"><span data-stu-id="271f8-153">Keep in mind this is just one way to use Batch, and this scenario describes only a few of its available features.</span></span> <span data-ttu-id="271f8-154">例如，您可以在每個計算節點上[以平行方式執行多項工作](batch-parallel-node-tasks.md)，也可以使用[作業準備和完成工作](batch-job-prep-release.md)來準備作業的節點，然後再清除。</span><span class="sxs-lookup"><span data-stu-id="271f8-154">For example, you can execute [multiple tasks in parallel](batch-parallel-node-tasks.md) on each compute node, and you can use [job preparation and completion tasks](batch-job-prep-release.md) to prepare the nodes for your jobs, then clean up afterward.</span></span>

## <a name="next-steps"></a><span data-ttu-id="271f8-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="271f8-155">Next steps</span></span>
<span data-ttu-id="271f8-156">既然您已大致了解 Batch 服務，現在可以更深入探索服務，了解如何使用它來處理計算密集平行工作負載。</span><span class="sxs-lookup"><span data-stu-id="271f8-156">Now that you have a high-level overview of the Batch service, it's time to dig deeper to learn how you can use it to process your compute-intensive parallel workloads.</span></span>

* <span data-ttu-id="271f8-157">請參閱 [適用於開發人員的 Batch 功能概觀](batch-api-basics.md)，這是任何準備使用 Batch 的人員不可或缺的資訊。</span><span class="sxs-lookup"><span data-stu-id="271f8-157">Read the [Batch feature overview for developers](batch-api-basics.md), essential information for anyone preparing to use Batch.</span></span> <span data-ttu-id="271f8-158">本文包含 Batch 服務資源 (例如集區、節點、作業和工作) 的詳細資訊，以及在建置 Batch 應用程式時可使用的許多 API 功能。</span><span class="sxs-lookup"><span data-stu-id="271f8-158">The article contains more detailed information about Batch service resources like pools, nodes, jobs, and tasks, and the many API features that you can use while building your Batch application.</span></span>
* <span data-ttu-id="271f8-159">了解可用來建置 Batch 解決方案的 [Batch API 和工具](batch-apis-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="271f8-159">Learn about the [Batch APIs and tools](batch-apis-tools.md) available for building Batch solutions.</span></span>
* <span data-ttu-id="271f8-160">[開始使用適用於 .NET 的 Azure Batch 程式庫](batch-dotnet-get-started.md) ，了解如何使用 C# 和 Batch .NET 程式庫，透過一般的批次工作流程來執行簡單的工作負載。</span><span class="sxs-lookup"><span data-stu-id="271f8-160">[Get started with the Azure Batch library for .NET](batch-dotnet-get-started.md) to learn how to use C# and the Batch .NET library to execute a simple workload using a common Batch workflow.</span></span> <span data-ttu-id="271f8-161">本文應該是您學習如何使用 Batch 服務的第一站。</span><span class="sxs-lookup"><span data-stu-id="271f8-161">This article should be one of your first stops while learning how to use the Batch service.</span></span> <span data-ttu-id="271f8-162">另外還有 [Python 版本](batch-python-tutorial.md) 的教學課程。</span><span class="sxs-lookup"><span data-stu-id="271f8-162">There is also a [Python version](batch-python-tutorial.md) of the tutorial.</span></span>
* <span data-ttu-id="271f8-163">下載 [GitHub 上的程式碼範例][github_samples]，看看 C# 和 Python 如何與 Batch 相互作用，以排程和處理範例工作負載。</span><span class="sxs-lookup"><span data-stu-id="271f8-163">Download the [code samples on GitHub][github_samples] to see how both C# and Python can interface with Batch to schedule and process sample workloads.</span></span>
* <span data-ttu-id="271f8-164">查看 [Batch 學習路徑][learning_path]，了解您在學習使用 Batch 時可用的資源。</span><span class="sxs-lookup"><span data-stu-id="271f8-164">Check out the [Batch Learning Path][learning_path] to get an idea of the resources available to you as you learn to work with Batch.</span></span>


[github_samples]: https://github.com/Azure/azure-batch-samples
[learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/

[1]: ./media/batch-technical-overview/tech_overview_01.png
[2]: ./media/batch-technical-overview/tech_overview_02.png
