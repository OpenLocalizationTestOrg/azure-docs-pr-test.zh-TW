---
title: "使用 Data Lake (Hadoop) tools for Visual Studio-Azure HDInsight aaaHive |Microsoft 文件"
description: "了解如何 toouse hello Data Lake 工具的 Visual Studio toorun Apache Hive 查詢的 Azure HDInsight 上的 Apache Hadoop。"
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
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a><span data-ttu-id="e681a-103">執行 Hive 查詢使用 hello Data Lake tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e681a-103">Run Hive queries using hello Data Lake tools for Visual Studio</span></span>

<span data-ttu-id="e681a-104">了解如何 toouse hello Data Lake 工具的 Visual Studio tooquery Apache hive 控制檔。</span><span class="sxs-lookup"><span data-stu-id="e681a-104">Learn how toouse hello Data Lake tools for Visual Studio tooquery Apache Hive.</span></span> <span data-ttu-id="e681a-105">hello Data Lake 工具可讓您 tooeasily 建立、 送出，並監視 Azure HDInsight 上的 Hive 查詢 tooHadoop。</span><span class="sxs-lookup"><span data-stu-id="e681a-105">hello Data Lake tools allow you tooeasily create, submit, and monitor Hive queries tooHadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="e681a-106"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="e681a-106"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="e681a-107">Azure HDInsight (HDInsight 上的 Hadoop) 叢集</span><span class="sxs-lookup"><span data-stu-id="e681a-107">An Azure HDInsight (Hadoop on HDInsight) cluster</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="e681a-108">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="e681a-108">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="e681a-109">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="e681a-109">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="e681a-110">Visual Studio （其中 hello 之後版本）：</span><span class="sxs-lookup"><span data-stu-id="e681a-110">Visual Studio (one of hello following versions):</span></span>

    * <span data-ttu-id="e681a-111">Visual Studio 2013 Community/Professional/Premium/Ultimate，含 Update 4</span><span class="sxs-lookup"><span data-stu-id="e681a-111">Visual Studio 2013 Community/Professional/Premium/Ultimate with Update 4</span></span>

    * <span data-ttu-id="e681a-112">Visual Studio 2015 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="e681a-112">Visual Studio 2015 (any edition)</span></span>

    * <span data-ttu-id="e681a-113">Visual Studio 2017 (任何版本)</span><span class="sxs-lookup"><span data-stu-id="e681a-113">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="e681a-114">HDInsight tools for Visual Studio 或 Azure Data Lake tools for Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="e681a-114">HDInsight tools for Visual Studio or Azure Data Lake tools for Visual Studio.</span></span> <span data-ttu-id="e681a-115">請參閱[開始使用 Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md)如需有關安裝和設定 hello 工具資訊。</span><span class="sxs-lookup"><span data-stu-id="e681a-115">See [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installing and configuring hello tools.</span></span>

## <span data-ttu-id="e681a-116"><a id="run"></a>執行使用 Visual Studio hello 的 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="e681a-116"><a id="run"></a> Run Hive queries using hello Visual Studio</span></span>

1. <span data-ttu-id="e681a-117">開啟 **Visual Studio**，然後選取 [新增]  >  [專案]  >  [Azure Data Lake]  >  [HIVE]  >  [Hive 應用程式]。</span><span class="sxs-lookup"><span data-stu-id="e681a-117">Open **Visual Studio** and select **New** > **Project** > **Azure Data Lake** > **HIVE** > **Hive Application**.</span></span> <span data-ttu-id="e681a-118">提供此專案的名稱。</span><span class="sxs-lookup"><span data-stu-id="e681a-118">Provide a name for this project.</span></span>

2. <span data-ttu-id="e681a-119">開啟 hello **Script.hql**檔案用來建立此專案，並貼上的下列 HiveQL 陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e681a-119">Open hello **Script.hql** file that is created with this project, and paste in hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    <span data-ttu-id="e681a-120">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="e681a-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="e681a-121">`DROP TABLE`： 如果 hello 資料表存在，此陳述式會刪除它。</span><span class="sxs-lookup"><span data-stu-id="e681a-121">`DROP TABLE`: If hello table exists, this statement deletes it.</span></span>

   * <span data-ttu-id="e681a-122">`CREATE EXTERNAL TABLE`在 Hive 中建立新的「外部」資料表。</span><span class="sxs-lookup"><span data-stu-id="e681a-122">`CREATE EXTERNAL TABLE`: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="e681a-123">外部資料表只儲存區 (hello 資料會保留在 hello 原始位置) 中的 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="e681a-123">External tables only store hello table definition in Hive (hello data is left in hello original location).</span></span>

     > [!NOTE]
     > <span data-ttu-id="e681a-124">當您希望產生 hello 由外部來源更新基礎資料 toobe，應該使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="e681a-124">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="e681a-125">例如，MapReduce 工作或 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="e681a-125">For example, a MapReduce job or Azure service.</span></span>
     >
     > <span data-ttu-id="e681a-126">卸除的外部資料表沒有**不**刪除 hello 資料、 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="e681a-126">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

   * <span data-ttu-id="e681a-127">`ROW FORMAT`： 會告知的 Hive hello 資料格式化的方式。</span><span class="sxs-lookup"><span data-stu-id="e681a-127">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="e681a-128">在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="e681a-128">In this case, hello fields in each log are separated by a space.</span></span>

   * <span data-ttu-id="e681a-129">`STORED AS TEXTFILE LOCATION`： 會告知 Hive 其中 hello 資料會儲存 （hello 範例/資料目錄），則會儲存為文字。</span><span class="sxs-lookup"><span data-stu-id="e681a-129">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text.</span></span>

   * <span data-ttu-id="e681a-130">`SELECT`： 選取所有資料列計數其中資料行`t4`包含 hello 值`[ERROR]`。</span><span class="sxs-lookup"><span data-stu-id="e681a-130">`SELECT`: Select a count of all rows where column `t4` contains hello value `[ERROR]`.</span></span> <span data-ttu-id="e681a-131">這個陳述式會傳回值 `3`，因為有三個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="e681a-131">This statement returns a value of `3` because there are three rows that contain this value.</span></span>

   * <span data-ttu-id="e681a-132">`INPUT__FILE__NAME LIKE '%.log'` - 告訴 Hive 我們只應該從檔名以 log 結尾的檔案中傳回資料。</span><span class="sxs-lookup"><span data-stu-id="e681a-132">`INPUT__FILE__NAME LIKE '%.log'` - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="e681a-133">這個子句會限制 hello 搜尋 toohello sample.log 包含 hello 資料檔案。</span><span class="sxs-lookup"><span data-stu-id="e681a-133">This clause restricts hello search toohello sample.log file that contains hello data.</span></span>

3. <span data-ttu-id="e681a-134">從 hello 工具列中，選取 hello **HDInsight 叢集**想要此查詢 toouse。</span><span class="sxs-lookup"><span data-stu-id="e681a-134">From hello toolbar, select hello **HDInsight Cluster** that you want toouse for this query.</span></span> <span data-ttu-id="e681a-135">選取**送出**toorun hello 陳述式，稱為 Hive 工作。</span><span class="sxs-lookup"><span data-stu-id="e681a-135">Select **Submit** toorun hello statements as a Hive job.</span></span>

   ![提交列](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. <span data-ttu-id="e681a-137">hello **Hive 工作摘要**隨即出現，並顯示 hello 執行作業的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e681a-137">hello **Hive Job Summary** appears and displays information about hello running job.</span></span> <span data-ttu-id="e681a-138">使用 hello**重新整理**連結 toorefresh hello 工作資訊，直到 hello**作業狀態**變更太**已完成**。</span><span class="sxs-lookup"><span data-stu-id="e681a-138">Use hello **Refresh** link toorefresh hello job information, until hello **Job Status** changes too**Completed**.</span></span>

   ![顯示已完成作業的作業摘要](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. <span data-ttu-id="e681a-140">使用 hello**作業輸出**連結 tooview hello 輸出，此作業。</span><span class="sxs-lookup"><span data-stu-id="e681a-140">Use hello **Job Output** link tooview hello output of this job.</span></span> <span data-ttu-id="e681a-141">它會顯示`[ERROR] 3`，這是此查詢所傳回的 hello 值。</span><span class="sxs-lookup"><span data-stu-id="e681a-141">It displays `[ERROR] 3`, which is hello value returned by this query.</span></span>

6. <span data-ttu-id="e681a-142">您也可以執行 Hive 查詢，而不需建立專案。</span><span class="sxs-lookup"><span data-stu-id="e681a-142">You can also run Hive queries without creating a project.</span></span> <span data-ttu-id="e681a-143">使用 [伺服器總管]，展開 [Azure] > [HDInsight]，在 HDInsight 伺服器上按一下滑鼠右鍵，然後選取 [撰寫 Hive 查詢]。</span><span class="sxs-lookup"><span data-stu-id="e681a-143">Using **Server Explorer**, expand **Azure** > **HDInsight**, right-click your HDInsight server, and then select **Write a Hive Query**.</span></span>

7. <span data-ttu-id="e681a-144">在 hello **temp.hql**文件出現，新增下列 HiveQL 陳述式的 hello:</span><span class="sxs-lookup"><span data-stu-id="e681a-144">In hello **temp.hql** document that appears, add hello following HiveQL statements:</span></span>

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    <span data-ttu-id="e681a-145">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="e681a-145">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="e681a-146">`CREATE TABLE IF NOT EXISTS`：建立資料表 (如果不存在)。</span><span class="sxs-lookup"><span data-stu-id="e681a-146">`CREATE TABLE IF NOT EXISTS`: Creates a table if it does not already exist.</span></span> <span data-ttu-id="e681a-147">因為 hello`EXTERNAL`不是關鍵字，這個陳述式會建立內部資料表。</span><span class="sxs-lookup"><span data-stu-id="e681a-147">Because hello `EXTERNAL` keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="e681a-148">內部資料表會儲存在 hello Hive 資料倉儲，而且由登錄區。</span><span class="sxs-lookup"><span data-stu-id="e681a-148">Internal tables are stored in hello Hive data warehouse and are managed by Hive.</span></span>

     > [!NOTE]
     > <span data-ttu-id="e681a-149">不同於`EXTERNAL`資料表，卸除內部資料表也會刪除基礎資料的 hello。</span><span class="sxs-lookup"><span data-stu-id="e681a-149">Unlike `EXTERNAL` tables, dropping an internal table also deletes hello underlying data.</span></span>

   * <span data-ttu-id="e681a-150">`STORED AS ORC`： 儲存 hello 單欄式 (ORC) 格式最佳化的資料列的資料。</span><span class="sxs-lookup"><span data-stu-id="e681a-150">`STORED AS ORC`: Stores hello data in optimized row columnar (ORC) format.</span></span> <span data-ttu-id="e681a-151">ORC 是高度最佳化且有效率的 Hive 資料儲存格式。</span><span class="sxs-lookup"><span data-stu-id="e681a-151">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

   * <span data-ttu-id="e681a-152">`INSERT OVERWRITE ... SELECT`： 選取資料列從 hello`log4jLogs`包含資料表`[ERROR]`，然後插入到 hello hello 資料`errorLogs`資料表。</span><span class="sxs-lookup"><span data-stu-id="e681a-152">`INSERT OVERWRITE ... SELECT`: Selects rows from hello `log4jLogs` table that contain `[ERROR]`, then inserts hello data into hello `errorLogs` table.</span></span>

8. <span data-ttu-id="e681a-153">從 [hello] 工具列中，選取**送出**toorun hello 作業。</span><span class="sxs-lookup"><span data-stu-id="e681a-153">From hello toolbar, select **Submit** toorun hello job.</span></span> <span data-ttu-id="e681a-154">使用 hello**作業狀態**toodetermine hello 工作已順利完成。</span><span class="sxs-lookup"><span data-stu-id="e681a-154">Use hello **Job Status** toodetermine that hello job has completed successfully.</span></span>

9. <span data-ttu-id="e681a-155">hello 建立 hello 資料表，請使用作業的 tooverify**伺服器總管**展開**Azure** > **HDInsight** > 您的 HDInsight 叢集 > **Hive 資料庫** > **預設**。</span><span class="sxs-lookup"><span data-stu-id="e681a-155">tooverify that hello job created hello table, use **Server Explorer** and expand **Azure** > **HDInsight** > your HDInsight cluster > **Hive Databases** > **default**.</span></span> <span data-ttu-id="e681a-156">hello**錯誤記錄檔**資料表和 hello **log4jLogs**資料表會列出。</span><span class="sxs-lookup"><span data-stu-id="e681a-156">hello **errorLogs** table and hello **log4jLogs** table are listed.</span></span>

## <span data-ttu-id="e681a-157"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="e681a-157"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="e681a-158">如您所見，hello HDInsight tools for Visual Studio 會提供使用 Hive 查詢輕鬆 toowork HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="e681a-158">As you can see, hello HDInsight tools for Visual Studio provide an easy way toowork with Hive queries on HDInsight.</span></span>

<span data-ttu-id="e681a-159">如需 HDInsight 中 Hive 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="e681a-159">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="e681a-160">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="e681a-160">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="e681a-161">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="e681a-161">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="e681a-162">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="e681a-162">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

* [<span data-ttu-id="e681a-163">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="e681a-163">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="e681a-164">如需有關 hello HDInsight tools for Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="e681a-164">For more information about hello HDInsight tools for Visual Studio:</span></span>

* [<span data-ttu-id="e681a-165">開始使用 HDInsight Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="e681a-165">Getting started with HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-visual-studio-tools-get-started.md)

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
