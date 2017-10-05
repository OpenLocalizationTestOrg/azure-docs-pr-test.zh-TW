---
title: "適用於 HDInsight 上 R 伺服器的計算內容選項 - Azure | Microsoft Docs"
description: "了解 HDInsight 上 R 伺服器之使用者可用的不同計算內容選項"
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 0deb0b1c-4094-459b-94fc-ec9b774c1f8a
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/19/2017
ms.author: bradsev
ms.openlocfilehash: 47f4441612be4f363ba82cc22b09786a6f3bfdc3
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a><span data-ttu-id="4fb09-103">適用於 HDInsight 上 R 伺服器的計算內容選項</span><span class="sxs-lookup"><span data-stu-id="4fb09-103">Compute context options for R Server on HDInsight</span></span>

<span data-ttu-id="4fb09-104">Azure HDInsight 上的 Microsoft R 伺服器控制如何透過設定計算內容來執行呼叫。</span><span class="sxs-lookup"><span data-stu-id="4fb09-104">Microsoft R Server on Azure HDInsight controls how calls are executed by setting the compute context.</span></span> <span data-ttu-id="4fb09-105">此文章概述可用於指定是否以及如何跨邊緣節點核心或 HDInsight 叢集將執行作業平行化的選項。</span><span class="sxs-lookup"><span data-stu-id="4fb09-105">This article outlines the options that are available to specify whether and how execution is parallelized across cores of the edge node or HDInsight cluster.</span></span>

<span data-ttu-id="4fb09-106">叢集的邊緣節點提供便利的地方，以便連線到叢集以及執行 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="4fb09-106">The edge node of a cluster provides a convenient place to connect to the cluster and to run your R scripts.</span></span> <span data-ttu-id="4fb09-107">有了邊緣節點之後，即可選擇跨邊緣節點伺服器的核心，執行 ScaleR 的平行分散式函數。</span><span class="sxs-lookup"><span data-stu-id="4fb09-107">With an edge node, you have the option of running the parallelized distributed functions of ScaleR across the cores of the edge node server.</span></span> <span data-ttu-id="4fb09-108">您也可以使用 ScaleR 的 Hadoop Map Reduce 或 Spark 計算內容，跨越叢集的節點來執行這些函數。</span><span class="sxs-lookup"><span data-stu-id="4fb09-108">You can also run them across the nodes of the cluster by using ScaleR’s Hadoop Map Reduce or Spark compute contexts.</span></span>

## <a name="microsoft-r-server-on-azure-hdinsight"></a><span data-ttu-id="4fb09-109">Azure HDInsight 上的 Microsoft R 伺服器</span><span class="sxs-lookup"><span data-stu-id="4fb09-109">Microsoft R Server on Azure HDInsight</span></span>
<span data-ttu-id="4fb09-110">[Azure HDInsight 上的 Microsoft R 伺服器](hdinsight-hadoop-r-server-overview.md)可提供最新的 R 型分析功能。</span><span class="sxs-lookup"><span data-stu-id="4fb09-110">[Microsoft R Server on Azure HDInsight](hdinsight-hadoop-r-server-overview.md) provides the latest capabilities for R-based analytics.</span></span> <span data-ttu-id="4fb09-111">它可以使用儲存在 [Azure Blob](../storage/common/storage-introduction.md "Azure Blob 儲存體") 儲存體帳戶、Data Lake Store 或本機 Linux 檔案系統上之 HDFS 容器中的資料。</span><span class="sxs-lookup"><span data-stu-id="4fb09-111">It can use data that is stored in an HDFS container in your [Azure Blob](../storage/common/storage-introduction.md "Azure Blob storage") storage account, a Data Lake store, or the local Linux file system.</span></span> <span data-ttu-id="4fb09-112">R 伺服器是根據開放原始碼 R 所建置，因此您建置的 R 型應用程式可以套用 8000 多個開放原始碼 R 套件中的任何一個。</span><span class="sxs-lookup"><span data-stu-id="4fb09-112">Since R Server is built on open source R, the R-based applications you build can apply any of the 8000+ open source R packages.</span></span> <span data-ttu-id="4fb09-113">它們也可以使用 [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler) (R 伺服器隨附的 Microsoft 巨量資料分析套件) 中的常式。</span><span class="sxs-lookup"><span data-stu-id="4fb09-113">They can also use the routines in [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), Microsoft’s big data analytics package that is included with R Server.</span></span>  

## <a name="compute-contexts-for-an-edge-node"></a><span data-ttu-id="4fb09-114">邊緣節點的計算內容</span><span class="sxs-lookup"><span data-stu-id="4fb09-114">Compute contexts for an edge node</span></span>
<span data-ttu-id="4fb09-115">一般而言，在邊緣節點上 R 伺服器中執行的 R 指令碼會在該節點上的 R 解譯器內執行。</span><span class="sxs-lookup"><span data-stu-id="4fb09-115">In general, an R script that's run in R Server on the edge node runs within the R interpreter on that node.</span></span> <span data-ttu-id="4fb09-116">但呼叫 ScaleR 函數的步驟則屬例外。</span><span class="sxs-lookup"><span data-stu-id="4fb09-116">The exceptions are those steps that call a ScaleR function.</span></span> <span data-ttu-id="4fb09-117">ScaleR 呼叫會在計算環境中執行，該環境是由您設定 ScaleR 計算內容的方式所決定。</span><span class="sxs-lookup"><span data-stu-id="4fb09-117">The ScaleR calls run in a compute environment that is determined by how you set the ScaleR compute context.</span></span>  <span data-ttu-id="4fb09-118">當您從邊緣節點執行 R 指令碼時，可能的計算內容值為：</span><span class="sxs-lookup"><span data-stu-id="4fb09-118">When you run your R script from an edge node, the possible values of the compute context are:</span></span>

- <span data-ttu-id="4fb09-119">本機循序 (*‘local’*)</span><span class="sxs-lookup"><span data-stu-id="4fb09-119">local sequential (*‘local’*)</span></span>
- <span data-ttu-id="4fb09-120">本機平行 (*‘localpar’*)</span><span class="sxs-lookup"><span data-stu-id="4fb09-120">local parallel (*‘localpar’*)</span></span>
- <span data-ttu-id="4fb09-121">Map Reduce</span><span class="sxs-lookup"><span data-stu-id="4fb09-121">Map Reduce</span></span>
- <span data-ttu-id="4fb09-122">Spark</span><span class="sxs-lookup"><span data-stu-id="4fb09-122">Spark</span></span>

<span data-ttu-id="4fb09-123">*‘local’* 和 *‘localpar’* 選項的差別只在於執行 **rxExec** 呼叫的方式。</span><span class="sxs-lookup"><span data-stu-id="4fb09-123">The *‘local’* and *‘localpar’* options differ only in how **rxExec** calls are executed.</span></span> <span data-ttu-id="4fb09-124">它們都會在所有可用的核心之間，以平行方式執行其他的 rx 函數呼叫，除非已指定，否則皆使用 ScaleR **numCoresToUse** 選項，例如 `rxOptions(numCoresToUse=6)`。</span><span class="sxs-lookup"><span data-stu-id="4fb09-124">They both execute other rx-function calls in a parallel manner across all available cores unless specified otherwise through use of the ScaleR **numCoresToUse** option, for example `rxOptions(numCoresToUse=6)`.</span></span> <span data-ttu-id="4fb09-125">平行執行選項提供最佳效能。</span><span class="sxs-lookup"><span data-stu-id="4fb09-125">Parallel execution options offer optimal performance.</span></span>

<span data-ttu-id="4fb09-126">下表摘要說明各種不同的計算內容選項來設定呼叫的執行方式：</span><span class="sxs-lookup"><span data-stu-id="4fb09-126">The following table summarizes the various compute context options to set how calls are executed:</span></span>

| <span data-ttu-id="4fb09-127">計算內容</span><span class="sxs-lookup"><span data-stu-id="4fb09-127">Compute context</span></span>  | <span data-ttu-id="4fb09-128">設定方式</span><span class="sxs-lookup"><span data-stu-id="4fb09-128">How to set</span></span>                      | <span data-ttu-id="4fb09-129">執行內容</span><span class="sxs-lookup"><span data-stu-id="4fb09-129">Execution context</span></span>                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| <span data-ttu-id="4fb09-130">本機循序</span><span class="sxs-lookup"><span data-stu-id="4fb09-130">Local sequential</span></span> | <span data-ttu-id="4fb09-131">rxSetComputeContext(‘local’)</span><span class="sxs-lookup"><span data-stu-id="4fb09-131">rxSetComputeContext(‘local’)</span></span>    | <span data-ttu-id="4fb09-132">跨邊緣節點伺服器的核心平行執行，只有 rxExec 為循序執行</span><span class="sxs-lookup"><span data-stu-id="4fb09-132">Parallelized execution across the cores of the edge node server, except for rxExec calls, which are executed serially</span></span> |
| <span data-ttu-id="4fb09-133">本機平行</span><span class="sxs-lookup"><span data-stu-id="4fb09-133">Local parallel</span></span>   | <span data-ttu-id="4fb09-134">rxSetComputeContext(‘localpar’)</span><span class="sxs-lookup"><span data-stu-id="4fb09-134">rxSetComputeContext(‘localpar’)</span></span> | <span data-ttu-id="4fb09-135">跨邊緣節點伺服器的核心平行執行</span><span class="sxs-lookup"><span data-stu-id="4fb09-135">Parallelized execution across the cores of the edge node server</span></span> |
| <span data-ttu-id="4fb09-136">Spark</span><span class="sxs-lookup"><span data-stu-id="4fb09-136">Spark</span></span>            | <span data-ttu-id="4fb09-137">RxSpark()</span><span class="sxs-lookup"><span data-stu-id="4fb09-137">RxSpark()</span></span>                       | <span data-ttu-id="4fb09-138">跨 HDI 叢集的節點透過 Spark 平行處理分散式執行</span><span class="sxs-lookup"><span data-stu-id="4fb09-138">Parallelized distributed execution via Spark across the nodes of the HDI cluster</span></span> |
| <span data-ttu-id="4fb09-139">Map Reduce</span><span class="sxs-lookup"><span data-stu-id="4fb09-139">Map Reduce</span></span>       | <span data-ttu-id="4fb09-140">RxHadoopMR()</span><span class="sxs-lookup"><span data-stu-id="4fb09-140">RxHadoopMR()</span></span>                    | <span data-ttu-id="4fb09-141">跨 HDI 叢集的節點透過 Map Reduce 平行處理分散式執行</span><span class="sxs-lookup"><span data-stu-id="4fb09-141">Parallelized distributed execution via Map Reduce across the nodes of the HDI cluster</span></span> |

## <a name="guidelines-for-deciding-on-a-compute-context"></a><span data-ttu-id="4fb09-142">用於決定計算內容的指導方針</span><span class="sxs-lookup"><span data-stu-id="4fb09-142">Guidelines for deciding on a compute context</span></span>

<span data-ttu-id="4fb09-143">在這三個提供平行執行的選項中，選擇哪個選項取決於資料的分析工作本質、大小與位置。</span><span class="sxs-lookup"><span data-stu-id="4fb09-143">Which of the three options you choose that provide parallelized execution depends on the nature of your analytics work, the size, and the location of your data.</span></span> <span data-ttu-id="4fb09-144">沒有任何簡單的公式可告訴您該使用哪個計算內容。</span><span class="sxs-lookup"><span data-stu-id="4fb09-144">There is no simple formula that tells you which compute context to use.</span></span> <span data-ttu-id="4fb09-145">不過，有一些指導原則可協助您做出正確的選擇，或至少幫助您縮小選擇範圍，然後再執行效能評定。</span><span class="sxs-lookup"><span data-stu-id="4fb09-145">There are, however, some guiding principles that can help you make the right choice, or, at least, help you narrow down your choices before you run a benchmark.</span></span> <span data-ttu-id="4fb09-146">這些指導原則包括︰</span><span class="sxs-lookup"><span data-stu-id="4fb09-146">These guiding principles include:</span></span>

- <span data-ttu-id="4fb09-147">本機 Linux 檔案系統比 HDFS 還快。</span><span class="sxs-lookup"><span data-stu-id="4fb09-147">The local Linux file system is faster than HDFS.</span></span>
- <span data-ttu-id="4fb09-148">如果資料位於本機，且是 XDF 格式，則重複分析會比較快。</span><span class="sxs-lookup"><span data-stu-id="4fb09-148">Repeated analyses are faster if the data is local, and if it's in XDF.</span></span>
- <span data-ttu-id="4fb09-149">建議您從文字資料來源串流少量資料。</span><span class="sxs-lookup"><span data-stu-id="4fb09-149">It's preferable to stream small amounts of data from a text data source.</span></span> <span data-ttu-id="4fb09-150">如果資料量比較大，請在分析之前先將它轉換為 XDF。</span><span class="sxs-lookup"><span data-stu-id="4fb09-150">If the amount of data is larger, convert it to XDF before analysis.</span></span>
- <span data-ttu-id="4fb09-151">對於非常大量的資料，將資料複製或串流至邊緣節點以進行分析的額外負荷會變得難以管理。</span><span class="sxs-lookup"><span data-stu-id="4fb09-151">The overhead of copying or streaming the data to the edge node for analysis becomes unmanageable for very large amounts of data.</span></span>
- <span data-ttu-id="4fb09-152">Spark 在 Hadoop 中的分析速度較 Map Reduce 快。</span><span class="sxs-lookup"><span data-stu-id="4fb09-152">Spark is faster than Map Reduce for analysis in Hadoop.</span></span>

<span data-ttu-id="4fb09-153">在給定這些原則的情況下，以下各節提供一些有關選取計算內容的一般準則。</span><span class="sxs-lookup"><span data-stu-id="4fb09-153">Given these principles, the following sections offer some general rules of thumb for selecting a compute context.</span></span>

### <a name="local"></a><span data-ttu-id="4fb09-154">本機</span><span class="sxs-lookup"><span data-stu-id="4fb09-154">Local</span></span>
* <span data-ttu-id="4fb09-155">如果要分析的資料量很小，而且不需要重複分析，請使用 *'local'* 或 *'localpar'* 直接將它串流到分析常式。</span><span class="sxs-lookup"><span data-stu-id="4fb09-155">If the amount of data to analyze is small and does not require repeated analysis, then stream it directly into the analysis routine using *'local'* or *'localpar'*.</span></span>
* <span data-ttu-id="4fb09-156">如果要分析的資料量很小或是中等大小，而且需要重複分析，請將它複製到本機檔案系統、匯入至 XDF，然後透過 *'local'* 或 *'localpar'* 分析。</span><span class="sxs-lookup"><span data-stu-id="4fb09-156">If the amount of data to analyze is small or medium-sized and requires repeated analysis, then copy it to the local file system, import it to XDF, and analyze it via *'local'* or *'localpar'*.</span></span>

### <a name="hadoop-spark"></a><span data-ttu-id="4fb09-157">Hadoop Spark</span><span class="sxs-lookup"><span data-stu-id="4fb09-157">Hadoop Spark</span></span>
* <span data-ttu-id="4fb09-158">如果要分析的資料量很大，請使用 **RxHiveData** 或 **RxParquetData** 將它匯入到 Spark DataFrame，或匯入到 HDFS 中的 XDF (除非儲存體會是問題)，然後使用 Spark 計算內容分析。</span><span class="sxs-lookup"><span data-stu-id="4fb09-158">If the amount of data to analyze is large, then import it to a Spark DataFrame using **RxHiveData** or **RxParquetData**, or to XDF in HDFS (unless storage is an issue), and analyze it using the Spark compute context.</span></span>

### <a name="hadoop-map-reduce"></a><span data-ttu-id="4fb09-159">Hadoop Map Reduce</span><span class="sxs-lookup"><span data-stu-id="4fb09-159">Hadoop Map Reduce</span></span>
* <span data-ttu-id="4fb09-160">只有在您使用 Spark 計算內容發生無法克服的問題時才使用 Map Reduce 計算內容，因為它的速度通常會比較慢。</span><span class="sxs-lookup"><span data-stu-id="4fb09-160">Use the Map Reduce compute context only if you encounter an insurmountable problem with the Spark compute context since it is generally slower.</span></span>  

## <a name="inline-help-on-rxsetcomputecontext"></a><span data-ttu-id="4fb09-161">rxSetComputeContext 的內嵌說明</span><span class="sxs-lookup"><span data-stu-id="4fb09-161">Inline help on rxSetComputeContext</span></span>
<span data-ttu-id="4fb09-162">如需 ScaleR 計算內容的詳細資訊和範例，請參閱 R 中有關 rxSetComputeContext 方法的內嵌說明，例如︰</span><span class="sxs-lookup"><span data-stu-id="4fb09-162">For more information and examples of ScaleR compute contexts, see the inline help in R on the rxSetComputeContext method, for example:</span></span>

    > ?rxSetComputeContext

<span data-ttu-id="4fb09-163">您也可以參閱可從 [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "MSDN 上的 R 伺服器") 文件庫取得的 [ScaleR 分散式計算指南](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing) \(英文\)。</span><span class="sxs-lookup"><span data-stu-id="4fb09-163">You can also refer to the “[ScaleR Distributed Computing Guide](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)” that's available from the [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server on MSDN") library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4fb09-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4fb09-164">Next steps</span></span>
<span data-ttu-id="4fb09-165">在此文章中，您可以了解可用於指定是否以及如何跨邊緣節點核心或 HDInsight 叢集將執行作業平行化的選項。</span><span class="sxs-lookup"><span data-stu-id="4fb09-165">In this article, you learned about the options that are available to specify whether and how execution is parallelized across cores of the edge node or HDInsight cluster.</span></span> <span data-ttu-id="4fb09-166">若要深入了解如何搭配 HDInsight 叢集使用 R 伺服器，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="4fb09-166">To learn more about how to use R Server with HDInsight clusters, see the following topics:</span></span>

* [<span data-ttu-id="4fb09-167">適用於 Hadoop 的 R 伺服器概觀</span><span class="sxs-lookup"><span data-stu-id="4fb09-167">Overview of R Server for Hadoop</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="4fb09-168">開始使用適用於 Hadoop 的 R 伺服器</span><span class="sxs-lookup"><span data-stu-id="4fb09-168">Get started with R Server for Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="4fb09-169">將 RStudio Server 新增至 HDInsight (若未在建立叢集期間新增)</span><span class="sxs-lookup"><span data-stu-id="4fb09-169">Add RStudio Server to HDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="4fb09-170">適用於 HDInsight 上 R 伺服器的 Azure 儲存體選項</span><span class="sxs-lookup"><span data-stu-id="4fb09-170">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

