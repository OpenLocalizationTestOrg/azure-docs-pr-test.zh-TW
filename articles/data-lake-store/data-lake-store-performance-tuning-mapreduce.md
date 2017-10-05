---
title: "Azure Data Lake Store MapReduce 效能微調方針 | Microsoft Docs"
description: "Azure Data Lake Store MapReduce 效能微調方針"
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
ms.openlocfilehash: 9528148792f083cb0e48d356e61cf61762ee954f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="88a75-103">HDInsight 和 Azure Data Lake Store 上的 MapReduce 效能微調方針</span><span class="sxs-lookup"><span data-stu-id="88a75-103">Performance tuning guidance for MapReduce on HDInsight and Azure Data Lake Store</span></span>


## <a name="prerequisites"></a><span data-ttu-id="88a75-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="88a75-104">Prerequisites</span></span>

* <span data-ttu-id="88a75-105">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="88a75-105">**An Azure subscription**.</span></span> <span data-ttu-id="88a75-106">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="88a75-106">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="88a75-107">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="88a75-107">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="88a75-108">如需有關如何建立帳戶的詳細指示，請參閱 [開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="88a75-108">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="88a75-109">**Azure HDInsight 叢集** 。</span><span class="sxs-lookup"><span data-stu-id="88a75-109">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="88a75-110">請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="88a75-110">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="88a75-111">請確實為叢集啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="88a75-111">Make sure you enable Remote Desktop for the cluster.</span></span>
* <span data-ttu-id="88a75-112">**在 HDInsight 上使用 MapReduce**。</span><span class="sxs-lookup"><span data-stu-id="88a75-112">**Using MapReduce on HDInsight**.</span></span>  <span data-ttu-id="88a75-113">如需詳細資訊，請參閱[在 HDInsight 上的 Hadoop 中使用 MapReduce](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)</span><span class="sxs-lookup"><span data-stu-id="88a75-113">For more information, see [Use MapReduce in Hadoop on HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)</span></span>  
* <span data-ttu-id="88a75-114">**ADLS 的效能微調指導方針**。</span><span class="sxs-lookup"><span data-stu-id="88a75-114">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="88a75-115">如需一般的效能概念，請參閱 [Data Lake Store 效能微調指導方針](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span><span class="sxs-lookup"><span data-stu-id="88a75-115">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>  

## <a name="parameters"></a><span data-ttu-id="88a75-116">參數</span><span class="sxs-lookup"><span data-stu-id="88a75-116">Parameters</span></span>

<span data-ttu-id="88a75-117">在執行 MapReduce 作業時，以下是可供您設定以在 ADLS 上增加效能的最重要參數︰</span><span class="sxs-lookup"><span data-stu-id="88a75-117">When running MapReduce jobs, here are the most important parameters that you can configure to increase performance on ADLS:</span></span>

* <span data-ttu-id="88a75-118">**Mapreduce.map.memory.mb** – 要配置給每個對應器的記憶體數量</span><span class="sxs-lookup"><span data-stu-id="88a75-118">**Mapreduce.map.memory.mb** – The amount of memory to allocate to each mapper</span></span>
* <span data-ttu-id="88a75-119">**Mapreduce.job.maps** – 每個作業的對應工作數目</span><span class="sxs-lookup"><span data-stu-id="88a75-119">**Mapreduce.job.maps** – The number of map tasks per job</span></span>
* <span data-ttu-id="88a75-120">**Mapreduce.reduce.memory.mb** – 要配置給每個歸納器的記憶體數量</span><span class="sxs-lookup"><span data-stu-id="88a75-120">**Mapreduce.reduce.memory.mb** – The amount of memory to allocate to each reducer</span></span>
* <span data-ttu-id="88a75-121">**Mapreduce.job.reduces** – 每個作業的縮減工作數目</span><span class="sxs-lookup"><span data-stu-id="88a75-121">**Mapreduce.job.reduces** – The number of reduce tasks per job</span></span>

<span data-ttu-id="88a75-122">**Mapreduce.map.memory / Mapreduce.reduce.memory** 這個數字應根據對應和/或縮減工作需要多少記憶體來進行調整。</span><span class="sxs-lookup"><span data-stu-id="88a75-122">**Mapreduce.map.memory / Mapreduce.reduce.memory** This number should be adjusted based on how much memory is needed for the map and/or reduce task.</span></span>  <span data-ttu-id="88a75-123">mapreduce.map.memory 和 mapreduce.reduce.memory 的預設值可以在 Ambari 中透過 Yarn 組態來檢視。</span><span class="sxs-lookup"><span data-stu-id="88a75-123">The default values of mapreduce.map.memory and mapreduce.reduce.memory can be viewed in Ambari via the Yarn configuration.</span></span>  <span data-ttu-id="88a75-124">在 Ambari 中，瀏覽至 YARN，然後檢視 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="88a75-124">In Ambari, navigate to YARN and view the Configs tab.</span></span>  <span data-ttu-id="88a75-125">YARN 記憶體將會顯示。</span><span class="sxs-lookup"><span data-stu-id="88a75-125">The YARN memory will be displayed.</span></span>  

<span data-ttu-id="88a75-126">**Mapreduce.job.maps / Mapreduce.job.reduces** 這會決定要建立的對應器或歸納器數目上限。</span><span class="sxs-lookup"><span data-stu-id="88a75-126">**Mapreduce.job.maps / Mapreduce.job.reduces** This will determine the maximum number of mappers or reducers to be created.</span></span>  <span data-ttu-id="88a75-127">分割數會決定要為 MapReduce 作業建立多少對應器。</span><span class="sxs-lookup"><span data-stu-id="88a75-127">The number of splits will determine how many mappers will be created for the MapReduce job.</span></span>  <span data-ttu-id="88a75-128">因此，如果分割數比要求的對應器數目少，您所得到的對應器可能會比您要求的少。</span><span class="sxs-lookup"><span data-stu-id="88a75-128">Therefore, you may get less mappers than you requested if there are less splits than the number of mappers requested.</span></span>       

## <a name="guidance"></a><span data-ttu-id="88a75-129">指引</span><span class="sxs-lookup"><span data-stu-id="88a75-129">Guidance</span></span>

<span data-ttu-id="88a75-130">**步驟 1︰決定執行的作業數目** - 根據預設，MapReduce 會為您的作業使用整個叢集。</span><span class="sxs-lookup"><span data-stu-id="88a75-130">**Step 1: Determine number of jobs running** - By default, MapReduce will use the entire cluster for your job.</span></span>  <span data-ttu-id="88a75-131">您可以使用比可用容器還少的對應器，來使用較少的叢集。</span><span class="sxs-lookup"><span data-stu-id="88a75-131">You can use less of the cluster by using less mappers than there are available containers.</span></span>  <span data-ttu-id="88a75-132">本文中的指導方針假設您的應用程式是叢集上唯一執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="88a75-132">The guidance in this document assumes that your application is the only application running on your cluster.</span></span>      

<span data-ttu-id="88a75-133">**步驟 2︰設定 mapreduce.map.memory/mapreduce.reduce.memory** – 對應和縮減工作的記憶體大小會取決於您的特定作業。</span><span class="sxs-lookup"><span data-stu-id="88a75-133">**Step 2: Set mapreduce.map.memory/mapreduce.reduce.memory** –  The size of the memory for map and reduce tasks will be dependent on your specific job.</span></span>  <span data-ttu-id="88a75-134">如果您想要增加並行能力，您可以減少記憶體大小。</span><span class="sxs-lookup"><span data-stu-id="88a75-134">You can reduce the memory size if you want to increase concurrency.</span></span>  <span data-ttu-id="88a75-135">並行執行工作的數目取決於容器數目。</span><span class="sxs-lookup"><span data-stu-id="88a75-135">The number of concurrently running tasks depends on the number of containers.</span></span>  <span data-ttu-id="88a75-136">藉由降低每個對應器或歸納器的記憶體數量，即可建立更多容器，而讓更多的對應器或歸納器並行執行。</span><span class="sxs-lookup"><span data-stu-id="88a75-136">By decreasing the amount of memory per mapper or reducer, more containers can be created, which enable more mappers or reducers to run concurrently.</span></span>  <span data-ttu-id="88a75-137">減少太多的記憶體數量可能會導致某些處理程序耗盡記憶體。</span><span class="sxs-lookup"><span data-stu-id="88a75-137">Decreasing the amount of memory too much may cause some processes to run out of memory.</span></span>  <span data-ttu-id="88a75-138">如果您在執行作業時遇到堆積錯誤，您應該增加每個對應器或歸納器的記憶體。</span><span class="sxs-lookup"><span data-stu-id="88a75-138">If you get a heap error when running your job, you should increase the memory per mapper or reducer.</span></span>  <span data-ttu-id="88a75-139">您應該考慮到，新增更多容器會對每個額外的容器新增額外的負擔，而可能降低效能。</span><span class="sxs-lookup"><span data-stu-id="88a75-139">You should consider that adding more containers will add extra overhead for each additional container, which can potentially degrade performance.</span></span>  <span data-ttu-id="88a75-140">另一個方式是使用擁有較高數量記憶體的叢集，或增加叢集中的節點數目，以獲得更多的記憶體。</span><span class="sxs-lookup"><span data-stu-id="88a75-140">Another alternative is to get more memory by using a cluster that has higher amounts of memory or increasing the number of nodes in your cluster.</span></span>  <span data-ttu-id="88a75-141">更多的記憶體就能使用更多的容器，亦即會有更多並行能力。</span><span class="sxs-lookup"><span data-stu-id="88a75-141">More memory will enable more containers to be used, which means more concurrency.</span></span>  

<span data-ttu-id="88a75-142">**步驟 3︰決定 YARN 記憶體總數** - 若要調整 mapreduce.job.maps/mapreduce.job.reduces，您應該考慮可供使用的 YARN 記憶體總數。</span><span class="sxs-lookup"><span data-stu-id="88a75-142">**Step 3: Determine Total YARN memory** - To tune mapreduce.job.maps/mapreduce.job.reduces, you should consider the amount of total YARN memory available for use.</span></span>  <span data-ttu-id="88a75-143">這項資訊可在 Ambari 中取得。</span><span class="sxs-lookup"><span data-stu-id="88a75-143">This information is available in Ambari.</span></span>  <span data-ttu-id="88a75-144">瀏覽至 YARN，然後檢視 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="88a75-144">Navigate to YARN and view the Configs tab.</span></span>  <span data-ttu-id="88a75-145">YARN 記憶體會顯示在此視窗中。</span><span class="sxs-lookup"><span data-stu-id="88a75-145">The YARN memory is displayed in this window.</span></span>  <span data-ttu-id="88a75-146">您應該將 YARN 記憶體乘上叢集中的節點數目，以算出 YARN 記憶體總數。</span><span class="sxs-lookup"><span data-stu-id="88a75-146">You should multiply the YARN memory with the number of nodes in your cluster to get the total YARN memory.</span></span>

    Total YARN memory = nodes * YARN memory per node
<span data-ttu-id="88a75-147">如果您使用空白叢集，則記憶體會是叢集的 YARN 記憶體總數。</span><span class="sxs-lookup"><span data-stu-id="88a75-147">If you are using an empty cluster, then memory can be the total YARN memory for your cluster.</span></span>  <span data-ttu-id="88a75-148">如果有其他應用程式使用記憶體，則您可以選擇僅使用部分的叢集記憶體，方法是將對應器或歸納器的數量減少為您想要使用的容器數量。</span><span class="sxs-lookup"><span data-stu-id="88a75-148">If other applications are using memory, then you can choose to only use a portion of your cluster’s memory by reducing the number of mappers or reducers to the number of containers you want to use.</span></span>  

<span data-ttu-id="88a75-149">**步驟 4︰計算 YARN 容器的數量** – YARN 容器會決定作業可用的並行數量。</span><span class="sxs-lookup"><span data-stu-id="88a75-149">**Step 4: Calculate number of YARN containers** – YARN containers dictate the amount of concurrency available for the job.</span></span>  <span data-ttu-id="88a75-150">取得 YARN 記憶體總數，然後除以 mapreduce.map.memory。</span><span class="sxs-lookup"><span data-stu-id="88a75-150">Take total YARN memory and divide that by mapreduce.map.memory.</span></span>  

    # of YARN containers = total YARN memory / mapreduce.map.memory

<span data-ttu-id="88a75-151">**步驟 5：設定 mapreduce.job.maps/mapreduce.job.reduces** 將 mapreduce.job.maps/mapreduce.job.reduces 設定為至少是可用容器的數目。</span><span class="sxs-lookup"><span data-stu-id="88a75-151">**Step 5: Set mapreduce.job.maps/mapreduce.job.reduces** Set mapreduce.job.maps/mapreduce.job.reduces to at least the number of available containers.</span></span>  <span data-ttu-id="88a75-152">您可以進一步試驗，將對應器和歸納器的數目增加，看看是否能獲得更好的效能。</span><span class="sxs-lookup"><span data-stu-id="88a75-152">You can experiment further by increasing the number of mappers and reducers to see if you get better performance.</span></span>  <span data-ttu-id="88a75-153">請記住，更多的對應器會產生額外的負擔，因此對應器過多可能會降低效能。</span><span class="sxs-lookup"><span data-stu-id="88a75-153">Keep in mind that more mappers will have additional overhead so having too many mappers may degrade performance.</span></span>  

<span data-ttu-id="88a75-154">CPU 排程和 CPU 隔離預設會關閉，因此 YARN 容器的數目會受記憶體所限制。</span><span class="sxs-lookup"><span data-stu-id="88a75-154">CPU scheduling and CPU isolation are turned off by default so the number of YARN containers is constrained by memory.</span></span>

## <a name="example-calculation"></a><span data-ttu-id="88a75-155">範例計算</span><span class="sxs-lookup"><span data-stu-id="88a75-155">Example Calculation</span></span>

<span data-ttu-id="88a75-156">設想您目前有由 8 個 D14 節點所組成的叢集，而且您想要執行 I/O 密集作業。</span><span class="sxs-lookup"><span data-stu-id="88a75-156">Let’s say you currently have a cluster composed of 8 D14 nodes and you want to run an I/O intensive job.</span></span>  <span data-ttu-id="88a75-157">以下是您應該進行的計算︰</span><span class="sxs-lookup"><span data-stu-id="88a75-157">Here are the calculations you should do:</span></span>

<span data-ttu-id="88a75-158">**步驟 1︰決定所執行作業的數目** - 在我們的範例中，我們假設我們的作業是唯一在執行的作業。</span><span class="sxs-lookup"><span data-stu-id="88a75-158">**Step 1: Determine number of jobs running** - for our example, we assume that our job is the only one running.</span></span>  

<span data-ttu-id="88a75-159">**步驟 2︰設定 mapreduce.map.memory/mapreduce.reduce.memory** – 在我們的範例中，您將會執行 I/O 密集作業，並決定 3 GB 的記憶體已足夠對應工作使用。</span><span class="sxs-lookup"><span data-stu-id="88a75-159">**Step 2: Set mapreduce.map.memory/mapreduce.reduce.memory** – for our example, you are running an I/O intensive job and decide that 3GB of memory for map tasks will be sufficient.</span></span>

    mapreduce.map.memory = 3GB
<span data-ttu-id="88a75-160">**步驟 3︰確定 YARN 記憶體總數**</span><span class="sxs-lookup"><span data-stu-id="88a75-160">**Step 3: Determine Total YARN memory**</span></span>

    total memory from the cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
<span data-ttu-id="88a75-161">**步驟 4︰計算 YARN 容器的數目**</span><span class="sxs-lookup"><span data-stu-id="88a75-161">**Step 4: Calculate # of YARN containers**</span></span>

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

<span data-ttu-id="88a75-162">**步驟 5：設定 mapreduce.job.maps/mapreduce.job.reduces**</span><span class="sxs-lookup"><span data-stu-id="88a75-162">**Step 5: Set mapreduce.job.maps/mapreduce.job.reduces**</span></span>

    mapreduce.map.jobs = 256

## <a name="limitations"></a><span data-ttu-id="88a75-163">限制</span><span class="sxs-lookup"><span data-stu-id="88a75-163">Limitations</span></span>

<span data-ttu-id="88a75-164">**ADLS 節流**</span><span class="sxs-lookup"><span data-stu-id="88a75-164">**ADLS throttling**</span></span>

<span data-ttu-id="88a75-165">ADLS 是多租用戶服務，因此會設定帳戶層級的頻寬限制。</span><span class="sxs-lookup"><span data-stu-id="88a75-165">As a multi-tenant service, ADLS sets account level bandwidth limits.</span></span>  <span data-ttu-id="88a75-166">如果您達到這些限制，您將會開始看到工作失敗。</span><span class="sxs-lookup"><span data-stu-id="88a75-166">If you hit these limits, you will start to see task failures.</span></span> <span data-ttu-id="88a75-167">透過觀察工作記錄檔中的節流錯誤即可加以識別。</span><span class="sxs-lookup"><span data-stu-id="88a75-167">This can be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="88a75-168">如果您的作業需要更多頻寬，請與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="88a75-168">If you need more bandwidth for your job, please contact us.</span></span>   

<span data-ttu-id="88a75-169">若要檢查您是否遭到節流，您必須在用戶端啟用偵錯記錄。</span><span class="sxs-lookup"><span data-stu-id="88a75-169">To check if you are getting throttled, you need to enable the debug logging on the client side.</span></span> <span data-ttu-id="88a75-170">做法如下：</span><span class="sxs-lookup"><span data-stu-id="88a75-170">Here’s how you can do that:</span></span>

1. <span data-ttu-id="88a75-171">將下列屬性放在 [Ambari] > [YARN] > [設定] > [進階 yarn-log4j] 的 log4j 屬性中：log4j.logger.com.microsoft.azure.datalake.store=DEBUG</span><span class="sxs-lookup"><span data-stu-id="88a75-171">Put the following property in the log4j properties in Ambari > YARN > Config > Advanced yarn-log4j: log4j.logger.com.microsoft.azure.datalake.store=DEBUG</span></span>

2. <span data-ttu-id="88a75-172">重新啟動所有節點/服務，以便讓設定生效。</span><span class="sxs-lookup"><span data-stu-id="88a75-172">Restart all the nodes/service for the config to take effect.</span></span>

3. <span data-ttu-id="88a75-173">如果您遭到節流，您會看到 YARN 記錄檔中有 HTTP 429 錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="88a75-173">If you are getting throttled, you’ll see the HTTP 429 error code in the YARN log file.</span></span> <span data-ttu-id="88a75-174">YARN 記錄檔位於 /tmp/&lt;user&gt;/yarn.log 中</span><span class="sxs-lookup"><span data-stu-id="88a75-174">The YARN log file is in /tmp/&lt;user&gt;/yarn.log</span></span>

## <a name="examples-to-run"></a><span data-ttu-id="88a75-175">要執行的範例</span><span class="sxs-lookup"><span data-stu-id="88a75-175">Examples to Run</span></span>

<span data-ttu-id="88a75-176">為了示範 MapReduce 在 Azure Data Lake Store 中的執行方式，以下提供了一些使用下列設定在叢集上執行的範例程式碼︰</span><span class="sxs-lookup"><span data-stu-id="88a75-176">To demonstrate how MapReduce runs on Azure Data Lake Store, below is some sample code that was run on a cluster with the following settings:</span></span>

* <span data-ttu-id="88a75-177">16 節點 D14v2</span><span class="sxs-lookup"><span data-stu-id="88a75-177">16 node D14v2</span></span>
* <span data-ttu-id="88a75-178">執行 HDI 3.6 的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="88a75-178">Hadoop cluster running HDI 3.6</span></span>

<span data-ttu-id="88a75-179">以下是一些用來執行 MapReduce Teragen、Terasort 和 Teravalidate 的範例命令，您可以從這邊來著手。</span><span class="sxs-lookup"><span data-stu-id="88a75-179">For a starting point, here are some example commands to run MapReduce Teragen, Terasort, and Teravalidate.</span></span>  <span data-ttu-id="88a75-180">您可以根據您的資源調整這些命令。</span><span class="sxs-lookup"><span data-stu-id="88a75-180">You can adjust these commands based on your resources.</span></span>

<span data-ttu-id="88a75-181">**Teragen**</span><span class="sxs-lookup"><span data-stu-id="88a75-181">**Teragen**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

<span data-ttu-id="88a75-182">**Terasort**</span><span class="sxs-lookup"><span data-stu-id="88a75-182">**Terasort**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

<span data-ttu-id="88a75-183">**Teravalidate**</span><span class="sxs-lookup"><span data-stu-id="88a75-183">**Teravalidate**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
