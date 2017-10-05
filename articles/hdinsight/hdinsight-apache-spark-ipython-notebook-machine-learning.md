---
title: "在 Azure HDInsight 上建置 Apache Spark 機器學習服務應用程式 | Microsoft Docs"
description: "逐步指示如何使用 Jupyter Notebook 在 HDInsight Spark 叢集上建置 Apache Spark 機器學習服務應用程式"
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
ms.openlocfilehash: 158ade4612104020e0231794e7123ea5cad6c459
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a><span data-ttu-id="ff48b-103">在 Azure HDInsight 上建置 Apache Spark 機器學習服務應用程式</span><span class="sxs-lookup"><span data-stu-id="ff48b-103">Build Apache Spark machine learning applications on Azure HDInsight</span></span>

<span data-ttu-id="ff48b-104">了解如何在 HDInsight 上使用 Spark 叢集建置 Apache Spark 機器學習服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff48b-104">Learn how to build an Apache Spark machine learning application using a Spark cluster on HDInsight.</span></span> <span data-ttu-id="ff48b-105">本文說明如何使用叢集隨附的 Jupyter Notebook 來建置及測試此應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff48b-105">This article shows how to use the Jupyter notebook available with the cluster to build and test this application.</span></span> <span data-ttu-id="ff48b-106">應用程式使用所有叢集預設提供的範例 HVAC.csv 資料。</span><span class="sxs-lookup"><span data-stu-id="ff48b-106">The application uses the sample HVAC.csv data that is available on all clusters by default.</span></span>

<span data-ttu-id="ff48b-107">**必要條件：**</span><span class="sxs-lookup"><span data-stu-id="ff48b-107">**Prerequisites:**</span></span>

<span data-ttu-id="ff48b-108">您必須滿足以下條件：</span><span class="sxs-lookup"><span data-stu-id="ff48b-108">You must have the following:</span></span>

* <span data-ttu-id="ff48b-109">HDInsight 上的 Apache Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="ff48b-109">An Apache Spark cluster on HDInsight.</span></span> <span data-ttu-id="ff48b-110">如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="ff48b-110">For instructions, see [Create Apache Spark clusters in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> 

## <span data-ttu-id="ff48b-111"><a name="data"></a>了解資料集</span><span class="sxs-lookup"><span data-stu-id="ff48b-111"><a name="data"></a>Understand the data set</span></span>
<span data-ttu-id="ff48b-112">在開始建置應用程式之前，我們先來了解要建置應用程式的資料結構，以及要針對資料執行的分析種類。</span><span class="sxs-lookup"><span data-stu-id="ff48b-112">Before we start building the application, let us understand the structure of the data for which we build the application and the kind of analysis we will do on the data.</span></span> 

<span data-ttu-id="ff48b-113">在本文中，我們使用的範例是 **HVAC.csv** 資料檔案，您可以在與 HDInsight 叢集相關聯的 Azure 儲存體帳戶中取得此檔案。</span><span class="sxs-lookup"><span data-stu-id="ff48b-113">In this article, we use the sample **HVAC.csv** data file that is available in the Azure Storage account that you associated with the HDInsight cluster.</span></span> <span data-ttu-id="ff48b-114">在儲存體帳戶中，檔案位於 **\HdiSamples\HdiSamples\SensorSampleData\hvac**。</span><span class="sxs-lookup"><span data-stu-id="ff48b-114">Within the storage account, the file is at **\HdiSamples\HdiSamples\SensorSampleData\hvac**.</span></span> <span data-ttu-id="ff48b-115">下載及開啟 CSV 檔案，以取得資料的快照。</span><span class="sxs-lookup"><span data-stu-id="ff48b-115">Download and open the CSV file to get a snapshot of the data.</span></span>  

<span data-ttu-id="ff48b-116">![用於 Spark 機器學習服務範例的資料快照集](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "用於 Spark 機器學習服務範例的資料快照集")</span><span class="sxs-lookup"><span data-stu-id="ff48b-116">![Snapshot of data used for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "Snapshot of data used for Spark machine learning example")</span></span>

<span data-ttu-id="ff48b-117">這項資料會顯示安裝 HVAC 系統之建築物的目標溫度和實際溫度。</span><span class="sxs-lookup"><span data-stu-id="ff48b-117">The data shows the target temperature and the actual temperature of a building that has HVAC systems installed.</span></span> <span data-ttu-id="ff48b-118">我們假設 [System] 資料行代表系統識別碼，而 [SystemAge] 資料行代表 HVAC 系統安裝在建築物中的年數。</span><span class="sxs-lookup"><span data-stu-id="ff48b-118">Let's assume the **System** column represents the system ID and the **SystemAge** column represents the number of years the HVAC system has been in place at the building.</span></span>

<span data-ttu-id="ff48b-119">在指定系統識別碼和系統年期的情況下，我們可以使用這些資料來預測建築物的溫度會比目標溫度高或低。</span><span class="sxs-lookup"><span data-stu-id="ff48b-119">We use this data to predict whether a building will be hotter or colder based on the target temperature, given a system ID and system age.</span></span>

## <span data-ttu-id="ff48b-120"><a name="app"></a>使用 Spark MLlib 撰寫 Spark 機器學習服務應用程式</span><span class="sxs-lookup"><span data-stu-id="ff48b-120"><a name="app"></a>Write a Spark machine learning application using Spark MLlib</span></span>
<span data-ttu-id="ff48b-121">在此應用程式中，我們會使用 Spark ML 管線來執行文件分類。</span><span class="sxs-lookup"><span data-stu-id="ff48b-121">In this application we use a Spark ML pipeline to perform a document classification.</span></span> <span data-ttu-id="ff48b-122">在管線中，我們將文件分割成單字、將單字轉換成數值特性向量，最後再使用特性向量和標籤建立預測模型。</span><span class="sxs-lookup"><span data-stu-id="ff48b-122">In the pipeline, we split the document into words, convert the words into a numerical feature vector, and finally build a prediction model using the feature vectors and labels.</span></span> <span data-ttu-id="ff48b-123">執行下列步驟以建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="ff48b-123">Perform the following steps to create the application.</span></span>

1. <span data-ttu-id="ff48b-124">在 [Azure 入口網站](https://portal.azure.com/)的開始面板中，按一下您的 Spark 叢集磚 (如果您已將其釘選到開始面板)。</span><span class="sxs-lookup"><span data-stu-id="ff48b-124">From the [Azure Portal](https://portal.azure.com/), from the startboard, click the tile for your Spark cluster (if you pinned it to the startboard).</span></span> <span data-ttu-id="ff48b-125">您也可以按一下 [瀏覽全部] > [HDInsight 叢集]，瀏覽至您的叢集。</span><span class="sxs-lookup"><span data-stu-id="ff48b-125">You can also navigate to your cluster under **Browse All** > **HDInsight Clusters**.</span></span>   
2. <span data-ttu-id="ff48b-126">從 Spark 叢集刀鋒視窗按一下 [叢集儀表板]，然後按一下 [Jupyter Notebook]。</span><span class="sxs-lookup"><span data-stu-id="ff48b-126">From the Spark cluster blade, click **Cluster Dashboard**, and then click **Jupyter Notebook**.</span></span> <span data-ttu-id="ff48b-127">出現提示時，輸入叢集的系統管理員認證。</span><span class="sxs-lookup"><span data-stu-id="ff48b-127">If prompted, enter the admin credentials for the cluster.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="ff48b-128">您也可以在瀏覽器中開啟下列 URL，來連接到您的叢集的 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="ff48b-128">You may also reach the Jupyter Notebook for your cluster by opening the following URL in your browser.</span></span> <span data-ttu-id="ff48b-129">使用您叢集的名稱取代 **CLUSTERNAME** ：</span><span class="sxs-lookup"><span data-stu-id="ff48b-129">Replace **CLUSTERNAME** with the name of your cluster:</span></span>
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. <span data-ttu-id="ff48b-130">建立新的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="ff48b-130">Create a new notebook.</span></span> <span data-ttu-id="ff48b-131">按一下 [新增]，然後按一下 [PySpark]。</span><span class="sxs-lookup"><span data-stu-id="ff48b-131">Click **New**, and then click **PySpark**.</span></span>
   
    <span data-ttu-id="ff48b-132">![建立 Spark 機器學習服務範例的 Jupyter Notebook](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "建立 Spark 機器學習服務範例的 Jupyter Notebook")</span><span class="sxs-lookup"><span data-stu-id="ff48b-132">![Create a Jupyter notebook for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "Create a Jupyter notebook for Spark machine learning example")</span></span>
4. <span data-ttu-id="ff48b-133">系統隨即會建立新 Notebook，並以 Untitled.pynb 的名稱開啟。</span><span class="sxs-lookup"><span data-stu-id="ff48b-133">A new notebook is created and opened with the name Untitled.pynb.</span></span> <span data-ttu-id="ff48b-134">在頂端按一下 Notebook 名稱，然後輸入好記的名稱。</span><span class="sxs-lookup"><span data-stu-id="ff48b-134">Click the notebook name at the top, and enter a friendly name.</span></span>
   
    <span data-ttu-id="ff48b-135">![提供 Spark 機器學習服務範例的 Notebook 名稱](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "提供 Spark 機器學習服務範例的 Notebook 名稱")</span><span class="sxs-lookup"><span data-stu-id="ff48b-135">![Provide a notebook name for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "Provide a notebook name for Spark machine learning example")</span></span>
5. <span data-ttu-id="ff48b-136">您使用 PySpark 核心建立 Notebook，因此不需要明確建立任何內容。</span><span class="sxs-lookup"><span data-stu-id="ff48b-136">Because you created a notebook using the PySpark kernel, you do not need to create any contexts explicitly.</span></span> <span data-ttu-id="ff48b-137">當您執行第一個程式碼儲存格時，系統會自動為您建立 Spark 和 Hive 內容。</span><span class="sxs-lookup"><span data-stu-id="ff48b-137">The Spark and Hive contexts will be automatically created for you when you run the first code cell.</span></span> <span data-ttu-id="ff48b-138">首先，您可以匯入此案例需要的類型。</span><span class="sxs-lookup"><span data-stu-id="ff48b-138">You can start by importing the types that are required for this scenario.</span></span> <span data-ttu-id="ff48b-139">將下列程式碼片段貼到空白儲存格中，然後按 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="ff48b-139">Paste the following snippet in an empty cell, and then press **SHIFT + ENTER**.</span></span> 
   
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
6. <span data-ttu-id="ff48b-140">您現在必須載入資料 (hvac.csv)、剖析資料，以及利用它來為模型定型。</span><span class="sxs-lookup"><span data-stu-id="ff48b-140">You must now load the data (hvac.csv), parse it, and use it to train the model.</span></span> <span data-ttu-id="ff48b-141">為此，您需要定義檢查建築物之實際溫度是否高於目標溫度的函示。</span><span class="sxs-lookup"><span data-stu-id="ff48b-141">For this, you define a function that checks whether the actual temperature of the building is greater than the target temperature.</span></span> <span data-ttu-id="ff48b-142">如果實際溫度較高，代表建築物是熱的，我們以 **1.0**值來表示這個狀態。</span><span class="sxs-lookup"><span data-stu-id="ff48b-142">If the actual temperature is greater, the building is hot, denoted by the value **1.0**.</span></span> <span data-ttu-id="ff48b-143">如果實際溫度較低，代表建築物是冷的，我們以 **0.0**值來表示這個狀態。</span><span class="sxs-lookup"><span data-stu-id="ff48b-143">If the actual temperature is lesser, the building is cold, denoted by the value **0.0**.</span></span> 
   
    <span data-ttu-id="ff48b-144">將下列程式碼片段貼到空白儲存格中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="ff48b-144">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>

        # List the structure of data for better understanding. Because the data will be
        # loaded as an array, this structure makes it easy to understand what each element
        # in the array corresponds to

        # 0 Date
        # 1 Time
        # 2 TargetTemp
        # 3 ActualTemp
        # 4 System
        # 5 SystemAge
        # 6 BuildingID

        LabeledDocument = Row("BuildingID", "SystemInfo", "label")

        # Define a function that parses the raw CSV file and returns an object of type LabeledDocument

        def parseDocument(line):
            values = [str(x) for x in line.split(',')]
            if (values[3] > values[2]):
                hot = 1.0
            else:
                hot = 0.0        

            textValue = str(values[4]) + " " + str(values[5])

            return LabeledDocument((values[6]), textValue, hot)

        # Load the raw HVAC.csv file, parse it using the function
        data = sc.textFile("wasb:///HdiSamples/HdiSamples/SensorSampleData/hvac/HVAC.csv")

        documents = data.filter(lambda s: "Date" not in s).map(parseDocument)
        training = documents.toDF()


1. <span data-ttu-id="ff48b-145">設定包含三個階段的 Spark 機器學習管線：tokenizer、hashingTF 及 lr。</span><span class="sxs-lookup"><span data-stu-id="ff48b-145">Configure the Spark machine learning pipeline that consists of three stages: tokenizer, hashingTF, and lr.</span></span> <span data-ttu-id="ff48b-146">如需了解什麼是管線，以及管線的運作方式，請參閱 <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark 機器學習管線</a>。</span><span class="sxs-lookup"><span data-stu-id="ff48b-146">For more information about what is a pipeline and how it works see <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark machine learning pipeline</a>.</span></span>
   
    <span data-ttu-id="ff48b-147">將下列程式碼片段貼到空白儲存格中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="ff48b-147">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. <span data-ttu-id="ff48b-148">讓管線符合訓練文件。</span><span class="sxs-lookup"><span data-stu-id="ff48b-148">Fit the pipeline to the training document.</span></span> <span data-ttu-id="ff48b-149">將下列程式碼片段貼到空白儲存格中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="ff48b-149">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        model = pipeline.fit(training)
3. <span data-ttu-id="ff48b-150">驗證訓練文件以根據應用程式的進度設立檢查點。</span><span class="sxs-lookup"><span data-stu-id="ff48b-150">Verify the training document to checkpoint your progress with the application.</span></span> <span data-ttu-id="ff48b-151">將下列程式碼片段貼到空白儲存格中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="ff48b-151">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        training.show()
   
    <span data-ttu-id="ff48b-152">如此應該會產生如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="ff48b-152">This should give the output similar to the following:</span></span>
   
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

    <span data-ttu-id="ff48b-153">返回並根據原始 CSV 檔案驗證輸出。</span><span class="sxs-lookup"><span data-stu-id="ff48b-153">Go back and verify the output against the raw CSV file.</span></span> <span data-ttu-id="ff48b-154">例如，CSV 檔案中第一個資料列的資料為：</span><span class="sxs-lookup"><span data-stu-id="ff48b-154">For example, the first row the CSV file has this data:</span></span>

    <span data-ttu-id="ff48b-155">![適用於 Spark 機器學習服務範例的輸出資料快照集](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "適用於 Spark 機器學習服務範例的輸出資料快照集")</span><span class="sxs-lookup"><span data-stu-id="ff48b-155">![Output data snapshot for Spark machine learning example](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "Output data snapshot for Spark machine learning example")</span></span>

    <span data-ttu-id="ff48b-156">請注意，實際溫度比目標溫度低的情況代表建築物處於低溫狀態。</span><span class="sxs-lookup"><span data-stu-id="ff48b-156">Notice how the actual temperature is less than the target temperature suggesting the building is cold.</span></span> <span data-ttu-id="ff48b-157">因此在訓練輸出中，第一個資料列的 [label] 值為 [0.0]，這代表建築物不是熱的。</span><span class="sxs-lookup"><span data-stu-id="ff48b-157">Hence in the training output, the value for **label** in the first row is **0.0**, which means the building is not hot.</span></span>

1. <span data-ttu-id="ff48b-158">準備要做為定型模型之執行依據的資料集。</span><span class="sxs-lookup"><span data-stu-id="ff48b-158">Prepare a data set to run the trained model against.</span></span> <span data-ttu-id="ff48b-159">方法是傳遞系統識別碼和系統年期 (在訓練輸出中以 **SystemInfo** 來代表)，然後模型會預測該系統識別碼和系統年期所屬的建築物溫度是較熱 (以 1.0 表示) 或較冷 (以 0.0 表示)。</span><span class="sxs-lookup"><span data-stu-id="ff48b-159">To do so, we would pass on a system ID and system age (denoted as **SystemInfo** in the training output), and the model would predict whether the building with that system ID and system age would be hotter (denoted by 1.0) or cooler (denoted by 0.0).</span></span>
   
   <span data-ttu-id="ff48b-160">將下列程式碼片段貼到空白儲存格中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="ff48b-160">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. <span data-ttu-id="ff48b-161">最後，根據測試資料進行預測。</span><span class="sxs-lookup"><span data-stu-id="ff48b-161">Finally, make predictions on the test data.</span></span> <span data-ttu-id="ff48b-162">將下列程式碼片段貼到空白儲存格中，然後按下 **SHIFT + ENTER**。</span><span class="sxs-lookup"><span data-stu-id="ff48b-162">Paste the following snippet in an empty cell and press **SHIFT + ENTER**.</span></span>
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. <span data-ttu-id="ff48b-163">您應該會看到如下所示的輸出：</span><span class="sxs-lookup"><span data-stu-id="ff48b-163">You should see an output similar to the following:</span></span>
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   <span data-ttu-id="ff48b-164">從預測的第一個資料列可看出，對於識別碼為 20 且年期為 25 年的 HVAC 系統而言，建築物將會是熱的 (**prediction=1.0**)。</span><span class="sxs-lookup"><span data-stu-id="ff48b-164">From the first row in the prediction, you can see that for an HVAC system with ID 20 and system age of 25 years, the building will be hot (**prediction=1.0**).</span></span> <span data-ttu-id="ff48b-165">DenseVector (0.49999) 的第一個值對應到預測 0.0，而第二個值 (0.5001) 對應到預測 1.0。</span><span class="sxs-lookup"><span data-stu-id="ff48b-165">The first value for DenseVector (0.49999) corresponds to the  prediction 0.0 and the second value (0.5001) corresponds to the prediction 1.0.</span></span> <span data-ttu-id="ff48b-166">在輸出中，即使第二個值只是稍微高一點，模型仍舊顯示 **prediction=1.0**。</span><span class="sxs-lookup"><span data-stu-id="ff48b-166">In the output, even though the second value is only marginally higher, the model shows **prediction=1.0**.</span></span>
4. <span data-ttu-id="ff48b-167">應用程式執行完畢之後，您應該要關閉 Notebook 來釋放資源。</span><span class="sxs-lookup"><span data-stu-id="ff48b-167">After you have finished running the application, you should shutdown the notebook to release the resources.</span></span> <span data-ttu-id="ff48b-168">若要這樣做，請從 Notebook 的 [檔案] 功能表中，按一下 [關閉並停止]。</span><span class="sxs-lookup"><span data-stu-id="ff48b-168">To do so, from the **File** menu on the notebook, click **Close and Halt**.</span></span> <span data-ttu-id="ff48b-169">這樣就能夠結束並關閉 Notebook。</span><span class="sxs-lookup"><span data-stu-id="ff48b-169">This will shutdown and close the notebook.</span></span>

## <span data-ttu-id="ff48b-170"><a name="anaconda"></a>使用適用於 Spark 機器學習服務的 Anaconda scikit-learn 程式庫</span><span class="sxs-lookup"><span data-stu-id="ff48b-170"><a name="anaconda"></a>Use Anaconda scikit-learn library for Spark machine learning</span></span>
<span data-ttu-id="ff48b-171">HDInsight 上的 Apache Spark 叢集包含 Anaconda 程式庫。</span><span class="sxs-lookup"><span data-stu-id="ff48b-171">Apache Spark clusters on HDInsight include Anaconda libraries.</span></span> <span data-ttu-id="ff48b-172">其中也包含適用於機器學習的 **scikit-learn** 程式庫。</span><span class="sxs-lookup"><span data-stu-id="ff48b-172">This also includes the **scikit-learn** library for machine learning.</span></span> <span data-ttu-id="ff48b-173">此程式庫另包含用來直接從 Jupyter Notebook 建置範例應用程式的各種資料集。</span><span class="sxs-lookup"><span data-stu-id="ff48b-173">The library also includes various data sets that you can use to build sample applications directly from a Jupyter notebook.</span></span> <span data-ttu-id="ff48b-174">如需使用 scikit-learn 程式庫的範例，請參閱 [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html)。</span><span class="sxs-lookup"><span data-stu-id="ff48b-174">For examples on using the scikit-learn library, see [http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html).</span></span>

## <span data-ttu-id="ff48b-175"><a name="seealso"></a>另請參閱</span><span class="sxs-lookup"><span data-stu-id="ff48b-175"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="ff48b-176">概觀：Azure HDInsight 上的 Apache Spark</span><span class="sxs-lookup"><span data-stu-id="ff48b-176">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="ff48b-177">案例</span><span class="sxs-lookup"><span data-stu-id="ff48b-177">Scenarios</span></span>
* [<span data-ttu-id="ff48b-178">Spark 和 BI：搭配 BI 工具來使用 HDInsight 中的 Spark 以執行互動式資料分析</span><span class="sxs-lookup"><span data-stu-id="ff48b-178">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ff48b-179">Spark 和機器學習：使用 HDInsight 中的 Spark 來預測食物檢查結果</span><span class="sxs-lookup"><span data-stu-id="ff48b-179">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ff48b-180">Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式</span><span class="sxs-lookup"><span data-stu-id="ff48b-180">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)
* [<span data-ttu-id="ff48b-181">使用 HDInsight 中的 Spark 進行網站記錄分析</span><span class="sxs-lookup"><span data-stu-id="ff48b-181">Website log analysis using Spark in HDInsight</span></span>](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a><span data-ttu-id="ff48b-182">建立及執行應用程式</span><span class="sxs-lookup"><span data-stu-id="ff48b-182">Create and run applications</span></span>
* [<span data-ttu-id="ff48b-183">使用 Scala 建立獨立應用程式</span><span class="sxs-lookup"><span data-stu-id="ff48b-183">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ff48b-184">利用 Livy 在 Spark 叢集上遠端執行作業</span><span class="sxs-lookup"><span data-stu-id="ff48b-184">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a><span data-ttu-id="ff48b-185">工具和擴充功能</span><span class="sxs-lookup"><span data-stu-id="ff48b-185">Tools and extensions</span></span>
* [<span data-ttu-id="ff48b-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons (使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式來建立和提交 Spark Scala 應用程式)</span><span class="sxs-lookup"><span data-stu-id="ff48b-186">Use HDInsight Tools Plugin for IntelliJ IDEA to create and submit Spark Scala applicatons</span></span>](hdinsight-apache-spark-intellij-tool-plugin.md)
* [<span data-ttu-id="ff48b-187">使用 IntelliJ IDEA 的 HDInsight Tools 外掛程式遠端偵錯 Spark 應用程式</span><span class="sxs-lookup"><span data-stu-id="ff48b-187">Use HDInsight Tools Plugin for IntelliJ IDEA to debug Spark applications remotely</span></span>](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [<span data-ttu-id="ff48b-188">利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook</span><span class="sxs-lookup"><span data-stu-id="ff48b-188">Use Zeppelin notebooks with a Spark cluster on HDInsight</span></span>](hdinsight-apache-spark-zeppelin-notebook.md)
* [<span data-ttu-id="ff48b-189">HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心</span><span class="sxs-lookup"><span data-stu-id="ff48b-189">Kernels available for Jupyter notebook in Spark cluster for HDInsight</span></span>](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [<span data-ttu-id="ff48b-190">搭配 Jupyter Notebook 使用外部套件</span><span class="sxs-lookup"><span data-stu-id="ff48b-190">Use external packages with Jupyter notebooks</span></span>](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [<span data-ttu-id="ff48b-191">在電腦上安裝 Jupyter 並連接到 HDInsight Spark 叢集</span><span class="sxs-lookup"><span data-stu-id="ff48b-191">Install Jupyter on your computer and connect to an HDInsight Spark cluster</span></span>](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a><span data-ttu-id="ff48b-192">管理資源</span><span class="sxs-lookup"><span data-stu-id="ff48b-192">Manage resources</span></span>
* [<span data-ttu-id="ff48b-193">在 Azure HDInsight 中管理 Apache Spark 叢集的資源</span><span class="sxs-lookup"><span data-stu-id="ff48b-193">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)
* [<span data-ttu-id="ff48b-194">追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業</span><span class="sxs-lookup"><span data-stu-id="ff48b-194">Track and debug jobs running on an Apache Spark cluster in HDInsight</span></span>](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
