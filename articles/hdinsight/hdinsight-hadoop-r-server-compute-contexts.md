---
title: "R 伺服器 HDInsight 的 Azure 上的 aaaCompute 內容選項 |Microsoft 文件"
description: "深入了解 hello 不同的計算內容選項可用 toousers 與 HDInsight 上的 R 伺服器"
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
ms.openlocfilehash: b3b0d0cc3caa390797dcff8c73d66cd3ad78bcaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="compute-context-options-for-r-server-on-hdinsight"></a><span data-ttu-id="24b43-103">適用於 HDInsight 上 R 伺服器的計算內容選項</span><span class="sxs-lookup"><span data-stu-id="24b43-103">Compute context options for R Server on HDInsight</span></span>

<span data-ttu-id="24b43-104">Azure HDInsight 上的 Microsoft R Server 控制設定 hello 計算內容執行呼叫的方式。</span><span class="sxs-lookup"><span data-stu-id="24b43-104">Microsoft R Server on Azure HDInsight controls how calls are executed by setting hello compute context.</span></span> <span data-ttu-id="24b43-105">本文概述 hello 選項可用 toospecify 是否及如何執行平行處理跨 hello 邊緣節點或 HDInsight 叢集的核心。</span><span class="sxs-lookup"><span data-stu-id="24b43-105">This article outlines hello options that are available toospecify whether and how execution is parallelized across cores of hello edge node or HDInsight cluster.</span></span>

<span data-ttu-id="24b43-106">hello 邊緣節點的叢集提供方便的位置 tooconnect toohello 叢集和 toorun R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="24b43-106">hello edge node of a cluster provides a convenient place tooconnect toohello cluster and toorun your R scripts.</span></span> <span data-ttu-id="24b43-107">邊緣節點之後，您有 hello 選項執行 hello 平行處理的分散式函式的 ScaleR 跨 hello 核心的 hello 邊緣節點伺服器。</span><span class="sxs-lookup"><span data-stu-id="24b43-107">With an edge node, you have hello option of running hello parallelized distributed functions of ScaleR across hello cores of hello edge node server.</span></span> <span data-ttu-id="24b43-108">您也可以執行這些 hello hello 叢集節點之間使用 ScaleR 的 Hadoop 對應減少或 Spark 計算內容。</span><span class="sxs-lookup"><span data-stu-id="24b43-108">You can also run them across hello nodes of hello cluster by using ScaleR’s Hadoop Map Reduce or Spark compute contexts.</span></span>

## <a name="microsoft-r-server-on-azure-hdinsight"></a><span data-ttu-id="24b43-109">Azure HDInsight 上的 Microsoft R 伺服器</span><span class="sxs-lookup"><span data-stu-id="24b43-109">Microsoft R Server on Azure HDInsight</span></span>
<span data-ttu-id="24b43-110">[Azure HDInsight 上的 Microsoft R Server](hdinsight-hadoop-r-server-overview.md) hello 最新功能，提供 R 為基礎的分析。</span><span class="sxs-lookup"><span data-stu-id="24b43-110">[Microsoft R Server on Azure HDInsight](hdinsight-hadoop-r-server-overview.md) provides hello latest capabilities for R-based analytics.</span></span> <span data-ttu-id="24b43-111">它可以使用儲存在 HDFS 容器中的資料您[Azure Blob](../storage/common/storage-introduction.md "Azure Blob 儲存體")儲存體帳戶、 資料湖存放區或 hello 本機 Linux 檔案系統。</span><span class="sxs-lookup"><span data-stu-id="24b43-111">It can use data that is stored in an HDFS container in your [Azure Blob](../storage/common/storage-introduction.md "Azure Blob storage") storage account, a Data Lake store, or hello local Linux file system.</span></span> <span data-ttu-id="24b43-112">因為 R Server 根據開放原始碼 R，hello R 為基礎的應用程式建置可以套用的任何 hello 8000 + 開放原始碼 R 封裝。</span><span class="sxs-lookup"><span data-stu-id="24b43-112">Since R Server is built on open source R, hello R-based applications you build can apply any of hello 8000+ open source R packages.</span></span> <span data-ttu-id="24b43-113">他們也可以使用中的 hello 常式[RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler)，隨附於 R Server 的 Microsoft 的巨量資料分析封裝。</span><span class="sxs-lookup"><span data-stu-id="24b43-113">They can also use hello routines in [RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler/scaler), Microsoft’s big data analytics package that is included with R Server.</span></span>  

## <a name="compute-contexts-for-an-edge-node"></a><span data-ttu-id="24b43-114">邊緣節點的計算內容</span><span class="sxs-lookup"><span data-stu-id="24b43-114">Compute contexts for an edge node</span></span>
<span data-ttu-id="24b43-115">一般情況下，在 hello 邊緣節點 R 伺服器中執行 R 指令碼 hello R 解譯器中執行，該節點上。</span><span class="sxs-lookup"><span data-stu-id="24b43-115">In general, an R script that's run in R Server on hello edge node runs within hello R interpreter on that node.</span></span> <span data-ttu-id="24b43-116">hello 例外狀況是呼叫 ScaleR 函式的步驟。</span><span class="sxs-lookup"><span data-stu-id="24b43-116">hello exceptions are those steps that call a ScaleR function.</span></span> <span data-ttu-id="24b43-117">hello ScaleR 呼叫都取決於您如何設定 hello ScaleR 計算內容的運算環境中執行。</span><span class="sxs-lookup"><span data-stu-id="24b43-117">hello ScaleR calls run in a compute environment that is determined by how you set hello ScaleR compute context.</span></span>  <span data-ttu-id="24b43-118">當您從邊緣節點執行 R 指令碼時，hello 的 hello 可能的值會計算內容是：</span><span class="sxs-lookup"><span data-stu-id="24b43-118">When you run your R script from an edge node, hello possible values of hello compute context are:</span></span>

- <span data-ttu-id="24b43-119">本機循序 (*‘local’*)</span><span class="sxs-lookup"><span data-stu-id="24b43-119">local sequential (*‘local’*)</span></span>
- <span data-ttu-id="24b43-120">本機平行 (*‘localpar’*)</span><span class="sxs-lookup"><span data-stu-id="24b43-120">local parallel (*‘localpar’*)</span></span>
- <span data-ttu-id="24b43-121">Map Reduce</span><span class="sxs-lookup"><span data-stu-id="24b43-121">Map Reduce</span></span>
- <span data-ttu-id="24b43-122">Spark</span><span class="sxs-lookup"><span data-stu-id="24b43-122">Spark</span></span>

<span data-ttu-id="24b43-123">hello *'local'*和*'localpar'*選項的差異只在於如何**rxExec**執行呼叫。</span><span class="sxs-lookup"><span data-stu-id="24b43-123">hello *‘local’* and *‘localpar’* options differ only in how **rxExec** calls are executed.</span></span> <span data-ttu-id="24b43-124">這些兩個其他 rx 函式呼叫中執行以平行方式分散到所有可用的核心除非另行指定，藉由使用 hello ScaleR **numCoresToUse**選項，例如`rxOptions(numCoresToUse=6)`。</span><span class="sxs-lookup"><span data-stu-id="24b43-124">They both execute other rx-function calls in a parallel manner across all available cores unless specified otherwise through use of hello ScaleR **numCoresToUse** option, for example `rxOptions(numCoresToUse=6)`.</span></span> <span data-ttu-id="24b43-125">平行執行選項提供最佳效能。</span><span class="sxs-lookup"><span data-stu-id="24b43-125">Parallel execution options offer optimal performance.</span></span>

<span data-ttu-id="24b43-126">hello 下表摘要說明各種計算如何執行呼叫的內容選項 tooset hello:</span><span class="sxs-lookup"><span data-stu-id="24b43-126">hello following table summarizes hello various compute context options tooset how calls are executed:</span></span>

| <span data-ttu-id="24b43-127">計算內容</span><span class="sxs-lookup"><span data-stu-id="24b43-127">Compute context</span></span>  | <span data-ttu-id="24b43-128">如何 tooset</span><span class="sxs-lookup"><span data-stu-id="24b43-128">How tooset</span></span>                      | <span data-ttu-id="24b43-129">執行內容</span><span class="sxs-lookup"><span data-stu-id="24b43-129">Execution context</span></span>                        |
| ---------------- | ------------------------------- | ---------------------------------------- |
| <span data-ttu-id="24b43-130">本機循序</span><span class="sxs-lookup"><span data-stu-id="24b43-130">Local sequential</span></span> | <span data-ttu-id="24b43-131">rxSetComputeContext(‘local’)</span><span class="sxs-lookup"><span data-stu-id="24b43-131">rxSetComputeContext(‘local’)</span></span>    | <span data-ttu-id="24b43-132">平行化的執行跨 hello 核心 hello 邊緣節點伺服器，會循序執行的 rxExec 呼叫除外</span><span class="sxs-lookup"><span data-stu-id="24b43-132">Parallelized execution across hello cores of hello edge node server, except for rxExec calls, which are executed serially</span></span> |
| <span data-ttu-id="24b43-133">本機平行</span><span class="sxs-lookup"><span data-stu-id="24b43-133">Local parallel</span></span>   | <span data-ttu-id="24b43-134">rxSetComputeContext(‘localpar’)</span><span class="sxs-lookup"><span data-stu-id="24b43-134">rxSetComputeContext(‘localpar’)</span></span> | <span data-ttu-id="24b43-135">平行化的執行跨 hello 核心 hello 邊緣節點伺服器</span><span class="sxs-lookup"><span data-stu-id="24b43-135">Parallelized execution across hello cores of hello edge node server</span></span> |
| <span data-ttu-id="24b43-136">Spark</span><span class="sxs-lookup"><span data-stu-id="24b43-136">Spark</span></span>            | <span data-ttu-id="24b43-137">RxSpark()</span><span class="sxs-lookup"><span data-stu-id="24b43-137">RxSpark()</span></span>                       | <span data-ttu-id="24b43-138">平行處理分散式經由執行 Spark hello 節點之間的 hello HDI 叢集</span><span class="sxs-lookup"><span data-stu-id="24b43-138">Parallelized distributed execution via Spark across hello nodes of hello HDI cluster</span></span> |
| <span data-ttu-id="24b43-139">Map Reduce</span><span class="sxs-lookup"><span data-stu-id="24b43-139">Map Reduce</span></span>       | <span data-ttu-id="24b43-140">RxHadoopMR()</span><span class="sxs-lookup"><span data-stu-id="24b43-140">RxHadoopMR()</span></span>                    | <span data-ttu-id="24b43-141">平行處理分散式的執行透過對應減少 hello 節點之間的 hello HDI 叢集</span><span class="sxs-lookup"><span data-stu-id="24b43-141">Parallelized distributed execution via Map Reduce across hello nodes of hello HDI cluster</span></span> |

## <a name="guidelines-for-deciding-on-a-compute-context"></a><span data-ttu-id="24b43-142">用於決定計算內容的指導方針</span><span class="sxs-lookup"><span data-stu-id="24b43-142">Guidelines for deciding on a compute context</span></span>

<span data-ttu-id="24b43-143">其中一個 hello 的三個選項選擇提供平行化的執行取決於 hello 本質的分析工作、 hello 大小和 hello 資料的位置。</span><span class="sxs-lookup"><span data-stu-id="24b43-143">Which of hello three options you choose that provide parallelized execution depends on hello nature of your analytics work, hello size, and hello location of your data.</span></span> <span data-ttu-id="24b43-144">沒有任何簡單的公式，告訴您的計算內容 toouse。</span><span class="sxs-lookup"><span data-stu-id="24b43-144">There is no simple formula that tells you which compute context toouse.</span></span> <span data-ttu-id="24b43-145">有，不過，有些可協助您進行 hello 正確的選擇，或至少，幫助您縮小您的選擇，然後再執行基準測試的指導原則。</span><span class="sxs-lookup"><span data-stu-id="24b43-145">There are, however, some guiding principles that can help you make hello right choice, or, at least, help you narrow down your choices before you run a benchmark.</span></span> <span data-ttu-id="24b43-146">這些指導原則包括︰</span><span class="sxs-lookup"><span data-stu-id="24b43-146">These guiding principles include:</span></span>

- <span data-ttu-id="24b43-147">hello 本機 Linux 檔案系統的速度比 HDFS。</span><span class="sxs-lookup"><span data-stu-id="24b43-147">hello local Linux file system is faster than HDFS.</span></span>
- <span data-ttu-id="24b43-148">如果 hello 資料在本機，而且如果它是在 XDF 重複的分析時，速度加快。</span><span class="sxs-lookup"><span data-stu-id="24b43-148">Repeated analyses are faster if hello data is local, and if it's in XDF.</span></span>
- <span data-ttu-id="24b43-149">它是比 toostream 少量的文字資料來源的資料。</span><span class="sxs-lookup"><span data-stu-id="24b43-149">It's preferable toostream small amounts of data from a text data source.</span></span> <span data-ttu-id="24b43-150">如果 hello 資料量大，請將它轉換 tooXDF 分析之前。</span><span class="sxs-lookup"><span data-stu-id="24b43-150">If hello amount of data is larger, convert it tooXDF before analysis.</span></span>
- <span data-ttu-id="24b43-151">hello 的複製或資料流分析的 hello 資料 toohello 邊緣節點的額外負荷變得難以管理的非常大量的資料。</span><span class="sxs-lookup"><span data-stu-id="24b43-151">hello overhead of copying or streaming hello data toohello edge node for analysis becomes unmanageable for very large amounts of data.</span></span>
- <span data-ttu-id="24b43-152">Spark 在 Hadoop 中的分析速度較 Map Reduce 快。</span><span class="sxs-lookup"><span data-stu-id="24b43-152">Spark is faster than Map Reduce for analysis in Hadoop.</span></span>

<span data-ttu-id="24b43-153">指定這些原則，hello 下列各節提供一些一般法則選取的計算內容。</span><span class="sxs-lookup"><span data-stu-id="24b43-153">Given these principles, hello following sections offer some general rules of thumb for selecting a compute context.</span></span>

### <a name="local"></a><span data-ttu-id="24b43-154">本機</span><span class="sxs-lookup"><span data-stu-id="24b43-154">Local</span></span>
* <span data-ttu-id="24b43-155">如果資料 tooanalyze hello 量小，而不需要重複的分析，然後進行串流處理它直接在 hello 分析常式使用*'local'*或*'localpar'*。</span><span class="sxs-lookup"><span data-stu-id="24b43-155">If hello amount of data tooanalyze is small and does not require repeated analysis, then stream it directly into hello analysis routine using *'local'* or *'localpar'*.</span></span>
* <span data-ttu-id="24b43-156">如果 hello 資料 tooanalyze 數量是小型或中型大小，且需要重複的分析，然後將它複製 toohello 本機檔案系統、 匯入它 tooXDF，以及分析透過*'local'*或*'localpar'*。</span><span class="sxs-lookup"><span data-stu-id="24b43-156">If hello amount of data tooanalyze is small or medium-sized and requires repeated analysis, then copy it toohello local file system, import it tooXDF, and analyze it via *'local'* or *'localpar'*.</span></span>

### <a name="hadoop-spark"></a><span data-ttu-id="24b43-157">Hadoop Spark</span><span class="sxs-lookup"><span data-stu-id="24b43-157">Hadoop Spark</span></span>
* <span data-ttu-id="24b43-158">如果 hello 資料 tooanalyze 數量很大，將它匯入 tooa Spark 資料框架使用**RxHiveData**或**RxParquetData**，或在 HDFS tooXDF （除非儲存體問題），並進行分析使用 hello Spark計算內容。</span><span class="sxs-lookup"><span data-stu-id="24b43-158">If hello amount of data tooanalyze is large, then import it tooa Spark DataFrame using **RxHiveData** or **RxParquetData**, or tooXDF in HDFS (unless storage is an issue), and analyze it using hello Spark compute context.</span></span>

### <a name="hadoop-map-reduce"></a><span data-ttu-id="24b43-159">Hadoop Map Reduce</span><span class="sxs-lookup"><span data-stu-id="24b43-159">Hadoop Map Reduce</span></span>
* <span data-ttu-id="24b43-160">如果您遇到 hello Spark 計算內容是無法克服問題，因為它是速度較慢，請使用 hello 對應減少的計算內容。</span><span class="sxs-lookup"><span data-stu-id="24b43-160">Use hello Map Reduce compute context only if you encounter an insurmountable problem with hello Spark compute context since it is generally slower.</span></span>  

## <a name="inline-help-on-rxsetcomputecontext"></a><span data-ttu-id="24b43-161">rxSetComputeContext 的內嵌說明</span><span class="sxs-lookup"><span data-stu-id="24b43-161">Inline help on rxSetComputeContext</span></span>
<span data-ttu-id="24b43-162">如需詳細資訊和範例 ScaleR 的計算內容，請參閱 hello 內嵌在 R 中的說明 hello rxSetComputeContext 方法，例如：</span><span class="sxs-lookup"><span data-stu-id="24b43-162">For more information and examples of ScaleR compute contexts, see hello inline help in R on hello rxSetComputeContext method, for example:</span></span>

    > ?rxSetComputeContext

<span data-ttu-id="24b43-163">您也可以參考 toohello"[ScaleR 分散式運算指南](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)"，而且可從 hello [R 伺服器 MSDN](https://msdn.microsoft.com/library/mt674634.aspx "MSDN 上的 R 伺服器")程式庫。</span><span class="sxs-lookup"><span data-stu-id="24b43-163">You can also refer toohello “[ScaleR Distributed Computing Guide](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)” that's available from hello [R Server MSDN](https://msdn.microsoft.com/library/mt674634.aspx "R Server on MSDN") library.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24b43-164">後續步驟</span><span class="sxs-lookup"><span data-stu-id="24b43-164">Next steps</span></span>
<span data-ttu-id="24b43-165">在本文中，您學可用 toospecify hello 選項是否及如何執行進行平行處理跨 hello 邊緣節點或 HDInsight 叢集的核心。</span><span class="sxs-lookup"><span data-stu-id="24b43-165">In this article, you learned about hello options that are available toospecify whether and how execution is parallelized across cores of hello edge node or HDInsight cluster.</span></span> <span data-ttu-id="24b43-166">toolearn 深入了解如何 toouse R 伺服器與 HDInsight 叢集，請參閱下列主題中的 hello:</span><span class="sxs-lookup"><span data-stu-id="24b43-166">toolearn more about how toouse R Server with HDInsight clusters, see hello following topics:</span></span>

* [<span data-ttu-id="24b43-167">適用於 Hadoop 的 R 伺服器概觀</span><span class="sxs-lookup"><span data-stu-id="24b43-167">Overview of R Server for Hadoop</span></span>](hdinsight-hadoop-r-server-overview.md)
* [<span data-ttu-id="24b43-168">開始使用適用於 Hadoop 的 R 伺服器</span><span class="sxs-lookup"><span data-stu-id="24b43-168">Get started with R Server for Hadoop</span></span>](hdinsight-hadoop-r-server-get-started.md)
* [<span data-ttu-id="24b43-169">新增 RStudio 伺服器 tooHDInsight （如果不在叢集建立期間新增）</span><span class="sxs-lookup"><span data-stu-id="24b43-169">Add RStudio Server tooHDInsight (if not added during cluster creation)</span></span>](hdinsight-hadoop-r-server-install-r-studio.md)
* [<span data-ttu-id="24b43-170">適用於 HDInsight R 伺服器的 Azure 儲存體選項</span><span class="sxs-lookup"><span data-stu-id="24b43-170">Azure Storage options for R Server on HDInsight</span></span>](hdinsight-hadoop-r-server-storage.md)

