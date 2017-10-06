---
title: "aaaAnalyze Spark-Azure 中的 Python 程式庫的網站記錄檔 |Microsoft 文件"
description: "筆記本會示範如何 tooanalyze 記錄 Azure HDInsight 上的 Spark 中使用自訂的程式庫的資料。"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c61c70f-fe7f-4f0f-a4ab-0cccee5668c9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 29e4308b2a359aee6d69494a98307d4da07f7909
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="e1878-103">使用自訂 Python 程式庫搭配 HDInsight 上的 Spark 叢集來分析網站記錄</span><span class="sxs-lookup"><span data-stu-id="e1878-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="e1878-104">筆記本會示範如何 tooanalyze 記錄 HDInsight 上的 Spark 中使用自訂的程式庫的資料。</span><span class="sxs-lookup"><span data-stu-id="e1878-104">This notebook demonstrates how tooanalyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="e1878-105">我們使用 hello 自訂文件庫是 Python 程式庫呼叫**iislogparser.py**。</span><span class="sxs-lookup"><span data-stu-id="e1878-105">hello custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="e1878-106">本教學課程也適用於您在 HDInsight 中所建立 Spark (Linux) 叢集上的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="e1878-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="e1878-107">hello 筆記本體驗可讓您從本身的 hello 筆記本執行 hello Python 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="e1878-107">hello notebook experience lets you run hello Python snippets from hello notebook itself.</span></span> <span data-ttu-id="e1878-108">tooperform hello 教學課程中的筆記本內建立 Spark 叢集，請啟動 Jupyter 筆記本 (`https://CLUSTERNAME.azurehdinsight.net/jupyter`)，然後執行 hello 筆記本**分析記錄檔與使用自訂 library.ipynb Spark**下 hello **PySpark**資料夾。</span><span class="sxs-lookup"><span data-stu-id="e1878-108">tooperform hello tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run hello notebook **Analyze logs with Spark using a custom library.ipynb** under hello **PySpark** folder.</span></span>
>
>

<span data-ttu-id="e1878-109">**先決條件：**</span><span class="sxs-lookup"><span data-stu-id="e1878-109">**Prerequisites:**</span></span>

<span data-ttu-id="e1878-110">您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="e1878-110">You must have hello following:</span></span>

* <span data-ttu-id="e1878-111">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="e1878-111">An Azure subscription.</span></span> <span data-ttu-id="e1878-112">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="e1878-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="e1878-113">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="e1878-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="e1878-114">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="e1878-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="e1878-115">將原始資料儲存為 RDD</span><span class="sxs-lookup"><span data-stu-id="e1878-115">Save raw data as an RDD</span></span>
<span data-ttu-id="e1878-116">在本節中，我們使用 hello [Jupyter](https://jupyter.org)筆記本 HDInsight toorun 工作處理未經處理的範例資料，並將它儲存為 Hive 資料表中的 Apache Spark 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="e1878-116">In this section, we use hello [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight toorun jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="e1878-117">上的.csv 檔案 (hvac.csv) 使用預設的所有叢集 hello 範例資料。</span><span class="sxs-lookup"><span data-stu-id="e1878-117">hello sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="e1878-118">一旦您的資料會儲存為 Hive 資料表，在 hello 下一節我們將連接使用 BI 工具，例如 Power BI 和 Tableau toohello Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="e1878-118">Once your data is saved as a Hive table, in hello next section we will connect toohello Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="e1878-119">從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。</span><span class="sxs-lookup"><span data-stu-id="e1878-119">From hello [Azure portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="e1878-120">您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="e1878-120">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="e1878-121">從 hello Spark 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **Jupyter 筆記本**。</span><span class="sxs-lookup"><span data-stu-id="e1878-121">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="e1878-122">如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="e1878-122">If prompted, enter hello admin credentials for hello cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e1878-123">您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="e1878-123">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="e1878-124">取代**CLUSTERNAME** hello 名稱，為您的叢集：</span><span class="sxs-lookup"><span data-stu-id="e1878-124">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="e1878-125">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="e1878-125">Create a new notebook.</span></span> <span data-ttu-id="e1878-126">按一下 新增，然後按一下PySpark。</span><span class="sxs-lookup"><span data-stu-id="e1878-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="e1878-127">![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "建立新的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="e1878-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="e1878-128">建立新的記事本，並開啟 hello 名稱 Untitled.pynb。</span><span class="sxs-lookup"><span data-stu-id="e1878-128">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="e1878-129">按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="e1878-129">Click hello notebook name at hello top, and enter a friendly name.</span></span>

    <span data-ttu-id="e1878-130">![提供的名稱 hello 筆記本](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "提供 hello 筆記本的名稱")</span><span class="sxs-lookup"><span data-stu-id="e1878-130">![Provide a name for hello notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for hello notebook")</span></span>
5. <span data-ttu-id="e1878-131">因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。</span><span class="sxs-lookup"><span data-stu-id="e1878-131">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="e1878-132">hello Spark 和 Hive 內容將會自動為您建立執行 hello 第一個程式碼儲存格時。</span><span class="sxs-lookup"><span data-stu-id="e1878-132">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="e1878-133">您可以啟動匯入此案例所需的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="e1878-133">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="e1878-134">貼上下列程式碼片段中的空白儲存格，hello，然後按下**SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="e1878-134">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="e1878-135">建立 hello 叢集上使用 hello 範例記錄檔資料已提供 RDD。</span><span class="sxs-lookup"><span data-stu-id="e1878-135">Create an RDD using hello sample log data already available on hello cluster.</span></span> <span data-ttu-id="e1878-136">您可以存取 hello 與 hello 叢集相關聯的預設儲存體帳戶中的 hello 資料**\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**。</span><span class="sxs-lookup"><span data-stu-id="e1878-136">You can access hello data in hello default storage account associated with hello cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="e1878-137">範例記錄檔設定 tooverify 該 hello 前一步驟已順利完成的擷取。</span><span class="sxs-lookup"><span data-stu-id="e1878-137">Retrieve a sample log set tooverify that hello previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="e1878-138">您應該會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="e1878-138">You should see an output similar toohello following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="e1878-139">使用自訂 Python 程式庫來分析記錄資料</span><span class="sxs-lookup"><span data-stu-id="e1878-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="e1878-140">上述 hello 輸出前, 幾行 hello 包含 hello 標頭資訊和每個其餘的列符合該標頭中所述的 hello 結構描述。</span><span class="sxs-lookup"><span data-stu-id="e1878-140">In hello output above, hello first couple lines include hello header information and each remaining line matches hello schema described in that header.</span></span> <span data-ttu-id="e1878-141">剖析這類記錄檔可能是複雜的作業。</span><span class="sxs-lookup"><span data-stu-id="e1878-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="e1878-142">因此，我們使用自訂 Python 程式庫 (**iislogparser.py**)，它可大幅簡化這類記錄檔的剖析。</span><span class="sxs-lookup"><span data-stu-id="e1878-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="e1878-143">依預設，此程式庫會包含在位於以下位置的 HDInsight 上的 Spark 叢集中： **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**。</span><span class="sxs-lookup"><span data-stu-id="e1878-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="e1878-144">不過，此程式庫不在 hello`PYTHONPATH`因此我們使用類似的匯入陳述式不能使用它`import iislogparser`。</span><span class="sxs-lookup"><span data-stu-id="e1878-144">However, this library is not in hello `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="e1878-145">toouse 此程式庫，我們必須將它散發 tooall hello 背景工作節點。</span><span class="sxs-lookup"><span data-stu-id="e1878-145">toouse this library, we must distribute it tooall hello worker nodes.</span></span> <span data-ttu-id="e1878-146">執行下列程式碼片段的 hello。</span><span class="sxs-lookup"><span data-stu-id="e1878-146">Run hello following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="e1878-147">`iislogparser`提供函式`parse_log_line`傳回`None`記錄列標頭資料列，並且傳回 hello 的執行個體如果`LogLine`遇到記錄列類別。</span><span class="sxs-lookup"><span data-stu-id="e1878-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of hello `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="e1878-148">使用 hello`LogLine`類別 tooextract 只 hello hello RDD 中的記錄程式行：</span><span class="sxs-lookup"><span data-stu-id="e1878-148">Use hello `LogLine` class tooextract only hello log lines from hello RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="e1878-149">擷取 hello 步驟已順利完成的擷取的記錄行 tooverify 數。</span><span class="sxs-lookup"><span data-stu-id="e1878-149">Retrieve a couple of extracted log lines tooverify that hello step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="e1878-150">hello 輸出應類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="e1878-150">hello output should be similar toohello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="e1878-151">hello`LogLine`類別，又具有一些有用的方法，例如`is_error()`，它會傳回記錄項目是否有錯誤程式碼。</span><span class="sxs-lookup"><span data-stu-id="e1878-151">hello `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="e1878-152">使用錯誤此 toocompute hello 數目 hello 擷取記錄行，並再記錄所有 hello 錯誤 tooa 不同的檔案。</span><span class="sxs-lookup"><span data-stu-id="e1878-152">Use this toocompute hello number of errors in hello extracted log lines, and then log all hello errors tooa different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="e1878-153">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="e1878-153">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="e1878-154">您也可以使用**Matplotlib** tooconstruct 的 hello 資料視覺效果。</span><span class="sxs-lookup"><span data-stu-id="e1878-154">You can also use **Matplotlib** tooconstruct a visualization of hello data.</span></span> <span data-ttu-id="e1878-155">例如，如果您想 tooisolate hello 造成長時間執行的要求，您可以採取 hello 大部分時間 tooserve 平均 toofind hello 檔案。</span><span class="sxs-lookup"><span data-stu-id="e1878-155">For example, if you want tooisolate hello cause of requests that run for a long time, you might want toofind hello files that take hello most time tooserve on average.</span></span>
   <span data-ttu-id="e1878-156">hello 以下程式碼片段會擷取 hello 前 25 資源所花費大部分時間 tooserve 要求。</span><span class="sxs-lookup"><span data-stu-id="e1878-156">hello snippet below retrieves hello top 25 resources that took most time tooserve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="e1878-157">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="e1878-157">You should see an output like hello following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [(u'/blogposts/mvc4/step13.png', 197.5),
        (u'/blogposts/mvc2/step10.jpg', 179.5),
        (u'/blogposts/extractusercontrol/step5.png', 170.0),
        (u'/blogposts/mvc4/step8.png', 159.0),
        (u'/blogposts/mvcrouting/step22.jpg', 155.0),
        (u'/blogposts/mvcrouting/step3.jpg', 152.0),
        (u'/blogposts/linqsproc1/step16.jpg', 138.75),
        (u'/blogposts/linqsproc1/step26.jpg', 137.33333333333334),
        (u'/blogposts/vs2008javascript/step10.jpg', 127.0),
        (u'/blogposts/nested/step2.jpg', 126.0),
        (u'/blogposts/adminpack/step1.png', 124.0),
        (u'/BlogPosts/datalistpaging/step2.png', 118.0),
        (u'/blogposts/mvc4/step35.png', 117.0),
        (u'/blogposts/mvcrouting/step2.jpg', 116.5),
        (u'/blogposts/aboutme/basketball.jpg', 109.0),
        (u'/blogposts/anonymoustypes/step11.jpg', 109.0),
        (u'/blogposts/mvc4/step12.png', 106.0),
        (u'/blogposts/linq8/step0.jpg', 105.5),
        (u'/blogposts/mvc2/step18.jpg', 104.0),
        (u'/blogposts/mvc2/step11.jpg', 104.0),
        (u'/blogposts/mvcrouting/step1.jpg', 104.0),
        (u'/blogposts/extractusercontrol/step1.png', 103.0),
        (u'/blogposts/sqlvideos/sqlvideos.jpg', 102.0),
        (u'/blogposts/mvcrouting/step21.jpg', 101.0),
        (u'/blogposts/mvc4/step1.png', 98.0)]
5. <span data-ttu-id="e1878-158">您也可以呈現 hello 表單區域的這項資訊。</span><span class="sxs-lookup"><span data-stu-id="e1878-158">You can also present this information in hello form of plot.</span></span> <span data-ttu-id="e1878-159">第一個步驟 toocreate 繪圖，讓我們先建立暫存資料表**AverageTime**。</span><span class="sxs-lookup"><span data-stu-id="e1878-159">As a first step toocreate a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="e1878-160">如果在任何特定時間沒有任何不尋常的延遲尖峰時間 toosee 記錄 hello 資料表群組 hello。</span><span class="sxs-lookup"><span data-stu-id="e1878-160">hello table groups hello logs by time toosee if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="e1878-161">然後，您可以執行下列 SQL 查詢 tooget hello hello 的所有記錄中 hello **AverageTime**資料表。</span><span class="sxs-lookup"><span data-stu-id="e1878-161">You can then run hello following SQL query tooget all hello records in hello **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="e1878-162">hello `%%sql` magic 後面`-o averagetime`可確保 hello 查詢的 hello 輸出保存在本機上 hello Jupyter 伺服器 （通常 hello 叢集的前端節點 hello 叢集）。</span><span class="sxs-lookup"><span data-stu-id="e1878-162">hello `%%sql` magic followed by `-o averagetime` ensures that hello output of hello query is persisted locally on hello Jupyter server (typically hello headnode of hello cluster).</span></span> <span data-ttu-id="e1878-163">hello 輸出會保存為[熊](http://pandas.pydata.org/)資料框架 hello 與指定名稱**averagetime**。</span><span class="sxs-lookup"><span data-stu-id="e1878-163">hello output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with hello specified name **averagetime**.</span></span>

   <span data-ttu-id="e1878-164">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="e1878-164">You should see an output like hello following:</span></span>

   <span data-ttu-id="e1878-165">![SQL 查詢輸出](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL 查詢輸出")</span><span class="sxs-lookup"><span data-stu-id="e1878-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="e1878-166">如需有關 hello `%%sql` magic，請參閱[hello 的支援參數 %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。</span><span class="sxs-lookup"><span data-stu-id="e1878-166">For more information about hello `%%sql` magic, see [Parameters supported with hello %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="e1878-167">您現在可以使用 Matplotlib、 文件庫使用的資料，toocreate 繪圖 tooconstruct 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="e1878-167">You can now use Matplotlib, a library used tooconstruct visualization of data, toocreate a plot.</span></span> <span data-ttu-id="e1878-168">因為必須從本機 hello 建立 hello 圖保存**averagetime**資料框架，hello 程式碼片段必須以 hello 開頭`%%local`識別常數。</span><span class="sxs-lookup"><span data-stu-id="e1878-168">Because hello plot must be created from hello locally persisted **averagetime** dataframe, hello code snippet must begin with hello `%%local` magic.</span></span> <span data-ttu-id="e1878-169">這可確保 hello 程式碼在本機執行 hello Jupyter 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="e1878-169">This ensures that hello code is run locally on hello Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="e1878-170">您應該會看到類似 hello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="e1878-170">You should see an output like hello following:</span></span>

   <span data-ttu-id="e1878-171">![Matplotlib 輸出](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib 輸出")</span><span class="sxs-lookup"><span data-stu-id="e1878-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="e1878-172">當您完成執行 hello 應用程式之後，您應該關閉 hello 筆記本 toorelease hello 資源。</span><span class="sxs-lookup"><span data-stu-id="e1878-172">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="e1878-173">toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。</span><span class="sxs-lookup"><span data-stu-id="e1878-173">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="e1878-174">這將會關機並關閉 hello 筆記本。</span><span class="sxs-lookup"><span data-stu-id="e1878-174">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="e1878-175"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="e1878-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="e1878-176">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="e1878-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="e1878-177">案例</span><span class="sxs-lookup"><span data-stu-id="e1878-177">Scenarios</span></span>
* [<span data-ttu-id="e1878-178">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="e1878-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="e1878-179">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="e1878-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="e1878-180">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="e1878-180">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="e1878-181">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="e1878-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="e1878-182">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="e1878-182">Create and run applications</span></span>
* [<span data-ttu-id="e1878-183">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="e1878-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="e1878-184">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="e1878-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="e1878-185">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="e1878-185">Tools and extensions</span></span>
* [<span data-ttu-id="e1878-186">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1878-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="e1878-187">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="e1878-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="e1878-188">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="e1878-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="e1878-189">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="e1878-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="e1878-190">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="e1878-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="e1878-191">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="e1878-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="e1878-192">管理資源</span><span class="sxs-lookup"><span data-stu-id="e1878-192">Manage resources</span></span>
* [<span data-ttu-id="e1878-193">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="e1878-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="e1878-194">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="e1878-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
