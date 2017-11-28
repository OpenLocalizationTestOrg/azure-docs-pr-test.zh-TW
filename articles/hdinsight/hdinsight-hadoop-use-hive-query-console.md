---
title: "hello HDInsight 的 Azure 中的 查詢主控台上 aaaUse Hadoop Hive |Microsoft 文件"
description: "了解如何 toouse hello 網頁查詢主控台 toorun Hive 查詢在 HDInsight Hadoop 叢集從您的瀏覽器。"
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
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a><span data-ttu-id="ec8bc-103">執行 Hive 查詢使用 hello 查詢主控台</span><span class="sxs-lookup"><span data-stu-id="ec8bc-103">Run Hive queries using hello Query Console</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="ec8bc-104">在本文中，您將學習如何 toouse hello HDInsight 查詢主控台 toorun Hive 查詢在 HDInsight Hadoop 叢集從您的瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-104">In this article, you will learn how toouse hello HDInsight Query Console toorun Hive queries on an HDInsight Hadoop cluster from your browser.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ec8bc-105">hello HDInsight 查詢主控台才可以使用 Windows 為基礎的 HDInsight 叢集上。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-105">hello HDInsight Query Console is only available on Windows-based HDInsight clusters.</span></span> <span data-ttu-id="ec8bc-106">Linux 為 hello 僅作業系統 HDInsight 3.4 或更新版本上使用。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ec8bc-107">如需詳細資訊，請參閱 [Windows 上的 HDInsight 淘汰](hdinsight-component-versioning.md#hdinsight-windows-retirement)。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="ec8bc-108">針對 HDInsight 3.4 或更新版本，請參閱[在 Ambari Hive 檢視中執行 Hive 查詢](hdinsight-hadoop-use-hive-ambari-view.md)，以取得有關從網頁瀏覽器執行 Hive 查詢的資訊。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-108">For HDInsight 3.4 or greater, see [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) for information on running Hive queries from a web browser.</span></span>

## <span data-ttu-id="ec8bc-109"><a id="prereq"></a>必要條件</span><span class="sxs-lookup"><span data-stu-id="ec8bc-109"><a id="prereq"></a>Prerequisites</span></span>
<span data-ttu-id="ec8bc-110">toocomplete hello 本文中的步驟，您將需要下列 hello。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-110">toocomplete hello steps in this article, you will need hello following.</span></span>

* <span data-ttu-id="ec8bc-111">Windows 型 HDInsight Hadoop 叢集</span><span class="sxs-lookup"><span data-stu-id="ec8bc-111">A Windows-based HDInsight Hadoop cluster</span></span>
* <span data-ttu-id="ec8bc-112">現代網頁瀏覽器</span><span class="sxs-lookup"><span data-stu-id="ec8bc-112">A modern web browser</span></span>

## <span data-ttu-id="ec8bc-113"><a id="run"></a>執行 Hive 查詢使用 hello 查詢主控台</span><span class="sxs-lookup"><span data-stu-id="ec8bc-113"><a id="run"></a> Run Hive queries using hello Query Console</span></span>
1. <span data-ttu-id="ec8bc-114">開啟網頁瀏覽器並瀏覽過**https://CLUSTERNAME.azurehdinsight.net**，其中**CLUSTERNAME** hello 您的 HDInsight 叢集名稱。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-114">Open a web browser and navigate too**https://CLUSTERNAME.azurehdinsight.net**, where **CLUSTERNAME** is hello name of your HDInsight cluster.</span></span> <span data-ttu-id="ec8bc-115">如果出現提示，請輸入 hello 使用者名稱和您在建立 hello 叢集時使用的密碼。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-115">If prompted, enter hello user name and password that you used when you created hello cluster.</span></span>
2. <span data-ttu-id="ec8bc-116">從 hello 頁面頂端的 hello hello 連結、 選取**登錄區編輯器**。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-116">From hello links at hello top of hello page, select **Hive Editor**.</span></span> <span data-ttu-id="ec8bc-117">這會顯示一個表單，可以是您想 toorun hello HDInsight 叢集中的使用的 tooenter hello HiveQL 陳述式。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-117">This displays a form that can be used tooenter hello HiveQL statements that you want toorun in hello HDInsight cluster.</span></span>

    ![hello 登錄區編輯器](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    <span data-ttu-id="ec8bc-119">取代 hello 文字`Select * from hivesampletable`以 hello 下列 HiveQL 陳述式：</span><span class="sxs-lookup"><span data-stu-id="ec8bc-119">Replace hello text `Select * from hivesampletable` with hello following HiveQL statements:</span></span>

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    <span data-ttu-id="ec8bc-120">這些陳述式會執行下列動作的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec8bc-120">These statements perform hello following actions:</span></span>

   * <span data-ttu-id="ec8bc-121">**DROP TABLE**: hello 資料表已存在時刪除 hello 資料表與 hello 資料檔。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-121">**DROP TABLE**: Deletes hello table and hello data file if hello table already exists.</span></span>
   * <span data-ttu-id="ec8bc-122">**CREATE EXTERNAL TABLE**：在 Hive 中建立新的「外部」資料表。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-122">**CREATE EXTERNAL TABLE**: Creates a new 'external' table in Hive.</span></span> <span data-ttu-id="ec8bc-123">外部資料表存放區; 只有 hello 資料表定義hello 資料會保留在 hello 原始位置。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-123">External tables store only hello table definition in Hive; hello data is left in hello original location.</span></span>

     > [!NOTE]
     > <span data-ttu-id="ec8bc-124">當您預期 hello 基礎資料 toobe 更新由外部來源 （例如自動化的資料上傳程序中） 或另一項 MapReduce 作業，但是您通常想要登錄區查詢 toouse hello 最新的資料，應該使用外部資料表。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-124">External tables should be used when you expect hello underlying data toobe updated by an external source (such as an automated data upload process) or by another MapReduce operation, but you always want Hive queries toouse hello latest data.</span></span>
     >
     > <span data-ttu-id="ec8bc-125">卸除的外部資料表沒有**不**刪除 hello 資料、 hello 資料表定義。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-125">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>
     >
     >
   * <span data-ttu-id="ec8bc-126">**資料列格式**: hello 資料格式化的方式會告知 hive 控制檔。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-126">**ROW FORMAT**: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="ec8bc-127">在此情況下，每個記錄檔中的 hello 欄位會以空格分隔。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-127">In this case, hello fields in each log are separated by a space.</span></span>
   * <span data-ttu-id="ec8bc-128">**儲存為文字檔位置**： 告訴 Hive 其中 hello 資料是儲存 （hello 範例/資料目錄），則會儲存為文字</span><span class="sxs-lookup"><span data-stu-id="ec8bc-128">**STORED AS TEXTFILE LOCATION**: Tells Hive where hello data is stored (hello example/data directory) and that it is stored as text</span></span>
   * <span data-ttu-id="ec8bc-129">**選取**： 選取所有資料列計數其中資料行**t4**包含 hello 值**[錯誤]**。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-129">**SELECT**: Select a count of all rows where column **t4** contain hello value **[ERROR]**.</span></span> <span data-ttu-id="ec8bc-130">這應該會傳回值 **3** ，因為有三個資料列包含此值。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-130">This should return a value of **3** because there are three rows that contain this value.</span></span>
   * <span data-ttu-id="ec8bc-131">**INPUT__FILE__NAME LIKE '%.log'** - 告訴 Hive 我們只應該從檔名以 log 結尾的檔案中傳回資料。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-131">**INPUT__FILE__NAME LIKE '%.log'** - Tells Hive that we should only return data from files ending in .log.</span></span> <span data-ttu-id="ec8bc-132">這會限制 hello 搜尋 toohello sample.log 檔案，其中包含 hello 資料，並防止從其他範例與 hello 我們所定義的結構描述不相符的資料檔案傳回資料。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-132">This restricts hello search toohello sample.log file that contains hello data, and keeps it from returning data from other example data files that do not match hello schema we defined.</span></span>
3. <span data-ttu-id="ec8bc-133">按一下 [提交] 。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-133">Click **Submit**.</span></span> <span data-ttu-id="ec8bc-134">hello**作業工作階段**在 hello hello 頁面底部應該會顯示 hello 工作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-134">hello **Job Session** at hello bottom of hello page should display details for hello job.</span></span>
4. <span data-ttu-id="ec8bc-135">當 hello**狀態**太欄位變更**已完成**，選取**檢視詳細資料**hello 作業。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-135">When hello **Status** field changes too**Completed**, select **View Details** for hello job.</span></span> <span data-ttu-id="ec8bc-136">在 hello 詳細資料頁面上，hello**作業輸出**包含`[ERROR]    3`。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-136">On hello details page, hello **Job Output** contains `[ERROR]    3`.</span></span> <span data-ttu-id="ec8bc-137">您可以使用 hello**下載**按鈕在此欄位 toodownload 包含 hello hello 工作輸出的檔案。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-137">You can use hello **Download** button under this field toodownload a file that contains hello output of hello job.</span></span>

## <span data-ttu-id="ec8bc-138"><a id="summary"></a>摘要</span><span class="sxs-lookup"><span data-stu-id="ec8bc-138"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="ec8bc-139">如您所見，查詢主控台提供簡單的方式 toorun hello Hive 查詢中的 HDInsight 叢集，監視 hello 作業狀態，並擷取 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-139">As you can see, hello Query Console provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

<span data-ttu-id="ec8bc-140">進一步了解使用 Hive 查詢主控台 toorun Hive 工作，toolearn 選取**入門**頂端 hello hello 查詢主控台，然後使用所提供的 hello 範例。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-140">toolearn more about using Hive Query Console toorun Hive jobs, select **Getting Started** at hello top of hello Query Console, then use hello samples that are provided.</span></span> <span data-ttu-id="ec8bc-141">每個範例會引導 hello 程序使用 Hive tooanalyze 資料，包括關於 hello 範例中所使用的 hello HiveQL 陳述式的說明。</span><span class="sxs-lookup"><span data-stu-id="ec8bc-141">Each sample walks through hello process of using Hive tooanalyze data, including explanations about hello HiveQL statements used in hello sample.</span></span>

## <span data-ttu-id="ec8bc-142"><a id="nextsteps"></a>接續步驟</span><span class="sxs-lookup"><span data-stu-id="ec8bc-142"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="ec8bc-143">如需 HDInsight 中 Hive 的一般資訊：</span><span class="sxs-lookup"><span data-stu-id="ec8bc-143">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="ec8bc-144">搭配使用 Hive 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ec8bc-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="ec8bc-145">如需您可以在 HDInsight 上使用 Hadoop 之其他方式的詳細資訊：</span><span class="sxs-lookup"><span data-stu-id="ec8bc-145">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="ec8bc-146">搭配使用 Pig 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ec8bc-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ec8bc-147">搭配使用 MapReduce 與 HDInsight 上的 Hadoop</span><span class="sxs-lookup"><span data-stu-id="ec8bc-147">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="ec8bc-148">如果您正在使用 Hive Tez，請參閱下列文件的偵錯資訊的 hello:</span><span class="sxs-lookup"><span data-stu-id="ec8bc-148">If you are using Tez with Hive, see hello following documents for debugging information:</span></span>

* [<span data-ttu-id="ec8bc-149">使用 Windows 為基礎的 HDInsight 上的 hello Tez UI</span><span class="sxs-lookup"><span data-stu-id="ec8bc-149">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="ec8bc-150">使用 hello Ambari Tez 以 Linux 為基礎的 HDInsight 上的檢視</span><span class="sxs-lookup"><span data-stu-id="ec8bc-150">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
