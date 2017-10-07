---
title: "資料湖存放區 Spark 效能調整指導方針 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: da1d172e9cb1199ad95605ea1718e78559f79650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-spark-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="8138e-103">HDInsight 和 Azure Data Lake Store 上的 Spark 效能微調方針</span><span class="sxs-lookup"><span data-stu-id="8138e-103">Performance tuning guidance for Spark on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="8138e-104">當微調效能上的 Spark，您需要將您的叢集執行的應用程式的 tooconsider hello 數。</span><span class="sxs-lookup"><span data-stu-id="8138e-104">When tuning performance on Spark, you need tooconsider hello number of apps that will be running on your cluster.</span></span>  <span data-ttu-id="8138e-105">根據預設，您可以執行 4 應用程式同時 HDI 叢集上的 (附註： hello 預設設定是主體 toochange)。</span><span class="sxs-lookup"><span data-stu-id="8138e-105">By default, you can run 4 apps concurrently on your HDI cluster (Note: hello default setting is subject toochange).</span></span>  <span data-ttu-id="8138e-106">您可能會決定 toouse 較少的應用程式讓您可以覆寫 hello 預設設定，並針對這些應用程式使用多個 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="8138e-106">You may decide toouse fewer apps so you can override hello default settings and use more of hello cluster for those apps.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="8138e-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="8138e-107">Prerequisites</span></span>

* <span data-ttu-id="8138e-108">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8138e-108">**An Azure subscription**.</span></span> <span data-ttu-id="8138e-109">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="8138e-109">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="8138e-110">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="8138e-110">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="8138e-111">如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="8138e-111">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="8138e-112">**Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="8138e-112">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="8138e-113">請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8138e-113">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="8138e-114">請確定您已啟用遠端桌面 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="8138e-114">Make sure you enable Remote Desktop for hello cluster.</span></span>
* <span data-ttu-id="8138e-115">**在 Azure Data Lake Store 上執行 Spark 叢集**。</span><span class="sxs-lookup"><span data-stu-id="8138e-115">**Running Spark cluster on Azure Data Lake Store**.</span></span>  <span data-ttu-id="8138e-116">如需詳細資訊，請參閱[資料湖存放區中的使用 HDInsight Spark 叢集 tooanalyze 資料](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)</span><span class="sxs-lookup"><span data-stu-id="8138e-116">For more information, see [Use HDInsight Spark cluster tooanalyze data in Data Lake Store](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-apache-spark-use-with-data-lake-store)</span></span>
* <span data-ttu-id="8138e-117">**ADLS 的效能微調指導方針**。</span><span class="sxs-lookup"><span data-stu-id="8138e-117">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="8138e-118">如需一般的效能概念，請參閱 [Data Lake Store 效能微調指導方針](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span><span class="sxs-lookup"><span data-stu-id="8138e-118">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span> 

## <a name="parameters"></a><span data-ttu-id="8138e-119">參數</span><span class="sxs-lookup"><span data-stu-id="8138e-119">Parameters</span></span>

<span data-ttu-id="8138e-120">當執行作業的 Spark，如下 hello 最重要的設定可微調的 tooincrease ADLS 效能：</span><span class="sxs-lookup"><span data-stu-id="8138e-120">When running Spark jobs, here are hello most important settings that can be tuned tooincrease performance on ADLS:</span></span>

* <span data-ttu-id="8138e-121">**Num 執行程式**-hello 的可執行的並行工作數。</span><span class="sxs-lookup"><span data-stu-id="8138e-121">**Num-executors** - hello number of concurrent tasks that can be executed.</span></span>

* <span data-ttu-id="8138e-122">**執行程式記憶體**-hello 配置的記憶體數量 tooeach 執行程式。</span><span class="sxs-lookup"><span data-stu-id="8138e-122">**Executor-memory** - hello amount of memory allocated tooeach executor.</span></span>

* <span data-ttu-id="8138e-123">**執行程式核心**-hello 核心數目配置 tooeach 執行程式。</span><span class="sxs-lookup"><span data-stu-id="8138e-123">**Executor-cores** - hello number of cores allocated tooeach executor.</span></span>                     

<span data-ttu-id="8138e-124">**Num 執行程式**Num 執行程式將會設定 hello 可以平行執行的工作數目上限。</span><span class="sxs-lookup"><span data-stu-id="8138e-124">**Num-executors** Num-executors will set hello maximum number of tasks that can run in parallel.</span></span>  <span data-ttu-id="8138e-125">hello 實際可以平行執行的工作數目會受限於 hello 記憶體和 CPU 資源在叢集中可用。</span><span class="sxs-lookup"><span data-stu-id="8138e-125">hello actual number of tasks that can run in parallel is bounded by hello memory and CPU resources available in your cluster.</span></span>

<span data-ttu-id="8138e-126">**執行程式記憶體**這是 hello tooeach 執行程式所配置的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="8138e-126">**Executor-memory** This is hello amount of memory that is being allocated tooeach executor.</span></span>  <span data-ttu-id="8138e-127">每一個執行程式所需的 hello 記憶體會視 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="8138e-127">hello memory needed for each executor is dependent on hello job.</span></span>  <span data-ttu-id="8138e-128">Hello 記憶體複雜的作業，需要 toobe 更高版本。</span><span class="sxs-lookup"><span data-stu-id="8138e-128">For complex operations, hello memory needs toobe higher.</span></span>  <span data-ttu-id="8138e-129">讀取和寫入等簡單作業的記憶體需求會較低。</span><span class="sxs-lookup"><span data-stu-id="8138e-129">For simple operations like read and write, memory requirements will be lower.</span></span>  <span data-ttu-id="8138e-130">Ambari 中，您可以檢視 hello 每一個執行程式的記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="8138e-130">hello amount of memory for each executor can be viewed in Ambari.</span></span>  <span data-ttu-id="8138e-131">在 Ambari 瀏覽 tooSpark 並檢視 hello 組態 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="8138e-131">In Ambari, navigate tooSpark and view hello Configs tab.</span></span>  

<span data-ttu-id="8138e-132">**執行程式核心**這會設定每個執行程式，會決定 hello 數目每執行者可以執行的平行執行緒使用的核心的 hello 數量。</span><span class="sxs-lookup"><span data-stu-id="8138e-132">**Executor-cores** This sets hello amount of cores used per executor, which determines hello number of parallel threads that can be run per executor.</span></span>  <span data-ttu-id="8138e-133">例如，如果執行者核心 = 2，則每一個執行程式可以在 hello 執行者執行 2 的平行工作。</span><span class="sxs-lookup"><span data-stu-id="8138e-133">For example, if executor-cores = 2, then each executor can run 2 parallel tasks in hello executor.</span></span>  <span data-ttu-id="8138e-134">hello executor 核心需要將會相依於 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="8138e-134">hello executor-cores needed will be dependent on hello job.</span></span>  <span data-ttu-id="8138e-135">需要大量 I/O 的作業所需的每一工作記憶體並不需要太多，因此每個執行程式可以處理更多的平行工作。</span><span class="sxs-lookup"><span data-stu-id="8138e-135">I/O heavy jobs do not require a large amount of memory per task so each executor can handle more parallel tasks.</span></span>

<span data-ttu-id="8138e-136">依預設，在 HDInsight 上執行 Spark 時，會為每個實體核心定義兩個虛擬 YARN 核心。</span><span class="sxs-lookup"><span data-stu-id="8138e-136">By default, two virtual YARN cores are defined for each physical core when running Spark on HDInsight.</span></span>  <span data-ttu-id="8138e-137">這個數量能在並行能力與從多個執行緒切換而來的內容數量取得良好平衡。</span><span class="sxs-lookup"><span data-stu-id="8138e-137">This number provides a good balance of concurrecy and amount of context switching from multiple threads.</span></span>  

## <a name="guidance"></a><span data-ttu-id="8138e-138">指引</span><span class="sxs-lookup"><span data-stu-id="8138e-138">Guidance</span></span>

<span data-ttu-id="8138e-139">在執行分析工作負載 toowork Spark 資料湖存放區中的資料，我們建議您搭配資料湖存放區使用 hello 最近 HDInsight 版本 tooget hello 達到最佳效能。</span><span class="sxs-lookup"><span data-stu-id="8138e-139">While running Spark analytic workloads toowork with data in Data Lake Store, we recommend that you use hello most recent HDInsight version tooget hello best performance with Data Lake Store.</span></span> <span data-ttu-id="8138e-140">當您的工作是多個密集的磁碟 I/O 時，某些參數可以是設定的 tooimprove 效能。</span><span class="sxs-lookup"><span data-stu-id="8138e-140">When your job is more I/O intensive, then certain parameters can be configured tooimprove performance.</span></span>  <span data-ttu-id="8138e-141">Azure Data Lake Store 是具有高擴充性的儲存體平台，可處理高輸送量。</span><span class="sxs-lookup"><span data-stu-id="8138e-141">Azure Data Lake Store is a highly scalable storage platform that can handle high throughput.</span></span>  <span data-ttu-id="8138e-142">如果 hello 作業主要是由讀取或寫入所組成，再增加並行存取從 Azure 資料湖存放區的 I/O tooand 無法提高效能。</span><span class="sxs-lookup"><span data-stu-id="8138e-142">If hello job mainly consists of read or writes, then increasing concurrency for I/O tooand from Azure Data Lake Store could increase performance.</span></span>

<span data-ttu-id="8138e-143">有幾個 I/O 密集的工作的一般方式 tooincrease 並行存取。</span><span class="sxs-lookup"><span data-stu-id="8138e-143">There are a few general ways tooincrease concurrency for I/O intensive jobs.</span></span>

<span data-ttu-id="8138e-144">**步驟 1： 決定多少應用程式正在執行您的叢集上**– 您應該知道多少應用程式正在執行包括 hello 目前 hello 叢集上。</span><span class="sxs-lookup"><span data-stu-id="8138e-144">**Step 1: Determine how many apps are running on your cluster** – You should know how many apps are running on hello cluster including hello current one.</span></span>  <span data-ttu-id="8138e-145">設定會假設每個 Spark 的 hello 預設值，有 4 同時執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8138e-145">hello default values for each Spark setting assumes that there are 4 apps running concurrently.</span></span>  <span data-ttu-id="8138e-146">因此，您將只有 25%的 hello 叢集中每個應用程式。</span><span class="sxs-lookup"><span data-stu-id="8138e-146">Therefore, you will only have 25% of hello cluster available for each app.</span></span>  <span data-ttu-id="8138e-147">tooget 更佳的效能，您可以覆寫 hello 預設值變更 hello 執行程式的數目。</span><span class="sxs-lookup"><span data-stu-id="8138e-147">tooget better performance, you can override hello defaults by changing hello number of executors.</span></span>  

<span data-ttu-id="8138e-148">**步驟 2： 設定執行程式記憶體**– hello tooset 首先是 hello executor 記憶體。</span><span class="sxs-lookup"><span data-stu-id="8138e-148">**Step 2: Set executor-memory** – hello first thing tooset is hello executor-memory.</span></span>  <span data-ttu-id="8138e-149">hello 記憶體將會相依於您是將 toorun hello 作業。</span><span class="sxs-lookup"><span data-stu-id="8138e-149">hello memory will be dependent on hello job that you are going toorun.</span></span>  <span data-ttu-id="8138e-150">您可以為每個執行程式配置較少的記憶體，以增加並行數量。</span><span class="sxs-lookup"><span data-stu-id="8138e-150">You can increase concurrency by allocating less memory per executor.</span></span>  <span data-ttu-id="8138e-151">如果您看見記憶體不足例外狀況時執行您的工作，您應該增加 hello 此參數的值。</span><span class="sxs-lookup"><span data-stu-id="8138e-151">If you see out of memory exceptions when you run your job, then you should increase hello value for this parameter.</span></span>  <span data-ttu-id="8138e-152">一個替代方法是 tooget 更多的記憶體使用具有較高的記憶體數量的叢集或叢集的 hello 大小增加。</span><span class="sxs-lookup"><span data-stu-id="8138e-152">One alternative is tooget more memory by using a cluster that has higher amounts of memory or increasing hello size of your cluster.</span></span>  <span data-ttu-id="8138e-153">更多的記憶體可讓多個執行程式 toobe 使用，這表示多個並行存取。</span><span class="sxs-lookup"><span data-stu-id="8138e-153">More memory will enable more executors toobe used, which means more concurrency.</span></span>

<span data-ttu-id="8138e-154">**步驟 3： 設定執行程式核心**– I/O 密集型工作負載沒有複雜的作業，對於良好 toostart 有大量的執行程式核心 tooincrease hello 每次執行程式的平行工作數。</span><span class="sxs-lookup"><span data-stu-id="8138e-154">**Step 3: Set executor-cores** – For I/O intensive workloads that do not have complex operations, it’s good toostart with a high number of executor-cores tooincrease hello number of parallel tasks per executor.</span></span>  <span data-ttu-id="8138e-155">設定執行程式核心 too4 是不錯的起點。</span><span class="sxs-lookup"><span data-stu-id="8138e-155">Setting executor-cores too4 is a good start.</span></span>   

    executor-cores = 4
<span data-ttu-id="8138e-156">增加執行程式核心的 hello 數目可讓您更多的平行處理原則讓您試驗不同的執行程式核心。</span><span class="sxs-lookup"><span data-stu-id="8138e-156">Increasing hello number of executor-cores will give you more parallelism so you can experiment with different executor-cores.</span></span>  <span data-ttu-id="8138e-157">對於有更複雜的作業的工作，您應該降低 hello 執行程式對每個核心的數目。</span><span class="sxs-lookup"><span data-stu-id="8138e-157">For jobs that have more complex operations, you should reduce hello number of cores per executor.</span></span>  <span data-ttu-id="8138e-158">如果 executor-cores 設定為高於 4，則記憶體回收可能會變得沒有效率而降低效能。</span><span class="sxs-lookup"><span data-stu-id="8138e-158">If executor-cores is set higher than 4, then garbage collection may become inefficient and degrade performance.</span></span>

<span data-ttu-id="8138e-159">**步驟 4︰決定叢集中的 YARN 記憶體數量** – 這項資訊可在 Ambari 中取得。</span><span class="sxs-lookup"><span data-stu-id="8138e-159">**Step 4: Determine amount of YARN memory in cluster** – This information is available in Ambari.</span></span>  <span data-ttu-id="8138e-160">瀏覽 tooYARN 並檢視 hello 組態 索引標籤。 hello YARN 記憶體會顯示此視窗中。</span><span class="sxs-lookup"><span data-stu-id="8138e-160">Navigate tooYARN and view hello Configs tab.  hello YARN memory is displayed in this window.</span></span>  
<span data-ttu-id="8138e-161">注意： 當您在 [hello] 視窗中，您也可以查看 hello 預設 YARN 容器大小。</span><span class="sxs-lookup"><span data-stu-id="8138e-161">Note: while you are in hello window, you can also see hello default YARN container size.</span></span>  <span data-ttu-id="8138e-162">hello YARN 容器大小是 hello 與記憶體每秒執行程式的參數相同。</span><span class="sxs-lookup"><span data-stu-id="8138e-162">hello YARN container size is hello same as memory per executor paramter.</span></span>

    Total YARN memory = nodes * YARN memory per node
<span data-ttu-id="8138e-163">**步驟 5︰計算 num-executors**</span><span class="sxs-lookup"><span data-stu-id="8138e-163">**Step 5: Calculate num-executors**</span></span>

<span data-ttu-id="8138e-164">**計算記憶體條件約束**-hello num 執行程式參數會限制記憶體或 CPU。</span><span class="sxs-lookup"><span data-stu-id="8138e-164">**Calculate memory constraint** - hello num-executors parameter is constrained either by memory or by CPU.</span></span>  <span data-ttu-id="8138e-165">您的應用程式可用的 YARN 記憶體的 hello 數量取決於 hello 記憶體條件約束。</span><span class="sxs-lookup"><span data-stu-id="8138e-165">hello memory constraint is determined by hello amount of available YARN memory for your application.</span></span>  <span data-ttu-id="8138e-166">您應該取得 YARN 記憶體總數，然後除以 executor-memory。</span><span class="sxs-lookup"><span data-stu-id="8138e-166">You should take total YARN memory and divide that by executor-memory.</span></span>  <span data-ttu-id="8138e-167">hello 的條件約束需要 toobe 取消採的應用程式的 hello 數讓我們除以 hello 應用程式數目。</span><span class="sxs-lookup"><span data-stu-id="8138e-167">hello constraint needs toobe de-scaled for hello number of apps so we divide by hello number of apps.</span></span>

    Memory constraint = (total YARN memory / executor memory) / # of apps   
<span data-ttu-id="8138e-168">**計算 CPU 的條件約束**-hello CPU 的條件約束會計算為 hello 除以 hello 每個執行程式的核心數目的虛擬核心總數。</span><span class="sxs-lookup"><span data-stu-id="8138e-168">**Calculate CPU constraint** - hello CPU constraint is calculated as hello total virtual cores divided by hello number of cores per executor.</span></span>  <span data-ttu-id="8138e-169">每個實體核心有 2 個虛擬核心。</span><span class="sxs-lookup"><span data-stu-id="8138e-169">There are 2 virtual cores for each physical core.</span></span>  <span data-ttu-id="8138e-170">類似 toohello 記憶體條件約束，我們有除以 hello 應用程式數目。</span><span class="sxs-lookup"><span data-stu-id="8138e-170">Similar toohello memory constraint, we have divide by hello number of apps.</span></span>

    virtual cores = (nodes in cluster * # of physical cores in node * 2)
    CPU constraint = (total virtual cores / # of cores per executor) / # of apps
<span data-ttu-id="8138e-171">**設定 num 執行程式**– hello num 執行程式的參數由採用 hello hello 記憶體條件約束和 hello CPU 的條件約束的最小值。</span><span class="sxs-lookup"><span data-stu-id="8138e-171">**Set num-executors** – hello num-executors parameter is determined by taking hello minimum of hello memory constraint and hello CPU constraint.</span></span> 

    num-executors = Min (total virtual Cores / # of cores per executor, available YARN memory / executor-memory)   
<span data-ttu-id="8138e-172">設定較高的 num-executors 數值未必能提升效能。</span><span class="sxs-lookup"><span data-stu-id="8138e-172">Setting a higher number of num-executors does not necessarily increase performance.</span></span>  <span data-ttu-id="8138e-173">您應該考慮到，新增更多執行程式會對每個額外的執行程式新增額外的負擔，而可能降低效能。</span><span class="sxs-lookup"><span data-stu-id="8138e-173">You should consider that adding more executors will add extra overhead for each additional executor, which can potentially degrade performance.</span></span>  <span data-ttu-id="8138e-174">Num 執行程式受限於 hello 叢集資源。</span><span class="sxs-lookup"><span data-stu-id="8138e-174">Num-executors is bounded by hello cluster resources.</span></span>    

## <a name="example-calculation"></a><span data-ttu-id="8138e-175">範例計算</span><span class="sxs-lookup"><span data-stu-id="8138e-175">Example Calculation</span></span>

<span data-ttu-id="8138e-176">例如，假設您目前已為應用程式包括 hello 一個要 toorun 執行 2 叢集 8 D4v2 節點所組成。</span><span class="sxs-lookup"><span data-stu-id="8138e-176">Let’s say you currently have a cluster composed of 8 D4v2 nodes that is running 2 apps including hello one you are going toorun.</span></span>  

<span data-ttu-id="8138e-177">**步驟 1： 決定多少應用程式正在執行您的叢集上**– 知道您有 2 上您的叢集，包括其中一個要 toorun hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8138e-177">**Step 1: Determine how many apps are running on your cluster** – you know that you have 2 apps on your cluster, including hello one you are going toorun.</span></span>  

<span data-ttu-id="8138e-178">**步驟 2︰設定 executor-memory** – 在此範例中，我們判斷 6 GB 的 executor-memory 就足夠 I/O 密集作業使用。</span><span class="sxs-lookup"><span data-stu-id="8138e-178">**Step 2: Set executor-memory** – for this example, we determine that 6GB of executor-memory will be sufficient for I/O intensive job.</span></span>  

    executor-memory = 6GB
<span data-ttu-id="8138e-179">**步驟 3： 設定執行程式核心**– 因為這是 I/O 密集工作，我們可以設定的每一個執行程式 too4 核心的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="8138e-179">**Step 3: Set executor-cores** – Since this is an I/O intensive job, we can set hello number of cores for each executor too4.</span></span>  <span data-ttu-id="8138e-180">大於 4 可能會導致記憶體回收集合問題，請設定每個執行者 toolarger 核心。</span><span class="sxs-lookup"><span data-stu-id="8138e-180">Setting cores per executor toolarger than 4 may cause garbage collection problems.</span></span>  

    executor-cores = 4
<span data-ttu-id="8138e-181">**步驟 4： 決定 YARN 叢集中的記憶體數量**– 我們巡覽 tooAmbari toofind 出每個 D4v2 有 25 GB 的 YARN 記憶體。</span><span class="sxs-lookup"><span data-stu-id="8138e-181">**Step 4: Determine amount of YARN memory in cluster** – We navigate tooAmbari toofind out that each D4v2 has 25GB of YARN memory.</span></span>  <span data-ttu-id="8138e-182">由於有 8 個節點，hello 可用 YARN 記憶體乘以 8。</span><span class="sxs-lookup"><span data-stu-id="8138e-182">Since there are 8 nodes, hello available YARN memory is multiplied by 8.</span></span>

    Total YARN memory = nodes * YARN memory* per node
    Total YARN memory = 8 nodes * 25GB = 200GB
<span data-ttu-id="8138e-183">**步驟 5： 計算 num 執行程式**– hello num 執行程式的參數取決於採取 hello 最少的 hello 記憶體條件約束和除以 hello hello CPU 條件約束數目上的 Spark 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="8138e-183">**Step 5: Calculate num-executors** – hello num-executors parameter is determined by taking hello minimum of hello memory constraint and hello CPU constraint divided by hello # of apps running on Spark.</span></span>    

<span data-ttu-id="8138e-184">**計算記憶體條件約束**– hello 記憶體條件約束的計算方式為 hello YARN 記憶體總數除以 hello 記憶體每秒執行程式。</span><span class="sxs-lookup"><span data-stu-id="8138e-184">**Calculate memory constraint** – hello memory constraint is calculated as hello total YARN memory divided by hello memory per executor.</span></span>

    Memory constraint = (total YARN memory / executor memory) / # of apps   
    Memory constraint = (200GB / 6GB) / 2   
    Memory constraint = 16 (rounded)
<span data-ttu-id="8138e-185">**計算 CPU 的條件約束**-hello CPU 的條件約束會計算為 hello 總 yarn 核心數目除以 hello 執行程式對每個核心的數目。</span><span class="sxs-lookup"><span data-stu-id="8138e-185">**Calculate CPU constraint** - hello CPU constraint is calculated as hello total yarn cores divided by hello number of cores per executor.</span></span>
    
    YARN cores = nodes in cluster * # of cores per node * 2   
    YARN cores = 8 nodes * 8 cores per D14 * 2 = 128
    CPU constraint = (total YARN cores / # of cores per executor) / # of apps
    CPU constraint = (128 / 4) / 2
    CPU constraint = 16
<span data-ttu-id="8138e-186">**設定 num-executors**</span><span class="sxs-lookup"><span data-stu-id="8138e-186">**Set num-executors**</span></span>

    num-executors = Min (memory constraint, CPU constraint)
    num-executors = Min (16, 16)
    num-executors = 16    

