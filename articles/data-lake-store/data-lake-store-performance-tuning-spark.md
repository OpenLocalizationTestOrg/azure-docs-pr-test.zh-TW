---
title: "Azure Data Lake Store Spark 效能微調方針 | Microsoft Docs"
description: "Azure Data Lake Store Spark 效能微調方針"
services: data-lake-store
documentationcenter: 
author: stewu
manager: amitkul
editor: stewu
ms.assetid: ebde7b9f-2e51-4d43-b7ab-566417221335
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/19/2016
ms.author: stewu
ms.openlocfilehash: 2109744fb7ffdfafb7a86bbea355e119718af099
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="ea40c-103">HDInsight 和 Azure Data Lake Store 上的 Spark 效能微調方針</span><span class="sxs-lookup"><span data-stu-id="ea40c-103">Performance tuning guidance for Spark on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="ea40c-104">在微調 Spark 的效能時，您必須考慮叢集上會執行的應用程式數目。</span><span class="sxs-lookup"><span data-stu-id="ea40c-104">When tuning performance on Spark, you need to consider the number of apps that will be running on your cluster.</span></span>  <span data-ttu-id="ea40c-105">根據預設，您可以在 HDI 叢集上並行執行 4 個應用程式 (附註︰預設設定有可能變更)。</span><span class="sxs-lookup"><span data-stu-id="ea40c-105">By default, you can run 4 apps concurrently on your HDI cluster (Note: the default setting is subject to change).</span></span>  <span data-ttu-id="ea40c-106">您可能會決定使用較少的應用程式，因此您可以覆寫預設設定，並使用更多的叢集來執行這些應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea40c-106">You may decide to use fewer apps so you can override the default settings and use more of the cluster for those apps.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="ea40c-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="ea40c-107">Prerequisites</span></span>

* <span data-ttu-id="ea40c-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="ea40c-108">**An Azure subscription**.</span></span> <span data-ttu-id="ea40c-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="ea40c-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ea40c-110">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="ea40c-110">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="ea40c-111">如需有關如何建立帳戶的詳細指示，請參閱 [開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="ea40c-111">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="ea40c-112">**Azure HDInsight 叢集** 。</span><span class="sxs-lookup"><span data-stu-id="ea40c-112">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="ea40c-113">請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="ea40c-113">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="ea40c-114">請確實為叢集啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="ea40c-114">Make sure you enable Remote Desktop for the cluster.</span></span>
* <span data-ttu-id="ea40c-115">**在 Azure Data Lake Store 上執行 Spark 叢集**。</span><span class="sxs-lookup"><span data-stu-id="ea40c-115">**Running Spark cluster on Azure Data Lake Store**.</span></span>  <span data-ttu-id="ea40c-116">如需詳細資訊，請參閱[使用 HDInsight Spark 叢集來分析 Data Lake Store 中的資料](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)</span><span class="sxs-lookup"><span data-stu-id="ea40c-116">For more information, see [Use HDInsight Spark cluster to analyze data in Data Lake Store](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)</span></span>
* <span data-ttu-id="ea40c-117">**ADLS 的效能微調指導方針**。</span><span class="sxs-lookup"><span data-stu-id="ea40c-117">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="ea40c-118">如需一般的效能概念，請參閱 [Data Lake Store 效能微調指導方針](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span><span class="sxs-lookup"><span data-stu-id="ea40c-118">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span> 

## <a name="parameters"></a><span data-ttu-id="ea40c-119">參數</span><span class="sxs-lookup"><span data-stu-id="ea40c-119">Parameters</span></span>

<span data-ttu-id="ea40c-120">在執行 Spark 作業時，以下是要增進 ADLS 效能所能微調的最重要設定︰</span><span class="sxs-lookup"><span data-stu-id="ea40c-120">When running Spark jobs, here are the most important settings that can be tuned to increase performance on ADLS:</span></span>

* <span data-ttu-id="ea40c-121">**Num-executors** - 可執行的並行工作數目。</span><span class="sxs-lookup"><span data-stu-id="ea40c-121">**Num-executors** - The number of concurrent tasks that can be executed.</span></span>

* <span data-ttu-id="ea40c-122">**Executor-memory** - 配置給每個執行程式的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="ea40c-122">**Executor-memory** - The amount of memory allocated to each executor.</span></span>

* <span data-ttu-id="ea40c-123">**Executor-cores** - 配置給每個執行程式的核心數目。</span><span class="sxs-lookup"><span data-stu-id="ea40c-123">**Executor-cores** - The number of cores allocated to each executor.</span></span>                     

<span data-ttu-id="ea40c-124">**Num-executors** Num-executors 會設定可平行執行的工作數目上限。</span><span class="sxs-lookup"><span data-stu-id="ea40c-124">**Num-executors** Num-executors will set the maximum number of tasks that can run in parallel.</span></span>  <span data-ttu-id="ea40c-125">可平行執行的實際工作數目會受限於叢集中可用的記憶體和 CPU 資源。</span><span class="sxs-lookup"><span data-stu-id="ea40c-125">The actual number of tasks that can run in parallel is bounded by the memory and CPU resources available in your cluster.</span></span>

<span data-ttu-id="ea40c-126">**Executor-memory** - 這是要配置給每個執行程式的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="ea40c-126">**Executor-memory** This is the amount of memory that is being allocated to each executor.</span></span>  <span data-ttu-id="ea40c-127">每個執行程式所需的記憶體取決於作業。</span><span class="sxs-lookup"><span data-stu-id="ea40c-127">The memory needed for each executor is dependent on the job.</span></span>  <span data-ttu-id="ea40c-128">複雜的作業需要較高的記憶體。</span><span class="sxs-lookup"><span data-stu-id="ea40c-128">For complex operations, the memory needs to be higher.</span></span>  <span data-ttu-id="ea40c-129">讀取和寫入等簡單作業的記憶體需求會較低。</span><span class="sxs-lookup"><span data-stu-id="ea40c-129">For simple operations like read and write, memory requirements will be lower.</span></span>  <span data-ttu-id="ea40c-130">您可以在 Ambari 中檢視每個執行程式的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="ea40c-130">The amount of memory for each executor can be viewed in Ambari.</span></span>  <span data-ttu-id="ea40c-131">在 Ambari 中，瀏覽至 Spark，然後檢視 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ea40c-131">In Ambari, navigate to Spark and view the Configs tab.</span></span>  

<span data-ttu-id="ea40c-132">**Executor-cores** 這會設定每個執行程式所使用的核心數量，進而決定每個執行程式可以執行的平行執行緒數目。</span><span class="sxs-lookup"><span data-stu-id="ea40c-132">**Executor-cores** This sets the amount of cores used per executor, which determines the number of parallel threads that can be run per executor.</span></span>  <span data-ttu-id="ea40c-133">例如，如果 executor-cores = 2，則每個執行程式可以在執行程式中執行 2 個平行工作。</span><span class="sxs-lookup"><span data-stu-id="ea40c-133">For example, if executor-cores = 2, then each executor can run 2 parallel tasks in the executor.</span></span>  <span data-ttu-id="ea40c-134">所需的 executor-cores 取決於該作業。</span><span class="sxs-lookup"><span data-stu-id="ea40c-134">The executor-cores needed will be dependent on the job.</span></span>  <span data-ttu-id="ea40c-135">需要大量 I/O 的作業所需的每一工作記憶體並不需要太多，因此每個執行程式可以處理更多的平行工作。</span><span class="sxs-lookup"><span data-stu-id="ea40c-135">I/O heavy jobs do not require a large amount of memory per task so each executor can handle more parallel tasks.</span></span>

<span data-ttu-id="ea40c-136">依預設，在 HDInsight 上執行 Spark 時，會為每個實體核心定義兩個虛擬 YARN 核心。</span><span class="sxs-lookup"><span data-stu-id="ea40c-136">By default, two virtual YARN cores are defined for each physical core when running Spark on HDInsight.</span></span>  <span data-ttu-id="ea40c-137">這個數量能在並行能力與從多個執行緒切換而來的內容數量取得良好平衡。</span><span class="sxs-lookup"><span data-stu-id="ea40c-137">This number provides a good balance of concurrecy and amount of context switching from multiple threads.</span></span>  

## <a name="guidance"></a><span data-ttu-id="ea40c-138">指引</span><span class="sxs-lookup"><span data-stu-id="ea40c-138">Guidance</span></span>

<span data-ttu-id="ea40c-139">針對 Data Lake Store 中的資料執行 Spark 分析工作負載時，我們建議您使用最新的 HDInsight 版本以取得最佳的 Data Lake Store 效能。</span><span class="sxs-lookup"><span data-stu-id="ea40c-139">While running Spark analytic workloads to work with data in Data Lake Store, we recommend that you use the most recent HDInsight version to get the best performance with Data Lake Store.</span></span> <span data-ttu-id="ea40c-140">當您的作業較為 I/O 密集時，您可以設定某些參數以提升效能。</span><span class="sxs-lookup"><span data-stu-id="ea40c-140">When your job is more I/O intensive, then certain parameters can be configured to improve performance.</span></span>  <span data-ttu-id="ea40c-141">Azure Data Lake Store 是具有高擴充性的儲存體平台，可處理高輸送量。</span><span class="sxs-lookup"><span data-stu-id="ea40c-141">Azure Data Lake Store is a highly scalable storage platform that can handle high throughput.</span></span>  <span data-ttu-id="ea40c-142">如果作業主要包含讀取和寫入，則為 I/O 提升針對 Azure Data Lake Store 的並行將會提升效能。</span><span class="sxs-lookup"><span data-stu-id="ea40c-142">If the job mainly consists of read or writes, then increasing concurrency for I/O to and from Azure Data Lake Store could increase performance.</span></span>

<span data-ttu-id="ea40c-143">有幾種基本的方法可以提升 I/O 密集作業的並行。</span><span class="sxs-lookup"><span data-stu-id="ea40c-143">There are a few general ways to increase concurrency for I/O intensive jobs.</span></span>

<span data-ttu-id="ea40c-144">**步驟 1︰確定叢集上所執行的應用程式數目** – 您應該要知道有多少個應用程式在叢集上執行，包括目前的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea40c-144">**Step 1: Determine how many apps are running on your cluster** – You should know how many apps are running on the cluster including the current one.</span></span>  <span data-ttu-id="ea40c-145">每個 Spark 設定的預設值會假設有 4 個應用程式在並行執行。</span><span class="sxs-lookup"><span data-stu-id="ea40c-145">The default values for each Spark setting assumes that there are 4 apps running concurrently.</span></span>  <span data-ttu-id="ea40c-146">因此，每個應用程式只能使用 25% 的叢集。</span><span class="sxs-lookup"><span data-stu-id="ea40c-146">Therefore, you will only have 25% of the cluster available for each app.</span></span>  <span data-ttu-id="ea40c-147">若要獲得更好的效能，您可以變更執行程式的數目來覆寫預設值。</span><span class="sxs-lookup"><span data-stu-id="ea40c-147">To get better performance, you can override the defaults by changing the number of executors.</span></span>  

<span data-ttu-id="ea40c-148">**步驟 2︰設定 executor-memory** – 首先要設定的是 executor-memory。</span><span class="sxs-lookup"><span data-stu-id="ea40c-148">**Step 2: Set executor-memory** – the first thing to set is the executor-memory.</span></span>  <span data-ttu-id="ea40c-149">記憶體會取決於您要執行的作業。</span><span class="sxs-lookup"><span data-stu-id="ea40c-149">The memory will be dependent on the job that you are going to run.</span></span>  <span data-ttu-id="ea40c-150">您可以為每個執行程式配置較少的記憶體，以增加並行數量。</span><span class="sxs-lookup"><span data-stu-id="ea40c-150">You can increase concurrency by allocating less memory per executor.</span></span>  <span data-ttu-id="ea40c-151">如果您在執行作業時看到記憶體不足的例外狀況，則應該增加此參數的值。</span><span class="sxs-lookup"><span data-stu-id="ea40c-151">If you see out of memory exceptions when you run your job, then you should increase the value for this parameter.</span></span>  <span data-ttu-id="ea40c-152">另一個方式是使用擁有較高數量記憶體的叢集，或增加叢集大小，以獲得更多的記憶體。</span><span class="sxs-lookup"><span data-stu-id="ea40c-152">One alternative is to get more memory by using a cluster that has higher amounts of memory or increasing the size of your cluster.</span></span>  <span data-ttu-id="ea40c-153">更多的記憶體就能使用更多的執行程式，亦即會有更多並行能力。</span><span class="sxs-lookup"><span data-stu-id="ea40c-153">More memory will enable more executors to be used, which means more concurrency.</span></span>

<span data-ttu-id="ea40c-154">**步驟 3︰設定 executor-cores** – 對於沒有複雜作業的 I/O 密集工作負載，最好是先設定較高的 executor-cores 數值，以增加每個執行程式的平行工作數目。</span><span class="sxs-lookup"><span data-stu-id="ea40c-154">**Step 3: Set executor-cores** – For I/O intensive workloads that do not have complex operations, it’s good to start with a high number of executor-cores to increase the number of parallel tasks per executor.</span></span>  <span data-ttu-id="ea40c-155">將 executor-cores 設定為 4 是不錯的開始。</span><span class="sxs-lookup"><span data-stu-id="ea40c-155">Setting executor-cores to 4 is a good start.</span></span>   

    executor-cores = 4
<span data-ttu-id="ea40c-156">增加 executor-cores 的數字可讓您更符合平行處理原則，因此請試試不同的 executor-cores。</span><span class="sxs-lookup"><span data-stu-id="ea40c-156">Increasing the number of executor-cores will give you more parallelism so you can experiment with different executor-cores.</span></span>  <span data-ttu-id="ea40c-157">對於具有較複雜作業的工作，您應該減少每個執行程式的核心數目。</span><span class="sxs-lookup"><span data-stu-id="ea40c-157">For jobs that have more complex operations, you should reduce the number of cores per executor.</span></span>  <span data-ttu-id="ea40c-158">如果 executor-cores 設定為高於 4，則記憶體回收可能會變得沒有效率而降低效能。</span><span class="sxs-lookup"><span data-stu-id="ea40c-158">If executor-cores is set higher than 4, then garbage collection may become inefficient and degrade performance.</span></span>

<span data-ttu-id="ea40c-159">**步驟 4︰決定叢集中的 YARN 記憶體數量** – 這項資訊可在 Ambari 中取得。</span><span class="sxs-lookup"><span data-stu-id="ea40c-159">**Step 4: Determine amount of YARN memory in cluster** – This information is available in Ambari.</span></span>  <span data-ttu-id="ea40c-160">瀏覽至 YARN，然後檢視 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="ea40c-160">Navigate to YARN and view the Configs tab.</span></span>  <span data-ttu-id="ea40c-161">YARN 記憶體會顯示在此視窗中。</span><span class="sxs-lookup"><span data-stu-id="ea40c-161">The YARN memory is displayed in this window.</span></span>  
<span data-ttu-id="ea40c-162">注意︰當您位於此視窗時，您也可以查看預設的 YARN 容器大小。</span><span class="sxs-lookup"><span data-stu-id="ea40c-162">Note: while you are in the window, you can also see the default YARN container size.</span></span>  <span data-ttu-id="ea40c-163">YARN 容器大小和每個執行程式參數的記憶體相同。</span><span class="sxs-lookup"><span data-stu-id="ea40c-163">The YARN container size is the same as memory per executor paramter.</span></span>

    Total YARN memory = nodes * YARN memory per node
<span data-ttu-id="ea40c-164">**步驟 5︰計算 num-executors**</span><span class="sxs-lookup"><span data-stu-id="ea40c-164">**Step 5: Calculate num-executors**</span></span>

<span data-ttu-id="ea40c-165">**計算記憶體限制** - num-executors 參數會受到記憶體或 CPU 所限制。</span><span class="sxs-lookup"><span data-stu-id="ea40c-165">**Calculate memory constraint** - The num-executors parameter is constrained either by memory or by CPU.</span></span>  <span data-ttu-id="ea40c-166">記憶體限制取決於應用程式的可用 YARN 記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="ea40c-166">The memory constraint is determined by the amount of available YARN memory for your application.</span></span>  <span data-ttu-id="ea40c-167">您應該取得 YARN 記憶體總數，然後除以 executor-memory。</span><span class="sxs-lookup"><span data-stu-id="ea40c-167">You should take total YARN memory and divide that by executor-memory.</span></span>  <span data-ttu-id="ea40c-168">應用程式數目的限制必須取消調整，因此我們除以應用程式數目。</span><span class="sxs-lookup"><span data-stu-id="ea40c-168">The constraint needs to be de-scaled for the number of apps so we divide by the number of apps.</span></span>

    Memory constraint = (total YARN memory / executor memory) / # of apps   
<span data-ttu-id="ea40c-169">**計算 CPU 限制**-CPU 限制的計算方式為虛擬核心總數除以每個執行程式的核心數目。</span><span class="sxs-lookup"><span data-stu-id="ea40c-169">**Calculate CPU constraint** - The CPU constraint is calculated as the total virtual cores divided by the number of cores per executor.</span></span>  <span data-ttu-id="ea40c-170">每個實體核心有 2 個虛擬核心。</span><span class="sxs-lookup"><span data-stu-id="ea40c-170">There are 2 virtual cores for each physical core.</span></span>  <span data-ttu-id="ea40c-171">和記憶體限制類似，我們除以應用程式數目。</span><span class="sxs-lookup"><span data-stu-id="ea40c-171">Similar to the memory constraint, we have divide by the number of apps.</span></span>

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
<span data-ttu-id="ea40c-172">**設定 num-executors**– num-executors 參數是由記憶體限制和 CPU 限制較小者來決定。</span><span class="sxs-lookup"><span data-stu-id="ea40c-172">**Set num-executors** – The num-executors parameter is determined by taking the minimum of the memory constraint and the CPU constraint.</span></span> 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
<span data-ttu-id="ea40c-173">設定較高的 num-executors 數值未必能提升效能。</span><span class="sxs-lookup"><span data-stu-id="ea40c-173">Setting a higher number of num-executors does not necessarily increase performance.</span></span>  <span data-ttu-id="ea40c-174">您應該考慮到，新增更多執行程式會對每個額外的執行程式新增額外的負擔，而可能降低效能。</span><span class="sxs-lookup"><span data-stu-id="ea40c-174">You should consider that adding more executors will add extra overhead for each additional executor, which can potentially degrade performance.</span></span>  <span data-ttu-id="ea40c-175">Num-executors 受到叢集資源的限制。</span><span class="sxs-lookup"><span data-stu-id="ea40c-175">Num-executors is bounded by the cluster resources.</span></span>    

## <a name="example-calculation"></a><span data-ttu-id="ea40c-176">範例計算</span><span class="sxs-lookup"><span data-stu-id="ea40c-176">Example Calculation</span></span>

<span data-ttu-id="ea40c-177">假設您目前有由 8 個 D4v2 節點所組成的叢集，其中執行了 2 個應用程式 (包括您要執行的應用程式在內)。</span><span class="sxs-lookup"><span data-stu-id="ea40c-177">Let’s say you currently have a cluster composed of 8 D4v2 nodes that is running 2 apps including the one you are going to run.</span></span>  

<span data-ttu-id="ea40c-178">**步驟 1︰確定叢集上所執行的應用程式數目** – 您知道您的叢集上有 2 個應用程式 (包括您要執行的應用程式在內)。</span><span class="sxs-lookup"><span data-stu-id="ea40c-178">**Step 1: Determine how many apps are running on your cluster** – you know that you have 2 apps on your cluster, including the one you are going to run.</span></span>  

<span data-ttu-id="ea40c-179">**步驟 2︰設定 executor-memory** – 在此範例中，我們判斷 6 GB 的 executor-memory 就足夠 I/O 密集作業使用。</span><span class="sxs-lookup"><span data-stu-id="ea40c-179">**Step 2: Set executor-memory** – for this example, we determine that 6GB of executor-memory will be sufficient for I/O intensive job.</span></span>  

    executor-memory = 6GB
<span data-ttu-id="ea40c-180">**步驟 3︰設定 executor-cores** – 這是 I/O 密集作業，因此我們可以將每個執行程式的核心數目設為 4。</span><span class="sxs-lookup"><span data-stu-id="ea40c-180">**Step 3: Set executor-cores** – Since this is an I/O intensive job, we can set the number of cores for each executor to 4.</span></span>  <span data-ttu-id="ea40c-181">將每個執行程式的核心設為大於 4，可能會造成記憶體回收問題。</span><span class="sxs-lookup"><span data-stu-id="ea40c-181">Setting cores per executor to larger than 4 may cause garbage collection problems.</span></span>  

    executor-cores = 4
<span data-ttu-id="ea40c-182">**步驟 4︰決定叢集中的 YARN 記憶體數量** – 我們瀏覽至 Ambari，發現每個 D4v2 有 25 GB 的 YARN 記憶體。</span><span class="sxs-lookup"><span data-stu-id="ea40c-182">**Step 4: Determine amount of YARN memory in cluster** – We navigate to Ambari to find out that each D4v2 has 25GB of YARN memory.</span></span>  <span data-ttu-id="ea40c-183">由於有 8 個節點，可用的 YARN 記憶體會乘以 8。</span><span class="sxs-lookup"><span data-stu-id="ea40c-183">Since there are 8 nodes, the available YARN memory is multiplied by 8.</span></span>

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
<span data-ttu-id="ea40c-184">**步驟 5︰計算 num-executors** – num-executors 參數是由記憶體限制和 CPU 限制較小者除以 Spark 上執行的應用程式數目來決定。</span><span class="sxs-lookup"><span data-stu-id="ea40c-184">**Step 5: Calculate num-executors** – The num-executors parameter is determined by taking the minimum of the memory constraint and the CPU constraint divided by the # of apps running on Spark.</span></span>    

<span data-ttu-id="ea40c-185">**計算記憶體限制** – 記憶體限制的計算方式為 YARN 記憶體總數除以每個執行程式的記憶體。</span><span class="sxs-lookup"><span data-stu-id="ea40c-185">**Calculate memory constraint** – The memory constraint is calculated as the total YARN memory divided by the memory per executor.</span></span>

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
<span data-ttu-id="ea40c-186">**計算 CPU 限制**-CPU 限制的計算方式為 YARN 核心總數除以每個執行程式的核心數目。</span><span class="sxs-lookup"><span data-stu-id="ea40c-186">**Calculate CPU constraint** - The CPU constraint is calculated as the total yarn cores divided by the number of cores per executor.</span></span>
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
<span data-ttu-id="ea40c-187">**設定 num-executors**</span><span class="sxs-lookup"><span data-stu-id="ea40c-187">**Set num-executors**</span></span>

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

