---
title: "在 HDInsight 中的查詢主控台上使用 Hadoop Hive - Azure | Microsoft Docs"
description: "學習如何使用 Web 型查詢主控台，透過瀏覽器在 HDInsight Hadoop 叢集上執行 Hive 查詢。"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 9ccac43ae365d79bfd6ac1edf4d9a799c11356a1
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-the-query-console"></a><span data-ttu-id="ba37f-103">使用查詢主控台執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="ba37f-103">Run Hive queries using the Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="ba37f-104">在本文中，您將學習如何使用 HDInsight 查詢主控台，透過瀏覽器在 HDInsight Hadoop 叢集上執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="ba37f-104">In this article, you will learn how to use the HDInsight Query Console to run Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba37f-105">只有在 Windows 型 HDInsight 叢集上才能使用 HDInsight 查詢主控台。</span><span class="sxs-lookup"><span data-stu-id="ba37f-105">The HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="ba37f-106">Linux 是唯一使用於 HDInsight 3.4 版或更新版本的作業系統。</span><span class="sxs-lookup"><span data-stu-id="ba37f-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ba37f-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="ba37f-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="ba37f-108">針對 HDInsight 3.4 或更新版本，請參閱[在 Ambari Hive 檢視中執行 Hive 查詢](hdinsight-hadoop-use-hive-ambari-view.md)，以取得有關從網頁瀏覽器執行 Hive 查詢的資訊。</span><span class="sxs-lookup"><span data-stu-id="ba37f-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="ba37f-109"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="ba37f-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="ba37f-110">若要完成本文中的步驟，您需要下列項目。</span><span class="sxs-lookup"><span data-stu-id="ba37f-110">To complete the steps in this article, you will need the following.</span></span>

* <span data-ttu-id="ba37f-111">Windows 型 HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="ba37f-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="ba37f-112">現代網頁瀏覽器</span><span class="sxs-lookup"><span data-stu-id="ba37f-112">A modern web browser</span></span>

## <span data-ttu-id="ba37f-113"><a id="run"></a> 使用查詢主控台執行 Hive 查詢</span><span class="sxs-lookup"><span data-stu-id="ba37f-113"><a id="run"></a> Run Hive queries using the Query Console</span></span>
1. <span data-ttu-id="ba37f-114">開啟網頁瀏覽器並瀏覽至 **https://CLUSTERNAME.azurehdinsight.net**，其中 **CLUSTERNAME** 是 HDInsight 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="ba37f-114">Open a web browser and navigate to **https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is the name of your HDInsight cluster.</span></span> <span data-ttu-id="ba37f-115">出現提示時，輸入您建立叢集時所使用的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="ba37f-115">If prompted, enter the user name and password that you used when you created the cluster.</span></span>
2. <span data-ttu-id="ba37f-116">在頁面頂端的連結中，選取 [ **Hive 編輯器**]。</span><span class="sxs-lookup"><span data-stu-id="ba37f-116">From the links at the top of the page, select **Hive Editor**.</span></span> <span data-ttu-id="ba37f-117">這會顯示一個表單，而此表單可用來輸入您要在 HDInsight 叢集中執行的 HiveQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="ba37f-117">This displays a form that can be used to enter the HiveQL statements that you want to run in the HDInsight cluster.</span></span>

    ![Hive 編輯器](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="ba37f-119">將文字 `Select * from hivesampletable` 取代為下列 HiveQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ba37f-119">Replace the text `Select * from hivesampletable` with the following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="ba37f-120">這些陳述式會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="ba37f-120">These statements perform the following actions:</span></span>

   * <span data-ttu-id="ba37f-121">**DROP TABLE**：刪除資料表和資料檔 (如果資料表已存在)。</span><span class="sxs-lookup"><span data-stu-id="ba37f-121">**DROP TABLE**: Deletes the table and the data file if the table already exists.</span></span>
   * <span data-ttu-id="ba37f-122">**CREATE EXTERNAL TABLE**：在 Hive 中建立新的「外部」資料表。</span><span class="sxs-lookup"><span data-stu-id="ba37f-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="ba37f-123">外部資料表只會在 Hive 中儲存資料表定義；資料會保留在原始位置。</span><span class="sxs-lookup"><span data-stu-id="ba37f-123">External tables store only the table definition in Hive; the data is left in the original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ba37f-124">當您預期以外部來源更新基礎資料 (例如自動化資料上傳程序)，或以其他 MapReduce 作業更新基礎資料，但希望 Hive 查詢一律使用最新資料時，必須使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="ba37f-124">External tables should be used when you expect the underlying data to be updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries to use the latest data.</span></span>
     >
     > <span data-ttu-id="ba37f-125">捨棄外部資料表並 **不會** 刪除資料，只會刪除資料表定義。</span><span class="sxs-lookup"><span data-stu-id="ba37f-125">Dropping an external table does **not** delete the data, only the table definition.</span></span>
     >
     >
   * <span data-ttu-id="ba37f-126">**ROW FORMAT**：告訴 Hive 如何格式化資料。</span><span class="sxs-lookup"><span data-stu-id="ba37f-126">**ROW FORMAT**: Tells Hive how the data is formatted.</span></span> <span data-ttu-id="ba37f-127">在此情況下，每個記錄中的欄位會以空格隔開。</span><span class="sxs-lookup"><span data-stu-id="ba37f-127">In this case, the fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="ba37f-128">**STORED AS TEXTFILE LOCATION**：將資料的儲存位置告訴 Hive (example/data 目錄)，且資料儲存為文字</span><span class="sxs-lookup"><span data-stu-id="ba37f-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where the data is stored (the example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="ba37f-129">**SELECT**：選擇其資料欄 **t4** 包含值 **[ERROR]** 的所有資料列計數。</span><span class="sxs-lookup"><span data-stu-id="ba37f-129">**SELECT**: Select a count of all rows where column **t4** contain the value **[ERROR]**.</span></span> <span data-ttu-id="ba37f-130">這應該會傳回值 **3** ，因為有三個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="ba37f-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="ba37f-131">**INPUT__FILE__NAME LIKE '%.log'** - 告訴 Hive 我們只應該從檔名以 log 結尾的檔案中傳回資料。</span><span class="sxs-lookup"><span data-stu-id="ba37f-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="ba37f-132">這將限制包含此資料的 sample.log 檔案搜尋，對於不符合我們所定義結構描述的其他範例資料檔案，會防止其傳回資料。</span><span class="sxs-lookup"><span data-stu-id="ba37f-132">This restricts the search to the sample.log file that contains the data, and keeps it from returning data from other example data files that do not match the schema we defined.</span></span>
3. <span data-ttu-id="ba37f-133">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="ba37f-133">Click **Submit**.</span></span> <span data-ttu-id="ba37f-134">頁面底部的 [作業工作階段] 應該會顯示工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ba37f-134">The **Job Session** at the bottom of the page should display details for the job.</span></span>
4. <span data-ttu-id="ba37f-135">當 [狀態] 欄位變更為 [已完成] 時，請選取工作的 [檢視詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="ba37f-135">When the **Status** field changes to **Completed**, select **View Details** for the job.</span></span> <span data-ttu-id="ba37f-136">在詳細資料頁面上，[工作輸出] 包含 `[ERROR]    3`。</span><span class="sxs-lookup"><span data-stu-id="ba37f-136">On the details page, the **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="ba37f-137">您可以使用此欄位下方的 [ **下載** ] 按鈕，下載含有工作輸出的檔案。</span><span class="sxs-lookup"><span data-stu-id="ba37f-137">You can use the **Download** button under this field to download a file that contains the output of the job.</span></span>

## <span data-ttu-id="ba37f-138"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="ba37f-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="ba37f-139">如您所見，[查詢主控台] 提供簡單的方法，在 HDInsight 叢集中執行 Hive 查詢、監視工作狀態，以及擷取輸出。</span><span class="sxs-lookup"><span data-stu-id="ba37f-139">As you can see, the Query Console provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

<span data-ttu-id="ba37f-140">若要深入了解如何使用 Hive 查詢主控台執行 Hive 工作，請選取 [查詢主控台] 頂端的 [ **入門** ]，然後使用提供的範例。</span><span class="sxs-lookup"><span data-stu-id="ba37f-140">To learn more about using Hive Query Console to run Hive jobs, select **Getting Started** at the top of the Query Console, then use the samples that are provided.</span></span> <span data-ttu-id="ba37f-141">每個範例都會逐步進行使用 Hive 分析資料的程序 (包括範例中所用之 HiveQL 陳述式的說明)。</span><span class="sxs-lookup"><span data-stu-id="ba37f-141">Each sample walks through the process of using Hive to analyze data, including explanations about the HiveQL statements used in the sample.</span></span>

## <span data-ttu-id="ba37f-142"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="ba37f-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="ba37f-143">如需 HDInsight 中 Hive 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="ba37f-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="ba37f-144">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ba37f-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="ba37f-145">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="ba37f-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ba37f-146">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ba37f-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ba37f-147">搭配 HDInsight 上的 Hadoop 使用 MapReduce</span><span class="sxs-lookup"><span data-stu-id="ba37f-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="ba37f-148">如果您搭配使用 Tez 和 Hive，請參閱下列文件所提供的偵錯資訊：</span><span class="sxs-lookup"><span data-stu-id="ba37f-148">If you are using Tez with Hive, see the following documents for debugging information:</span></span>

* [<span data-ttu-id="ba37f-149">在以 Windows 為基礎的 HDInsight 上使用 Tez UI</span><span class="sxs-lookup"><span data-stu-id="ba37f-149">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="ba37f-150">在以 Linux 為基礎的 HDInsight 上使用 Ambari Tez 檢視</span><span class="sxs-lookup"><span data-stu-id="ba37f-150">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
