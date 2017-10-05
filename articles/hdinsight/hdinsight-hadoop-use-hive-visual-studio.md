---
title: "搭配使用 Hive 與 Data Lake (Hadoop) Tools for Visual Studio - Azure HDInsight | Microsoft Docs"
description: "了解如何使用 Data Lake Tools for Visual Studio 在 Azure HDInsight 上搭配 Apache Hadoop 執行 Apache Hive 查詢。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 3411c59fee73aa2e26a05d70e1dae11cdfc865ff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-data-lake-tools-for-visual-studio"></a><span data-ttu-id="9146b-103">使用 Data Lake Tools for Visual Studio 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="9146b-103">Run Hive queries using the Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="9146b-104">了解如何使用 Data Lake Tools for Visual Studio 查詢 Apache Hive。</span><span class="sxs-lookup"><span data-stu-id="9146b-104">Learn how to use the Data Lake tools for Visual Studio to query Apache Hive.</span></span> <span data-ttu-id="9146b-105">Data Lake Tools 可讓您在 Azure HDInsight 上輕鬆地建立、提交和監視對 Hadoop 的 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="9146b-105">The Data Lake tools allow you to easily create, submit, and monitor Hive queries to Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="9146b-106"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="9146b-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="9146b-107">Azure HDInsight (HDInsight 上的 Hadoop) 叢集</span><span class="sxs-lookup"><span data-stu-id="9146b-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="9146b-108">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="9146b-108">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="9146b-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="9146b-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="9146b-110">Visual Studio (下列其中一個版本)：</span><span class="sxs-lookup"><span data-stu-id="9146b-110">Visual Studio (one of the following versions):</span></span>

    * <span data-ttu-id="9146b-111">Visual Studio 2013 Community/Professional/Premium/Ultimate，含 Update 4</span><span class="sxs-lookup"><span data-stu-id="9146b-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="9146b-112">Visual Studio 2015 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="9146b-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="9146b-113">Visual Studio 2017 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="9146b-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="9146b-114">HDInsight tools for Visual Studio 或 Azure Data Lake tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="9146b-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="9146b-115">如需有關安裝和設定工具的資訊，請參閱 [開始使用 Visual Studio Hadoop Tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) 。</span><span class="sxs-lookup"><span data-stu-id="9146b-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring the tools.</span></span>

## <span data-ttu-id="9146b-116"><a id="run"></a> 使用 Visual Studio 執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="9146b-116"><a id="run"></a> Run Hive queries using the Visual Studio</span></span>

1. <span data-ttu-id="9146b-117">開啟 **Visual Studio**，然後選取 [新增]  >  [專案]  >  [Azure Data Lake]  >  [HIVE]  >  [Hive 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="9146b-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="9146b-118">提供此專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="9146b-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="9146b-119">開啟使用此專案所建立的 **Script.hql** 檔案，並貼入下列 HiveQL 陳述式中：</span><span class="sxs-lookup"><span data-stu-id="9146b-119">Open the **Script.hql** file that is created with this project, and paste in the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="9146b-120">這些陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9146b-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="9146b-121">`DROP TABLE`︰如果資料表存在，此陳述式將刪除它。</span><span class="sxs-lookup"><span data-stu-id="9146b-121">`DROP TABLE`: If the table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="9146b-122">`CREATE EXTERNAL TABLE`在 Hive 中建立新的「外部」資料表。</span><span class="sxs-lookup"><span data-stu-id="9146b-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="9146b-123">外部資料表只會在 Hive 中儲存資料表定義 (資料會保留在原始位置)。</span><span class="sxs-lookup"><span data-stu-id="9146b-123">External tables only store the table definition in Hive (the data is left in the original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="9146b-124">當您預期會由外部來源來更新基礎資料時，請使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="9146b-124">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="9146b-125">例如，MapReduce 工作或 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="9146b-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="9146b-126">捨棄外部資料表並 **不會** 刪除資料，只會刪除資料表定義。</span><span class="sxs-lookup"><span data-stu-id="9146b-126">Dropping an external table does **not** delete the data, only the table definition.</span></span>

   * <span data-ttu-id="9146b-127">`ROW FORMAT`：告訴 Hive 如何格式化資料。</span><span class="sxs-lookup"><span data-stu-id="9146b-127">`ROW FORMAT`: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="9146b-128">在此情況下，每個記錄中的欄位會以空格隔開。</span><span class="sxs-lookup"><span data-stu-id="9146b-128">In this case, the fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="9146b-129">`STORED AS TEXTFILE LOCATION`：將資料的儲存位置告訴 Hive (example/data 目錄)，且資料儲存為文字。</span><span class="sxs-lookup"><span data-stu-id="9146b-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where the data is stored (the example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="9146b-130">`SELECT`：選擇其資料欄 `t4` 包含值 `[ERROR]` 的所有資料列計數。</span><span class="sxs-lookup"><span data-stu-id="9146b-130">`SELECT`: Select a count of all rows where column `t4` contains the value `[ERROR]`.</span></span> <span data-ttu-id="9146b-131">這個陳述式會傳回值 `3`，因為有三個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="9146b-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="9146b-132">`INPUT__FILE__NAME LIKE '%.log'` - 告訴 Hive 我們只應該從檔名以 log 結尾的檔案中傳回資料。</span><span class="sxs-lookup"><span data-stu-id="9146b-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="9146b-133">這個子句會將搜尋限制為包含資料的 sample.log 檔案。</span><span class="sxs-lookup"><span data-stu-id="9146b-133">This clause restricts the search to the sample.log file that contains the data.</span></span>

3. <span data-ttu-id="9146b-134">從工具列中，選取您想要用於此查詢的 **Hdinsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="9146b-134">From the toolbar, select the **HDInsight Cluster** that you want to use for this query.</span></span> <span data-ttu-id="9146b-135">選取**提交**以 Hive 作業形式執行陳述式。</span><span class="sxs-lookup"><span data-stu-id="9146b-135">Select **Submit** to run the statements as a Hive job.</span></span>

   ![提交列](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="9146b-137">[Hive 工作摘要] 將會出現並顯示執行中工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="9146b-137">The **Hive Job Summary** appears and displays information about the running job.</span></span> <span data-ttu-id="9146b-138">使用 [重新整理] 連結來重新整理工作資訊，直到 [工作狀態] 變更為 [已完成] 為止。</span><span class="sxs-lookup"><span data-stu-id="9146b-138">Use the **Refresh** link to refresh the job information, until the **Job Status** changes to **Completed**.</span></span>

   ![顯示已完成作業的作業摘要](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="9146b-140">使用 [ **工作輸出** ] 連結檢視此工作的輸出。</span><span class="sxs-lookup"><span data-stu-id="9146b-140">Use the **Job Output** link to view the output of this job.</span></span> <span data-ttu-id="9146b-141">它會顯示 `[ERROR] 3`，這是此查詢所傳回的值。</span><span class="sxs-lookup"><span data-stu-id="9146b-141">It displays `[ERROR] 3`, which is the value returned by this query.</span></span>

6. <span data-ttu-id="9146b-142">您也可以執行 Hive 查詢，而不需建立專案。</span><span class="sxs-lookup"><span data-stu-id="9146b-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="9146b-143">使用 [伺服器總管]，展開 [Azure] > [HDInsight]，在 HDInsight 伺服器上按一下滑鼠右鍵，然後選取 [撰寫 Hive 查詢]。</span><span class="sxs-lookup"><span data-stu-id="9146b-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="9146b-144">在出現的 **temp.hql** 文件，新增下列 HiveQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="9146b-144">In the **temp.hql** document that appears, add the following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="9146b-145">這些陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="9146b-145">These statements perform the following actions:</span></span>

   * <span data-ttu-id="9146b-146">`CREATE TABLE IF NOT EXISTS`：建立資料表 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="9146b-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="9146b-147">因為未使用 `EXTERNAL` 關鍵字，這個陳述式會建立內部資料表。</span><span class="sxs-lookup"><span data-stu-id="9146b-147">Because the `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="9146b-148">內部資料表儲存在 Hive 資料倉儲中，並受到 Hive 所管理。</span><span class="sxs-lookup"><span data-stu-id="9146b-148">Internal tables are stored in the Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="9146b-149">與 `EXTERNAL` 資料表不同之處在於，捨棄內部資料表也會刪除基礎資料。</span><span class="sxs-lookup"><span data-stu-id="9146b-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes the underlying data.</span></span>

   * <span data-ttu-id="9146b-150">`STORED AS ORC`：以最佳化資料列單欄式 (Optimized Row Columnar, ORC) 格式儲存資料。</span><span class="sxs-lookup"><span data-stu-id="9146b-150">`STORED AS ORC`: Stores the data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="9146b-151">ORC 是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="9146b-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="9146b-152">`INSERT OVERWRITE ... SELECT`︰從含有 `[ERROR]`的 `log4jLogs` 資料表選取資料列，然後將資料插入 `errorLogs` 資料表。</span><span class="sxs-lookup"><span data-stu-id="9146b-152">`INSERT OVERWRITE ... SELECT`: Selects rows from the `log4jLogs` table that contain `[ERROR]`, then inserts the data into the `errorLogs` table.</span></span>

8. <span data-ttu-id="9146b-153">從工具列中，選取 [ **提交** ] 來執行工作。</span><span class="sxs-lookup"><span data-stu-id="9146b-153">From the toolbar, select **Submit** to run the job.</span></span> <span data-ttu-id="9146b-154">使用 [ **工作狀態** ] 來判斷工作是否已順利完成。</span><span class="sxs-lookup"><span data-stu-id="9146b-154">Use the **Job Status** to determine that the job has completed successfully.</span></span>

9. <span data-ttu-id="9146b-155">若要確認作業已建立資料表，請使用 [伺服器總管] 並展開 [Azure] > [HDInsight] > 您的 HDInsight 叢集 > [Hive 資料庫] > [預設]。</span><span class="sxs-lookup"><span data-stu-id="9146b-155">To verify that the job created the table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="9146b-156">會列出 **errorLogs** 資料表和 **log4jLogs** 資料表。</span><span class="sxs-lookup"><span data-stu-id="9146b-156">The **errorLogs** table and the **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="9146b-157"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="9146b-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="9146b-158">如您所見，HDInsight tools for Visual Studio 提供簡單的方法，可在 HDInsight 上使用 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="9146b-158">As you can see, the HDInsight tools for Visual Studio provide an easy way to work with Hive queries on HDInsight.</span></span>

<span data-ttu-id="9146b-159">如需 HDInsight 中 Hive 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="9146b-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="9146b-160">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="9146b-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="9146b-161">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="9146b-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="9146b-162">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="9146b-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="9146b-163">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="9146b-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="9146b-164">如需 HDInsight Tools for Visual Studio 的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="9146b-164">For more information about the HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="9146b-165">開始使用 HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9146b-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
