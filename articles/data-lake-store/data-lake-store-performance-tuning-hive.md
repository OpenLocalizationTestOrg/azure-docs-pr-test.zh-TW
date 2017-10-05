---
title: "Azure Data Lake Store Hive 效能微調方針 | Microsoft Docs"
description: "Azure Data Lake Store Hive 效能微調方針"
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
ms.openlocfilehash: e10bf8f7cbae2b81d22823ff74fe652c6bcb2da3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="db534-103">HDInsight 和 Azure Data Lake Store 上的 Hive 效能微調方針</span><span class="sxs-lookup"><span data-stu-id="db534-103">Performance tuning guidance for Hive on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="db534-104">預設設定已設定好，以便在許多不同的使用案例中提供良好的效能。</span><span class="sxs-lookup"><span data-stu-id="db534-104">The default settings have been set to provide good performance across many different use cases.</span></span>  <span data-ttu-id="db534-105">針對 I/O 密集的查詢，Hive 可進行微調，以在 ADLS 取得更好的效能。</span><span class="sxs-lookup"><span data-stu-id="db534-105">For I/O intensive queries, Hive can be tuned to get better performance with ADLS.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="db534-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="db534-106">Prerequisites</span></span>

* <span data-ttu-id="db534-107">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="db534-107">**An Azure subscription**.</span></span> <span data-ttu-id="db534-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="db534-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="db534-109">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="db534-109">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="db534-110">如需有關如何建立帳戶的詳細指示，請參閱 [開始使用 Azure Data Lake Store](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="db534-110">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="db534-111">**Azure HDInsight 叢集** 。</span><span class="sxs-lookup"><span data-stu-id="db534-111">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="db534-112">請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="db534-112">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="db534-113">請確實為叢集啟用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="db534-113">Make sure you enable Remote Desktop for the cluster.</span></span>
* <span data-ttu-id="db534-114">**在 HDInsight 上執行 Hive**。</span><span class="sxs-lookup"><span data-stu-id="db534-114">**Running Hive on HDInsight**.</span></span>  <span data-ttu-id="db534-115">若要了解如何在 HDInsight 上執行 Hive 作業，請參閱 [使用 HDInsight 上的 Hive] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span><span class="sxs-lookup"><span data-stu-id="db534-115">To learn about running Hive jobs on HDInsight, see [Use Hive on HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span></span>
* <span data-ttu-id="db534-116">**ADLS 的效能微調指導方針**。</span><span class="sxs-lookup"><span data-stu-id="db534-116">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="db534-117">如需一般的效能概念，請參閱 [Data Lake Store 效能微調指導方針](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span><span class="sxs-lookup"><span data-stu-id="db534-117">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>

## <a name="parameters"></a><span data-ttu-id="db534-118">參數</span><span class="sxs-lookup"><span data-stu-id="db534-118">Parameters</span></span>

<span data-ttu-id="db534-119">以下是要改善 ADLS 效能所應微調的最重要設定︰</span><span class="sxs-lookup"><span data-stu-id="db534-119">Here are the most important settings to tune for improved ADLS performance:</span></span>

* <span data-ttu-id="db534-120">**hive.tez.container.size** – 每個工作所使用的記憶體數量</span><span class="sxs-lookup"><span data-stu-id="db534-120">**hive.tez.container.size** – the amount of memory used by each tasks</span></span>

* <span data-ttu-id="db534-121">**tez.grouping.min-size** – 每個對應器的大小下限</span><span class="sxs-lookup"><span data-stu-id="db534-121">**tez.grouping.min-size** – minimum size of each mapper</span></span>

* <span data-ttu-id="db534-122">**tez.grouping.max-size** – 每個對應器的大小上限</span><span class="sxs-lookup"><span data-stu-id="db534-122">**tez.grouping.max-size** – maximum size of each mapper</span></span>

* <span data-ttu-id="db534-123">**hive.exec.reducer.bytes.per.reducer** – 每個歸納器的大小</span><span class="sxs-lookup"><span data-stu-id="db534-123">**hive.exec.reducer.bytes.per.reducer** – size of each reducer</span></span>

<span data-ttu-id="db534-124">**hive.tez.container.size** - 容器大小會決定每個工作可以使用多少記憶體。</span><span class="sxs-lookup"><span data-stu-id="db534-124">**hive.tez.container.size** - The container size determines how much memory is available for each task.</span></span>  <span data-ttu-id="db534-125">這是用來控制 Hive 中之並行能力的主要輸入。</span><span class="sxs-lookup"><span data-stu-id="db534-125">This is the main input for controlling the concurrency in Hive.</span></span>  

<span data-ttu-id="db534-126">**tez.grouping.min-size** – 此參數可讓您設定每個對應器的大小下限。</span><span class="sxs-lookup"><span data-stu-id="db534-126">**tez.grouping.min-size** – This parameter allows you to set the minimum size of each mapper.</span></span>  <span data-ttu-id="db534-127">如果 Tez 選擇的對應器數目小於此參數的值，Tez 會使用此處設定的值。</span><span class="sxs-lookup"><span data-stu-id="db534-127">If the number of mappers that Tez chooses is smaller than the value of this parameter, then Tez will use the value set here.</span></span>  

<span data-ttu-id="db534-128">**tez.grouping.max-size** – 此參數可讓您設定每個對應器的大小上限。</span><span class="sxs-lookup"><span data-stu-id="db534-128">**tez.grouping.max-size** – The parameter allows you to set the maximum size of each mapper.</span></span>  <span data-ttu-id="db534-129">如果 Tez 選擇的對應器數目大於此參數的值，Tez 會使用此處設定的值。</span><span class="sxs-lookup"><span data-stu-id="db534-129">If the number of mappers that Tez chooses is larger than the value of this parameter, then Tez will use the value set here.</span></span>  

<span data-ttu-id="db534-130">**hive.exec.reducer.bytes.per.reducer** – 此參數會設定每個歸納器的大小。</span><span class="sxs-lookup"><span data-stu-id="db534-130">**hive.exec.reducer.bytes.per.reducer** – This parameter sets the size of each reducer.</span></span>  <span data-ttu-id="db534-131">根據預設，每個歸納器為 256 MB。</span><span class="sxs-lookup"><span data-stu-id="db534-131">By default, each reducer is 256MB.</span></span>  

## <a name="guidance"></a><span data-ttu-id="db534-132">指引</span><span class="sxs-lookup"><span data-stu-id="db534-132">Guidance</span></span>

<span data-ttu-id="db534-133">**Set hive.exec.reducer.bytes.per.reducer** – 資料若未壓縮，預設值就很適用。</span><span class="sxs-lookup"><span data-stu-id="db534-133">**Set hive.exec.reducer.bytes.per.reducer** – The default value works well when the data is uncompressed.</span></span>  <span data-ttu-id="db534-134">資料若有壓縮，則應縮減歸納器的大小。</span><span class="sxs-lookup"><span data-stu-id="db534-134">For data that is compressed, you should reduce the size of the reducer.</span></span>  

<span data-ttu-id="db534-135">**Set hive.tez.container.size** – 在每個節點中，記憶體會由 yarn.nodemanager.resource.memory-mb 指定，且預設應該會在 HDI 叢集上正確設定。</span><span class="sxs-lookup"><span data-stu-id="db534-135">**Set hive.tez.container.size** – In each node, memory is specified by yarn.nodemanager.resource.memory-mb and should be correctly set on HDI cluster by default.</span></span>  <span data-ttu-id="db534-136">如需在 YARN 中設定適當記憶體的詳細資訊，請參閱這篇[文章](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom)。</span><span class="sxs-lookup"><span data-stu-id="db534-136">For additional information on setting the appropriate memory in YARN, see this [post](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).</span></span>

<span data-ttu-id="db534-137">I/O 密集工作負載可以透過減少 Tez 容器大小，而從更符合平行處理原則受益。</span><span class="sxs-lookup"><span data-stu-id="db534-137">I/O intensive workloads can benefit from more parallelism by decreasing the Tez container size.</span></span> <span data-ttu-id="db534-138">這會讓使用者獲得更多容器，而增加並行能力。</span><span class="sxs-lookup"><span data-stu-id="db534-138">This gives the user more containers which increases concurrency.</span></span>  <span data-ttu-id="db534-139">不過，某些 Hive 查詢需要大量的記憶體 (例如 MapJoin)。</span><span class="sxs-lookup"><span data-stu-id="db534-139">However, some Hive queries require a significant amount of memory (e.g. MapJoin).</span></span>  <span data-ttu-id="db534-140">如果工作沒有足夠的記憶體，您會在執行階段期間遇到記憶體不足的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="db534-140">If the task does not have enough memory, you will get an out of memory exception during runtime.</span></span>  <span data-ttu-id="db534-141">如果您遇到記憶體不足的例外狀況，則應增加記憶體。</span><span class="sxs-lookup"><span data-stu-id="db534-141">If you receive out of memory exceptions, then you should increase the memory.</span></span>   

<span data-ttu-id="db534-142">並行執行的工作數或平行處理原則會受到 YARN 記憶體總數的限制。</span><span class="sxs-lookup"><span data-stu-id="db534-142">The concurrent number of tasks running or parallelism will be bounded by the total YARN memory.</span></span>  <span data-ttu-id="db534-143">YARN 容器數目會決定可以執行多少並行工作。</span><span class="sxs-lookup"><span data-stu-id="db534-143">The number of YARN containers will dictate how many concurrent tasks can run.</span></span>  <span data-ttu-id="db534-144">若要尋找每個節點的 YARN 記憶體，您可以前往 Ambari。</span><span class="sxs-lookup"><span data-stu-id="db534-144">To find the YARN memory per node, you can go to Ambari.</span></span>  <span data-ttu-id="db534-145">瀏覽至 YARN，然後檢視 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="db534-145">Navigate to YARN and view the Configs tab.</span></span>  <span data-ttu-id="db534-146">YARN 記憶體會顯示在此視窗中。</span><span class="sxs-lookup"><span data-stu-id="db534-146">The YARN memory is displayed in this window.</span></span>  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
<span data-ttu-id="db534-147">使用 ADLS 來改善效能的關鍵是盡可能地增加並行能力。</span><span class="sxs-lookup"><span data-stu-id="db534-147">The key to improving performance using ADLS is to increase the concurrency as much as possible.</span></span>  <span data-ttu-id="db534-148">Tez 會自動計算應該建立的工作數目，因此您並不需要設定。</span><span class="sxs-lookup"><span data-stu-id="db534-148">Tez automatically calculates the number of tasks that should be created so you do not need to set it.</span></span>   

## <a name="example-calculation"></a><span data-ttu-id="db534-149">範例計算</span><span class="sxs-lookup"><span data-stu-id="db534-149">Example Calculation</span></span>

<span data-ttu-id="db534-150">假設您有 8 節點的 D14 叢集。</span><span class="sxs-lookup"><span data-stu-id="db534-150">Let’s say you have an 8 node D14 cluster.</span></span>  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a><span data-ttu-id="db534-151">限制</span><span class="sxs-lookup"><span data-stu-id="db534-151">Limitations</span></span>
<span data-ttu-id="db534-152">**ADLS 節流**</span><span class="sxs-lookup"><span data-stu-id="db534-152">**ADLS throttling**</span></span> 

<span data-ttu-id="db534-153">如果您達到 ADLS 所提供的頻寬限制，您會開始看到工作失敗。</span><span class="sxs-lookup"><span data-stu-id="db534-153">UIf you hit the limits of bandwidth provided by ADLS, you would start to see task failures.</span></span> <span data-ttu-id="db534-154">透過觀察工作記錄檔中的節流錯誤即可加以識別。</span><span class="sxs-lookup"><span data-stu-id="db534-154">This could be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="db534-155">您可以藉由增加 Tez 容器大小來減少平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="db534-155">You can decrease the parallelism by increasing Tez container size.</span></span>  <span data-ttu-id="db534-156">如果您的作業需要更多並行能力，請與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="db534-156">If you need more concurrency for your job, please contact us.</span></span>   

<span data-ttu-id="db534-157">若要檢查您是否遭到節流，您必須在用戶端啟用偵錯記錄。</span><span class="sxs-lookup"><span data-stu-id="db534-157">To check if you are getting throttled, you need to enable the debug logging on the client side.</span></span> <span data-ttu-id="db534-158">做法如下：</span><span class="sxs-lookup"><span data-stu-id="db534-158">Here’s how you can do that:</span></span>

1. <span data-ttu-id="db534-159">將下列屬性放在 Hive 組態中的 log4j 屬性內。</span><span class="sxs-lookup"><span data-stu-id="db534-159">Put the following property in the log4j properties in Hive config.</span></span> <span data-ttu-id="db534-160">做法是從 Ambari 檢視︰log4j.logger.com.microsoft.azure.datalake.store=DEBUG 重新啟動所有節點/服務以便讓組態生效。</span><span class="sxs-lookup"><span data-stu-id="db534-160">This can be done from Ambari view: log4j.logger.com.microsoft.azure.datalake.store=DEBUG Restart all the nodes/service for the config to take effect.</span></span>

2. <span data-ttu-id="db534-161">如果您遭到節流，您會看到 Hive 記錄檔中有 HTTP 429 錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="db534-161">If you are getting throttled, you’ll see the HTTP 429 error code in the hive log file.</span></span> <span data-ttu-id="db534-162">Hive 記錄檔位於 /tmp/&lt;user&gt;/hive.log</span><span class="sxs-lookup"><span data-stu-id="db534-162">The hive log file is in /tmp/&lt;user&gt;/hive.log</span></span>

## <a name="further-information-on-hive-tuning"></a><span data-ttu-id="db534-163">關於微調 Hive 的進一步資訊</span><span class="sxs-lookup"><span data-stu-id="db534-163">Further information on Hive tuning</span></span>

<span data-ttu-id="db534-164">以下是一些有助於微調 Hive 查詢的部落格︰</span><span class="sxs-lookup"><span data-stu-id="db534-164">Here are a few blogs that will help tune your Hive queries:</span></span>
* [<span data-ttu-id="db534-165">在 Hdinsight 中最佳化 Hadoop 的 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="db534-165">Optimize Hive queries for Hadoop in HDInsight</span></span>](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [<span data-ttu-id="db534-166">針對 Hive 查詢的效能進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="db534-166">Troubleshooting Hive query performance</span></span>](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [<span data-ttu-id="db534-167">Ignite 講解如何將 HDInsight 上的 Hive 最佳化</span><span class="sxs-lookup"><span data-stu-id="db534-167">Ignite talk on optimize Hive on HDInsight</span></span>](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
