---
title: "記憶體不足錯誤中 Azure HDInsight Hive aaaFix |Microsoft 文件"
description: "修正 HDInsight 中的 Hive 記憶體不足錯誤。 hello 客戶案例中是許多大型資料表查詢。"
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
ms.openlocfilehash: 00a12969322c1e74434ba6593ffd098f342edd84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="fix-a-hive-out-of-memory-error-in-azure-hdinsight"></a><span data-ttu-id="bcb75-105">修正 Azure HDInsight 中的 Hive 記憶體不足錯誤</span><span class="sxs-lookup"><span data-stu-id="bcb75-105">Fix a Hive out of memory error in Azure HDInsight</span></span>

<span data-ttu-id="bcb75-106">深入了解如何 toofix Hive 記憶體不足錯誤時所設定的登錄區的記憶體中處理大型資料表。</span><span class="sxs-lookup"><span data-stu-id="bcb75-106">Learn how toofix a Hive out of memory error when process large tables by configuring Hive memory settings.</span></span>

## <a name="run-hive-query-against-large-tables"></a><span data-ttu-id="bcb75-107">針對大型資料表執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="bcb75-107">Run Hive query against large tables</span></span>

<span data-ttu-id="bcb75-108">某個客戶執行了 Hive 查詢：</span><span class="sxs-lookup"><span data-stu-id="bcb75-108">A customer ran a Hive query:</span></span>

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

<span data-ttu-id="bcb75-109">此查詢的一些細微差異：</span><span class="sxs-lookup"><span data-stu-id="bcb75-109">Some nuances of this query:</span></span>

* <span data-ttu-id="bcb75-110">T1 有進行別名 tooa 大型資料表，TABLE1、 有大量的字串資料行類型。</span><span class="sxs-lookup"><span data-stu-id="bcb75-110">T1 is an alias tooa big table, TABLE1, which has lots of STRING column types.</span></span>
* <span data-ttu-id="bcb75-111">其他資料表的規模沒有那麼大，但還是有許多資料行。</span><span class="sxs-lookup"><span data-stu-id="bcb75-111">Other tables are not that big but do have many columns.</span></span>
* <span data-ttu-id="bcb75-112">所有資料表都會彼此聯結，在某些情況下，是透過 TABLE1 和其他資料表中的多個資料行來聯結。</span><span class="sxs-lookup"><span data-stu-id="bcb75-112">All tables are joining each other, in some cases with multiple columns in TABLE1 and others.</span></span>

<span data-ttu-id="bcb75-113">hello Hive 查詢花費 26 分鐘 toofinish 24 節點 A3 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="bcb75-113">hello Hive query took 26 minutes toofinish on a 24 node A3 HDInsight cluster.</span></span> <span data-ttu-id="bcb75-114">hello 客戶受到注意的 hello 下列警告訊息：</span><span class="sxs-lookup"><span data-stu-id="bcb75-114">hello customer noticed hello following warning messages:</span></span>

    Warning: Map Join MAPJOIN[428][bigTable=?] in task 'Stage-21:MAPRED' is a cross product
    Warning: Shuffle Join JOIN[8][tables = [t1933775, t1932766]] in Stage 'Stage-4:MAPRED' is a cross product

<span data-ttu-id="bcb75-115">使用 hello Tez 執行引擎。</span><span class="sxs-lookup"><span data-stu-id="bcb75-115">By using hello Tez execution engine.</span></span> <span data-ttu-id="bcb75-116">相同的查詢執行 15 分鐘，並且再擲回下列錯誤 hello hello:</span><span class="sxs-lookup"><span data-stu-id="bcb75-116">hello same query ran for 15 minutes, and then threw hello following error:</span></span>

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

<span data-ttu-id="bcb75-117">使用較大的虛擬機器 (例如，D12) 時，會保留 hello 錯誤。</span><span class="sxs-lookup"><span data-stu-id="bcb75-117">hello error remains when using a bigger virtual machine (for example, D12).</span></span>


## <a name="debug-hello-out-of-memory-error"></a><span data-ttu-id="bcb75-118">偵錯 hello 記憶體不足錯誤</span><span class="sxs-lookup"><span data-stu-id="bcb75-118">Debug hello out of memory error</span></span>

<span data-ttu-id="bcb75-119">我們支援和工程小組一起發現其中一個 hello 問題造成記憶體不足錯誤 hello[已知 hello Apache JIRA 中所述的問題](https://issues.apache.org/jira/browse/HIVE-8306):</span><span class="sxs-lookup"><span data-stu-id="bcb75-119">Our support and engineering teams together found one of hello issues causing hello out of memory error was a [known issue described in hello Apache JIRA](https://issues.apache.org/jira/browse/HIVE-8306):</span></span>

    When hive.auto.convert.join.noconditionaltask = true we check noconditionaltask.size and if hello sum  of tables sizes in hello map join is less than noconditionaltask.size hello plan would generate a Map join, hello issue with this is that hello calculation doesnt take into account hello overhead introduced by different HashTable implementation as results if hello sum of input sizes is smaller than hello noconditionaltask size by a small margin queries will hit OOM.

<span data-ttu-id="bcb75-120">hello **hive.auto.convert.join.noconditionaltask**在 hello hive-site.xml 檔案設太**true**:</span><span class="sxs-lookup"><span data-stu-id="bcb75-120">hello **hive.auto.convert.join.noconditionaltask** in hello hive-site.xml file was set too**true**:</span></span>

    <property>
        <name>hive.auto.convert.join.noconditionaltask</name>
        <value>true</value>
        <description>
              Whether Hive enables hello optimization about converting common join into mapjoin based on hello input file size.
              If this parameter is on, and hello sum of size for n-1 of hello tables/partitions for a n-way join is smaller than the
              specified size, hello join is directly converted tooa mapjoin (there is no conditional task).
        </description>
      </property>

<span data-ttu-id="bcb75-121">可能是對應聯結已 hello 原因 hello Java 堆積空間我們的記憶體時發生錯誤。</span><span class="sxs-lookup"><span data-stu-id="bcb75-121">It is likely map join was hello cause of hello Java Heap Space our of memory error.</span></span> <span data-ttu-id="bcb75-122">Hello 部落格文章所述[HDInsight 中的 Hadoop Yarn 記憶體設定](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx)，當執行引擎會使用使用的 hello 堆積空間 Tez 實際上所屬 toohello Tez 容器。</span><span class="sxs-lookup"><span data-stu-id="bcb75-122">As explained in hello blog post [Hadoop Yarn memory settings in HDInsight](http://blogs.msdn.com/b/shanyu/archive/2014/07/31/hadoop-yarn-memory-settings-in-hdinsigh.aspx), when Tez execution engine is used hello heap space used actually belongs toohello Tez container.</span></span> <span data-ttu-id="bcb75-123">請參閱下列映像描述 hello Tez 容器記憶體 hello。</span><span class="sxs-lookup"><span data-stu-id="bcb75-123">See hello following image describing hello Tez container memory.</span></span>

![Tez 容器記憶體圖表：Hive 記憶體不足錯誤](./media/hdinsight-hadoop-hive-out-of-memory-error-oom/hive-out-of-memory-error-oom-tez-container-memory.png)

<span data-ttu-id="bcb75-125">下列兩個記憶體設定 hello 如 hello 部落格文章所示，定義 hello 堆積的 hello 容器記憶體： **hive.tez.container.size**和**hive.tez.java.opts**。</span><span class="sxs-lookup"><span data-stu-id="bcb75-125">As hello blog post suggests, hello following two memory settings define hello container memory for hello heap: **hive.tez.container.size** and **hive.tez.java.opts**.</span></span> <span data-ttu-id="bcb75-126">從我們的經驗，超出記憶體例外狀況的 hello 不表示 hello 容器大小太小。</span><span class="sxs-lookup"><span data-stu-id="bcb75-126">From our experience, hello out of memory exception does not mean hello container size is too small.</span></span> <span data-ttu-id="bcb75-127">它表示 hello Java 堆積大小 (hive.tez.java.opts) 太小。</span><span class="sxs-lookup"><span data-stu-id="bcb75-127">It means hello Java heap size (hive.tez.java.opts) is too small.</span></span> <span data-ttu-id="bcb75-128">因此每當您看見記憶體不足，您可以嘗試 tooincrease **hive.tez.java.opts**。</span><span class="sxs-lookup"><span data-stu-id="bcb75-128">So whenever you see out of memory, you can try tooincrease **hive.tez.java.opts**.</span></span> <span data-ttu-id="bcb75-129">必要時您可能必須 tooincrease **hive.tez.container.size**。</span><span class="sxs-lookup"><span data-stu-id="bcb75-129">If needed you might have tooincrease **hive.tez.container.size**.</span></span> <span data-ttu-id="bcb75-130">hello **java.opts**設定應該大約 80%的**container.size**。</span><span class="sxs-lookup"><span data-stu-id="bcb75-130">hello **java.opts** setting should be around 80% of **container.size**.</span></span>

> [!NOTE]
> <span data-ttu-id="bcb75-131">hello 設定**hive.tez.java.opts**必須一律小於**hive.tez.container.size**。</span><span class="sxs-lookup"><span data-stu-id="bcb75-131">hello setting **hive.tez.java.opts** must always be smaller than **hive.tez.container.size**.</span></span>
> 
> 

<span data-ttu-id="bcb75-132">因為 D12 機器 28 GB 記憶體，所以我們決定 toouse 10 GB (10240 MB) 的容器大小，並指定 80 %toojava.opts:</span><span class="sxs-lookup"><span data-stu-id="bcb75-132">Because a D12 machine has 28GB memory, we decided toouse a container size of 10GB (10240MB) and assign 80% toojava.opts:</span></span>

    SET hive.tez.container.size=10240
    SET hive.tez.java.opts=-Xmx8192m

<span data-ttu-id="bcb75-133">Hello 新的設定，與 hello 查詢已順利執行在 10 分鐘。</span><span class="sxs-lookup"><span data-stu-id="bcb75-133">With hello new settings, hello query successfully ran in under 10 minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bcb75-134">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bcb75-134">Next steps</span></span>

<span data-ttu-id="bcb75-135">取得 OOM 錯誤不一定表示 hello 容器大小太小。</span><span class="sxs-lookup"><span data-stu-id="bcb75-135">Getting an OOM error doesn't necessarily mean hello container size is too small.</span></span> <span data-ttu-id="bcb75-136">相反地，您應該設定 hello 記憶體設定，使 hello 堆積大小會增加，而在至少 80%的 hello 容器記憶體大小。</span><span class="sxs-lookup"><span data-stu-id="bcb75-136">Instead, you should configure hello memory settings so that hello heap size is increased and is at least 80% of hello container memory size.</span></span> <span data-ttu-id="bcb75-137">若要了解如何將 Hive 查詢最佳化，請參閱[在 HDInsight 中最佳化 Hadoop 的 Hive 查詢](hdinsight-hadoop-optimize-hive-query.md)。</span><span class="sxs-lookup"><span data-stu-id="bcb75-137">For optimizing Hive queries, see [Optimize Hive queries for Hadoop in HDInsight](hdinsight-hadoop-optimize-hive-query.md).</span></span>
