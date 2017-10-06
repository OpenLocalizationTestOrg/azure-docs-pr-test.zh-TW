---
title: "aaaUse Hadoop Hive 和 HDInsight 的 Azure 中的遠端桌面 |Microsoft 文件"
description: "了解如何 tooconnect tooHadoop HDInsight 中使用叢集的遠端桌面，並使用 hello hive 控制檔的命令列介面，以執行 Hive 查詢。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="eff7e-103">利用遠端桌面搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="eff7e-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="eff7e-104">在本文中，您將學習如何 tooconnect tooan HDInsight 叢集使用遠端桌面，然後再執行 Hive 查詢使用 hello hive 控制檔的命令列介面 (CLI)。</span><span class="sxs-lookup"><span data-stu-id="eff7e-104">In this article, you will learn how tooconnect tooan HDInsight cluster by using Remote Desktop, and then run Hive queries by using hello Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eff7e-105">只有在使用 Windows 做為 hello 作業系統的 HDInsight 叢集上使用遠端桌面。</span><span class="sxs-lookup"><span data-stu-id="eff7e-105">Remote Desktop is only available on HDInsight clusters that use Windows as hello operating system.</span></span> <span data-ttu-id="eff7e-106">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="eff7e-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="eff7e-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="eff7e-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="eff7e-108">HDInsight 3.4 或更高，請參閱[使用 Hive 與 HDInsight Beeline](hdinsight-hadoop-use-hive-beeline.md)直接在 hello 叢集上執行 Hive 查詢，從命令列上的資訊。</span><span class="sxs-lookup"><span data-stu-id="eff7e-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on hello cluster from a command-line.</span></span>

## <span data-ttu-id="eff7e-109"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="eff7e-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="eff7e-110">toocomplete hello 本文中的步驟，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="eff7e-110">toocomplete hello steps in this article, you will need hello following:</span></span>

* <span data-ttu-id="eff7e-111">Windows 型 HDInsight (HDInsight 上的 Hadoop) 叢集</span><span class="sxs-lookup"><span data-stu-id="eff7e-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="eff7e-112">執行 Windows 10、Windows 8 或 Windows 7 的用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="eff7e-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="eff7e-113"><a id="connect"></a>使用遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="eff7e-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="eff7e-114">Hello HDInsight 叢集，啟用遠端桌面，然後依照指示 hello 連接 tooit[連接使用 RDP tooHDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)。</span><span class="sxs-lookup"><span data-stu-id="eff7e-114">Enable Remote Desktop for hello HDInsight cluster, then connect tooit by following hello instructions at [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="eff7e-115"><a id="hive"></a>使用 hello Hive 命令</span><span class="sxs-lookup"><span data-stu-id="eff7e-115"><a id="hive"></a>Use hello Hive command</span></span>
<span data-ttu-id="eff7e-116">當您有連接 toohello 桌面 hello HDInsight 叢集時，使用下列步驟 toowork Hive 與 hello:</span><span class="sxs-lookup"><span data-stu-id="eff7e-116">When you have connected toohello desktop for hello HDInsight cluster, use hello following steps toowork with Hive:</span></span>

1. <span data-ttu-id="eff7e-117">從 hello HDInsight 桌面啟動 hello **Hadoop 命令列**。</span><span class="sxs-lookup"><span data-stu-id="eff7e-117">From hello HDInsight desktop, start hello **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="eff7e-118">輸入下列命令 toostart hello Hive CLI hello:</span><span class="sxs-lookup"><span data-stu-id="eff7e-118">Enter hello following command toostart hello Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="eff7e-119">Hello CLI 啟動之後，您會看到 hello Hive CLI 提示： `hive>`。</span><span class="sxs-lookup"><span data-stu-id="eff7e-119">When hello CLI has started, you will see hello Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="eff7e-120">使用 hello CLI 中，輸入下列陳述式 toocreate 名為的新資料表的 hello **log4jLogs**使用範例資料：</span><span class="sxs-lookup"><span data-stu-id="eff7e-120">Using hello CLI, enter hello following statements toocreate a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="eff7e-121">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="eff7e-121">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="eff7e-122">**DROP TABLE**: hello 資料表已存在時刪除 hello 資料表與 hello 資料檔。</span><span class="sxs-lookup"><span data-stu-id="eff7e-122">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="eff7e-123">**CREATE EXTERNAL TABLE**：在 Hive 中建立新的「外部」資料表。</span><span class="sxs-lookup"><span data-stu-id="eff7e-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="eff7e-124">外部資料表 (資料會保留在 hello 原始位置中的 hello) 登錄區中儲存只有 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="eff7e-124">External tables store only hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="eff7e-125">當您預期 hello 基礎資料 toobe 更新由外部來源 （例如自動化的資料上傳程序中） 或另一項 MapReduce 作業，但是您通常想要登錄區查詢 toouse hello 最新的資料，應該使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="eff7e-125">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="eff7e-126">卸除的外部資料表沒有**不**刪除 hello 資料、 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="eff7e-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="eff7e-127">**資料列格式**: hello 資料格式化的方式會告知 hive 控制檔。</span><span class="sxs-lookup"><span data-stu-id="eff7e-127">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="eff7e-128">在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="eff7e-128">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="eff7e-129">**儲存為文字檔位置**： 告訴 Hive 其中 hello 資料是儲存 （hello 範例/資料目錄），則會儲存為文字。</span><span class="sxs-lookup"><span data-stu-id="eff7e-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="eff7e-130">**選取**： 選取所有資料列計數其中資料行**t4**包含 hello 值**[錯誤]**。</span><span class="sxs-lookup"><span data-stu-id="eff7e-130">**SELECT**: Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="eff7e-131">這應該會傳回值 **3** ，因為有三個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="eff7e-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="eff7e-132">**INPUT__FILE__NAME LIKE '%.log'** - 告訴 Hive 我們只應該從檔名以 log 結尾的檔案中傳回資料。</span><span class="sxs-lookup"><span data-stu-id="eff7e-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="eff7e-133">這會限制 hello 搜尋 toohello sample.log 檔案，其中包含 hello 資料，並防止從其他範例與 hello 我們所定義的結構描述不相符的資料檔案傳回資料。</span><span class="sxs-lookup"><span data-stu-id="eff7e-133">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
4. <span data-ttu-id="eff7e-134">下列陳述式 toocreate 名為 'internal' 新的資料表使用 hello**錯誤記錄檔**:</span><span class="sxs-lookup"><span data-stu-id="eff7e-134">Use hello following statements toocreate a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="eff7e-135">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="eff7e-135">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="eff7e-136">**CREATE TABLE IF NOT EXISTS**：建立資料表 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="eff7e-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="eff7e-137">因為 hello**外部**關鍵字不是，這是內部的資料表，hello Hive 資料倉儲中所儲存且受完全登錄區。</span><span class="sxs-lookup"><span data-stu-id="eff7e-137">Because hello **EXTERNAL** keyword is not used, this is an internal table, which is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="eff7e-138">不同於**外部**資料表，卸除內部資料表也會刪除基礎資料的 hello。</span><span class="sxs-lookup"><span data-stu-id="eff7e-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes hello underlying data.</span></span>
     >
     >
   * <span data-ttu-id="eff7e-139">**儲存 AS ORC**: hello 資料儲存最佳化的資料列單欄式 (ORC) 格式。</span><span class="sxs-lookup"><span data-stu-id="eff7e-139">**STORED AS ORC**: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="eff7e-140">這是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="eff7e-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="eff7e-141">**INSERT OVERWRITE ...選取**： 選取資料列從 hello **log4jLogs**包含資料表**[錯誤]**，然後插入到 hello hello 資料**錯誤記錄檔**資料表。</span><span class="sxs-lookup"><span data-stu-id="eff7e-141">**INSERT OVERWRITE ... SELECT**: Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

     <span data-ttu-id="eff7e-142">只有資料列的 tooverify 包含**[錯誤]**資料行 t4 是預存的 toohello**錯誤記錄檔**資料表，請使用下列陳述式 tooreturn 所有 hello 中的資料列的 hello**錯誤記錄檔**:</span><span class="sxs-lookup"><span data-stu-id="eff7e-142">tooverify that only rows that contain **[ERROR]** in column t4 were stored toohello **errorLogs** table, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

       <span data-ttu-id="eff7e-143">SELECT * from errorLogs;</span><span class="sxs-lookup"><span data-stu-id="eff7e-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="eff7e-144">應該傳回三個資料列，且在資料行 t4 中全部包含 **[ERROR]** 。</span><span class="sxs-lookup"><span data-stu-id="eff7e-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="eff7e-145"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="eff7e-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="eff7e-146">如您所見，hello hello Hive 命令提供的 HDInsight 叢集上執行 Hive 查詢輕鬆 toointeractively，監視 hello 工作的狀態，和擷取 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="eff7e-146">As you can see, hello hello Hive command provides an easy way toointeractively run Hive queries on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="eff7e-147"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="eff7e-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="eff7e-148">如需 HDInsight 中 Hive 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="eff7e-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="eff7e-149">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="eff7e-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="eff7e-150">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="eff7e-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="eff7e-151">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="eff7e-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="eff7e-152">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="eff7e-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="eff7e-153">如果您正在使用 Hive Tez，請參閱下列文件的偵錯資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="eff7e-153">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="eff7e-154">使用 Windows 為基礎的 HDInsight 上的 hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="eff7e-154">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="eff7e-155">使用 hello Ambari Tez 以 Linux 為基礎的 HDInsight 上的檢視</span><span class="sxs-lookup"><span data-stu-id="eff7e-155">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
