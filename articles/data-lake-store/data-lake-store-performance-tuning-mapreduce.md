---
title: "資料湖存放區 MapReduce 效能調整指導方針 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: e21414a23530e65613c85156af0209c88ec54d2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-mapreduce-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="3ebf5-103">HDInsight 和 Azure Data Lake Store 上的 MapReduce 效能微調方針</span><span class="sxs-lookup"><span data-stu-id="3ebf5-103">Performance tuning guidance for MapReduce on HDInsight and Azure Data Lake Store</span></span>


## <a name="prerequisites"></a><span data-ttu-id="3ebf5-104">必要條件</span><span class="sxs-lookup"><span data-stu-id="3ebf5-104">Prerequisites</span></span>

* <span data-ttu-id="3ebf5-105">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-105">**An Azure subscription**.</span></span> <span data-ttu-id="3ebf5-106">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-106">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3ebf5-107">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-107">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="3ebf5-108">如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="3ebf5-108">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="3ebf5-109">**Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-109">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="3ebf5-110">請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-110">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="3ebf5-111">請確定您已啟用遠端桌面 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-111">Make sure you enable Remote Desktop for hello cluster.</span></span>
* <span data-ttu-id="3ebf5-112">**在 HDInsight 上使用 MapReduce**。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-112">**Using MapReduce on HDInsight**.</span></span>  <span data-ttu-id="3ebf5-113">如需詳細資訊，請參閱[在 HDInsight 上的 Hadoop 中使用 MapReduce](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)</span><span class="sxs-lookup"><span data-stu-id="3ebf5-113">For more information, see [Use MapReduce in Hadoop on HDInsight](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-mapreduce)</span></span>  
* <span data-ttu-id="3ebf5-114">**ADLS 的效能微調指導方針**。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-114">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="3ebf5-115">如需一般的效能概念，請參閱 [Data Lake Store 效能微調指導方針](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span><span class="sxs-lookup"><span data-stu-id="3ebf5-115">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>  

## <a name="parameters"></a><span data-ttu-id="3ebf5-116">參數</span><span class="sxs-lookup"><span data-stu-id="3ebf5-116">Parameters</span></span>

<span data-ttu-id="3ebf5-117">當執行 MapReduce 工作，以下是 hello 最重要的參數，您可以在 ADLS 設定 tooincrease 效能：</span><span class="sxs-lookup"><span data-stu-id="3ebf5-117">When running MapReduce jobs, here are hello most important parameters that you can configure tooincrease performance on ADLS:</span></span>

* <span data-ttu-id="3ebf5-118">**Mapreduce.map.memory.mb** – 記憶體 tooallocate tooeach 對應工具的 hello 數量</span><span class="sxs-lookup"><span data-stu-id="3ebf5-118">**Mapreduce.map.memory.mb** – hello amount of memory tooallocate tooeach mapper</span></span>
* <span data-ttu-id="3ebf5-119">**Mapreduce.job.maps** – hello 對應每個作業的工作數目</span><span class="sxs-lookup"><span data-stu-id="3ebf5-119">**Mapreduce.job.maps** – hello number of map tasks per job</span></span>
* <span data-ttu-id="3ebf5-120">**Mapreduce.reduce.memory.mb** – 記憶體 tooallocate tooeach 減壓器的 hello 數量</span><span class="sxs-lookup"><span data-stu-id="3ebf5-120">**Mapreduce.reduce.memory.mb** – hello amount of memory tooallocate tooeach reducer</span></span>
* <span data-ttu-id="3ebf5-121">**Mapreduce.job.reduces** – hello 減少每個作業的工作數目</span><span class="sxs-lookup"><span data-stu-id="3ebf5-121">**Mapreduce.job.reduces** – hello number of reduce tasks per job</span></span>

<span data-ttu-id="3ebf5-122">**Mapreduce.map.memory / Mapreduce.reduce.memory**這個數字應該根據 hello 對應需要的記憶體容量調整和/或減少工作。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-122">**Mapreduce.map.memory / Mapreduce.reduce.memory** This number should be adjusted based on how much memory is needed for hello map and/or reduce task.</span></span>  <span data-ttu-id="3ebf5-123">mapreduce.map.memory 與 mapreduce.reduce.memory hello 預設值可以透過 hello Yarn 組態 Ambari 進行檢視。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-123">hello default values of mapreduce.map.memory and mapreduce.reduce.memory can be viewed in Ambari via hello Yarn configuration.</span></span>  <span data-ttu-id="3ebf5-124">在 Ambari 瀏覽 tooYARN 並檢視 hello 組態 索引標籤。 將會顯示 hello YARN 記憶體。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-124">In Ambari, navigate tooYARN and view hello Configs tab.  hello YARN memory will be displayed.</span></span>  

<span data-ttu-id="3ebf5-125">**Mapreduce.job.maps / Mapreduce.job.reduces**這會決定 hello 自行或 reducers toobe 建立的數目上限。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-125">**Mapreduce.job.maps / Mapreduce.job.reduces** This will determine hello maximum number of mappers or reducers toobe created.</span></span>  <span data-ttu-id="3ebf5-126">hello 分割數會決定多少自行建立 hello MapReduce 工作。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-126">hello number of splits will determine how many mappers will be created for hello MapReduce job.</span></span>  <span data-ttu-id="3ebf5-127">因此，您可能會收到較少自行比您要求是否有較少分割比 hello 自行要求數目。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-127">Therefore, you may get less mappers than you requested if there are less splits than hello number of mappers requested.</span></span>       

## <a name="guidance"></a><span data-ttu-id="3ebf5-128">指引</span><span class="sxs-lookup"><span data-stu-id="3ebf5-128">Guidance</span></span>

<span data-ttu-id="3ebf5-129">**步驟 1： 決定執行工作的數目**-根據預設，MapReduce 將適用於您作業使用 hello 整個叢集。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-129">**Step 1: Determine number of jobs running** - By default, MapReduce will use hello entire cluster for your job.</span></span>  <span data-ttu-id="3ebf5-130">您可以使用更少的 hello 叢集使用較少對應工具中有可用的容器。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-130">You can use less of hello cluster by using less mappers than there are available containers.</span></span>  <span data-ttu-id="3ebf5-131">這份文件中的 hello 指導方針會假設您的應用程式在您的叢集上執行 hello 只有應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-131">hello guidance in this document assumes that your application is hello only application running on your cluster.</span></span>      

<span data-ttu-id="3ebf5-132">**步驟 2： 設定 mapreduce.map.memory/mapreduce.reduce.memory** – hello hello 記憶體對應的大小並降低工作將會相依於您特定的工作。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-132">**Step 2: Set mapreduce.map.memory/mapreduce.reduce.memory** –  hello size of hello memory for map and reduce tasks will be dependent on your specific job.</span></span>  <span data-ttu-id="3ebf5-133">如果您想 tooincrease 並行存取，您可以減少 hello 記憶體大小。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-133">You can reduce hello memory size if you want tooincrease concurrency.</span></span>  <span data-ttu-id="3ebf5-134">同時執行工作的 hello 數目取決於 hello 數目的容器。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-134">hello number of concurrently running tasks depends on hello number of containers.</span></span>  <span data-ttu-id="3ebf5-135">藉由降低 hello 每個對應或減壓器的記憶體數量，多個容器可以建立，可讓多個對應或 reducers toorun 同時。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-135">By decreasing hello amount of memory per mapper or reducer, more containers can be created, which enable more mappers or reducers toorun concurrently.</span></span>  <span data-ttu-id="3ebf5-136">太多記憶體的遞減 hello 數量可能會導致某些處理程序 toorun，記憶體不足。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-136">Decreasing hello amount of memory too much may cause some processes toorun out of memory.</span></span>  <span data-ttu-id="3ebf5-137">如果執行您的工作時，您可以取得堆積錯誤，您應該增加每個對應或減壓器 hello 記憶體。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-137">If you get a heap error when running your job, you should increase hello memory per mapper or reducer.</span></span>  <span data-ttu-id="3ebf5-138">您應該考慮到，新增更多容器會對每個額外的容器新增額外的負擔，而可能降低效能。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-138">You should consider that adding more containers will add extra overhead for each additional container, which can potentially degrade performance.</span></span>  <span data-ttu-id="3ebf5-139">另一個替代方法是 tooget 更多的記憶體使用擁有較高的記憶體數量的叢集，或增加 hello 叢集中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-139">Another alternative is tooget more memory by using a cluster that has higher amounts of memory or increasing hello number of nodes in your cluster.</span></span>  <span data-ttu-id="3ebf5-140">更多的記憶體可讓多個容器 toobe 使用，這表示多個並行存取。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-140">More memory will enable more containers toobe used, which means more concurrency.</span></span>  

<span data-ttu-id="3ebf5-141">**步驟 3： 決定總 YARN 記憶體**-tootune mapreduce.job.maps/mapreduce.job.reduces，您應該考慮 hello 可供使用的總 YARN 記憶體數量。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-141">**Step 3: Determine Total YARN memory** - tootune mapreduce.job.maps/mapreduce.job.reduces, you should consider hello amount of total YARN memory available for use.</span></span>  <span data-ttu-id="3ebf5-142">這項資訊可在 Ambari 中取得。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-142">This information is available in Ambari.</span></span>  <span data-ttu-id="3ebf5-143">瀏覽 tooYARN 並檢視 hello 組態 索引標籤。 hello YARN 記憶體會顯示此視窗中。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-143">Navigate tooYARN and view hello Configs tab.  hello YARN memory is displayed in this window.</span></span>  <span data-ttu-id="3ebf5-144">您應該在叢集 tooget hello 總 YARN 記憶體乘以 hello YARN 記憶體與 hello 節點數目。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-144">You should multiply hello YARN memory with hello number of nodes in your cluster tooget hello total YARN memory.</span></span>

    Total YARN memory = nodes * YARN memory per node
<span data-ttu-id="3ebf5-145">如果您使用空白的叢集，記憶體可以是 hello YARN 記憶體總計為您的叢集。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-145">If you are using an empty cluster, then memory can be hello total YARN memory for your cluster.</span></span>  <span data-ttu-id="3ebf5-146">如果其他應用程式可以藉由減少 hello 自行或 reducers toohello 數目的容器數目選擇 tooonly 使用您的叢集記憶體的一部分使用的記憶體，您會想 toouse。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-146">If other applications are using memory, then you can choose tooonly use a portion of your cluster’s memory by reducing hello number of mappers or reducers toohello number of containers you want toouse.</span></span>  

<span data-ttu-id="3ebf5-147">**步驟 4： 計算 YARN 容器數目**– YARN 容器聽寫 hello 可用 hello 作業並行處理的數量。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-147">**Step 4: Calculate number of YARN containers** – YARN containers dictate hello amount of concurrency available for hello job.</span></span>  <span data-ttu-id="3ebf5-148">取得 YARN 記憶體總數，然後除以 mapreduce.map.memory。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-148">Take total YARN memory and divide that by mapreduce.map.memory.</span></span>  

    # of YARN containers = total YARN memory / mapreduce.map.memory

<span data-ttu-id="3ebf5-149">**步驟 5： 設定 mapreduce.job.maps/mapreduce.job.reduces**設定 mapreduce.job.maps/mapreduce.job.reduces tooat 可用的容器的最小 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-149">**Step 5: Set mapreduce.job.maps/mapreduce.job.reduces** Set mapreduce.job.maps/mapreduce.job.reduces tooat least hello number of available containers.</span></span>  <span data-ttu-id="3ebf5-150">您可以試驗進一步增加 hello 自行和 reducers toosee 數目，如果您取得較佳的效能。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-150">You can experiment further by increasing hello number of mappers and reducers toosee if you get better performance.</span></span>  <span data-ttu-id="3ebf5-151">請記住，更多的對應器會產生額外的負擔，因此對應器過多可能會降低效能。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-151">Keep in mind that more mappers will have additional overhead so having too many mappers may degrade performance.</span></span>  

<span data-ttu-id="3ebf5-152">CPU 排程和 CPU 隔離會關閉預設讓 hello YARN 容器的數目由記憶體限制。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-152">CPU scheduling and CPU isolation are turned off by default so hello number of YARN containers is constrained by memory.</span></span>

## <a name="example-calculation"></a><span data-ttu-id="3ebf5-153">範例計算</span><span class="sxs-lookup"><span data-stu-id="3ebf5-153">Example Calculation</span></span>

<span data-ttu-id="3ebf5-154">讓我們假設您目前有 8 個 D14 節點所組成的叢集，而且您想 toorun I/O 大量工作。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-154">Let’s say you currently have a cluster composed of 8 D14 nodes and you want toorun an I/O intensive job.</span></span>  <span data-ttu-id="3ebf5-155">以下是您應該執行的 hello 計算：</span><span class="sxs-lookup"><span data-stu-id="3ebf5-155">Here are hello calculations you should do:</span></span>

<span data-ttu-id="3ebf5-156">**步驟 1： 決定執行工作的數目**-此範例中，我們假設我們的責任是 hello 只有一個執行。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-156">**Step 1: Determine number of jobs running** - for our example, we assume that our job is hello only one running.</span></span>  

<span data-ttu-id="3ebf5-157">**步驟 2︰設定 mapreduce.map.memory/mapreduce.reduce.memory** – 在我們的範例中，您將會執行 I/O 密集作業，並決定 3 GB 的記憶體已足夠對應工作使用。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-157">**Step 2: Set mapreduce.map.memory/mapreduce.reduce.memory** – for our example, you are running an I/O intensive job and decide that 3GB of memory for map tasks will be sufficient.</span></span>

    mapreduce.map.memory = 3GB
<span data-ttu-id="3ebf5-158">**步驟 3︰確定 YARN 記憶體總數**</span><span class="sxs-lookup"><span data-stu-id="3ebf5-158">**Step 3: Determine Total YARN memory**</span></span>

    total memory from hello cluster is 8 nodes * 96GB of YARN memory for a D14 = 768GB
<span data-ttu-id="3ebf5-159">**步驟 4︰計算 YARN 容器的數目**</span><span class="sxs-lookup"><span data-stu-id="3ebf5-159">**Step 4: Calculate # of YARN containers**</span></span>

    # of YARN containers = 768GB of available memory / 3 GB of memory =   256

<span data-ttu-id="3ebf5-160">**步驟 5：設定 mapreduce.job.maps/mapreduce.job.reduces**</span><span class="sxs-lookup"><span data-stu-id="3ebf5-160">**Step 5: Set mapreduce.job.maps/mapreduce.job.reduces**</span></span>

    mapreduce.map.jobs = 256

## <a name="limitations"></a><span data-ttu-id="3ebf5-161">限制</span><span class="sxs-lookup"><span data-stu-id="3ebf5-161">Limitations</span></span>

<span data-ttu-id="3ebf5-162">**ADLS 節流**</span><span class="sxs-lookup"><span data-stu-id="3ebf5-162">**ADLS throttling**</span></span>

<span data-ttu-id="3ebf5-163">ADLS 是多租用戶服務，因此會設定帳戶層級的頻寬限制。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-163">As a multi-tenant service, ADLS sets account level bandwidth limits.</span></span>  <span data-ttu-id="3ebf5-164">如果您叫用這些限制，您將啟動 toosee 工作失敗。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-164">If you hit these limits, you will start toosee task failures.</span></span> <span data-ttu-id="3ebf5-165">透過觀察工作記錄檔中的節流錯誤即可加以識別。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-165">This can be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="3ebf5-166">如果您的作業需要更多頻寬，請與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-166">If you need more bandwidth for your job, please contact us.</span></span>   

<span data-ttu-id="3ebf5-167">如果您節流 toocheck，您需要 tooenable hello 偵錯記錄 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-167">toocheck if you are getting throttled, you need tooenable hello debug logging on hello client side.</span></span> <span data-ttu-id="3ebf5-168">做法如下：</span><span class="sxs-lookup"><span data-stu-id="3ebf5-168">Here’s how you can do that:</span></span>

1. <span data-ttu-id="3ebf5-169">Put hello 下列 hello log4j 屬性中 Ambari 屬性 > YARN > 組態 > 進階 yarn log4j: log4j.logger.com.microsoft.azure.datalake.store=DEBUG</span><span class="sxs-lookup"><span data-stu-id="3ebf5-169">Put hello following property in hello log4j properties in Ambari > YARN > Config > Advanced yarn-log4j: log4j.logger.com.microsoft.azure.datalake.store=DEBUG</span></span>

2. <span data-ttu-id="3ebf5-170">重新啟動所有 hello 節點/服務 hello config tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-170">Restart all hello nodes/service for hello config tootake effect.</span></span>

3. <span data-ttu-id="3ebf5-171">如果您節流，您會看到 hello YARN 記錄檔中的 hello HTTP 429 錯誤程式碼。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-171">If you are getting throttled, you’ll see hello HTTP 429 error code in hello YARN log file.</span></span> <span data-ttu-id="3ebf5-172">hello YARN 記錄檔位於 /tmp/&lt;使用者&gt;/yarn.log</span><span class="sxs-lookup"><span data-stu-id="3ebf5-172">hello YARN log file is in /tmp/&lt;user&gt;/yarn.log</span></span>

## <a name="examples-toorun"></a><span data-ttu-id="3ebf5-173">範例 tooRun</span><span class="sxs-lookup"><span data-stu-id="3ebf5-173">Examples tooRun</span></span>

<span data-ttu-id="3ebf5-174">toodemonstrate 如何在 Azure 資料湖存放區上執行 MapReduce 下面是一些已在叢集執行，以下列設定的 hello 的範例程式碼：</span><span class="sxs-lookup"><span data-stu-id="3ebf5-174">toodemonstrate how MapReduce runs on Azure Data Lake Store, below is some sample code that was run on a cluster with hello following settings:</span></span>

* <span data-ttu-id="3ebf5-175">16 節點 D14v2</span><span class="sxs-lookup"><span data-stu-id="3ebf5-175">16 node D14v2</span></span>
* <span data-ttu-id="3ebf5-176">執行 HDI 3.6 的 Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="3ebf5-176">Hadoop cluster running HDI 3.6</span></span>

<span data-ttu-id="3ebf5-177">起點，以下是一些範例命令 toorun MapReduce Teragen、 Terasort 和 Teravalidate。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-177">For a starting point, here are some example commands toorun MapReduce Teragen, Terasort, and Teravalidate.</span></span>  <span data-ttu-id="3ebf5-178">您可以根據您的資源調整這些命令。</span><span class="sxs-lookup"><span data-stu-id="3ebf5-178">You can adjust these commands based on your resources.</span></span>

<span data-ttu-id="3ebf5-179">**Teragen**</span><span class="sxs-lookup"><span data-stu-id="3ebf5-179">**Teragen**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teragen -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 10000000000 adl://example/data/1TB-sort-input

<span data-ttu-id="3ebf5-180">**Terasort**</span><span class="sxs-lookup"><span data-stu-id="3ebf5-180">**Terasort**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar terasort -Dmapreduce.job.maps=2048 -Dmapreduce.map.memory.mb=3072 -Dmapreduce.job.reduces=512 -Dmapreduce.reduce.memory.mb=3072 adl://example/data/1TB-sort-input adl://example/data/1TB-sort-output

<span data-ttu-id="3ebf5-181">**Teravalidate**</span><span class="sxs-lookup"><span data-stu-id="3ebf5-181">**Teravalidate**</span></span>

    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar teravalidate -Dmapreduce.job.maps=512 -Dmapreduce.map.memory.mb=3072 adl://example/data/1TB-sort-output adl://example/data/1TB-sort-validate
