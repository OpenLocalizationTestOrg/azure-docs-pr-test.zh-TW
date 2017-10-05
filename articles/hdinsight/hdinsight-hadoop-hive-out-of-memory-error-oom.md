---
title: "修正 Azure HDInsight 中的 Hive 記憶體錯誤 | Microsoft Docs"
description: "修正 HDInsight 中的 Hive 記憶體不足錯誤。 客戶案例是一個橫跨許多大型資料表的查詢。"
keywords: "記憶體不足錯誤, OOM, Hive 設定"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 7bce3dff-9825-4fa0-a568-c52a9f7d1dad
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/17/2017
ms.author: jgao
ms.openlocfilehash: da1247070ade11f78b505524f5e970e18eb16d10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="2fe32-105">修正 Azure HDInsight 中的 Hive 記憶體不足錯誤</span><span class="sxs-lookup"><span data-stu-id="2fe32-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="2fe32-106">了解如何在處理大型資料表時，透過設定 Hive 記憶體設定，修正 Hive 記憶體不足的錯誤。</span><span class="sxs-lookup"><span data-stu-id="2fe32-106">Learn how to fix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="2fe32-107">針對大型資料表執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="2fe32-107">Run Hive query against large tables</span></span>

<span data-ttu-id="2fe32-108">某個客戶執行了 Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="2fe32-108">A customer ran a Hive query:</span></span>

    SELECT
        COUNT (T1.COLUMN1) as DisplayColumn1,
        …
        …
        ….
    FROM
        TABLE1 T1,
        TABLE2 T2,
        TABLE3 T3,
        TABLE5 T4,
        TABLE6 T5,
        TABLE7 T6
    where (T1.KEY1 = T2.KEY1….
        …
        …

<span data-ttu-id="2fe32-109">此查詢的一些細微差異：</span><span class="sxs-lookup"><span data-stu-id="2fe32-109">Some nuances of this query:</span></span>

* <span data-ttu-id="2fe32-110">T1 是大型資料表 TABLE1 的別名，其中包含多個 STRING 資料行類型。</span><span class="sxs-lookup"><span data-stu-id="2fe32-110">T1 is an alias to a big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="2fe32-111">其他資料表的規模沒有那麼大，但還是有許多資料行。</span><span class="sxs-lookup"><span data-stu-id="2fe32-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="2fe32-112">所有資料表都會彼此聯結，在某些情況下，是透過 TABLE1 和其他資料表中的多個資料行來聯結。</span><span class="sxs-lookup"><span data-stu-id="2fe32-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="2fe32-113">此 Hive 查詢在一個有 24 個節點的 A3 HDInsight 叢集上花費 26 分鐘完成執行。</span><span class="sxs-lookup"><span data-stu-id="2fe32-113">The Hive query took 26 minutes to finish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="2fe32-114">該客戶注意到下列警告訊息：</span><span class="sxs-lookup"><span data-stu-id="2fe32-114">The customer noticed the following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="2fe32-115">在使用 Tez 執行引擎的情況下，</span><span class="sxs-lookup"><span data-stu-id="2fe32-115">By using the Tez execution engine.</span></span> <span data-ttu-id="2fe32-116">相同查詢執行了 15 分鐘，然後擲回下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="2fe32-116">The same query ran for 15 minutes, and then threw the following error:</span></span>

    Status: Failed
    Vertex failed, vertexName=Map 5, vertexId=vertex_1443634917922_0008_1_05, diagnostics=[Task failed, taskId=task_1443634917922_0008_1_05_000006, diagnostics=[TaskAttempt 0 failed, info=[Error: Failure while running task:java.lang.RuntimeException: java.lang.OutOfMemoryError: Java heap space
        at
    org.apache.hadoop.hive.ql.exec.tez.TezProcessor.initializeAndRunProcessor(TezProcessor.java:172)
        at org.apache.hadoop.hive.ql.exec.tez.TezProcessor.run(TezProcessor.java:138)
        at
    org.apache.tez.runtime.LogicalIOProcessorRuntimeTask.run(LogicalIOProcessorRuntimeTask.java:324)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:176)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable$1.run(TezTaskRunner.java:168)
        at java.security.AccessController.doPrivileged(Native Method)
        at javax.security.auth.Subject.doAs(Subject.java:415)
        at org.apache.hadoop.security.UserGroupInformation.doAs(UserGroupInformation.java:1628)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:168)
        at
    org.apache.tez.runtime.task.TezTaskRunner$TaskRunnerCallable.call(TezTaskRunner.java:163)
        at java.util.concurrent.FutureTask.run(FutureTask.java:262)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1145)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:615)
        at java.lang.Thread.run(Thread.java:745)
    Caused by: java.lang.OutOfMemoryError: Java heap space

<span data-ttu-id="2fe32-117">當使用較大的虛擬機器 (例如 D12) 時，該錯誤仍然存在。</span><span class="sxs-lookup"><span data-stu-id="2fe32-117">The error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-the-out-of-memory-error"></a><span data-ttu-id="2fe32-118">針對記憶體不足錯誤進行偵錯</span><span class="sxs-lookup"><span data-stu-id="2fe32-118">Debug the out of memory error</span></span>

<span data-ttu-id="2fe32-119">我們的支援小組和工程小組一起發現造成記憶體不足錯誤的其中一個問題是一個 [Apache JIRA 中所述的已知問題](https://issues.apache.org/jira/browse/HIVE-8306)：</span><span class="sxs-lookup"><span data-stu-id="2fe32-119">Our support and engineering teams together found one of the issues causing the out of memory error was a [known issue described in the Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if the sum  of tables sizes in the map join is less than noconditionaltask.size the plan would generate a Map join, the issue with this is that the calculation doesnt take into account the overhead introduced by different HashTable implementation as results if the sum of input sizes is smaller than the noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="2fe32-120">hive-site.xml 檔案中的 **hive.auto.convert.join.noconditionaltask** 已設定為 **true**：</span><span class="sxs-lookup"><span data-stu-id="2fe32-120">The **hive.auto.convert.join.noconditionaltask** in the hive-site.xml file was set to **true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables the optimization about converting common join into mapjoin based on the input file size.
              If this parameter is on, and the sum of size for n-1 of the tables/partitions for a n-way join is smaller than the
              specified size, the join is directly converted to a mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="2fe32-121">對應聯結有可能是「Java 堆積空間」記憶體不足錯誤的原因。</span><span class="sxs-lookup"><span data-stu-id="2fe32-121">It is likely map join was the cause of the Java Heap Space our of memory error.</span></span> <span data-ttu-id="2fe32-122">如部落格文章 [HDInsight 中的 Hadoop Yarn 記憶體設定](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx)中所述，使用 Tez 執行引擎時，所使用的堆積空間實際上是屬於 Tez 容器。</span><span class="sxs-lookup"><span data-stu-id="2fe32-122">As explained in the blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used the heap space used actually belongs to the Tez container.</span></span> <span data-ttu-id="2fe32-123">查看下面說明 Tez 容器記憶體的影像。</span><span class="sxs-lookup"><span data-stu-id="2fe32-123">See the following image describing the Tez container memory.</span></span>

![Tez 容器記憶體圖表：Hive 記憶體不足錯誤](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="2fe32-125">如部落格文章所建議，下列兩個記憶體設定會定義堆積的容器記憶體：**hive.tez.container.size** 和 **hive.tez.java.opts**。</span><span class="sxs-lookup"><span data-stu-id="2fe32-125">As the blog post suggests, the following two memory settings define the container memory for the heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="2fe32-126">從我們的經驗來看，記憶體不足例外狀況並不代表容器大小太小。</span><span class="sxs-lookup"><span data-stu-id="2fe32-126">From our experience, the out of memory exception does not mean the container size is too small.</span></span> <span data-ttu-id="2fe32-127">它表示 Java 堆積大小 (hive.tez.java.opts) 太小。</span><span class="sxs-lookup"><span data-stu-id="2fe32-127">It means the Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="2fe32-128">因此，每當您看到記憶體不足時，可嘗試增加 **hive.tez.java.opts**。</span><span class="sxs-lookup"><span data-stu-id="2fe32-128">So whenever you see out of memory, you can try to increase **hive.tez.java.opts**.</span></span> <span data-ttu-id="2fe32-129">必要時，您可能需要增加 **hive.tez.container.size**。</span><span class="sxs-lookup"><span data-stu-id="2fe32-129">If needed you might have to increase **hive.tez.container.size**.</span></span> <span data-ttu-id="2fe32-130">**Java.opts** 設定應該大約為 **container.size** 的 80%。</span><span class="sxs-lookup"><span data-stu-id="2fe32-130">The **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="2fe32-131">**hive.tez.java.opts** 設定必須一律小於 **hive.tez.container.size**。</span><span class="sxs-lookup"><span data-stu-id="2fe32-131">The setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="2fe32-132">由於 D12 機器具有 28 GB 記憶體，因此我們決定使用 10 GB (10240 MB) 的容器大小並指派 80% 給 java.opts：</span><span class="sxs-lookup"><span data-stu-id="2fe32-132">Because a D12 machine has 28GB memory, we decided to use a container size of 10GB (10240MB) and assign 80% to java.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="2fe32-133">使用新設定之後，查詢順利在 10 分鐘內完成執行。</span><span class="sxs-lookup"><span data-stu-id="2fe32-133">With the new settings, the query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2fe32-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2fe32-134">Next steps</span></span>

<span data-ttu-id="2fe32-135">遇到 OOM 錯誤不一定表示容器大小太小。</span><span class="sxs-lookup"><span data-stu-id="2fe32-135">Getting an OOM error doesn't necessarily mean the container size is too small.</span></span> <span data-ttu-id="2fe32-136">相反地，您應該設定記憶體設定，以增加堆積大小，至少是容器記憶體大小的 80%。</span><span class="sxs-lookup"><span data-stu-id="2fe32-136">Instead, you should configure the memory settings so that the heap size is increased and is at least 80% of the container memory size.</span></span> <span data-ttu-id="2fe32-137">若要了解如何將 Hive 查詢最佳化，請參閱[在 HDInsight 中最佳化 Hadoop 的 Hive 查詢](hdinsight-hadoop-optimize-hive-query.md)。</span><span class="sxs-lookup"><span data-stu-id="2fe32-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>