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
# <a name="build-apache-spark-machine-learning-applications-on-azure-hdinsight"></a>在 Azure HDInsight 上建置 Apache Spark 機器學習服務應用程式

了解如何 toobuild Apache Spark 機器學習應用程式使用的 Spark 叢集 HDInsight 上。 本文將說明如何 toouse hello Jupyter 筆記本隨附 hello 叢集 toobuild 及測試這個應用程式。 hello 應用程式會使用 hello 範例 HVAC.csv 資料可在預設情況下的所有叢集上。

**先決條件：**

您必須擁有 hello 下列：

* HDInsight 上的 Apache Spark 叢集。 如需指示，請參閱 [在 Azure HDInsight 中建立 Apache Spark 叢集](hdinsight-apache-spark-jupyter-spark-sql.md)。 

## <a name="data"></a>了解 hello 資料集
開始建置 hello 應用程式之前，讓我們了解 hello hello 資料，我們 hello 應用程式在建置和 hello 種類，我們會執行的分析的 hello 資料結構。 

在本文中，我們會使用 hello 範例**HVAC.csv** hello 與 hello HDInsight 叢集相關聯的 Azure 儲存體帳戶中可用的資料檔案。 Hello 的儲存體帳戶內 hello 檔案位於**\HdiSamples\HdiSamples\SensorSampleData\hvac**。 下載並開啟 hello CSV 檔案 tooget hello 資料快照集。  

![用於 Spark 機器學習服務範例的資料快照集](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-understand-data.png "用於 Spark 機器學習服務範例的資料快照集")

hello 資料會顯示 hello 目標溫度和 hello 實際溫度的已安裝的 HVAC 系統建置。 讓我們假設 hello**系統**資料行代表 hello 系統識別碼和 hello **SystemAge**資料行代表 hello hello HVAC 系統已經在 hello 建置中的年數。

我們會使用此資料 toopredict 是否建置將會更高或 colder hello 目標溫度，根據給定的系統識別碼和系統存留期。

## <a name="app"></a>使用 Spark MLlib 撰寫 Spark 機器學習服務應用程式
在此應用程式中，我們使用 Spark ML 管線 tooperform 文件分類。 在 hello 管線中，我們將 hello 文件分割成單字、 hello 字轉換成數值特徵向量，和最後建立預測模型使用 hello 特徵向量和標籤。 執行下列步驟 toocreate hello 應用程式的 hello。

1. 從 hello [Azure 入口網站](https://portal.azure.com/)，從 hello 開始面板中，按一下 Spark 叢集中的 hello 磚 （如果您釘選它 toohello 開始面板）。 您也可以導覽 tooyour 叢集下的**瀏覽所有** > **HDInsight 叢集**。   
2. 從 hello Spark 叢集刀鋒視窗中，按一下 **叢集儀表板**，然後按一下 **Jupyter 筆記本**。 如果出現提示，請輸入 hello 叢集 hello 系統管理員認證。
   
   > [!NOTE]
   > 您也可能由下列 URL 在瀏覽器中開啟 hello 叢集到達 hello Jupyter 筆記本。 取代**CLUSTERNAME** hello 名稱，為您的叢集：
   > 
   > `https://CLUSTERNAME.azurehdinsight.net/jupyter`
   > 
   > 
3. 建立新的 Notebook。 按一下 新增，然後按一下PySpark。
   
    ![建立 Spark 機器學習服務範例的 Jupyter Notebook](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-create-notebook.png "建立 Spark 機器學習服務範例的 Jupyter Notebook")
4. 建立新的記事本，並開啟 hello 名稱 Untitled.pynb。 按一下頂端 hello hello 筆記本名稱並輸入好記的名稱。
   
    ![提供 Spark 機器學習服務範例的 Notebook 名稱](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-notebook-name.png "提供 Spark 機器學習服務範例的 Notebook 名稱")
5. 因為您建立使用 hello PySpark 核心筆記本，您不需要 toocreate 任何內容明確。 hello Spark 和 Hive 內容將會自動為您建立執行 hello 第一個程式碼儲存格時。 您可以啟動匯入此案例所需的 hello 型別。 貼上下列程式碼片段中的空白儲存格，hello，然後按下**SHIFT + ENTER**。 
   
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
6. 您必須立即載入 hello 資料 (hvac.csv)、 剖析，並使用它 tootrain hello 模型。 這麼做，您可以定義的函式，會檢查 hello 的 hello 建置實際的溫度是否大於 hello 目標溫度。 如果 hello 實際溫度較大，hello 大樓是熱，hello 值所表示**1.0**。 如果較小者 hello 實際溫度，hello 大樓是冷，hello 值所表示**0.0**。 
   
    貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。

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


1. 設定 hello Spark 機器學習管線包含三個階段： tokenizer、 hashingTF 和 lr。 如需了解什麼是管線，以及管線的運作方式，請參閱 <a href="http://spark.apache.org/docs/latest/ml-guide.html#how-it-works" target="_blank">Spark 機器學習管線</a>。
   
    貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。
   
        tokenizer = Tokenizer(inputCol="SystemInfo", outputCol="words")
        hashingTF = HashingTF(inputCol=tokenizer.getOutputCol(), outputCol="features")
        lr = LogisticRegression(maxIter=10, regParam=0.01)
        pipeline = Pipeline(stages=[tokenizer, hashingTF, lr])
2. 調整的 hello 管線 toohello 訓練文件。 貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。
   
        model = pipeline.fit(training)
3. 請確認 hello 訓練文件 toocheckpoint hello 應用程式的進度。 貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。
   
        training.show()
   
    這應該會產生 hello 輸出類似 toohello 下列：
   
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

    請返回並確認 hello 輸出針對 hello 未經處理的 CSV 檔案。 例如，hello 第一個資料列 hello CSV 檔案具有這項資料：

    ![適用於 Spark 機器學習服務範例的輸出資料快照集](./media/hdinsight-apache-spark-ipython-notebook-machine-learning/spark-machine-learning-output-data.png "適用於 Spark 機器學習服務範例的輸出資料快照集")

    請注意如何 hello 實際溫度小於 hello 目標溫度建議 hello 建置是陌生。 因此在 hello 訓練輸出中，hello 值**標籤**hello 在第一個資料列是**0.0**，這代表 hello 建置熱。

1. 準備資料集 toorun hello 定型的模型。 toodo 因此，我們會傳送系統識別碼與系統存留期 (表示為**簡明**hello 訓練輸出中)，而且 hello 模型會預測是否 hello 建置與該系統的識別碼和系統存留期會更高 （以表示 1.0） 或冷卻器 （以 0.0 表示）。
   
   貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。
   
       # SystemInfo here is a combination of system ID followed by system age
       Document = Row("id", "SystemInfo")
       test = sc.parallelize([(1L, "20 25"),
                     (2L, "4 15"),
                     (3L, "16 9"),
                     (4L, "9 22"),
                     (5L, "17 10"),
                     (6L, "7 22")]) \
           .map(lambda x: Document(*x)).toDF() 
2. 最後，在 hello 測試資料上進行預測。 貼上下列程式碼片段中的空白資料格與按下的 hello **SHIFT + ENTER**。
   
        # Make predictions on test documents and print columns of interest
        prediction = model.transform(test)
        selected = prediction.select("SystemInfo", "prediction", "probability")
        for row in selected.collect():
            print row
3. 您應該會看到類似 toohello 下列輸出：
   
       Row(SystemInfo=u'20 25', prediction=1.0, probability=DenseVector([0.4999, 0.5001]))
       Row(SystemInfo=u'4 15', prediction=0.0, probability=DenseVector([0.5016, 0.4984]))
       Row(SystemInfo=u'16 9', prediction=1.0, probability=DenseVector([0.4785, 0.5215]))
       Row(SystemInfo=u'9 22', prediction=1.0, probability=DenseVector([0.4549, 0.5451]))
       Row(SystemInfo=u'17 10', prediction=1.0, probability=DenseVector([0.4925, 0.5075]))
       Row(SystemInfo=u'7 22', prediction=0.0, probability=DenseVector([0.5015, 0.4985]))
   
   從 hello hello 預測中第一個資料列，您可以查看對於 HVAC 系統識別碼 20 與 25 年系統存留期，hello 建置將會作用 (**預測 = 1.0**)。 hello DenseVector (0.49999) 的第一個值對應 toohello 預測 0.0，而第二個值 (0.5001) hello 對應 toohello 預測 1.0。 在 hello 輸出中，即使 hello 第二個值只是稍微更高版本，hello 模型顯示**預測 = 1.0**。
4. 當您完成執行 hello 應用程式之後，您應該關閉 hello 筆記本 toorelease hello 資源。 toodo 的話，從 hello**檔案**hello 筆記本功能表按一下**關閉而停止**。 這將會關機並關閉 hello 筆記本。

## <a name="anaconda"></a>使用適用於 Spark 機器學習服務的 Anaconda scikit-learn 程式庫
HDInsight 上的 Apache Spark 叢集包含 Anaconda 程式庫。 這也包括 hello **scikit-了解**機器學習程式庫。 hello 程式庫也包含可讓您直接從 Jupyter 筆記本 toobuild 範例應用程式的各種資料集。 如需使用範例 hello scikit-了解文件庫，請參閱[http://scikit-learn.org/stable/auto_examples/index.html](http://scikit-learn.org/stable/auto_examples/index.html)。

## <a name="seealso"></a>另請參閱
* [概觀：Azure HDInsight 上的 Apache Spark](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>案例
* [Spark 和 BI：在 HDInsight 中搭配使用 Spark 和 BI 工具執行互動式資料分析](hdinsight-apache-spark-use-bi-tools.md)
* [機器學習的 Spark： 使用 HDInsight toopredict 食物檢查結果中的 Spark](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [Spark 串流：使用 HDInsight 中的 Spark 來建置即時串流應用程式](hdinsight-apache-spark-eventhub-streaming.md)
* [使用 HDInsight 中的 Spark 進行網站記錄分析](hdinsight-apache-spark-custom-library-website-log-analysis.md)

### <a name="create-and-run-applications"></a>建立及執行應用程式
* [使用 Scala 建立獨立應用程式](hdinsight-apache-spark-create-standalone-application.md)
* [利用 Livy 在 Spark 叢集上遠端執行作業](hdinsight-apache-spark-livy-rest-interface.md)

### <a name="tools-and-extensions"></a>工具和擴充功能
* [HDInsight 工具外掛程式用於 IntelliJ 概念 toocreate 並提交 Spark Scala 個應用程式](hdinsight-apache-spark-intellij-tool-plugin.md)
* [從遠端使用 HDInsight Tools 外掛程式 IntelliJ 概念 toodebug Spark 應用程式](hdinsight-apache-spark-intellij-tool-plugin-debug-jobs-remotely.md)
* [利用 HDInsight 上的 Spark 叢集來使用 Zeppelin Notebook](hdinsight-apache-spark-zeppelin-notebook.md)
* [HDInsight 的 Spark 叢集中 Jupyter Notebook 可用的核心](hdinsight-apache-spark-jupyter-notebook-kernels.md)
* [搭配 Jupyter Notebook 使用外部套件](hdinsight-apache-spark-jupyter-notebook-use-external-packages.md)
* [在您的電腦上安裝 Jupyter 並連接 tooan HDInsight Spark 叢集](hdinsight-apache-spark-jupyter-notebook-install-locally.md)

### <a name="manage-resources"></a>管理資源
* [管理 Azure HDInsight 中的 hello Apache Spark 叢集的資源](hdinsight-apache-spark-resource-manager.md)
* [追蹤和偵錯在 HDInsight 中的 Apache Spark 叢集上執行的作業](hdinsight-apache-spark-job-debugging.md)

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-weblogs-sample]: hdinsight-hive-analyze-website-log.md
[hdinsight-sensor-data-sample]: hdinsight-hive-analyze-sensor-data.md

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
