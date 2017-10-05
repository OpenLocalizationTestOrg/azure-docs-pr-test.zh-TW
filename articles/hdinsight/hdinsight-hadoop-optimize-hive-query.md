---
title: "將 Azure HDInsight 中的 Hive 查詢最佳化 | Microsoft Docs"
description: "了解如何在 HDInsight 中最佳化 Hadoop 的 Hive 查詢。"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d6174c08-06aa-42ac-8e9b-8b8718d9978e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/26/2016
ms.author: jgao
ms.openlocfilehash: edbf797e6277a65b5311e4939f5ab72776b11557
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="44507-103">將 Azure HDInsight 中的 Hive 查詢最佳化</span><span class="sxs-lookup"><span data-stu-id="44507-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="44507-104">根據預設，Hadoop 叢集不會為了效能進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="44507-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="44507-105">本文涵蓋幾個最常見 Hive 效能最佳化方法，您可將這些方法套用於我們的查詢。</span><span class="sxs-lookup"><span data-stu-id="44507-105">This article covers some most common Hive performance optimization methods that you can apply to your queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="44507-106">相應放大背景工作節點</span><span class="sxs-lookup"><span data-stu-id="44507-106">Scale out worker nodes</span></span>

<span data-ttu-id="44507-107">增加叢集中的背景工作節點數目，即可運用更多平行執行的對應器和歸納器。</span><span class="sxs-lookup"><span data-stu-id="44507-107">Increasing the number of worker nodes in a cluster can leverage more mappers and reducers to be run in parallel.</span></span> <span data-ttu-id="44507-108">在 HDInsight 中您有兩種方法可相應放大：</span><span class="sxs-lookup"><span data-stu-id="44507-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="44507-109">在佈建階段，您可以使用 Azure 入口網站、Azure PowerShell 或跨平台命令列介面來指定背景工作節點的數目。</span><span class="sxs-lookup"><span data-stu-id="44507-109">At the provision time, you can specify the number of worker nodes using the Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="44507-110">如需詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="44507-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="44507-111">下列畫面顯示 Azure 入口網站上的背景工作節點組態：</span><span class="sxs-lookup"><span data-stu-id="44507-111">The following screenshot shows the worker node configuration on the Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="44507-113">在執行階段，您可以也相應放大叢集，而不需重新一個叢集：</span><span class="sxs-lookup"><span data-stu-id="44507-113">At the run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="44507-115">如需 HDInsight 支援之各種虛擬機器的相關資訊，請參閱 [HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="44507-115">For more information about the different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="44507-116">啟用 Tez</span><span class="sxs-lookup"><span data-stu-id="44507-116">Enable Tez</span></span>

<span data-ttu-id="44507-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) 是 MapReduce 引擎的替代執行引擎：</span><span class="sxs-lookup"><span data-stu-id="44507-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine to the MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="44507-119">Tez 比較迅速，因為：</span><span class="sxs-lookup"><span data-stu-id="44507-119">Tez is faster because:</span></span>

* <span data-ttu-id="44507-120">**在 MapReduce 引擎中執行有向非循環圖 (DAG) 作為單一作業**。</span><span class="sxs-lookup"><span data-stu-id="44507-120">**Execute Directed Acyclic Graph (DAG) as a single job in the MapReduce engine**.</span></span> <span data-ttu-id="44507-121">DAG 要求每一組對應程式後面有一組歸納器。</span><span class="sxs-lookup"><span data-stu-id="44507-121">The DAG requires each set of mappers to be followed by one set of reducers.</span></span> <span data-ttu-id="44507-122">這會導致多個 MapReduce 工作針對每個 Hive 查詢而分拆。</span><span class="sxs-lookup"><span data-stu-id="44507-122">This causes multiple MapReduce jobs to be spun off for each Hive query.</span></span> <span data-ttu-id="44507-123">Tez 沒有此種條件約束，並可將複雜的 DAG 當作一項工作處理，因而將工作啟動的額外負荷降至最低。</span><span class="sxs-lookup"><span data-stu-id="44507-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="44507-124">**避免不必要的寫入**。</span><span class="sxs-lookup"><span data-stu-id="44507-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="44507-125">由於 MapReduce 引擎中有多項作業針對相同的 Hive 查詢運作，每項作業的輸出都會寫入中繼資料的 HDFS。</span><span class="sxs-lookup"><span data-stu-id="44507-125">Due to multiple jobs being spun for the same Hive query in the MapReduce engine, the output of each job is written to HDFS for intermediate data.</span></span> <span data-ttu-id="44507-126">Tez 可以將每個 Hive 查詢的工作數目降至最低，所以能夠避免不必要的寫入。</span><span class="sxs-lookup"><span data-stu-id="44507-126">Since Tez minimizes number of jobs for each Hive query it is able to avoid unnecessary write.</span></span>
* <span data-ttu-id="44507-127">**將啟動延遲最小化**。</span><span class="sxs-lookup"><span data-stu-id="44507-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="44507-128">Tez 會減少需要啟動的對應器數目，同時提升整個最佳化，因此較能夠將啟動延遲降到最低。</span><span class="sxs-lookup"><span data-stu-id="44507-128">Tez is better able to minimize start-up delay by reducing the number of mappers it needs to start and also improving optimization throughout.</span></span>
* <span data-ttu-id="44507-129">**重複使用容器**。</span><span class="sxs-lookup"><span data-stu-id="44507-129">**Reuses containers**.</span></span> <span data-ttu-id="44507-130">Tez 會儘可能重複使用容器，確保減少因為啟動容器而產生的延遲。</span><span class="sxs-lookup"><span data-stu-id="44507-130">Whenever possible Tez is able to reuse containers to ensure that latency due to starting up containers is reduced.</span></span>
* <span data-ttu-id="44507-131">**連續最佳化技巧**。</span><span class="sxs-lookup"><span data-stu-id="44507-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="44507-132">習慣上，是在編譯階段進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="44507-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="44507-133">但是有更多關於輸入的資訊可用，所以在執行階段進行最佳化比較理想。</span><span class="sxs-lookup"><span data-stu-id="44507-133">However more information about the inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="44507-134">Tez 會使用連續最佳化技巧，進一步在執行階段將計劃最佳化。</span><span class="sxs-lookup"><span data-stu-id="44507-134">Tez uses continuous optimization techniques that allows it to optimize the plan further into the runtime phase.</span></span>

<span data-ttu-id="44507-135">如需這些概念的詳細資訊，請參閱 [Apache Tez](http://hortonworks.com/hadoop/tez/)。</span><span class="sxs-lookup"><span data-stu-id="44507-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="44507-136">在查詢的前面加上以下設定，即可啟用任何 Hive 查詢 Tez：</span><span class="sxs-lookup"><span data-stu-id="44507-136">You can make any Hive query Tez enabled by prefixing the query with the setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="44507-137">Linux 的 HDInsight 叢集預設會啟用 Tez。</span><span class="sxs-lookup"><span data-stu-id="44507-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="44507-138">Hive 分割</span><span class="sxs-lookup"><span data-stu-id="44507-138">Hive partitioning</span></span>

<span data-ttu-id="44507-139">I/O 作業是執行 Hive 查詢的主要效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="44507-139">I/O operation is the major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="44507-140">如果可以減少需要讀取的資料量，即可改善效能。</span><span class="sxs-lookup"><span data-stu-id="44507-140">The performance can be improved if the amount of data that needs to be read can be reduced.</span></span> <span data-ttu-id="44507-141">根據預設，Hive 查詢會掃描整個 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="44507-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="44507-142">這很適合資料表掃描之類的查詢。</span><span class="sxs-lookup"><span data-stu-id="44507-142">This is great for queries like table scans.</span></span> <span data-ttu-id="44507-143">但是，對於只需要掃描少量資料的查詢 (例如具有篩選的查詢)，這種行為就會產生不必要的額外負荷。</span><span class="sxs-lookup"><span data-stu-id="44507-143">However for queries that only need to scan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="44507-144">Hive 分割可讓 Hive 查詢只存取 Hive 資料表中所需的資料量。</span><span class="sxs-lookup"><span data-stu-id="44507-144">Hive partitioning allows Hive queries to access only the necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="44507-145">Hive 分割的實作方法是將未經處理的資料重新整理成新的目錄，而每個分割區都有自己的目錄 - 其中的分割區是由使用者定義。</span><span class="sxs-lookup"><span data-stu-id="44507-145">Hive partitioning is implemented by reorganizing the raw data into new directories with each partition having its own directory - where the partition is defined by the user.</span></span> <span data-ttu-id="44507-146">下圖說明如何依據 *年度*資料行來分割 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="44507-146">The following diagram illustrates partitioning a Hive table by the column *Year*.</span></span> <span data-ttu-id="44507-147">每年都會建立新的目錄。</span><span class="sxs-lookup"><span data-stu-id="44507-147">A new directory is created for each year.</span></span>

![分割][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="44507-149">一些分割考量：</span><span class="sxs-lookup"><span data-stu-id="44507-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="44507-150">**請勿分割不足** - 依據只有少數幾個值的資料行進行分割，可能會造成很少的分割區。</span><span class="sxs-lookup"><span data-stu-id="44507-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="44507-151">例如，依據性別進行分割，只會建立兩個分割區 (男性和女性)，因此只會降低最多一半的延遲。</span><span class="sxs-lookup"><span data-stu-id="44507-151">For example, partitioning on gender only creates two partitions to be created (male and female), thus only reduce the latency by a maximum of half.</span></span>
* <span data-ttu-id="44507-152">**請勿過度分割** - 另一方面，在具有唯一值 (例如，使用者識別碼) 的資料行建立分割區會造成多個分割區。</span><span class="sxs-lookup"><span data-stu-id="44507-152">**Do not over partition** - On the other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="44507-153">過度分割會在叢集 namenode 上造成太多壓力，因為它必須處理大量目錄。</span><span class="sxs-lookup"><span data-stu-id="44507-153">Over partition causes much stress on the cluster namenode as it has to handle the large number of directories.</span></span>
* <span data-ttu-id="44507-154">**避免資料扭曲** - 明智地選擇分割索引鍵，讓所有分割區的大小平均。</span><span class="sxs-lookup"><span data-stu-id="44507-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="44507-155">例如，依據 *州* 進行分割可能造成加州的記錄數目幾乎是佛蒙特州的記錄數目的 30 倍 (因為人口差異)。</span><span class="sxs-lookup"><span data-stu-id="44507-155">An example is partitioning on *State* may cause the number of records under California to be almost 30x that of Vermont due to the difference in population.</span></span>

<span data-ttu-id="44507-156">若要建立分割資料表，請使用 *Partitioned By* 子句：</span><span class="sxs-lookup"><span data-stu-id="44507-156">To create a partition table, use the *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="44507-157">建立分割資料表後，您可以建立靜態分割或動態分割。</span><span class="sxs-lookup"><span data-stu-id="44507-157">Once the partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="44507-158">**靜態分割** 表示您已在適當的目錄中將資料分區，而且可以手動要求以目錄位置為基礎的 Hive 分割區。</span><span class="sxs-lookup"><span data-stu-id="44507-158">**Static partitioning** means that you have already sharded data in the appropriate directories and you can ask Hive partitions manually based on the directory location.</span></span> <span data-ttu-id="44507-159">下列範例為程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="44507-159">The following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="44507-160">**動態分割** 表示您要 Hive 為您自動建立分割區。</span><span class="sxs-lookup"><span data-stu-id="44507-160">**Dynamic partitioning** means that you want Hive to create partitions automatically for you.</span></span> <span data-ttu-id="44507-161">我們已從暫存資料表建立分割資料表，所以我們只需要將資料插入至分割資料表：</span><span class="sxs-lookup"><span data-stu-id="44507-161">Since we have already created the partitioning table from the staging table, all we need to do is insert data to the partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="44507-162">如需詳細資訊，請參閱 [分割的資料表](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables)。</span><span class="sxs-lookup"><span data-stu-id="44507-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-the-orcfile-format"></a><span data-ttu-id="44507-163">使用 ORCFile 格式</span><span class="sxs-lookup"><span data-stu-id="44507-163">Use the ORCFile format</span></span>
<span data-ttu-id="44507-164">Hive 支援不同的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="44507-164">Hive supports different file formats.</span></span> <span data-ttu-id="44507-165">例如：</span><span class="sxs-lookup"><span data-stu-id="44507-165">For example:</span></span>

* <span data-ttu-id="44507-166">**文字**：這是預設檔案格式，適用於大部分的案例</span><span class="sxs-lookup"><span data-stu-id="44507-166">**Text**: this is the default file format and works with most scenarios</span></span>
* <span data-ttu-id="44507-167">**Avro**：適用於互通性案例</span><span class="sxs-lookup"><span data-stu-id="44507-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="44507-168">**ORC/Parquet**：最適合處理效能</span><span class="sxs-lookup"><span data-stu-id="44507-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="44507-169">ORC (最佳化的資料列單欄式) 格式是儲存 Hive 資料的高效率方式。</span><span class="sxs-lookup"><span data-stu-id="44507-169">ORC (Optimized Row Columnar) format is a highly efficient way to store Hive data.</span></span> <span data-ttu-id="44507-170">相較於其他格式，ORC 具有下列優點：</span><span class="sxs-lookup"><span data-stu-id="44507-170">Compared to other formats, ORC has the following advantages:</span></span>

* <span data-ttu-id="44507-171">支援複雜的類型，包括 DateTime 和複雜和半結構化類型</span><span class="sxs-lookup"><span data-stu-id="44507-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="44507-172">高達 70% 的壓縮</span><span class="sxs-lookup"><span data-stu-id="44507-172">up to 70% compression</span></span>
* <span data-ttu-id="44507-173">每 10,000 個資料列的索引可讓您略過一些資料列</span><span class="sxs-lookup"><span data-stu-id="44507-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="44507-174">執行階段的執行大幅減少</span><span class="sxs-lookup"><span data-stu-id="44507-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="44507-175">若要啟用 ORC 格式，請先使用子句 *Stored as ORC*建立資料表：</span><span class="sxs-lookup"><span data-stu-id="44507-175">To enable ORC format, you first create a table with the clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="44507-176">接著，將資料從暫存資料表插入至 ORC 資料表。</span><span class="sxs-lookup"><span data-stu-id="44507-176">Next, you insert data to the ORC table from the staging table.</span></span> <span data-ttu-id="44507-177">例如：</span><span class="sxs-lookup"><span data-stu-id="44507-177">For example:</span></span>

    INSERT INTO TABLE lineitem_orc
    SELECT L_ORDERKEY as L_ORDERKEY, 
           L_PARTKEY as L_PARTKEY , 
           L_SUPPKEY as L_SUPPKEY,
           L_LINENUMBER as L_LINENUMBER,
            L_QUANTITY as L_QUANTITY, 
           L_EXTENDEDPRICE as L_EXTENDEDPRICE,
           L_DISCOUNT as L_DISCOUNT,
           L_TAX as L_TAX,
           L_RETURNFLAG as L_RETURNFLAG,
           L_LINESTATUS as L_LINESTATUS,
           L_SHIPDATE as L_SHIPDATE,
           L_COMMITDATE as L_COMMITDATE,
           L_RECEIPTDATE as L_RECEIPTDATE, 
           L_SHIPINSTRUCT as L_SHIPINSTRUCT,
           L_SHIPMODE as L_SHIPMODE,
           L_COMMENT as L_COMMENT
    FROM lineitem;

<span data-ttu-id="44507-178">您可以在 [這裡](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC)進一步了解 ORC 格式。</span><span class="sxs-lookup"><span data-stu-id="44507-178">You can read more on the ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="44507-179">向量化</span><span class="sxs-lookup"><span data-stu-id="44507-179">Vectorization</span></span>

<span data-ttu-id="44507-180">向量化可讓 Hive 以批次方式同時處理 1024 個資料列，而不是一次處理一個資料列。</span><span class="sxs-lookup"><span data-stu-id="44507-180">Vectorization allows Hive to process a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="44507-181">這表示，因為需要執行的內部程式碼較少，所以簡單的作業會更快完成。</span><span class="sxs-lookup"><span data-stu-id="44507-181">It means that simple operations are done faster because less internal code needs to run.</span></span>

<span data-ttu-id="44507-182">若要啟用向量化，請在 Hive 查詢的前面加上以下列設定：</span><span class="sxs-lookup"><span data-stu-id="44507-182">To enable vectorization prefix your Hive query with the following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="44507-183">如需詳細資訊，請參閱 [向量化查詢執行](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution)。</span><span class="sxs-lookup"><span data-stu-id="44507-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="44507-184">其他最佳化方法</span><span class="sxs-lookup"><span data-stu-id="44507-184">Other optimization methods</span></span>
<span data-ttu-id="44507-185">您有更多最佳化方法可以考慮，例如：</span><span class="sxs-lookup"><span data-stu-id="44507-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="44507-186">**Hive 值區：** 能將大型資料集叢集化或分段以最佳化查詢效能的技術。</span><span class="sxs-lookup"><span data-stu-id="44507-186">**Hive bucketing:** a technique that allows to cluster or segment large sets of data to optimize query performance.</span></span>
* <span data-ttu-id="44507-187">**聯結最佳化：** Hive 的查詢執行計劃最佳化，可改善聯結的效率並減少使用者提示的需求。</span><span class="sxs-lookup"><span data-stu-id="44507-187">**Join optimization:** optimization of Hive's query execution planning to improve the efficiency of joins and reduce the need for user hints.</span></span> <span data-ttu-id="44507-188">如需詳細資訊，請參閱 [聯結最佳化](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization)。</span><span class="sxs-lookup"><span data-stu-id="44507-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="44507-189">**增加歸納器**。</span><span class="sxs-lookup"><span data-stu-id="44507-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44507-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="44507-190">Next steps</span></span>
<span data-ttu-id="44507-191">在本文中，您學到幾種常見的 Hive 查詢最佳化方法。</span><span class="sxs-lookup"><span data-stu-id="44507-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="44507-192">若要深入了解，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="44507-192">To learn more, see the following articles:</span></span>

* [<span data-ttu-id="44507-193">在 HDInsight 中使用 Apache Hive</span><span class="sxs-lookup"><span data-stu-id="44507-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="44507-194">在 HDInsight 中使用 Hive 分析航班延誤資料</span><span class="sxs-lookup"><span data-stu-id="44507-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="44507-195">在 HDInsight 中使用 Hive 分析 Twitter 資料</span><span class="sxs-lookup"><span data-stu-id="44507-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="44507-196">在 HDInsight 的 Hadoop 上使用 Hive 查詢主控台分析感應器資料</span><span class="sxs-lookup"><span data-stu-id="44507-196">Analyze sensor data using the Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="44507-197">使用 HDInsight 上的 Hive 分析網站的記錄</span><span class="sxs-lookup"><span data-stu-id="44507-197">Use Hive with HDInsight to analyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
