---
title: "在 Spark 中搭配 Python 程式庫分析網站記錄 - Azure | Microsoft Docs"
description: "此 Notebook 示範如何使用自訂程式庫搭配 Azure HDInsight 上的 Spark 來分析記錄資料。"
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
ms.openlocfilehash: 2a028beb1e9eae89d32238e61b6f67c4c059a94a
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="analyze-website-logs-using-a-custom-python-library-with-spark-cluster-on-hdinsight"></a><span data-ttu-id="a9699-103">使用自訂 Python 程式庫搭配 HDInsight 上的 Spark 叢集來分析網站記錄</span><span class="sxs-lookup"><span data-stu-id="a9699-103">Analyze website logs using a custom Python library with Spark cluster on HDInsight</span></span>

<span data-ttu-id="a9699-104">此 Notebook 示範如何使用自訂程式庫搭配 HDInsight 上的 Spark 來分析記錄資料。</span><span class="sxs-lookup"><span data-stu-id="a9699-104">This notebook demonstrates how to analyze log data using a custom library with Spark on HDInsight.</span></span> <span data-ttu-id="a9699-105">我們使用的自訂程式庫是名為 **iislogparser.py**的 Python 程式庫。</span><span class="sxs-lookup"><span data-stu-id="a9699-105">The custom library we use is a Python library called **iislogparser.py**.</span></span>

> [!TIP]
> <span data-ttu-id="a9699-106">本教學課程也適用於您在 HDInsight 中所建立 Spark (Linux) 叢集上的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="a9699-106">This tutorial is also available as a Jupyter notebook on a Spark (Linux) cluster that you create in HDInsight.</span></span> <span data-ttu-id="a9699-107">Notebook 的體驗能讓您從 Notebook 本身執行 Python 程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="a9699-107">The notebook experience lets you run the Python snippets from the notebook itself.</span></span> <span data-ttu-id="a9699-108">如果要從 Notebook 中執行本教學課程，請建立 Spark 叢集、啟動 Jupyter Notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`)，然後執行 **PySpark** 資料夾下的 Notebook **使用自訂 library.ipynb 透過 Spark 分析記錄**。</span><span class="sxs-lookup"><span data-stu-id="a9699-108">To perform the tutorial from within a notebook, create a Spark cluster, launch a Jupyter notebook (`https://CLUSTERNAME.azurehdinsight.net/jupyter`), and then run the notebook **Analyze logs with Spark using a custom library.ipynb** under the **PySpark** folder.</span></span>
>
>

<span data-ttu-id="a9699-109">**必要條件：**</span><span class="sxs-lookup"><span data-stu-id="a9699-109">**Prerequisites:**</span></span>

<span data-ttu-id="a9699-110">您必須滿足以下條件：</span><span class="sxs-lookup"><span data-stu-id="a9699-110">You must have the following:</span></span>

* <span data-ttu-id="a9699-111">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a9699-111">An Azure subscription.</span></span> <span data-ttu-id="a9699-112">請參閱 [取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="a9699-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="a9699-113">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="a9699-113">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="a9699-114">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="a9699-114">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span>

## <a name="save-raw-data-as-an-rdd"></a><span data-ttu-id="a9699-115">將原始資料儲存為 RDD</span><span class="sxs-lookup"><span data-stu-id="a9699-115">Save raw data as an RDD</span></span>
<span data-ttu-id="a9699-116">在本節中，我們會使用與 HDInsight 中的 Apache Spark 叢集相關聯的 [Jupyter](https://jupyter.org) Notebook，來執行會處理原始範例資料，並將這些資料儲存成 Hive 資料表的作業。</span><span class="sxs-lookup"><span data-stu-id="a9699-116">In this section, we use the [Jupyter](https://jupyter.org) notebook associated with an Apache Spark cluster in HDInsight to run jobs that process your raw sample data and save it as a Hive table.</span></span> <span data-ttu-id="a9699-117">範例資料是所有叢集在預設情況下均有的 .csv 檔案 (hvac.csv)。</span><span class="sxs-lookup"><span data-stu-id="a9699-117">The sample data is a .csv file (hvac.csv) available on all clusters by default.</span></span>

<span data-ttu-id="a9699-118">一旦將資料儲存成 Hive 資料表之後，下一節我們將使用 Power BI 和 Tableau 等 BI 工具連接 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="a9699-118">Once your data is saved as a Hive table, in the next section we will connect to the Hive table using BI tools such as Power BI and Tableau.</span></span>

1. <span data-ttu-id="a9699-119">在 [Azure 入口網站](https://portal.azure.com/)的開始面板中，按一下您的 Spark 叢集格圖格 (如果您已將其釘選到開始面板)。</span><span class="sxs-lookup"><span data-stu-id="a9699-119">From the [Azure portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="a9699-120">您也可以按一下 [瀏覽全部] > [HDInsight 叢集] 來瀏覽至您的叢集。</span><span class="sxs-lookup"><span data-stu-id="a9699-120">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="a9699-121">從 Spark 叢集刀鋒視窗按一下 [叢集儀表板]，然後按一下 [Jupyter Notebook]。</span><span class="sxs-lookup"><span data-stu-id="a9699-121">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="a9699-122">出現提示時，輸入叢集的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="a9699-122">If prompted, enter the admin credentials for the cluster.</span></span>

   > [!NOTE]
   > <span data-ttu-id="a9699-123">您也可以在瀏覽器中開啟下列 URL，來連接到您的叢集的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="a9699-123">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="a9699-124">使用您叢集的名稱取代 **CLUSTERNAME** ：</span><span class="sxs-lookup"><span data-stu-id="a9699-124">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   >
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   >
   >
3. <span data-ttu-id="a9699-125">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="a9699-125">Create a new notebook.</span></span> <span data-ttu-id="a9699-126">按一下 [新增]，然後按一下 [PySpark]。</span><span class="sxs-lookup"><span data-stu-id="a9699-126">Click **New**, and then click **PySpark**.</span></span>

    <span data-ttu-id="a9699-127">![建立新的 Jupyter Notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "建立新的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="a9699-127">![Create a new Jupyter notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-create-jupyter-notebook.png "Create a new Jupyter notebook")</span></span>
4. <span data-ttu-id="a9699-128">系統隨即會建立新 Notebook，並以 Untitled.pynb 的名稱開啟。</span><span class="sxs-lookup"><span data-stu-id="a9699-128">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="a9699-129">在頂端按一下 Notebook 名稱，然後輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="a9699-129">Click the notebook name at the top, and enter a friendly name.</span></span>

    <span data-ttu-id="a9699-130">![提供 Notebook 的名稱](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "提供 Notebook 的名稱")</span><span class="sxs-lookup"><span data-stu-id="a9699-130">![Provide a name for the notebook](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-name-jupyter-notebook.png "Provide a name for the notebook")</span></span>
5. <span data-ttu-id="a9699-131">您使用 PySpark 核心建立 Notebook，因此不需要明確建立任何內容。</span><span class="sxs-lookup"><span data-stu-id="a9699-131">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="a9699-132">當您執行第一個程式碼儲存格時，系統會自動為您建立 Spark 和 Hive 內容。</span><span class="sxs-lookup"><span data-stu-id="a9699-132">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="a9699-133">首先，您可以匯入此案例需要的類型。</span><span class="sxs-lookup"><span data-stu-id="a9699-133">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="a9699-134">將下列程式碼片段貼到空白儲存格中，然後按 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="a9699-134">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span>

        from pyspark.sql import Row
        from pyspark.sql.types import *


1. <span data-ttu-id="a9699-135">使用叢集上已有的範例記錄資料來建立 RDD。</span><span class="sxs-lookup"><span data-stu-id="a9699-135">Create an RDD using the sample log data already available on the cluster.</span></span> <span data-ttu-id="a9699-136">您可以在 **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log** 上存取與叢集相關聯之預設儲存體帳戶中的資料。</span><span class="sxs-lookup"><span data-stu-id="a9699-136">You can access the data in the default storage account associated with the cluster at **\HdiSamples\HdiSamples\WebsiteLogSampleData\SampleLog\909f2b.log**.</span></span>

        logs = sc.textFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b.log')


1. <span data-ttu-id="a9699-137">擷取範例記錄組，以確認先前的步驟已順利完成。</span><span class="sxs-lookup"><span data-stu-id="a9699-137">Retrieve a sample log set to verify that the previous step completed successfully.</span></span>

        logs.take(5)

    <span data-ttu-id="a9699-138">您應該會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="a9699-138">You should see an output similar to the following:</span></span>

        # -----------------
        # THIS IS AN OUTPUT
        # -----------------

        [u'#Software: Microsoft Internet Information Services 8.0',
         u'#Fields: date time s-sitename cs-method cs-uri-stem cs-uri-query s-port cs-username c-ip cs(User-Agent) cs(Cookie) cs(Referer) cs-host sc-status sc-substatus sc-win32-status sc-bytes cs-bytes time-taken',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32',
         u'2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step4.png X-ARR-LOG-ID=4bea5b3d-8ac9-46c9-9b8c-ec3e9500cbea 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 72177 871 47']

## <a name="analyze-log-data-using-a-custom-python-library"></a><span data-ttu-id="a9699-139">使用自訂 Python 程式庫來分析記錄資料</span><span class="sxs-lookup"><span data-stu-id="a9699-139">Analyze log data using a custom Python library</span></span>
1. <span data-ttu-id="a9699-140">在上述輸出中，前幾行包含標頭資訊，其餘各行則符合該標頭中所說明的結構描述。</span><span class="sxs-lookup"><span data-stu-id="a9699-140">In the output above, the first couple lines include the header information and each remaining line matches the schema described in that header.</span></span> <span data-ttu-id="a9699-141">剖析這類記錄檔可能是複雜的作業。</span><span class="sxs-lookup"><span data-stu-id="a9699-141">Parsing such logs could be complicated.</span></span> <span data-ttu-id="a9699-142">因此，我們使用自訂 Python 程式庫 (**iislogparser.py**)，它可大幅簡化這類記錄檔的剖析。</span><span class="sxs-lookup"><span data-stu-id="a9699-142">So, we use a custom Python library (**iislogparser.py**) that makes parsing such logs much easier.</span></span> <span data-ttu-id="a9699-143">依預設，此程式庫會包含在位於以下位置的 HDInsight 上的 Spark 叢集中： **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**。</span><span class="sxs-lookup"><span data-stu-id="a9699-143">By default, this library is included with your Spark cluster on HDInsight at **/HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py**.</span></span>

    <span data-ttu-id="a9699-144">不過，此程式庫不在 `PYTHONPATH` 中，因此無法藉由 `import iislogparser` 之類的匯入陳述式來使用它。</span><span class="sxs-lookup"><span data-stu-id="a9699-144">However, this library is not in the `PYTHONPATH` so we cannot use it by using an import statement like `import iislogparser`.</span></span> <span data-ttu-id="a9699-145">若要使用此程式庫，我們必須將它散發到所有的背景工作角色節點。</span><span class="sxs-lookup"><span data-stu-id="a9699-145">To use this library, we must distribute it to all the worker nodes.</span></span> <span data-ttu-id="a9699-146">執行下列程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="a9699-146">Run the following snippet.</span></span>

        sc.addPyFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/iislogparser.py')


1. <span data-ttu-id="a9699-147">`iislogparser` 提供一個函數 `parse_log_line`，在記錄行為標頭資料列時會傳回 `None`，在發現記錄行時則傳回 `LogLine` 類別的執行個體。</span><span class="sxs-lookup"><span data-stu-id="a9699-147">`iislogparser` provides a function `parse_log_line` that returns `None` if a log line is a header row, and returns an instance of the `LogLine` class if it encounters a log line.</span></span> <span data-ttu-id="a9699-148">使用 `LogLine` 類別，僅從 RDD 擷取記錄行：</span><span class="sxs-lookup"><span data-stu-id="a9699-148">Use the `LogLine` class to extract only the log lines from the RDD:</span></span>

        def parse_line(l):
            import iislogparser
            return iislogparser.parse_log_line(l)
        logLines = logs.map(parse_line).filter(lambda p: p is not None).cache()
2. <span data-ttu-id="a9699-149">擷取幾個記錄行，以確認步驟已順利完成。</span><span class="sxs-lookup"><span data-stu-id="a9699-149">Retrieve a couple of extracted log lines to verify that the step completed successfully.</span></span>

       logLines.take(2)

   <span data-ttu-id="a9699-150">輸出應該類似如下範例：</span><span class="sxs-lookup"><span data-stu-id="a9699-150">The output should be similar to the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       [2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step2.png X-ARR-LOG-ID=2ec4b8ad-3cf0-4442-93ab-837317ece6a1 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 53175 871 46,
        2014-01-01 02:01:09 SAMPLEWEBSITE GET /blogposts/mvc4/step3.png X-ARR-LOG-ID=9eace870-2f49-4efd-b204-0d170da46b4a 80 - 1.54.23.196 Mozilla/5.0+(Windows+NT+6.3;+WOW64)+AppleWebKit/537.36+(KHTML,+like+Gecko)+Chrome/31.0.1650.63+Safari/537.36 - http://weblogs.asp.net/sample/archive/2007/12/09/asp-net-mvc-framework-part-4-handling-form-edit-and-post-scenarios.aspx www.sample.com 200 0 0 51237 871 32]
3. <span data-ttu-id="a9699-151">`LogLine` 類別也有一些有用的方法，像是 `is_error()`，它會傳回記錄項目是否有錯誤碼。</span><span class="sxs-lookup"><span data-stu-id="a9699-151">The `LogLine` class, in turn, has some useful methods, like `is_error()`, which returns whether a log entry has an error code.</span></span> <span data-ttu-id="a9699-152">它可用來計算已擷取的記錄行中有多少錯誤，然後將所有錯誤記錄到另一個檔案。</span><span class="sxs-lookup"><span data-stu-id="a9699-152">Use this to compute the number of errors in the extracted log lines, and then log all the errors to a different file.</span></span>

       errors = logLines.filter(lambda p: p.is_error())
       numLines = logLines.count()
       numErrors = errors.count()
       print 'There are', numErrors, 'errors and', numLines, 'log entries'
       errors.map(lambda p: str(p)).saveAsTextFile('wasb:///HdiSamples/HdiSamples/WebsiteLogSampleData/SampleLog/909f2b-2.log')

   <span data-ttu-id="a9699-153">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="a9699-153">You should see an output like the following:</span></span>

       # -----------------
       # THIS IS AN OUTPUT
       # -----------------

       There are 30 errors and 646 log entries
4. <span data-ttu-id="a9699-154">您也可以使用 **Matplotlib** 來建構資料的視覺效果。</span><span class="sxs-lookup"><span data-stu-id="a9699-154">You can also use **Matplotlib** to construct a visualization of the data.</span></span> <span data-ttu-id="a9699-155">例如，如果您想要找出要求長時間執行的原因，您可以尋找平均佔用最多服務資源的檔案。</span><span class="sxs-lookup"><span data-stu-id="a9699-155">For example, if you want to isolate the cause of requests that run for a long time, you might want to find the files that take the most time to serve on average.</span></span>
   <span data-ttu-id="a9699-156">下列程式碼片段會擷取耗費最多時間為要求提供服務的前 25 個資源。</span><span class="sxs-lookup"><span data-stu-id="a9699-156">The snippet below retrieves the top 25 resources that took most time to serve a request.</span></span>

       def avgTimeTakenByKey(rdd):
           return rdd.combineByKey(lambda line: (line.time_taken, 1),
                                   lambda x, line: (x[0] + line.time_taken, x[1] + 1),
                                   lambda x, y: (x[0] + y[0], x[1] + y[1]))\
                     .map(lambda x: (x[0], float(x[1][0]) / float(x[1][1])))

       avgTimeTakenByKey(logLines.map(lambda p: (p.cs_uri_stem, p))).top(25, lambda x: x[1])

   <span data-ttu-id="a9699-157">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="a9699-157">You should see an output like the following:</span></span>

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
5. <span data-ttu-id="a9699-158">您也可以用繪圖的形式呈現這項資訊。</span><span class="sxs-lookup"><span data-stu-id="a9699-158">You can also present this information in the form of plot.</span></span> <span data-ttu-id="a9699-159">建立繪圖的第一個步驟是建立暫存資料表 **AverageTime**。</span><span class="sxs-lookup"><span data-stu-id="a9699-159">As a first step to create a plot, let us first create a temporary table **AverageTime**.</span></span> <span data-ttu-id="a9699-160">此資料表會依時間將記錄分組，以查看在任何特定時間中是否出現異常的延遲尖峰。</span><span class="sxs-lookup"><span data-stu-id="a9699-160">The table groups the logs by time to see if there were any unusual latency spikes at any particular time.</span></span>

       avgTimeTakenByMinute = avgTimeTakenByKey(logLines.map(lambda p: (p.datetime.minute, p))).sortByKey()
       schema = StructType([StructField('Minutes', IntegerType(), True),
                            StructField('Time', FloatType(), True)])

       avgTimeTakenByMinuteDF = sqlContext.createDataFrame(avgTimeTakenByMinute, schema)
       avgTimeTakenByMinuteDF.registerTempTable('AverageTime')
6. <span data-ttu-id="a9699-161">接著，您可以執行下列 SQL 查詢取得 **AverageTime** 資料表中的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="a9699-161">You can then run the following SQL query to get all the records in the **AverageTime** table.</span></span>

       %%sql -o averagetime
       SELECT * FROM AverageTime

   <span data-ttu-id="a9699-162">`%%sql` magic 後面緊接著 `-o averagetime` 可確保查詢的輸出會保存在 Jupyter 伺服器的本機上 (通常是叢集的前端節點)。</span><span class="sxs-lookup"><span data-stu-id="a9699-162">The `%%sql` magic followed by `-o averagetime` ensures that the output of the query is persisted locally on the Jupyter server (typically the headnode of the cluster).</span></span> <span data-ttu-id="a9699-163">輸出內容會以具有指定名稱 [averagetime](http://pandas.pydata.org/) 的 **Pandas**資料框架保存。</span><span class="sxs-lookup"><span data-stu-id="a9699-163">The output is persisted as a [Pandas](http://pandas.pydata.org/) dataframe with the specified name **averagetime**.</span></span>

   <span data-ttu-id="a9699-164">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="a9699-164">You should see an output like the following:</span></span>

   <span data-ttu-id="a9699-165">![SQL 查詢輸出](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL 查詢輸出")</span><span class="sxs-lookup"><span data-stu-id="a9699-165">![SQL query output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-jupyter-sql-qyery-output.png "SQL query output")</span></span>

   <span data-ttu-id="a9699-166">如需 `%%sql` magic 的詳細資訊，請參閱 [%%sql magic 支援的參數](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic)。</span><span class="sxs-lookup"><span data-stu-id="a9699-166">For more information about the `%%sql` magic, see [Parameters supported with the %%sql magic](hdinsight-apache-spark-jupyter-notebook-kernels.md#parameters-supported-with-the-sql-magic).</span></span>
7. <span data-ttu-id="a9699-167">現在您可以使用 Matplotlib (用於建構資料視覺效果的程式庫) 建立繪圖。</span><span class="sxs-lookup"><span data-stu-id="a9699-167">You can now use Matplotlib, a library used to construct visualization of data, to create a plot.</span></span> <span data-ttu-id="a9699-168">因為必須從保存在本機上的 **averagetime** 資料框架建立繪圖，所以程式碼片段的開頭必須為 `%%local` magic。</span><span class="sxs-lookup"><span data-stu-id="a9699-168">Because the plot must be created from the locally persisted **averagetime** dataframe, the code snippet must begin with the `%%local` magic.</span></span> <span data-ttu-id="a9699-169">這可確保程式碼是在 Jupyter 伺服器的本機上執行。</span><span class="sxs-lookup"><span data-stu-id="a9699-169">This ensures that the code is run locally on the Jupyter server.</span></span>

       %%local
       %matplotlib inline
       import matplotlib.pyplot as plt

       plt.plot(averagetime['Minutes'], averagetime['Time'], marker='o', linestyle='--')
       plt.xlabel('Time (min)')
       plt.ylabel('Average time taken for request (ms)')

   <span data-ttu-id="a9699-170">您應該會看到如下的輸出：</span><span class="sxs-lookup"><span data-stu-id="a9699-170">You should see an output like the following:</span></span>

   <span data-ttu-id="a9699-171">![Matplotlib 輸出](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib 輸出")</span><span class="sxs-lookup"><span data-stu-id="a9699-171">![Matplotlib output](./media/hdinsight-apache-spark-custom-library-website-log-analysis/hdinsight-apache-spark-web-log-analysis-plot.png "Matplotlib output")</span></span>
8. <span data-ttu-id="a9699-172">應用程式執行完畢之後，您應該要關閉 Notebook 來釋放資源。</span><span class="sxs-lookup"><span data-stu-id="a9699-172">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="a9699-173">若要這樣做，請從 Notebook 的 [檔案] 功能表中，按一下 [關閉並停止]。</span><span class="sxs-lookup"><span data-stu-id="a9699-173">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="a9699-174">這樣就能夠結束並關閉 Notebook。</span><span class="sxs-lookup"><span data-stu-id="a9699-174">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="a9699-175"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="a9699-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="a9699-176">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="a9699-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="a9699-177">案例</span><span class="sxs-lookup"><span data-stu-id="a9699-177">Scenarios</span></span>
* [<span data-ttu-id="a9699-178">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="a9699-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="a9699-179">Spark 和機器學習服務：使用 HDInsight 中的 Spark，利用 HVAC 資料來分析建築物溫度</span><span class="sxs-lookup"><span data-stu-id="a9699-179">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="a9699-180">Spark 和機器學習服務：使用 HDInsight 中的 Spark 來預測食品檢查結果</span><span class="sxs-lookup"><span data-stu-id="a9699-180">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="a9699-181">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="a9699-181">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="a9699-182">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="a9699-182">Create and run applications</span></span>
* [<span data-ttu-id="a9699-183">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="a9699-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="a9699-184">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="a9699-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="a9699-185">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="a9699-185">Tools and extensions</span></span>
* [<span data-ttu-id="a9699-186">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式</span><span class="sxs-lookup"><span data-stu-id="a9699-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applications</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="a9699-187">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="a9699-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="a9699-188">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="a9699-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="a9699-189">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="a9699-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="a9699-190">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="a9699-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="a9699-191">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="a9699-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="a9699-192">管理資源</span><span class="sxs-lookup"><span data-stu-id="a9699-192">Manage resources</span></span>
* [<span data-ttu-id="a9699-193">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="a9699-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="a9699-194">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="a9699-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)
