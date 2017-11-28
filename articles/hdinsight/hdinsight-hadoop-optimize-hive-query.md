---
title: "Azure HDInsight aaaOptimize Hive 查詢 |Microsoft 文件"
description: "了解如何 toooptimize 您 Hive 查詢在 HDInsight Hadoop。"
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
ms.openlocfilehash: d27f8100e1e9f4823040ff9f693e7b78d6192c6e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-hive-queries-in-azure-hdinsight"></a><span data-ttu-id="336ad-103">將 Azure HDInsight 中的 Hive 查詢最佳化</span><span class="sxs-lookup"><span data-stu-id="336ad-103">Optimize Hive queries in Azure HDInsight</span></span>

<span data-ttu-id="336ad-104">根據預設，Hadoop 叢集不會為了效能進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="336ad-104">By default, Hadoop clusters are not optimized for performance.</span></span> <span data-ttu-id="336ad-105">本文涵蓋您可以套用 tooyour 查詢一些最常見 Hive 效能最佳化方法。</span><span class="sxs-lookup"><span data-stu-id="336ad-105">This article covers some most common Hive performance optimization methods that you can apply tooyour queries.</span></span>

## <a name="scale-out-worker-nodes"></a><span data-ttu-id="336ad-106">相應放大背景工作節點</span><span class="sxs-lookup"><span data-stu-id="336ad-106">Scale out worker nodes</span></span>

<span data-ttu-id="336ad-107">增加 hello 叢集中的背景工作角色節點的數目可以利用多個自行和 reducers toobe 以平行方式執行。</span><span class="sxs-lookup"><span data-stu-id="336ad-107">Increasing hello number of worker nodes in a cluster can leverage more mappers and reducers toobe run in parallel.</span></span> <span data-ttu-id="336ad-108">在 HDInsight 中您有兩種方法可相應放大：</span><span class="sxs-lookup"><span data-stu-id="336ad-108">There are two ways you can increase scale out in HDInsight:</span></span>

* <span data-ttu-id="336ad-109">在 hello 佈建時，您可以指定 hello 使用 hello Azure 入口網站、 Azure PowerShell 或跨平台命令列介面的背景工作節點數。</span><span class="sxs-lookup"><span data-stu-id="336ad-109">At hello provision time, you can specify hello number of worker nodes using hello Azure portal, Azure PowerShell, or Cross-platform command-line interface.</span></span>  <span data-ttu-id="336ad-110">如需詳細資訊，請參閱[建立 HDInsight 叢集](hdinsight-hadoop-provision-linux-clusters.md)。</span><span class="sxs-lookup"><span data-stu-id="336ad-110">For more information, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="336ad-111">hello 下列螢幕擷取畫面顯示 hello 背景工作節點組態 hello Azure 入口網站上：</span><span class="sxs-lookup"><span data-stu-id="336ad-111">hello following screenshot shows hello worker node configuration on hello Azure portal:</span></span>
  
    ![scaleout_1][image-hdi-optimize-hive-scaleout_1]
* <span data-ttu-id="336ad-113">在執行階段的 hello，您可以也向外延展叢集就必須重新建立其中一個：</span><span class="sxs-lookup"><span data-stu-id="336ad-113">At hello run time, you can also scale out a cluster without recreating one:</span></span>

    ![scaleout_1][image-hdi-optimize-hive-scaleout_2]

<span data-ttu-id="336ad-115">多個 hello 支援 HDInsight 不同虛擬機器的詳細資訊，請參閱[HDInsight 定價](https://azure.microsoft.com/pricing/details/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="336ad-115">For more information about hello different virtual machines supported by HDInsight, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="enable-tez"></a><span data-ttu-id="336ad-116">啟用 Tez</span><span class="sxs-lookup"><span data-stu-id="336ad-116">Enable Tez</span></span>

<span data-ttu-id="336ad-117">[Apache Tez](http://hortonworks.com/hadoop/tez/)是替代的執行引擎 toohello MapReduce 引擎：</span><span class="sxs-lookup"><span data-stu-id="336ad-117">[Apache Tez](http://hortonworks.com/hadoop/tez/) is an alternative execution engine toohello MapReduce engine:</span></span>

![tez_1][image-hdi-optimize-hive-tez_1]

<span data-ttu-id="336ad-119">Tez 比較迅速，因為：</span><span class="sxs-lookup"><span data-stu-id="336ad-119">Tez is faster because:</span></span>

* <span data-ttu-id="336ad-120">**以單一工作 hello MapReduce 引擎中執行導向非循環圖 (DAG)**。</span><span class="sxs-lookup"><span data-stu-id="336ad-120">**Execute Directed Acyclic Graph (DAG) as a single job in hello MapReduce engine**.</span></span> <span data-ttu-id="336ad-121">hello DAG 需要自行 toobe 後面接著一組 reducers 每組。</span><span class="sxs-lookup"><span data-stu-id="336ad-121">hello DAG requires each set of mappers toobe followed by one set of reducers.</span></span> <span data-ttu-id="336ad-122">這會導致多個 MapReduce 工作 toobe 開始每個 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="336ad-122">This causes multiple MapReduce jobs toobe spun off for each Hive query.</span></span> <span data-ttu-id="336ad-123">Tez 沒有此種條件約束，並可將複雜的 DAG 當作一項工作處理，因而將工作啟動的額外負荷降至最低。</span><span class="sxs-lookup"><span data-stu-id="336ad-123">Tez does not have such constraint and can process complex DAG as one job thus minimizing job startup overhead.</span></span>
* <span data-ttu-id="336ad-124">**避免不必要的寫入**。</span><span class="sxs-lookup"><span data-stu-id="336ad-124">**Avoids unnecessary writes**.</span></span> <span data-ttu-id="336ad-125">由於 toomultiple 作業正在開始 hello 撰寫 tooHDFS 中繼資料相同的 Hive 查詢 hello MapReduce 引擎，每個工作的 hello 輸出中。</span><span class="sxs-lookup"><span data-stu-id="336ad-125">Due toomultiple jobs being spun for hello same Hive query in hello MapReduce engine, hello output of each job is written tooHDFS for intermediate data.</span></span> <span data-ttu-id="336ad-126">因為 Tez 降到最低的每個 Hive 查詢能夠 tooavoid 不必要的寫入作業數目。</span><span class="sxs-lookup"><span data-stu-id="336ad-126">Since Tez minimizes number of jobs for each Hive query it is able tooavoid unnecessary write.</span></span>
* <span data-ttu-id="336ad-127">**將啟動延遲最小化**。</span><span class="sxs-lookup"><span data-stu-id="336ad-127">**Minimizes start-up delays**.</span></span> <span data-ttu-id="336ad-128">Tez 是更好的無法 toominimize 啟動延遲時間減少 hello 自行它需要 toostart，並在整個也改善最佳化數目。</span><span class="sxs-lookup"><span data-stu-id="336ad-128">Tez is better able toominimize start-up delay by reducing hello number of mappers it needs toostart and also improving optimization throughout.</span></span>
* <span data-ttu-id="336ad-129">**重複使用容器**。</span><span class="sxs-lookup"><span data-stu-id="336ad-129">**Reuses containers**.</span></span> <span data-ttu-id="336ad-130">只要可能 Tez 無法 tooreuse 容器 tooensure 到期，延遲 toostarting 向上容器會降低。</span><span class="sxs-lookup"><span data-stu-id="336ad-130">Whenever possible Tez is able tooreuse containers tooensure that latency due toostarting up containers is reduced.</span></span>
* <span data-ttu-id="336ad-131">**連續最佳化技巧**。</span><span class="sxs-lookup"><span data-stu-id="336ad-131">**Continuous optimization techniques**.</span></span> <span data-ttu-id="336ad-132">習慣上，是在編譯階段進行最佳化。</span><span class="sxs-lookup"><span data-stu-id="336ad-132">Traditionally optimization was done during compilation phase.</span></span> <span data-ttu-id="336ad-133">不過 hello 輸入的相關詳細資訊，讓較佳的最佳化在執行階段。</span><span class="sxs-lookup"><span data-stu-id="336ad-133">However more information about hello inputs is available that allow for better optimization during runtime.</span></span> <span data-ttu-id="336ad-134">Tez 使用連續的最佳化技術，好讓它在 hello 執行階段 」 階段的進一步 toooptimize hello 計劃。</span><span class="sxs-lookup"><span data-stu-id="336ad-134">Tez uses continuous optimization techniques that allows it toooptimize hello plan further into hello runtime phase.</span></span>

<span data-ttu-id="336ad-135">如需這些概念的詳細資訊，請參閱 [Apache Tez](http://hortonworks.com/hadoop/tez/)。</span><span class="sxs-lookup"><span data-stu-id="336ad-135">For more details on these concepts, see [Apache TEZ](http://hortonworks.com/hadoop/tez/).</span></span>

<span data-ttu-id="336ad-136">您可以進行任何 Hive 查詢 Tez hello 設定下列前置詞 hello 查詢的方式啟用：</span><span class="sxs-lookup"><span data-stu-id="336ad-136">You can make any Hive query Tez enabled by prefixing hello query with hello setting below:</span></span>

    set hive.execution.engine=tez;

<span data-ttu-id="336ad-137">Linux 的 HDInsight 叢集預設會啟用 Tez。</span><span class="sxs-lookup"><span data-stu-id="336ad-137">Linux-based HDInsight clusters have Tez enabled by default.</span></span>


## <a name="hive-partitioning"></a><span data-ttu-id="336ad-138">Hive 分割</span><span class="sxs-lookup"><span data-stu-id="336ad-138">Hive partitioning</span></span>

<span data-ttu-id="336ad-139">I/O 作業已執行 Hive 查詢的 hello 重大效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="336ad-139">I/O operation is hello major performance bottleneck for running Hive queries.</span></span> <span data-ttu-id="336ad-140">如果資料需要 toobe hello 量唯讀，則可以是可改善 hello 效能降低。</span><span class="sxs-lookup"><span data-stu-id="336ad-140">hello performance can be improved if hello amount of data that needs toobe read can be reduced.</span></span> <span data-ttu-id="336ad-141">根據預設，Hive 查詢會掃描整個 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="336ad-141">By default, Hive queries scan entire Hive tables.</span></span> <span data-ttu-id="336ad-142">這很適合資料表掃描之類的查詢。</span><span class="sxs-lookup"><span data-stu-id="336ad-142">This is great for queries like table scans.</span></span> <span data-ttu-id="336ad-143">不過對於只需要 tooscan 小量的資料 （例如，查詢的篩選） 的查詢，這種行為會建立不必要額外負荷。</span><span class="sxs-lookup"><span data-stu-id="336ad-143">However for queries that only need tooscan a small amount of data (for example, queries with filtering), this behavior creates unnecessary overhead.</span></span> <span data-ttu-id="336ad-144">登錄區的資料分割允許 Hive 資料表中的 Hive 查詢 tooaccess 只有 hello 必要的資料量。</span><span class="sxs-lookup"><span data-stu-id="336ad-144">Hive partitioning allows Hive queries tooaccess only hello necessary amount of data in Hive tables.</span></span>

<span data-ttu-id="336ad-145">分割區被藉由重新 hello 未經處理資料分割成新的目錄組織擁有它自己的目錄-hello 資料分割定義 hello 使用者所在的每一個資料分割。</span><span class="sxs-lookup"><span data-stu-id="336ad-145">Hive partitioning is implemented by reorganizing hello raw data into new directories with each partition having its own directory - where hello partition is defined by hello user.</span></span> <span data-ttu-id="336ad-146">hello 下列圖表說明 hello 資料行的資料分割的 Hive 資料表*年*。</span><span class="sxs-lookup"><span data-stu-id="336ad-146">hello following diagram illustrates partitioning a Hive table by hello column *Year*.</span></span> <span data-ttu-id="336ad-147">每年都會建立新的目錄。</span><span class="sxs-lookup"><span data-stu-id="336ad-147">A new directory is created for each year.</span></span>

![分割][image-hdi-optimize-hive-partitioning_1]

<span data-ttu-id="336ad-149">一些分割考量：</span><span class="sxs-lookup"><span data-stu-id="336ad-149">Some partitioning considerations:</span></span>

* <span data-ttu-id="336ad-150">**請勿分割不足** - 依據只有少數幾個值的資料行進行分割，可能會造成很少的分割區。</span><span class="sxs-lookup"><span data-stu-id="336ad-150">**Do not under partition** - Partitioning on columns with only a few values can cause few partitions.</span></span> <span data-ttu-id="336ad-151">例如，依性別分割只會建立兩個資料分割 toobe 建立 （男性和女性），因此只有減少 hello 延遲上限的一半。</span><span class="sxs-lookup"><span data-stu-id="336ad-151">For example, partitioning on gender only creates two partitions toobe created (male and female), thus only reduce hello latency by a maximum of half.</span></span>
* <span data-ttu-id="336ad-152">**不是透過資料分割進行**： 在 hello 其他極端的做法是，在具有唯一值 （例如，使用者識別碼） 的資料行上建立資料分割會造成多個資料分割。</span><span class="sxs-lookup"><span data-stu-id="336ad-152">**Do not over partition** - On hello other extreme, creating a partition on a column with a unique value (for example, userid) causes multiple partitions.</span></span> <span data-ttu-id="336ad-153">透過資料分割會導致多壓力 hello 叢集 namenode 因為它具有 toohandle hello 大量的目錄。</span><span class="sxs-lookup"><span data-stu-id="336ad-153">Over partition causes much stress on hello cluster namenode as it has toohandle hello large number of directories.</span></span>
* <span data-ttu-id="336ad-154">**避免資料扭曲** - 明智地選擇分割索引鍵，讓所有分割區的大小平均。</span><span class="sxs-lookup"><span data-stu-id="336ad-154">**Avoid data skew** - Choose your partitioning key wisely so that all partitions are even size.</span></span> <span data-ttu-id="336ad-155">上的範例分割區*狀態*可能會造成 hello 數目記錄在加州 toobe 幾乎 30 x 的 Vermont 到期 toohello 母體擴展中的差異。</span><span class="sxs-lookup"><span data-stu-id="336ad-155">An example is partitioning on *State* may cause hello number of records under California toobe almost 30x that of Vermont due toohello difference in population.</span></span>

<span data-ttu-id="336ad-156">toocreate 資料分割資料表，使用 hello*分割所*子句：</span><span class="sxs-lookup"><span data-stu-id="336ad-156">toocreate a partition table, use hello *Partitioned By* clause:</span></span>

    CREATE TABLE lineitem_part
        (L_ORDERKEY INT, L_PARTKEY INT, L_SUPPKEY INT,L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE            STRING, L_SHIPINSTRUCT STRING, L_SHIPMODE STRING,
         L_COMMENT STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY '\t'
    STORED AS TEXTFILE;

<span data-ttu-id="336ad-157">Hello 分割區的資料表建立之後，您可以建立資料分割的靜態或動態磁碟分割。</span><span class="sxs-lookup"><span data-stu-id="336ad-157">Once hello partitioned table is created, you can either create static partitioning or dynamic partitioning.</span></span>

* <span data-ttu-id="336ad-158">**靜態分割**hello 在已經分區化資料的方式適當的目錄，而且您可以詢問 Hive 手動 hello 目錄位置為基礎的資料分割。</span><span class="sxs-lookup"><span data-stu-id="336ad-158">**Static partitioning** means that you have already sharded data in hello appropriate directories and you can ask Hive partitions manually based on hello directory location.</span></span> <span data-ttu-id="336ad-159">下列程式碼片段的 hello 是範例。</span><span class="sxs-lookup"><span data-stu-id="336ad-159">hello following code snippet is an example.</span></span>
  
        INSERT OVERWRITE TABLE lineitem_part
        PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’)
        SELECT * FROM lineitem 
        WHERE lineitem.L_SHIPDATE = ‘5/23/1996 12:00:00 AM’
  
        ALTER TABLE lineitem_part ADD PARTITION (L_SHIPDATE = ‘5/23/1996 12:00:00 AM’))
        LOCATION ‘wasb://sampledata@ignitedemo.blob.core.windows.net/partitions/5_23_1996/'
* <span data-ttu-id="336ad-160">**動態磁碟分割**表示的 Hive toocreate 分割區會自動為您。</span><span class="sxs-lookup"><span data-stu-id="336ad-160">**Dynamic partitioning** means that you want Hive toocreate partitions automatically for you.</span></span> <span data-ttu-id="336ad-161">由於我們已經建立 hello 分割 hello 暫存資料表中的資料表，我們只需要 toodo 為插入資料分割的 toohello 資料表：</span><span class="sxs-lookup"><span data-stu-id="336ad-161">Since we have already created hello partitioning table from hello staging table, all we need toodo is insert data toohello partitioned table:</span></span>
  
        SET hive.exec.dynamic.partition = true;
        SET hive.exec.dynamic.partition.mode = nonstrict;
        INSERT INTO TABLE lineitem_part
        PARTITION (L_SHIPDATE)
        SELECT L_ORDERKEY as L_ORDERKEY, L_PARTKEY as L_PARTKEY , 
             L_SUPPKEY as L_SUPPKEY, L_LINENUMBER as L_LINENUMBER,
              L_QUANTITY as L_QUANTITY, L_EXTENDEDPRICE as L_EXTENDEDPRICE,
             L_DISCOUNT as L_DISCOUNT, L_TAX as L_TAX, L_RETURNFLAG as           L_RETURNFLAG, L_LINESTATUS as L_LINESTATUS, L_SHIPDATE as           L_SHIPDATE_PS, L_COMMITDATE as L_COMMITDATE, L_RECEIPTDATE as      L_RECEIPTDATE, L_SHIPINSTRUCT as L_SHIPINSTRUCT, L_SHIPMODE as      L_SHIPMODE, L_COMMENT as L_COMMENT, L_SHIPDATE as L_SHIPDATE FROM lineitem;

<span data-ttu-id="336ad-162">如需詳細資訊，請參閱 [分割的資料表](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables)。</span><span class="sxs-lookup"><span data-stu-id="336ad-162">For more details, see [Partitioned Tables](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+DDL#LanguageManualDDL-PartitionedTables).</span></span>

## <a name="use-hello-orcfile-format"></a><span data-ttu-id="336ad-163">使用 hello ORCFile 格式</span><span class="sxs-lookup"><span data-stu-id="336ad-163">Use hello ORCFile format</span></span>
<span data-ttu-id="336ad-164">Hive 支援不同的檔案格式。</span><span class="sxs-lookup"><span data-stu-id="336ad-164">Hive supports different file formats.</span></span> <span data-ttu-id="336ad-165">例如：</span><span class="sxs-lookup"><span data-stu-id="336ad-165">For example:</span></span>

* <span data-ttu-id="336ad-166">**文字**： 這是 hello 預設檔案格式，而且適用於大部分的案例</span><span class="sxs-lookup"><span data-stu-id="336ad-166">**Text**: this is hello default file format and works with most scenarios</span></span>
* <span data-ttu-id="336ad-167">**Avro**：適用於互通性案例</span><span class="sxs-lookup"><span data-stu-id="336ad-167">**Avro**: works well for interoperability scenarios</span></span>
* <span data-ttu-id="336ad-168">**ORC/Parquet**：最適合處理效能</span><span class="sxs-lookup"><span data-stu-id="336ad-168">**ORC/Parquet**: best suited for performance</span></span>

<span data-ttu-id="336ad-169">高效率的方式 toostore Hive 資料 ORC （最佳化的資料列單欄式） 格式。</span><span class="sxs-lookup"><span data-stu-id="336ad-169">ORC (Optimized Row Columnar) format is a highly efficient way toostore Hive data.</span></span> <span data-ttu-id="336ad-170">比較的 tooother 格式，ORC 具有下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="336ad-170">Compared tooother formats, ORC has hello following advantages:</span></span>

* <span data-ttu-id="336ad-171">支援複雜的類型，包括 DateTime 和複雜和半結構化類型</span><span class="sxs-lookup"><span data-stu-id="336ad-171">support for complex types including DateTime and complex and semi-structured types</span></span>
* <span data-ttu-id="336ad-172">向上 too70%壓縮</span><span class="sxs-lookup"><span data-stu-id="336ad-172">up too70% compression</span></span>
* <span data-ttu-id="336ad-173">每 10,000 個資料列的索引可讓您略過一些資料列</span><span class="sxs-lookup"><span data-stu-id="336ad-173">indexes every 10,000 rows, which allow skipping rows</span></span>
* <span data-ttu-id="336ad-174">執行階段的執行大幅減少</span><span class="sxs-lookup"><span data-stu-id="336ad-174">a significant drop in run-time execution</span></span>

<span data-ttu-id="336ad-175">tooenable ORC 格式，您先建立資料表以 hello 子句*儲存為 ORC*:</span><span class="sxs-lookup"><span data-stu-id="336ad-175">tooenable ORC format, you first create a table with hello clause *Stored as ORC*:</span></span>

    CREATE TABLE lineitem_orc_part
        (L_ORDERKEY INT, L_PARTKEY INT,L_SUPPKEY INT, L_LINENUMBER INT,
         L_QUANTITY DOUBLE, L_EXTENDEDPRICE DOUBLE, L_DISCOUNT DOUBLE,
         L_TAX DOUBLE, L_RETURNFLAG STRING, L_LINESTATUS STRING,
         L_SHIPDATE_PS STRING, L_COMMITDATE STRING, L_RECEIPTDATE STRING,
         L_SHIPINSTRUCT STRING, L_SHIPMODE STRING, L_COMMENT      STRING)
    PARTITIONED BY(L_SHIPDATE STRING)
    STORED AS ORC;

<span data-ttu-id="336ad-176">接下來，您會從暫存資料表的 hello 插入資料表 toohello ORC。</span><span class="sxs-lookup"><span data-stu-id="336ad-176">Next, you insert data toohello ORC table from hello staging table.</span></span> <span data-ttu-id="336ad-177">例如：</span><span class="sxs-lookup"><span data-stu-id="336ad-177">For example:</span></span>

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

<span data-ttu-id="336ad-178">您可以深入 hello ORC 格式[這裡](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC)。</span><span class="sxs-lookup"><span data-stu-id="336ad-178">You can read more on hello ORC format [here](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+ORC).</span></span>

## <a name="vectorization"></a><span data-ttu-id="336ad-179">向量化</span><span class="sxs-lookup"><span data-stu-id="336ad-179">Vectorization</span></span>

<span data-ttu-id="336ad-180">向量化可讓 Hive tooprocess 1024 個批次一起資料列而非一次處理一個資料列。</span><span class="sxs-lookup"><span data-stu-id="336ad-180">Vectorization allows Hive tooprocess a batch of 1024 rows together instead of processing one row at a time.</span></span> <span data-ttu-id="336ad-181">這表示因為較少內部的程式碼需要 toorun 簡單的作業會更快完成。</span><span class="sxs-lookup"><span data-stu-id="336ad-181">It means that simple operations are done faster because less internal code needs toorun.</span></span>

<span data-ttu-id="336ad-182">tooenable 向量化首碼 Hive 查詢以 hello 下列設定：</span><span class="sxs-lookup"><span data-stu-id="336ad-182">tooenable vectorization prefix your Hive query with hello following setting:</span></span>

    set hive.vectorized.execution.enabled = true;

<span data-ttu-id="336ad-183">如需詳細資訊，請參閱 [向量化查詢執行](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution)。</span><span class="sxs-lookup"><span data-stu-id="336ad-183">For more information, see [Vectorized query execution](https://cwiki.apache.org/confluence/display/Hive/Vectorized+Query+Execution).</span></span>

## <a name="other-optimization-methods"></a><span data-ttu-id="336ad-184">其他最佳化方法</span><span class="sxs-lookup"><span data-stu-id="336ad-184">Other optimization methods</span></span>
<span data-ttu-id="336ad-185">您有更多最佳化方法可以考慮，例如：</span><span class="sxs-lookup"><span data-stu-id="336ad-185">There are more optimization methods that you can consider, for example:</span></span>

* <span data-ttu-id="336ad-186">**Hive 值區：**允許 toocluster 或區段大量資料 toooptimize 查詢效能的技術。</span><span class="sxs-lookup"><span data-stu-id="336ad-186">**Hive bucketing:** a technique that allows toocluster or segment large sets of data toooptimize query performance.</span></span>
* <span data-ttu-id="336ad-187">**聯結最佳化：**的登錄區的查詢執行計劃 tooimprove 最佳化 hello 聯結的效率和減少 hello 使用者提示的需要。</span><span class="sxs-lookup"><span data-stu-id="336ad-187">**Join optimization:** optimization of Hive's query execution planning tooimprove hello efficiency of joins and reduce hello need for user hints.</span></span> <span data-ttu-id="336ad-188">如需詳細資訊，請參閱 [聯結最佳化](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization)。</span><span class="sxs-lookup"><span data-stu-id="336ad-188">For more information, see [Join optimization](https://cwiki.apache.org/confluence/display/Hive/LanguageManual+JoinOptimization#LanguageManualJoinOptimization-JoinOptimization).</span></span>
* <span data-ttu-id="336ad-189">**增加歸納器**。</span><span class="sxs-lookup"><span data-stu-id="336ad-189">**Increase Reducers**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="336ad-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="336ad-190">Next steps</span></span>
<span data-ttu-id="336ad-191">在本文中，您學到幾種常見的 Hive 查詢最佳化方法。</span><span class="sxs-lookup"><span data-stu-id="336ad-191">In this article, you have learned several common Hive query optimization methods.</span></span> <span data-ttu-id="336ad-192">toolearn 詳細資訊，請參閱下列文章 hello:</span><span class="sxs-lookup"><span data-stu-id="336ad-192">toolearn more, see hello following articles:</span></span>

* [<span data-ttu-id="336ad-193">在 HDInsight 中使用 Apache Hive</span><span class="sxs-lookup"><span data-stu-id="336ad-193">Use Apache Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="336ad-194">在 HDInsight 中使用 Hive 分析航班延誤資料</span><span class="sxs-lookup"><span data-stu-id="336ad-194">Analyze flight delay data by using Hive in HDInsight</span></span>](hdinsight-analyze-flight-delay-data.md)
* [<span data-ttu-id="336ad-195">在 HDInsight 中使用 Hive 分析 Twitter 資料</span><span class="sxs-lookup"><span data-stu-id="336ad-195">Analyze Twitter data using Hive in HDInsight</span></span>](hdinsight-analyze-twitter-data.md)
* [<span data-ttu-id="336ad-196">分析在 HDInsight 中的 Hadoop 使用 hello Hive 查詢主控台感應器資料</span><span class="sxs-lookup"><span data-stu-id="336ad-196">Analyze sensor data using hello Hive Query Console on Hadoop in HDInsight</span></span>](hdinsight-hive-analyze-sensor-data.md)
* [<span data-ttu-id="336ad-197">使用從網站的 HDInsight tooanalyze 記錄檔的登錄區</span><span class="sxs-lookup"><span data-stu-id="336ad-197">Use Hive with HDInsight tooanalyze logs from websites</span></span>](hdinsight-hive-analyze-website-log.md)

[image-hdi-optimize-hive-scaleout_1]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_1.png
[image-hdi-optimize-hive-scaleout_2]: ./media/hdinsight-hadoop-optimize-hive-query/scaleout_2.png
[image-hdi-optimize-hive-tez_1]: ./media/hdinsight-hadoop-optimize-hive-query/tez_1.png
[image-hdi-optimize-hive-partitioning_1]: ./media/hdinsight-hadoop-optimize-hive-query/partitioning_1.png
