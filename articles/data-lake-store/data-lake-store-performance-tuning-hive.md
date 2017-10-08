---
title: "資料湖存放區 Hive 效能調整指導方針 aaaAzure |Microsoft 文件"
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
ms.openlocfilehash: e44daeb6ad3b64e893c709df63b56444a330729f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tuning-guidance-for-hive-on-hdinsight-and-azure-data-lake-store"></a><span data-ttu-id="50abb-103">HDInsight 和 Azure Data Lake Store 上的 Hive 效能微調方針</span><span class="sxs-lookup"><span data-stu-id="50abb-103">Performance tuning guidance for Hive on HDInsight and Azure Data Lake Store</span></span>

<span data-ttu-id="50abb-104">hello 預設設定已設 tooprovide 良好的效能在許多不同的使用案例。</span><span class="sxs-lookup"><span data-stu-id="50abb-104">hello default settings have been set tooprovide good performance across many different use cases.</span></span>  <span data-ttu-id="50abb-105">I/O 密集的查詢，Hive 可以微調的 tooget ADLS 與更好的效能。</span><span class="sxs-lookup"><span data-stu-id="50abb-105">For I/O intensive queries, Hive can be tuned tooget better performance with ADLS.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="50abb-106">必要條件</span><span class="sxs-lookup"><span data-stu-id="50abb-106">Prerequisites</span></span>

* <span data-ttu-id="50abb-107">**Azure 訂用帳戶**。</span><span class="sxs-lookup"><span data-stu-id="50abb-107">**An Azure subscription**.</span></span> <span data-ttu-id="50abb-108">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="50abb-108">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="50abb-109">**Azure Data Lake Store 帳戶**。</span><span class="sxs-lookup"><span data-stu-id="50abb-109">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="50abb-110">如需有關指示 toocreate 一個，請參閱[開始使用 Azure 資料湖存放區](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="50abb-110">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="50abb-111">**Azure HDInsight 叢集**與存取 tooa Data Lake Store 帳戶。</span><span class="sxs-lookup"><span data-stu-id="50abb-111">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="50abb-112">請參閱 [建立具有 Data Lake Store 的 HDInsight 叢集](data-lake-store-hdinsight-hadoop-use-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="50abb-112">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="50abb-113">請確定您已啟用遠端桌面 hello 叢集。</span><span class="sxs-lookup"><span data-stu-id="50abb-113">Make sure you enable Remote Desktop for hello cluster.</span></span>
* <span data-ttu-id="50abb-114">**在 HDInsight 上執行 Hive**。</span><span class="sxs-lookup"><span data-stu-id="50abb-114">**Running Hive on HDInsight**.</span></span>  <span data-ttu-id="50abb-115">在 HDInsight 上執行 Hive 工作相關的 toolearn 請參閱 [使用 HDInsight 上的登錄區] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span><span class="sxs-lookup"><span data-stu-id="50abb-115">toolearn about running Hive jobs on HDInsight, see [Use Hive on HDInsight] (https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-use-hive)</span></span>
* <span data-ttu-id="50abb-116">**ADLS 的效能微調指導方針**。</span><span class="sxs-lookup"><span data-stu-id="50abb-116">**Performance tuning guidelines on ADLS**.</span></span>  <span data-ttu-id="50abb-117">如需一般的效能概念，請參閱 [Data Lake Store 效能微調指導方針](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span><span class="sxs-lookup"><span data-stu-id="50abb-117">For general performance concepts, see [Data Lake Store Performance Tuning Guidance](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-performance-tuning-guidance)</span></span>

## <a name="parameters"></a><span data-ttu-id="50abb-118">參數</span><span class="sxs-lookup"><span data-stu-id="50abb-118">Parameters</span></span>

<span data-ttu-id="50abb-119">以下是 hello 最重要設定 tootune 改善 ADLS 效能：</span><span class="sxs-lookup"><span data-stu-id="50abb-119">Here are hello most important settings tootune for improved ADLS performance:</span></span>

* <span data-ttu-id="50abb-120">**hive.tez.container.size** – hello 每個工作所使用的記憶體數量</span><span class="sxs-lookup"><span data-stu-id="50abb-120">**hive.tez.container.size** – hello amount of memory used by each tasks</span></span>

* <span data-ttu-id="50abb-121">**tez.grouping.min-size** – 每個對應器的大小下限</span><span class="sxs-lookup"><span data-stu-id="50abb-121">**tez.grouping.min-size** – minimum size of each mapper</span></span>

* <span data-ttu-id="50abb-122">**tez.grouping.max-size** – 每個對應器的大小上限</span><span class="sxs-lookup"><span data-stu-id="50abb-122">**tez.grouping.max-size** – maximum size of each mapper</span></span>

* <span data-ttu-id="50abb-123">**hive.exec.reducer.bytes.per.reducer** – 每個歸納器的大小</span><span class="sxs-lookup"><span data-stu-id="50abb-123">**hive.exec.reducer.bytes.per.reducer** – size of each reducer</span></span>

<span data-ttu-id="50abb-124">**hive.tez.container.size** -hello 容器大小會決定多少記憶體可供每項工作。</span><span class="sxs-lookup"><span data-stu-id="50abb-124">**hive.tez.container.size** - hello container size determines how much memory is available for each task.</span></span>  <span data-ttu-id="50abb-125">這是控制 hello 並行登錄區中的 hello 主要輸入。</span><span class="sxs-lookup"><span data-stu-id="50abb-125">This is hello main input for controlling hello concurrency in Hive.</span></span>  

<span data-ttu-id="50abb-126">**tez.grouping.min 大小**– 此參數可讓您的每個對應工具 tooset hello 最小大小。</span><span class="sxs-lookup"><span data-stu-id="50abb-126">**tez.grouping.min-size** – This parameter allows you tooset hello minimum size of each mapper.</span></span>  <span data-ttu-id="50abb-127">如果自行 Tez 所選擇的 hello 數目小於 hello 值，這個參數，Tez 會使用 hello 這裡設定的值。</span><span class="sxs-lookup"><span data-stu-id="50abb-127">If hello number of mappers that Tez chooses is smaller than hello value of this parameter, then Tez will use hello value set here.</span></span>  

<span data-ttu-id="50abb-128">**tez.grouping.max 大小**– hello 參數可讓您的每個對應工具 tooset hello 最大大小。</span><span class="sxs-lookup"><span data-stu-id="50abb-128">**tez.grouping.max-size** – hello parameter allows you tooset hello maximum size of each mapper.</span></span>  <span data-ttu-id="50abb-129">如果自行 Tez 所選擇的 hello 數目大於 hello 值，這個參數，Tez 會使用 hello 這裡設定的值。</span><span class="sxs-lookup"><span data-stu-id="50abb-129">If hello number of mappers that Tez chooses is larger than hello value of this parameter, then Tez will use hello value set here.</span></span>  

<span data-ttu-id="50abb-130">**hive.exec.reducer.bytes.per.reducer** – 這個參數會設定每個減壓器 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="50abb-130">**hive.exec.reducer.bytes.per.reducer** – This parameter sets hello size of each reducer.</span></span>  <span data-ttu-id="50abb-131">根據預設，每個歸納器為 256 MB。</span><span class="sxs-lookup"><span data-stu-id="50abb-131">By default, each reducer is 256MB.</span></span>  

## <a name="guidance"></a><span data-ttu-id="50abb-132">指引</span><span class="sxs-lookup"><span data-stu-id="50abb-132">Guidance</span></span>

<span data-ttu-id="50abb-133">**設定 hive.exec.reducer.bytes.per.reducer** – hello 預設值就非常適合 hello 資料時未壓縮。</span><span class="sxs-lookup"><span data-stu-id="50abb-133">**Set hive.exec.reducer.bytes.per.reducer** – hello default value works well when hello data is uncompressed.</span></span>  <span data-ttu-id="50abb-134">壓縮的資料，您應該縮小 hello hello 減壓器。</span><span class="sxs-lookup"><span data-stu-id="50abb-134">For data that is compressed, you should reduce hello size of hello reducer.</span></span>  

<span data-ttu-id="50abb-135">**Set hive.tez.container.size** – 在每個節點中，記憶體會由 yarn.nodemanager.resource.memory-mb 指定，且預設應該會在 HDI 叢集上正確設定。</span><span class="sxs-lookup"><span data-stu-id="50abb-135">**Set hive.tez.container.size** – In each node, memory is specified by yarn.nodemanager.resource.memory-mb and should be correctly set on HDI cluster by default.</span></span>  <span data-ttu-id="50abb-136">如需有關設定 YARN hello 適當的記憶體的詳細資訊，請參閱此[張貼](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom)。</span><span class="sxs-lookup"><span data-stu-id="50abb-136">For additional information on setting hello appropriate memory in YARN, see this [post](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-hive-out-of-memory-error-oom).</span></span>

<span data-ttu-id="50abb-137">I/O 密集型工作負載可以從多個平行處理原則獲益，藉由降低 hello Tez 容器大小。</span><span class="sxs-lookup"><span data-stu-id="50abb-137">I/O intensive workloads can benefit from more parallelism by decreasing hello Tez container size.</span></span> <span data-ttu-id="50abb-138">這可讓使用者 hello 可增加並行處理多個容器。</span><span class="sxs-lookup"><span data-stu-id="50abb-138">This gives hello user more containers which increases concurrency.</span></span>  <span data-ttu-id="50abb-139">不過，某些 Hive 查詢需要大量的記憶體 (例如 MapJoin)。</span><span class="sxs-lookup"><span data-stu-id="50abb-139">However, some Hive queries require a significant amount of memory (e.g. MapJoin).</span></span>  <span data-ttu-id="50abb-140">如果 hello 工作沒有足夠的記憶體，您會收到記憶體不足例外狀況在執行階段。</span><span class="sxs-lookup"><span data-stu-id="50abb-140">If hello task does not have enough memory, you will get an out of memory exception during runtime.</span></span>  <span data-ttu-id="50abb-141">如果您收到記憶體不足例外狀況，您應該增加 hello 記憶體。</span><span class="sxs-lookup"><span data-stu-id="50abb-141">If you receive out of memory exceptions, then you should increase hello memory.</span></span>   

<span data-ttu-id="50abb-142">hello 並行工作執行或數目平行處理原則將限於 hello YARN 記憶體總數。</span><span class="sxs-lookup"><span data-stu-id="50abb-142">hello concurrent number of tasks running or parallelism will be bounded by hello total YARN memory.</span></span>  <span data-ttu-id="50abb-143">hello YARN 容器的數目會指定多少並行工作可以執行。</span><span class="sxs-lookup"><span data-stu-id="50abb-143">hello number of YARN containers will dictate how many concurrent tasks can run.</span></span>  <span data-ttu-id="50abb-144">每個節點的 toofind hello YARN 記憶體，您可以移 tooAmbari。</span><span class="sxs-lookup"><span data-stu-id="50abb-144">toofind hello YARN memory per node, you can go tooAmbari.</span></span>  <span data-ttu-id="50abb-145">瀏覽 tooYARN 並檢視 hello 組態 索引標籤。 hello YARN 記憶體會顯示此視窗中。</span><span class="sxs-lookup"><span data-stu-id="50abb-145">Navigate tooYARN and view hello Configs tab.  hello YARN memory is displayed in this window.</span></span>  

        Total YARN memory = nodes * YARN memory per node
        # of YARN containers = Total YARN memory / Tez container size
<span data-ttu-id="50abb-146">使用 ADLS hello 金鑰 tooimproving 效能是盡可能 tooincrease hello 並行。</span><span class="sxs-lookup"><span data-stu-id="50abb-146">hello key tooimproving performance using ADLS is tooincrease hello concurrency as much as possible.</span></span>  <span data-ttu-id="50abb-147">Tez 自動計算 hello 數項工作，因此您不需要 tooset 應該建立它。</span><span class="sxs-lookup"><span data-stu-id="50abb-147">Tez automatically calculates hello number of tasks that should be created so you do not need tooset it.</span></span>   

## <a name="example-calculation"></a><span data-ttu-id="50abb-148">範例計算</span><span class="sxs-lookup"><span data-stu-id="50abb-148">Example Calculation</span></span>

<span data-ttu-id="50abb-149">假設您有 8 節點的 D14 叢集。</span><span class="sxs-lookup"><span data-stu-id="50abb-149">Let’s say you have an 8 node D14 cluster.</span></span>  

    Total YARN memory = nodes * YARN memory per node
    Total YARN memory = 8 nodes * 96GB = 768GB
    # of YARN containers = 768GB / 3072MB = 256

## <a name="limitations"></a><span data-ttu-id="50abb-150">限制</span><span class="sxs-lookup"><span data-stu-id="50abb-150">Limitations</span></span>
<span data-ttu-id="50abb-151">**ADLS 節流**</span><span class="sxs-lookup"><span data-stu-id="50abb-151">**ADLS throttling**</span></span> 

<span data-ttu-id="50abb-152">點擊 hello UIf 限制的頻寬提供根據 ADLS，您會啟動 toosee 工作失敗。</span><span class="sxs-lookup"><span data-stu-id="50abb-152">UIf you hit hello limits of bandwidth provided by ADLS, you would start toosee task failures.</span></span> <span data-ttu-id="50abb-153">透過觀察工作記錄檔中的節流錯誤即可加以識別。</span><span class="sxs-lookup"><span data-stu-id="50abb-153">This could be identified by observing throttling errors in task logs.</span></span>  <span data-ttu-id="50abb-154">您可以藉由增加 Tez 容器大小減少 hello 平行處理原則。</span><span class="sxs-lookup"><span data-stu-id="50abb-154">You can decrease hello parallelism by increasing Tez container size.</span></span>  <span data-ttu-id="50abb-155">如果您的作業需要更多並行能力，請與我們連絡。</span><span class="sxs-lookup"><span data-stu-id="50abb-155">If you need more concurrency for your job, please contact us.</span></span>   

<span data-ttu-id="50abb-156">如果您節流 toocheck，您需要 tooenable hello 偵錯記錄 hello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="50abb-156">toocheck if you are getting throttled, you need tooenable hello debug logging on hello client side.</span></span> <span data-ttu-id="50abb-157">做法如下：</span><span class="sxs-lookup"><span data-stu-id="50abb-157">Here’s how you can do that:</span></span>

1. <span data-ttu-id="50abb-158">將下列屬性 Hive 組態中的 hello log4j 屬性中的 hello。這可藉由 Ambari 檢視： log4j.logger.com.microsoft.azure.datalake.store=DEBUG 重新啟動所有 hello 節點/服務 hello config tootake 效果。</span><span class="sxs-lookup"><span data-stu-id="50abb-158">Put hello following property in hello log4j properties in Hive config. This can be done from Ambari view: log4j.logger.com.microsoft.azure.datalake.store=DEBUG Restart all hello nodes/service for hello config tootake effect.</span></span>

2. <span data-ttu-id="50abb-159">如果您節流，您會看到 hello hive 記錄檔中的 hello HTTP 429 錯誤程式碼。</span><span class="sxs-lookup"><span data-stu-id="50abb-159">If you are getting throttled, you’ll see hello HTTP 429 error code in hello hive log file.</span></span> <span data-ttu-id="50abb-160">hello hive 記錄檔位於 /tmp/&lt;使用者&gt;/hive.log</span><span class="sxs-lookup"><span data-stu-id="50abb-160">hello hive log file is in /tmp/&lt;user&gt;/hive.log</span></span>

## <a name="further-information-on-hive-tuning"></a><span data-ttu-id="50abb-161">關於微調 Hive 的進一步資訊</span><span class="sxs-lookup"><span data-stu-id="50abb-161">Further information on Hive tuning</span></span>

<span data-ttu-id="50abb-162">以下是一些有助於微調 Hive 查詢的部落格︰</span><span class="sxs-lookup"><span data-stu-id="50abb-162">Here are a few blogs that will help tune your Hive queries:</span></span>
* [<span data-ttu-id="50abb-163">在 Hdinsight 中最佳化 Hadoop 的 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="50abb-163">Optimize Hive queries for Hadoop in HDInsight</span></span>](https://azure.microsoft.com/en-us/documentation/articles/hdinsight-hadoop-optimize-hive-query/)
* [<span data-ttu-id="50abb-164">針對 Hive 查詢的效能進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="50abb-164">Troubleshooting Hive query performance</span></span>](https://blogs.msdn.microsoft.com/bigdatasupport/2015/08/13/troubleshooting-hive-query-performance-in-hdinsight-hadoop-cluster/)
* [<span data-ttu-id="50abb-165">Ignite 講解如何將 HDInsight 上的 Hive 最佳化</span><span class="sxs-lookup"><span data-stu-id="50abb-165">Ignite talk on optimize Hive on HDInsight</span></span>](https://channel9.msdn.com/events/Machine-Learning-and-Data-Sciences-Conference/Data-Science-Summit-2016/MSDSS25)
