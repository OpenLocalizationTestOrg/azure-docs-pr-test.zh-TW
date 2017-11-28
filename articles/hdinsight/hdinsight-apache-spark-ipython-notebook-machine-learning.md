---
title: "aaaBuild Apache Spark 機器學習 Azure HDInsight 上的應用程式 |Microsoft 文件"
description: "Toobuild Apache Spark 機器學習服務應用程式上 HDInsight Spark 叢集使用 Jupyter 筆記本的逐步指示"
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: f584ca5e-abee-4b7c-ae58-2e45dfc56bf4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: nitinme
ms.openlocfilehash: 332bd89876f7ebf178f7573d6018d064edfe9a8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="9ccb0-103">在 Azure HDInsight 上建置 Apache Spark 機器學習服務應用程式</span><span class="sxs-lookup"><span data-stu-id="9ccb0-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="9ccb0-104">了解如何 toobuild Apache Spark 機器學習應用程式使用的 Spark 叢集 HDInsight 上。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-104">Learn how toobuild an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="9ccb0-105">本文將說明如何 toouse hello Jupyter 筆記本隨附 hello 叢集 toobuild 及測試這個應用程式。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-105">This article shows how toouse hello Jupyter notebook available with hello cluster toobuild and test this application.</span></span> <span data-ttu-id="9ccb0-106">hello 應用程式會使用 hello 範例 HVAC.csv 資料可在預設情況下的所有叢集上。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-106">hello application uses hello sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="9ccb0-107">**先決條件：**</span><span class="sxs-lookup"><span data-stu-id="9ccb0-107">**Prerequisites:**</span></span>

<span data-ttu-id="9ccb0-108">您必須擁有 hello 下列：</span><span class="sxs-lookup"><span data-stu-id="9ccb0-108">You must have hello following:</span></span>

* <span data-ttu-id="9ccb0-109">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="9ccb0-110">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="9ccb0-111"><a name="data"></a>了解 hello 資料集</span><span class="sxs-lookup"><span data-stu-id="9ccb0-111"><a name="data"></a>Understand hello data set</span></span>
<span data-ttu-id="9ccb0-112">開始建置 hello 應用程式之前，讓我們了解 hello hello 資料，我們 hello 應用程式在建置和 hello 種類，我們會執行的分析的 hello 資料結構。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-112">Before we start building hello application, let us understand hello structure of hello data for which we build hello application and hello kind of analysis we will do on hello data.</span></span> 

<span data-ttu-id="9ccb0-113">在本文中，我們會使用 hello 範例**HVAC.csv** hello 與 hello HDInsight 叢集相關聯的 Azure 儲存體帳戶中可用的資料檔案。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-113">In this article, we use hello sample **HVAC.csv** data file that is available in hello Azure Storage account that you associated with hello HDInsight cluster.</span></span> <span data-ttu-id="9ccb0-114">Hello 的儲存體帳戶內 hello 檔案位於**\HdiSamples\HdiSamples\SensorSampleData\hvac**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-114">Within hello storage account, hello file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="9ccb0-115">下載並開啟 hello CSV 檔案 tooget hello 資料快照集。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-115">Download and open hello CSV file tooget a snapshot of hello data.</span></span>  

<span data-ttu-id="9ccb0-116">![用於 Spark 機器學習服務範例的資料快照集](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "用於 Spark 機器學習服務範例的資料快照集")</span><span class="sxs-lookup"><span data-stu-id="9ccb0-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="9ccb0-117">hello 資料會顯示 hello 目標溫度和 hello 實際溫度的已安裝的 HVAC 系統建置。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-117">hello data shows hello target temperature and hello actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="9ccb0-118">讓我們假設 hello**系統**資料行代表 hello 系統識別碼和 hello **SystemAge**資料行代表 hello hello HVAC 系統已經在 hello 建置中的年數。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-118">Let's assume hello **System** column represents hello system ID and hello **SystemAge** column represents hello number of years hello HVAC system has been in place at hello building.</span></span>

<span data-ttu-id="9ccb0-119">我們會使用此資料 toopredict 是否建置將會更高或 colder hello 目標溫度，根據給定的系統識別碼和系統存留期。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-119">We use this data toopredict whether a building will be hotter or colder based on hello target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="9ccb0-120"><a name="app"></a>使用 Spark MLlib 撰寫 Spark 機器學習服務應用程式</span><span class="sxs-lookup"><span data-stu-id="9ccb0-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="9ccb0-121">在此應用程式中，我們使用 Spark ML 管線 tooperform 文件分類。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-121">In this application we use a Spark ML pipeline tooperform a document classification.</span></span> <span data-ttu-id="9ccb0-122">在 hello 管線中，我們將 hello 文件分割成單字、 hello 字轉換成數值特徵向量，和最後建立預測模型使用 hello 特徵向量和標籤。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-122">In hello pipeline, we split hello document into words, convert hello words into a numerical feature vector, and finally build a prediction model using hello feature vectors and labels.</span></span> <span data-ttu-id="9ccb0-123">執行下列步驟 toocreate hello 應用程式的 hello。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-123">Perform hello following steps toocreate hello application.</span></span>

1. <span data-ttu-id="9ccb0-124">從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-124">From hello [Azure Portal](https://portal.azure.com/), from hello startboard, click hello tile for your Spark cluster (if you pinned it toohello startboard).</span></span> <span data-ttu-id="9ccb0-125">您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-125">You can also navigate tooyour cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="9ccb0-126">從 hello Spark 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **Jupyter 筆記本**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-126">From hello Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="9ccb0-127">如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-127">If prompted, enter hello admin credentials for hello cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="9ccb0-128">您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-128">You may also reach hello Jupyter Notebook for your cluster by opening hello following URL in your browser.</span></span> <span data-ttu-id="9ccb0-129">取代**CLUSTERNAME** hello 名稱，為您的叢集：</span><span class="sxs-lookup"><span data-stu-id="9ccb0-129">Replace **CLUSTERNAME** with hello name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="9ccb0-130">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-130">Create a new notebook.</span></span> <span data-ttu-id="9ccb0-131">按一下 新增，然後按一下PySpark。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="9ccb0-132">![建立 Spark 機器學習服務範例的 Jupyter Notebook](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "建立 Spark 機器學習服務範例的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="9ccb0-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="9ccb0-133">建立新的記事本，並開啟 hello 名稱 Untitled.pynb。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-133">A new notebook is created and opened with hello name Untitled.pynb.</span></span> <span data-ttu-id="9ccb0-134">按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-134">Click hello notebook name at hello top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="9ccb0-135">![提供 Spark 機器學習服務範例的 Notebook 名稱](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "提供 Spark 機器學習服務範例的 Notebook 名稱")</span><span class="sxs-lookup"><span data-stu-id="9ccb0-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="9ccb0-136">因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-136">Because you created a notebook using hello PySpark kernel, you do not need toocreate any contexts explicitly.</span></span> <span data-ttu-id="9ccb0-137">hello Spark 和 Hive 內容將會自動為您建立執行 hello 第一個程式碼儲存格時。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-137">hello Spark and Hive contexts will be automatically created for you when you run hello first code cell.</span></span> <span data-ttu-id="9ccb0-138">您可以啟動匯入此案例所需的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-138">You can start by importing hello types that are required for this scenario.</span></span> <span data-ttu-id="9ccb0-139">貼上下列程式碼片段中的空白儲存格，hello，然後按下**SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-139">Paste hello following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
        from pyspark.ml import Pipeline
        from pyspark.ml.classification import LogisticRegression
        from pyspark.ml.feature import HashingTF, Tokenizer
        from pyspark.sql import Row
   
        import os
        import sys
        from pyspark.sql.types import *
   
        from pyspark.mllib.classification import LogisticRegressionWithSGD
        from pyspark.mllib.regression import LabeledPoint
        from numpy import array
6. <span data-ttu-id="9ccb0-140">您必須立即載入 hello 資料 (hvac.csv)、 剖析，並使用它 tootrain hello 模型。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-140">You must now load hello data (hvac.csv), parse it, and use it tootrain hello model.</span></span> <span data-ttu-id="9ccb0-141">這麼做，您可以定義的函式，會檢查 hello 的 hello 建置實際的溫度是否大於 hello 目標溫度。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-141">For this, you define a function that checks whether hello actual temperature of hello building is greater than hello target temperature.</span></span> <span data-ttu-id="9ccb0-142">如果 hello 實際溫度較大，hello 大樓是熱，hello 值所表示**1.0**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-142">If hello actual temperature is greater, hello building is hot, denoted by hello value **1.0**.</span></span> <span data-ttu-id="9ccb0-143">如果較小者 hello 實際溫度，hello 大樓是冷，hello 值所表示**0.0**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-143">If hello actual temperature is lesser, hello building is cold, denoted by hello value **0.0**.</span></span> 
   
    <span data-ttu-id="9ccb0-144">貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-144">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List hello structure of data for better understanding. Because hello data will be
        # loaded as an array, this structure makes it easy toounderstand what each element
        # in hello array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses hello raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load hello raw HVAC.csv file, parse it using hello function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="9ccb0-145">設定 hello Spark 機器學習管線包含三個階段： tokenizer、 hashingTF 和 lr。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-145">Configure hello Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="9ccb0-146">如需了解什麼是管線，以及管線的運作方式，請參閱 <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark 機器學習管線</a>。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="9ccb0-147">貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-147">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="9ccb0-148">調整的 hello 管線 toohello 訓練文件。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-148">Fit hello pipeline toohello training document.</span></span> <span data-ttu-id="9ccb0-149">貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-149">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="9ccb0-150">請確認 hello 訓練文件 toocheckpoint hello 應用程式的進度。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-150">Verify hello training document toocheckpoint your progress with hello application.</span></span> <span data-ttu-id="9ccb0-151">貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-151">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="9ccb0-152">這應該會產生 hello 輸出類似 toohello 下列：</span><span class="sxs-lookup"><span data-stu-id="9ccb0-152">This should give hello output similar toohello following:</span></span>
   
        +----------+----------+-----+
        |BuildingID|SystemInfo|label|
        +----------+----------+-----+
        |         4|     13 20|  0.0|
        |        17|      3 20|  0.0|
        |        18|     17 20|  1.0|
        |        15|      2 23|  0.0|
        |         3|      16 9|  1.0|
        |         4|     13 28|  0.0|
        |         2|     12 24|  0.0|
        |        16|     20 26|  1.0|
        |         9|      16 9|  1.0|
        |        12|       6 5|  0.0|
        |        15|     10 17|  1.0|
        |         7|      2 11|  0.0|
        |        15|      14 2|  1.0|
        |         6|       3 2|  0.0|
        |        20|     19 22|  0.0|
        |         8|     19 11|  0.0|
        |         6|      15 7|  0.0|
        |        13|      12 5|  0.0|
        |         4|      8 22|  0.0|
        |         7|      17 5|  0.0|
        +----------+----------+-----+

    <span data-ttu-id="9ccb0-153">請返回並確認 hello 輸出針對 hello 未經處理的 CSV 檔案。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-153">Go back and verify hello output against hello raw CSV file.</span></span> <span data-ttu-id="9ccb0-154">例如，hello 第一個資料列 hello CSV 檔案具有這項資料：</span><span class="sxs-lookup"><span data-stu-id="9ccb0-154">For example, hello first row hello CSV file has this data:</span></span>

    <span data-ttu-id="9ccb0-155">![適用於 Spark 機器學習服務範例的輸出資料快照集](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "適用於 Spark 機器學習服務範例的輸出資料快照集")</span><span class="sxs-lookup"><span data-stu-id="9ccb0-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="9ccb0-156">請注意如何 hello 實際溫度小於 hello 目標溫度建議 hello 建置是陌生。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-156">Notice how hello actual temperature is less than hello target temperature suggesting hello building is cold.</span></span> <span data-ttu-id="9ccb0-157">因此在 hello 訓練輸出中，hello 值**標籤**hello 在第一個資料列是**0.0**，這代表 hello 建置熱。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-157">Hence in hello training output, hello value for **label** in hello first row is **0.0**, which means hello building is not hot.</span></span>

1. <span data-ttu-id="9ccb0-158">準備資料集 toorun hello 定型的模型。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-158">Prepare a data set toorun hello trained model against.</span></span> <span data-ttu-id="9ccb0-159">toodo 因此，我們會傳送系統識別碼與系統存留期 (表示為**簡明**hello 訓練輸出中)，而且 hello 模型會預測是否 hello 建置與該系統的識別碼和系統存留期會更高 （以表示 1.0） 或冷卻器 （以 0.0 表示）。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-159">toodo so, we would pass on a system ID and system age (denoted as **SystemInfo** in hello training output), and hello model would predict whether hello building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="9ccb0-160">貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-160">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="9ccb0-161">最後，在 hello 測試資料上進行預測。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-161">Finally, make predictions on hello test data.</span></span> <span data-ttu-id="9ccb0-162">貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-162">Paste hello following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="9ccb0-163">您應該會看到類似 toohello 下列輸出：</span><span class="sxs-lookup"><span data-stu-id="9ccb0-163">You should see an output similar toohello following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="9ccb0-164">從 hello hello 預測中第一個資料列，您可以查看對於 HVAC 系統識別碼 20 與 25 年系統存留期，hello 建置將會作用 (**預測 = 1.0**)。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-164">From hello first row in hello prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, hello building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="9ccb0-165">hello DenseVector (0.49999) 的第一個值對應 toohello 預測 0.0，而第二個值 (0.5001) hello 對應 toohello 預測 1.0。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-165">hello first value for DenseVector (0.49999) corresponds toohello  prediction 0.0 and hello second value (0.5001) corresponds toohello prediction 1.0.</span></span> <span data-ttu-id="9ccb0-166">在 hello 輸出中，即使 hello 第二個值只是稍微更高版本，hello 模型顯示**預測 = 1.0**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-166">In hello output, even though hello second value is only marginally higher, hello model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="9ccb0-167">當您完成執行 hello 應用程式之後，您應該關閉 hello 筆記本 toorelease hello 資源。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-167">After you have finished running hello application, you should shutdown hello notebook toorelease hello resources.</span></span> <span data-ttu-id="9ccb0-168">toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-168">toodo so, from hello **File** menu on hello notebook, click **Close and Halt**.</span></span> <span data-ttu-id="9ccb0-169">這將會關機並關閉 hello 筆記本。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-169">This will shutdown and close hello notebook.</span></span>

## <span data-ttu-id="9ccb0-170"><a name="anaconda"></a>使用適用於 Spark 機器學習服務的 Anaconda scikit-learn 程式庫</span><span class="sxs-lookup"><span data-stu-id="9ccb0-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="9ccb0-171">HDInsight 上的 Apache Spark 叢集包含 Anaconda 程式庫。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="9ccb0-172">這也包括 hello **scikit-了解**機器學習程式庫。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-172">This also includes hello **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="9ccb0-173">hello 程式庫也包含可讓您直接從 Jupyter 筆記本 toobuild 範例應用程式的各種資料集。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-173">hello library also includes various data sets that you can use toobuild sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="9ccb0-174">如需使用範例 hello scikit-了解文件庫，請參閱[http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html)。</span><span class="sxs-lookup"><span data-stu-id="9ccb0-174">For examples on using hello scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="9ccb0-175"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="9ccb0-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="9ccb0-176">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="9ccb0-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="9ccb0-177">案例</span><span class="sxs-lookup"><span data-stu-id="9ccb0-177">Scenarios</span></span>
* [<span data-ttu-id="9ccb0-178">Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="9ccb0-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="9ccb0-179">機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark</span><span class="sxs-lookup"><span data-stu-id="9ccb0-179">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="9ccb0-180">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="9ccb0-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="9ccb0-181">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="9ccb0-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="9ccb0-182">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="9ccb0-182">Create and run applications</span></span>
* [<span data-ttu-id="9ccb0-183">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="9ccb0-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="9ccb0-184">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="9ccb0-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="9ccb0-185">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="9ccb0-185">Tools and extensions</span></span>
* [<span data-ttu-id="9ccb0-186">HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 個應用程式</span><span class="sxs-lookup"><span data-stu-id="9ccb0-186">Use HDInsight Tools Plugin for IntelliJ IDEA toocreate and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="9ccb0-187">從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="9ccb0-187">Use HDInsight Tools Plugin for IntelliJ IDEA toodebug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="9ccb0-188">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="9ccb0-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="9ccb0-189">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="9ccb0-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="9ccb0-190">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="9ccb0-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="9ccb0-191">在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="9ccb0-191">Install Jupyter on your computer and connect tooan HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="9ccb0-192">管理資源</span><span class="sxs-lookup"><span data-stu-id="9ccb0-192">Manage resources</span></span>
* [<span data-ttu-id="9ccb0-193">管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="9ccb0-193">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="9ccb0-194">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="9ccb0-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
