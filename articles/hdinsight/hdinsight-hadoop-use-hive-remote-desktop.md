---
title: "在 HDInsight 中使用 Hadoop Hive 與遠端桌面 - Azure | Microsoft Docs"
description: "學習如何使用遠端桌面連接到 HDInsight 中的 Hadoop 叢集，然後使用 Hive 命令列介面執行 Hive 查詢。"
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
ms.openlocfilehash: 187c7cb413b3707e58eea387857375053d267189
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a><span data-ttu-id="80621-103">利用遠端桌面搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="80621-103">Use Hive with Hadoop on HDInsight with Remote Desktop</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="80621-104">在本文中，您將學習如何使用遠端桌面連接到 HDInsight 叢集，然後使用 Hive 命令列介面 (CLI) 執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="80621-104">In this article, you will learn how to connect to an HDInsight cluster by using Remote Desktop, and then run Hive queries by using the Hive Command-Line Interface (CLI).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80621-105">只有在使用 Windows 作為作業系統的 HDInsight 叢集上才能使用「遠端桌面」。</span><span class="sxs-lookup"><span data-stu-id="80621-105">Remote Desktop is only available on HDInsight clusters that use Windows as the operating system.</span></span> <span data-ttu-id="80621-106">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="80621-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="80621-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="80621-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="80621-108">針對 HDInsight 3.4 或更新版本，請參閱[使用 Hive 搭配 HDInsight 和 Beeline](hdinsight-hadoop-use-hive-beeline.md)，以了解如何從命令列直接在叢集上執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="80621-108">For HDInsight 3.4 or greater, see [Use Hive with HDInsight and Beeline](hdinsight-hadoop-use-hive-beeline.md) for information on running Hive queries directly on the cluster from a command-line.</span></span>

## <span data-ttu-id="80621-109"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="80621-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="80621-110">若要完成本文中的步驟，您需要下列項目。</span><span class="sxs-lookup"><span data-stu-id="80621-110">To complete the steps in this article, you will need the following:</span></span>

* <span data-ttu-id="80621-111">Windows 型 HDInsight (HDInsight 上的 Hadoop) 叢集</span><span class="sxs-lookup"><span data-stu-id="80621-111">A Windows-based HDInsight (Hadoop on HDInsight) cluster</span></span>
* <span data-ttu-id="80621-112">執行 Windows 10、Windows 8 或 Windows 7 的用戶端電腦</span><span class="sxs-lookup"><span data-stu-id="80621-112">A client computer running Windows 10, Window 8, or Windows 7</span></span>

## <span data-ttu-id="80621-113"><a id="connect"></a>使用遠端桌面連線</span><span class="sxs-lookup"><span data-stu-id="80621-113"><a id="connect"></a>Connect with Remote Desktop</span></span>
<span data-ttu-id="80621-114">依照 [使用 RDP 連線到 HDInsight 叢集](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp)中的指示，為 HDInsight 叢集啟用遠端桌面，然後進行連線。</span><span class="sxs-lookup"><span data-stu-id="80621-114">Enable Remote Desktop for the HDInsight cluster, then connect to it by following the instructions at [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>

## <span data-ttu-id="80621-115"><a id="hive"></a>使用 Hive 命令</span><span class="sxs-lookup"><span data-stu-id="80621-115"><a id="hive"></a>Use the Hive command</span></span>
<span data-ttu-id="80621-116">當您連線到 HDInsight 叢集的桌面時，請使用下列步驟來使用 Hive：</span><span class="sxs-lookup"><span data-stu-id="80621-116">When you have connected to the desktop for the HDInsight cluster, use the following steps to work with Hive:</span></span>

1. <span data-ttu-id="80621-117">從 HDInsight 桌面，啟動 **Hadoop 命令列**。</span><span class="sxs-lookup"><span data-stu-id="80621-117">From the HDInsight desktop, start the **Hadoop Command Line**.</span></span>
2. <span data-ttu-id="80621-118">輸入下列命令以啟動 Hive CLI：</span><span class="sxs-lookup"><span data-stu-id="80621-118">Enter the following command to start the Hive CLI:</span></span>

        %hive_home%\bin\hive

    <span data-ttu-id="80621-119">啟動 CLI 之後，將會看到 Hive CLI 提示字元： `hive>`。</span><span class="sxs-lookup"><span data-stu-id="80621-119">When the CLI has started, you will see the Hive CLI prompt: `hive>`.</span></span>
3. <span data-ttu-id="80621-120">使用 CLI，輸入下列陳述式，以使用範例資料來建立名為 **log4jLogs** 的新資料表：</span><span class="sxs-lookup"><span data-stu-id="80621-120">Using the CLI, enter the following statements to create a new table named **log4jLogs** using sample data:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="80621-121">這些陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="80621-121">These statements perform the following actions:</span></span>

   * <span data-ttu-id="80621-122">**DROP TABLE**：刪除資料表和資料檔 (如果資料表已存在)。</span><span class="sxs-lookup"><span data-stu-id="80621-122">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="80621-123">**CREATE EXTERNAL TABLE**：在 Hive 中建立新的「外部」資料表。</span><span class="sxs-lookup"><span data-stu-id="80621-123">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="80621-124">外部資料表只會在 Hive 中儲存資料表定義 (資料會保留在原始位置)。</span><span class="sxs-lookup"><span data-stu-id="80621-124">External tables store only the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="80621-125">當您預期以外部來源更新基礎資料 (例如自動化資料上傳程序)，或以其他 MapReduce 作業更新基礎資料，但希望 Hive 查詢一律使用最新資料時，必須使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="80621-125">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="80621-126">捨棄外部資料表並 **不會** 刪除資料，只會刪除資料表定義。</span><span class="sxs-lookup"><span data-stu-id="80621-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="80621-127">**ROW FORMAT**：告訴 Hive 如何格式化資料。</span><span class="sxs-lookup"><span data-stu-id="80621-127">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="80621-128">在此情況下，每個記錄中的欄位會以空格隔開。</span><span class="sxs-lookup"><span data-stu-id="80621-128">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="80621-129">**STORED AS TEXTFILE LOCATION**：告訴 Hive 資料的儲存位置 (example/data 目錄) 且資料儲存為文字。</span><span class="sxs-lookup"><span data-stu-id="80621-129">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>
   * <span data-ttu-id="80621-130">**SELECT**：選擇其資料欄 **t4** 包含值 **[ERROR]** 的所有資料列計數。</span><span class="sxs-lookup"><span data-stu-id="80621-130">**SELECT**: Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="80621-131">這應該會傳回值 **3** ，因為有三個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="80621-131">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="80621-132">**INPUT__FILE__NAME LIKE '%.log'** - 告訴 Hive 我們只應該從檔名以 log 結尾的檔案中傳回資料。</span><span class="sxs-lookup"><span data-stu-id="80621-132">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="80621-133">這將限制包含此資料的 sample.log 檔案搜尋，對於不符合我們所定義結構描述的其他範例資料檔案，會防止其傳回資料。</span><span class="sxs-lookup"><span data-stu-id="80621-133">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
4. <span data-ttu-id="80621-134">使用下列陳述式來建立名為 **errorLogs**的新「內部」資料表：</span><span class="sxs-lookup"><span data-stu-id="80621-134">Use the following statements to create a new 'internal' table named **errorLogs**:</span></span>

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    <span data-ttu-id="80621-135">這些陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="80621-135">These statements perform the following actions:</span></span>

   * <span data-ttu-id="80621-136">**CREATE TABLE IF NOT EXISTS**：建立資料表 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="80621-136">**CREATE TABLE IF NOT EXISTS**: Creates a table if it does not already exist.</span></span> <span data-ttu-id="80621-137">因為未使用 **EXTERNAL** 關鍵字，所以這是內部資料表，而內部資料表儲存在 Hive 資料倉儲中，並完全透過 Hive 來管理。</span><span class="sxs-lookup"><span data-stu-id="80621-137">Because the **EXTERNAL** keyword is not used, this is an internal table, which is stored in the Hive data warehouse and is managed completely by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="80621-138">與 **EXTERNAL** 資料表不同之處在於，捨棄內部資料表也會刪除基礎資料。</span><span class="sxs-lookup"><span data-stu-id="80621-138">Unlike **EXTERNAL** tables, dropping an internal table also deletes the underlying data.</span></span>
     >
     >
   * <span data-ttu-id="80621-139">**STORED AS ORC**：以最佳化資料列單欄式 (Optimized Row Columnar, ORC) 格式儲存資料。</span><span class="sxs-lookup"><span data-stu-id="80621-139">**STORED AS ORC**: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="80621-140">這是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="80621-140">This is a highly optimized and efficient format for storing Hive data.</span></span>
   * <span data-ttu-id="80621-141">**INSERT OVERWRITE ...SELECT**：從包含 **[ERROR]** 的 **log4jLogs** 資料表選取資料列，然後將資料插入 **errorLogs** 資料表。</span><span class="sxs-lookup"><span data-stu-id="80621-141">**INSERT OVERWRITE ... SELECT**: Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

     <span data-ttu-id="80621-142">若要確認只將資料行 t4 中包含 **[ERROR]** 的資料列儲存至 **errorLogs** 資料表，請使用下列陳述式，傳回 **errorLogs** 中的所有資料列：</span><span class="sxs-lookup"><span data-stu-id="80621-142">To verify that only rows that contain **[ERROR]** in column t4 were stored to the **errorLogs** table, use the following statement to return all the rows from **errorLogs**:</span></span>

       <span data-ttu-id="80621-143">SELECT * from errorLogs;</span><span class="sxs-lookup"><span data-stu-id="80621-143">SELECT * from errorLogs;</span></span>

     <span data-ttu-id="80621-144">應該傳回三個資料列，且在資料行 t4 中全部包含 **[ERROR]** 。</span><span class="sxs-lookup"><span data-stu-id="80621-144">Three rows of data should be returned, all containing **[ERROR]** in column t4.</span></span>

## <span data-ttu-id="80621-145"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="80621-145"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="80621-146">如您所見，Hive 命令提供簡單的方法，以互動方式在 HDInsight 叢集上執行 Hive 查詢、監視工作狀態，以及擷取輸出。</span><span class="sxs-lookup"><span data-stu-id="80621-146">As you can see, the the Hive command provides an easy way to interactively run Hive queries on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="80621-147"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="80621-147"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="80621-148">如需 HDInsight 中 Hive 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="80621-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="80621-149">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="80621-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="80621-150">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="80621-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="80621-151">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="80621-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="80621-152">搭配 HDInsight 上的 Hadoop 使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="80621-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="80621-153">如果您搭配使用 Tez 和 Hive，請參閱下列文件所提供的偵錯資訊：</span><span class="sxs-lookup"><span data-stu-id="80621-153">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="80621-154">在以 Windows 為基礎的 HDInsight 上使用 Tez UI</span><span class="sxs-lookup"><span data-stu-id="80621-154">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="80621-155">在以 Linux 為基礎的 HDInsight 上使用 Ambari Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="80621-155">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
