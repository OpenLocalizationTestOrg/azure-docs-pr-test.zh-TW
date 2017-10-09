---
title: "aaaData 科學在 Azure 上使用 Scala 和 Spark |Microsoft 文件"
description: "如何為受監督的機器學習服務工作與 toouse Scala hello Spark 可調式 MLlib 和 Spark ML 封裝 Azure HDInsight Spark 叢集上。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: a7c97153-583e-48fe-b301-365123db3780
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev;deguhath
ms.openlocfilehash: e32ebd0b91417183fe48ee10ebc7929fd9605762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a>在 Azure 上使用 Scala 與 Spark 的資料科學
本文示範 toouse Scala hello Spark 可擴充 MLlib 與 Spark ML 受監督的機器學習工作的 Azure HDInsight Spark 叢集上的封裝。 它會引導您完成 hello 工作構成 hello[資料科學程序](http://aka.ms/datascienceprocess)： 擷取資料並探索、 視覺效果、 功能工程、 模型和模型耗用量。 hello 文件中的 hello 模型包括羅吉斯和線性迴歸、 隨機樹系和漸層促進式樹狀結構 (GBTs)、 tootwo 常見受監督的機器學習工作此外：

* 迴歸問題： 計程車路線的 hello 提示 amount （$） 的預測
* 二進位分類︰計程車車程的小費或不給小費 (1/0) 預測

hello 模型程序需要定型和測試資料集和相關的精確度標準的評估。 在本文中，您可以了解如何 toostore 這些模型在 Azure Blob 儲存體以及 tooscore 並評估其預測的效能。 本文亦涵蓋 hello 更進階的 toooptimize 模型使用交叉驗證和超參數牽涉的如何主題。 使用 hello 資料是範例 hello 2013 NYC 計程車行程及價位資料集可在 GitHub 上取得。

[Scala](http://www.scala-lang.org/)，hello Java 虛擬機器，為基礎的語言整合物件導向與功能性語言概念。 它是可擴充的語言，是很適合的 toodistributed hello 雲端中的處理，而 Azure Spark 叢集上執行。

[Spark](http://spark.apache.org/)一種開放原始碼平行處理架構支援記憶體中處理 tooboost hello 巨量資料分析應用程式效能。 hello Spark 處理引擎內建的速度、 容易使用，且複雜的分析。 Spark 的記憶體內分散式計算功能，使其成為機器學習和圖表計算中反覆演算法的絕佳選擇。 hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html)套件提供一組一致的框架，可協助您建立及微調實際的機器學習管線中的資料之上建立高階應用程式開發介面。 [MLlib](http://spark.apache.org/mllib/)是 Spark 的可調整的機器學習文件庫，它將模型化功能 toothis 分散式的環境。

[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md)是 hello Azure 託管服務的開放原始碼 Spark。 它也包含支援 Jupyter Scala 筆記本 hello Spark 叢集，並可以執行的 Spark SQL 的互動式查詢 tootransform，篩選和 Azure Blob 儲存體中的資料視覺化。 hello Scala 的程式碼片段中這篇文章提供 hello 解決方案，並顯示 hello 相關繪圖 toovisualize hello 資料執行中 Jupyter 筆記本 hello Spark 叢集上安裝。 這些主題中的 hello 模型步驟的程式碼您 tootrain，如何評估、 儲存和取用每一個輸入模型的該節目。

hello 安裝步驟與本文章中的程式碼適用於 Azure HDInsight 3.4 Spark 1.6。 不過，hello hello 和本文中的程式碼[Scala Jupyter 筆記本](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb)泛型以及應該使用任何 Spark 叢集上。 hello 叢集設定，而且管理步驟可能稍有不同如果您不想要使用 HDInsight Spark 顯示本文章中。

> [!NOTE]
> 顯示 toouse Python，而不是 Scala toocomplete 端對端資料科學處理程序的工作的主題，請參閱[使用 Azure HDInsight 上的 Spark 資料科學](machine-learning-data-science-spark-overview.md)。
> 
> 

## <a name="prerequisites"></a>必要條件
* 您必須擁有 Azure 訂用帳戶。 如果還沒有， [請取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。
* 您需要下列程序的 Azure HDInsight 3.4 Spark 1.6 叢集 toocomplete hello。 toocreate 叢集中，請參閱中的 hello 指示[快速入門： 建立 Azure HDInsight 上的 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)。 Hello 叢集類型與版本設定 hello**選取叢集類型**功能表。

![HDInsight 叢集類型組態](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

如需說明的 hello NYC 計程車路線資料以及 tooexecute 來自 Jupyter 筆記本 hello Spark 叢集上的程式碼的相關指示，請參閱 hello 相關章節[概觀的資料科學使用 Azure HDInsight 上的 Spark](machine-learning-data-science-spark-overview.md)。  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a>從 Jupyter 筆記本 hello Spark 叢集上執行 Scala 程式碼
您可以啟動 Jupyter 筆記本從 hello Azure 入口網站。 尋找在您的儀表板，hello Spark 叢集，並按一下它 tooenter hello 管理頁面，為您的叢集。 接下來，按一下**叢集儀表板**，然後按一下 **Jupyter 筆記本**tooopen hello 筆記本 hello Spark 叢集相關聯。

![叢集儀表板和 Jupyter Notebook](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

您也可以在 https://&lt;clustername&gt;.azurehdinsight.net/jupyter 存取 Jupyter Notebook。 取代*clustername*與 hello 叢集的名稱。 您需要您系統管理員帳戶 tooaccess hello Jupyter 筆記本 hello 密碼。

![經過 tooJupyter 筆記本 hello 叢集名稱](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

選取**Scala** toosee 該使用 hello PySpark API 有幾個範例的套裝筆記本目錄。 使用此套件的 Spark 主題位於包含 hello 程式碼範例的 Scala.ipynb 筆記本 hello 瀏覽模型及計分[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala)。

您可以上傳直接從 GitHub toohello Jupyter 筆記本伺服器 hello 筆記本，您的 Spark 叢集上。 在您 Jupyter 首頁上，按一下 hello**上傳** 按鈕。 在 hello 檔案總管 中，貼上 hello GitHub （未經處理的內容） URL，hello Scala 筆記本，，然後按一下**開啟**。 hello Scala 筆記本會位於下列 URL 的 hello:

[Exploration-Modeling-and-Scoring-using-Scala.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a>安裝程式︰預設的 Spark 和 Hive 內容、Spark Magic 和 Spark 程式庫
### <a name="preset-spark-and-hive-contexts"></a>預設的 Spark 和 Hive 內容
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


所提供的 Jupyter 筆記本 hello Spark 核心有預設的內容。 您開始使用您所開發的 hello 應用程式之前，您不需要 tooexplicitly 組 hello Spark 或登錄區內容。 hello 預先設定的內容如下：

* `sc` 代表 SparkContext
* `sqlContext` 代表 HiveContext

### <a name="spark-magics"></a>Spark Magic
hello Spark 核心提供一些預先定義 「"我們，這是特殊的命令，您可以呼叫與`%%`。 兩個命令會使用下列程式碼範例的 hello。

* `%%local`指定在本機執行接下來幾行中的 hello 程式碼。 hello 程式碼必須是有效的 Scala 程式碼。
* `%%sql -o <variable name>` 針對 `sqlContext` 執行 Hive 查詢。 如果 hello`-o`參數傳遞，hello hello 查詢結果會持續保留在 hello `%%local` Scala 成為 Spark 資料框架的內容。

您的 hello 核心 Jupyter 筆記本和其預先定義的詳細資訊 」 magics"的呼叫與`%%`(比方說， `%%local`)，請參閱[與 HDInsight Spark Linux Jupyter 筆記本的可用的核心叢集上HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)。

### <a name="import-libraries"></a>匯入程式庫
匯入 hello Spark、 MLlib 和其他文件庫，您必須使用下列程式碼的 hello。

    # IMPORT SPARK AND JAVA LIBRARIES
    import org.apache.spark.sql.SQLContext
    import org.apache.spark.sql.functions._
    import java.text.SimpleDateFormat
    import java.util.Calendar
    import sqlContext.implicits._
    import org.apache.spark.sql.Row

    # IMPORT SPARK SQL FUNCTIONS
    import org.apache.spark.sql.types.{StructType, StructField, StringType, IntegerType, FloatType, DoubleType}
    import org.apache.spark.sql.functions.rand

    # IMPORT SPARK ML FUNCTIONS
    import org.apache.spark.ml.Pipeline
    import org.apache.spark.ml.feature.{StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer, Binarizer}
    import org.apache.spark.ml.tuning.{ParamGridBuilder, TrainValidationSplit, CrossValidator}
    import org.apache.spark.ml.regression.{LinearRegression, LinearRegressionModel, RandomForestRegressor, RandomForestRegressionModel, GBTRegressor, GBTRegressionModel}
    import org.apache.spark.ml.classification.{LogisticRegression, LogisticRegressionModel, RandomForestClassifier, RandomForestClassificationModel, GBTClassifier, GBTClassificationModel}
    import org.apache.spark.ml.evaluation.{BinaryClassificationEvaluator, RegressionEvaluator, MulticlassClassificationEvaluator}

    # IMPORT SPARK MLLIB FUNCTIONS
    import org.apache.spark.mllib.linalg.{Vector, Vectors}
    import org.apache.spark.mllib.util.MLUtils
    import org.apache.spark.mllib.classification.{LogisticRegressionWithLBFGS, LogisticRegressionModel}
    import org.apache.spark.mllib.regression.{LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel}
    import org.apache.spark.mllib.tree.{GradientBoostedTrees, RandomForest}
    import org.apache.spark.mllib.tree.configuration.BoostingStrategy
    import org.apache.spark.mllib.tree.model.{GradientBoostedTreesModel, RandomForestModel, Predict}
    import org.apache.spark.mllib.evaluation.{BinaryClassificationMetrics, MulticlassMetrics, RegressionMetrics}

    # SPECIFY SQLCONTEXT
    val sqlContext = new SQLContext(sc)


## <a name="data-ingestion"></a>資料擷取
hello hello 資料科學程序中的第一個步驟是您想 tooanalyze tooingest hello 資料。 您將 hello 資料從外部來源或系統資料探索和模型環境的所在位置。 在本文中，您所擷取的 hello 資料會是聯結的 0.1 %hello 計程車行程及價位檔範例 （儲存為.tsv 檔案）。 hello 資料探索和模型環境是 Spark。 本節包含一系列的工作後 hello 程式碼 toocomplete hello:

1. 設定資料和模型儲存體的目錄路徑。
2. 讀取 hello 輸入資料集中 （儲存為.tsv 檔案）。
3. 定義 hello 和全新 hello 資料的結構描述。
4. 建立已清除的資料框架，並在記憶體中加以快取。
5. 註冊 hello 資料 SQLContext 中的暫存資料表。
6. 查詢 hello 資料表和 hello 結果匯入至資料框架。

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a>在 Azure Blob 儲存體中設定儲存位置的目錄路徑
Spark 可讀寫 tooAzure Blob 儲存體。 您可以使用 Spark tooprocess 任何現有的資料，並再儲存 hello 結果 Blob 儲存體中。

toosave 模型或 Blob 儲存體中的檔案，您需要 tooproperly 指定 hello 路徑。 參考 hello 預設容器使用的路徑，開頭附加 toohello Spark 叢集`wasb:///`。 使用 `wasb://`參考其他位置。

hello 下列程式碼範例指定 hello hello 模型儲存的位置讀取的 hello 輸入的資料 toobe 和 hello 路徑 tooBlob 存放裝置附加的 toohello Spark 叢集的位置。

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a>匯入資料、 建立 RDD，以及定義根據 toohello 結構描述資料框架
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello SCHEMA BASED ON hello HEADER OF hello FILE
    val sqlContext = new SQLContext(sc)
    val taxi_schema = StructType(
        Array(
            StructField("medallion", StringType, true),
            StructField("hack_license", StringType, true),
            StructField("vendor_id", StringType, true),
            StructField("rate_code", DoubleType, true),
            StructField("store_and_fwd_flag", StringType, true),
            StructField("pickup_datetime", StringType, true),
            StructField("dropoff_datetime", StringType, true),
            StructField("pickup_hour", DoubleType, true),
            StructField("pickup_week", DoubleType, true),
            StructField("weekday", DoubleType, true),
            StructField("passenger_count", DoubleType, true),
            StructField("trip_time_in_secs", DoubleType, true),
            StructField("trip_distance", DoubleType, true),
            StructField("pickup_longitude", DoubleType, true),
            StructField("pickup_latitude", DoubleType, true),
            StructField("dropoff_longitude", DoubleType, true),
            StructField("dropoff_latitude", DoubleType, true),
            StructField("direct_distance", StringType, true),
            StructField("payment_type", StringType, true),
            StructField("fare_amount", DoubleType, true),
            StructField("surcharge", DoubleType, true),
            StructField("mta_tax", DoubleType, true),
            StructField("tip_amount", DoubleType, true),
            StructField("tolls_amount", DoubleType, true),
            StructField("total_amount", DoubleType, true),
            StructField("tipped", DoubleType, true),
            StructField("tip_class", DoubleType, true)
            )
        )

    # CAST VARIABLES ACCORDING toohello SCHEMA
    val taxi_temp = (taxi_train_file.map(_.split("\t"))
                            .filter((r) => r(0) != "medallion")
                            .map(p => Row(p(0), p(1), p(2),
                                p(3).toDouble, p(4), p(5), p(6), p(7).toDouble, p(8).toDouble, p(9).toDouble, p(10).toDouble,
                                p(11).toDouble, p(12).toDouble, p(13).toDouble, p(14).toDouble, p(15).toDouble, p(16).toDouble,
                                p(17), p(18), p(19).toDouble, p(20).toDouble, p(21).toDouble, p(22).toDouble,
                                p(23).toDouble, p(24).toDouble, p(25).toDouble, p(26).toDouble)))


    # CREATE AN INITIAL DATA FRAME AND DROP COLUMNS, AND THEN CREATE A CLEANED DATA FRAME BY FILTERING FOR UNWANTED VALUES OR OUTLIERS
    val taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    val taxi_df_train_cleaned = (taxi_train_df.drop(taxi_train_df.col("medallion"))
            .drop(taxi_train_df.col("hack_license")).drop(taxi_train_df.col("store_and_fwd_flag"))
            .drop(taxi_train_df.col("pickup_datetime")).drop(taxi_train_df.col("dropoff_datetime"))
            .drop(taxi_train_df.col("pickup_longitude")).drop(taxi_train_df.col("pickup_latitude"))
            .drop(taxi_train_df.col("dropoff_longitude")).drop(taxi_train_df.col("dropoff_latitude"))
            .drop(taxi_train_df.col("surcharge")).drop(taxi_train_df.col("mta_tax"))
            .drop(taxi_train_df.col("direct_distance")).drop(taxi_train_df.col("tolls_amount"))
            .drop(taxi_train_df.col("total_amount")).drop(taxi_train_df.col("tip_class"))
            .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200"));

    # CACHE AND MATERIALIZE hello CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER hello DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**輸出：**

時間 toorun hello 資料格： 8 秒。

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a>查詢 hello 資料表，並匯入資料框架中的結果
下一步，查詢 hello 資料表價位、 旅客，和 tip 資料;篩選出損毀且外圍的資料。也會列印數個資料列。

    # QUERY hello DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY hello TOP THREE ROWS
    sqlResultsDF.show(3)

**輸出：**

| fare_amount | passenger_count | tip_amount | tipped |
| --- | --- | --- | --- |
|        13.5 |1.0 |2.9 |1.0 |
|        16.0 |2.0 |3.4 |1.0 |
|        10.5 |2.0 |1.0 |1.0 |

## <a name="data-exploration-and-visualization"></a>資料探索和虛擬化
Hello 資料帶入 Spark 之後，hello hello 資料科學程序中的下一個步驟是 toogain hello 資料探索和視覺效果的更深入了解。 在本節中，您可以檢查 hello 計程車資料使用 SQL 查詢。 然後，匯入資料框架 tooplot hello 結果 hello 目標變數和潛在的功能，如 visual 檢查使用 Jupyter hello 自動視覺效果功能。

### <a name="use-local-and-sql-magic-tooplot-data"></a>使用本機和 SQL magic tooplot 資料
根據預設，您從 Jupyter 筆記本執行任何程式碼片段的 hello 輸出可 hello hello 保存在 hello 背景工作節點的工作階段內容中。 如果希望 toosave 路線 toohello 背景工作角色節點的每個計算，且如果所有 hello 您需要您計算是在本機上 hello Jupyter 伺服器節點 （即 hello 前端節點） 可用的資料，您可以使用 hello `%%local` magic toorun hello 程式碼hello Jupyter 伺服器上的程式碼片段。

* **SQL magic** (`%%sql`)。 hello HDInsight Spark 核心支援 SQLContext 輕鬆內嵌 HiveQL 查詢。 hello (`-o VARIABLE_NAME`) 引數會保存 hello 的 hello SQL 查詢的輸出為熊資料框架 hello Jupyter 伺服器上。 這表示，將無法在 hello 本機模式中。
* `%%local` **magic**。 hello `%%local` magic hello 程式碼會在本機執行 hello Jupyter 在伺服器上，也就是 hello hello HDInsight 叢集前端節點。 通常，您會使用`%%local`magic 搭配 hello`%%sql`魔法與 hello`-o`參數。 hello`-o`參數會保存在本機，hello SQL 查詢的 hello 輸出，然後`%%local`magic 會觸發 hello 下在本機憑藉保存在本機上的 hello 輸出的 hello SQL 查詢的程式碼片段 toorun 一組。

### <a name="query-hello-data-by-using-sql"></a>使用 SQL 查詢 hello 資料
此查詢會擷取 hello 計程車往返價位量、 旅客計數的提示數量。

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

在下列程式碼的 hello，hello `%%local` magic 會建立本機資料框架，sqlResults。 您可以使用 sqlResults tooplot 使用 matplotlib。

> [!TIP]
> 本文中會多次使用本機 magic。 如果您的資料集很大，請範例 toocreate 本機記憶體內可容納的資料框架。
> 
> 

### <a name="plot-hello-data"></a>繪製 hello 的資料
您可以繪製後 hello 資料框架會成為資料框架，熊本機內容中使用的 Python 程式碼。

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 hello Spark 核心執行 hello 程式碼之後，自動視覺化 hello 的 SQL (HiveQL) 查詢的輸出。 您可以選擇數種類型的視覺效果︰

* 資料表
* 圓形圖
* 折線圖
* 領域
* 長條圖

以下是 hello 程式碼 tooplot hello 資料：

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # PLOT TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # PLOT TIP AMOUNT BY FARE AMOUNT; SCALE POINTS BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 80, -2, 20])
    plt.show()


**輸出：**

![小費金額長條圖](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![按乘客計數排列的小費金額](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![按費用金額排列的小費金額](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a>建立特徵和轉換特徵，然後準備資料輸入模型化函式
對於從 Spark ML 和 MLlib 樹狀結構為基礎的模型化函式，您需要 tooprepare 目標和功能使用各種不同的技術，例如分類收納、 索引、 一個熱門的編碼方式，與向量化。 以下是本節中的 hello 程序 toofollow:

1. 將小時 **納入** 流量時間值區以建立新特徵。
2. 套用**編製索引和一個熱編碼**toocategorical 功能。
3. **取樣和分割 hello 資料集**成定型集和測試的分數。
4. **指定訓練變數和特徵**，然後建立已編製索引或已進行 one-hot 編碼的訓練和測試輸入標示點彈性分散式資料集 (RDD) 或資料框架。
5. 自動**分類和向量化的功能和目標**toouse 做為輸入的機器學習模型。

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>將小時納入流量時間值區以建立新特徵
這段程式碼會示範 toocreate 的新功能的分類收納成流量時間的小時的值區及如何 toocache hello 產生資料框架，在記憶體中。 重複使用 RDDs 和資料框架，快取會導致 tooimproved 執行時間。 因此，您會在 hello 下列程序中的數個階段快取 RDDs 和資料框架。

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    val sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night"
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush"
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train
    """
    val taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE hello DATA FRAME IN MEMORY AND MATERIALIZE hello DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a>索引和 one-hot 編碼分類功能
hello 模型和預測的 MLlib 函式需要功能與類別的輸入的資料 toobe 編製索引，或編碼先前 toouse。 這個區段會顯示如何 tooindex 或編碼的輸入 hello 模型函式的類別特徵。

您需要 tooindex 或編碼您的模型，以不同的方式，視 hello 模型而定。 例如，羅吉斯和線性迴歸模型需要 one-hot 編碼。 例如，有三個類別的特徵可展開成三個特徵資料行。 每個資料行可能包含 0 或 1，視所觀察 hello 分類。 MLlib 提供 hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder)函式的其中一個熱門的編碼方式。 此編碼器將對應的二進位的向量，使用最多為單一其中一個值的標籤索引 tooa 資料行的資料行。 使用這種編碼方式，所預期的數字的重要的功能，例如羅吉斯迴歸演算法可以套用的 toocategorical 功能。

這裡您轉換只能有四個變數 tooshow 範例是字元字串。 您也可以將其他以數值表示的變數 (例如工作日) 編製索引為類別變數。

如需編製索引，請使用 `StringIndexer()`，如需進行 one-hot 編碼，請使用 MLlib 中的 `OneHotEncoder()` 函式。 以下是 hello tooindex 程式碼，並將編碼類別特徵：

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # INDEX AND ENCODE VENDOR_ID
    val stringIndexer = new StringIndexer().setInputCol("vendor_id").setOutputCol("vendorIndex").fit(taxi_df_train_with_newFeatures)
    val indexed = stringIndexer.transform(taxi_df_train_with_newFeatures)
    val encoder = new OneHotEncoder().setInputCol("vendorIndex").setOutputCol("vendorVec")
    val encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    val stringIndexer = new StringIndexer().setInputCol("rate_code").setOutputCol("rateIndex").fit(encoded1)
    val indexed = stringIndexer.transform(encoded1)
    val encoder = new OneHotEncoder().setInputCol("rateIndex").setOutputCol("rateVec")
    val encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    val stringIndexer = new StringIndexer().setInputCol("payment_type").setOutputCol("paymentIndex").fit(encoded2)
    val indexed = stringIndexer.transform(encoded2)
    val encoder = new OneHotEncoder().setInputCol("paymentIndex").setOutputCol("paymentVec")
    val encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    val stringIndexer = new StringIndexer().setInputCol("TrafficTimeBins").setOutputCol("TrafficTimeBinsIndex").fit(encoded3)
    val indexed = stringIndexer.transform(encoded3)
    val encoder = new OneHotEncoder().setInputCol("TrafficTimeBinsIndex").setOutputCol("TrafficTimeBinsVec")
    val encodedFinal = encoder.transform(indexed)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**輸出：**

儲存格-toorun hello 時間： 4 秒。

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a>取樣和分割成定型集和測試分數中 hello 資料集
此程式碼會建立隨機取樣的 hello 資料 （在此範例中，25%)。 取樣不需要因為 toohello 大小 hello 資料集的這個範例中，雖然 hello 文章向您示範如何可以取樣，以了解如何 toouse 它自己時所需的問題。 如果樣本數較大，這可以在訓練模型時節省大量時間。 接下來，將 hello 範例分割成定型部分 （在此範例中，75%) 和測試組件 （在此範例中，25%) toouse 分類和迴歸模型中的。

加入在定型期間可使用的 tooselect 交叉驗證摺疊資料隨機數字 （介於 0 和 1） tooeach 列 （在"rand 」 資料行中）。

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    val samplingFraction = 0.25;
    val trainingFraction = 0.75;
    val testingFraction = (1-trainingFraction);
    val seed = 1234;
    val encodedFinalSampledTmp = encodedFinal.sample(withReplacement = false, fraction = samplingFraction, seed = seed)
    val sampledDFcount = encodedFinalSampledTmp.count().toInt

    val generateRandomDouble = udf(() => {
        scala.util.Random.nextDouble
    })

    # ADD A RANDOM NUMBER FOR CROSS-VALIDATION
    val encodedFinalSampled = encodedFinalSampledTmp.withColumn("rand", generateRandomDouble());

    # SPLIT hello SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**輸出：**

時間 toorun hello 資料格： 2 秒。

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a>指定訓練變數和特徵，然後建立已編製索引或已進行 one-hot 編碼的訓練和測試輸入標示點 RDD 或資料框架
本節包含示範如何 tooindex 類別的文字資料加上標籤與資料類型及加以編碼，因此您可以使用它 tootrain 和測試 MLlib 羅吉斯迴歸和其他分類模型的程式碼。 標示點物件是 RDD，其格式化成適合 MLlib 中大部分機器學習演算法所需的輸入資料。 [標示點](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 是本機向量 (密集或疏鬆)，與標籤/回應相關聯。

在此程式碼中，您可以指定 hello 目標 （相依） 變數和 hello 功能 toouse tootrain 模型。 然後，建立已編製索引或已進行 one-hot 編碼的訓練和測試輸入標示點 RDD 或資料框架。

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY hello TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE tooTRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**輸出：**

儲存格-toorun hello 時間： 4 秒。

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a>自動分類，並做為機器學習模型的輸入向量化的功能和目標 toouse
您可以使用 Spark ML toocategorize hello 目標和功能 toouse 中樹狀結構為基礎的模型功能。 hello 程式碼會完成兩項工作：

* 藉由使用臨界值為 0.5，將指派 0 或 1 tooeach 資料點，介於 0 和 1 之間的值建立二進位分類的目標。
* 自動將功能分類。 如果小於 32 hello 相異值數目的數字的任何功能，並屬於該功能。

以下是這兩個工作的 hello 程式碼。

    # CATEGORIZE FEATURES AND BINARIZE hello TARGET FOR hello BINARY CLASSIFICATION PROBLEM

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTRAINbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTRAINwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTrainwithCatFeat = indexerModel.transform(indexedTESTbinaryDF)
    val binarizer: Binarizer = new Binarizer().setInputCol("label").setOutputCol("labelBin").setThreshold(0.5)
    val indexedTESTwithCatFeatBinTarget = binarizer.transform(indexedTrainwithCatFeat)

    # CATEGORIZE FEATURES FOR hello REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a>二進位分類模型：預測是否應支付小費
在本節中，您可以建立三種類型的二元分類模型 toopredict 應該付費秘訣：

* A**羅吉斯迴歸模型**使用 hello Spark ML`LogisticRegression()`函式
* A**隨機樹系分類模型**使用 hello Spark ML`RandomForestClassifier()`函式
* A**漸層停駐提升樹分類模型**使用 hello MLlib`GradientBoostedTrees()`函式

### <a name="create-a-logistic-regression-model"></a>建立羅吉斯迴歸模型
接下來，建立羅吉斯迴歸模型使用 hello Spark ML`LogisticRegression()`函式。 您建立 hello 模型建立一系列的步驟中的程式碼：

1. **定型 hello 模型**具有一個參數集的資料。
2. **評估 hello 模型**上測試資料集 （包括計量）。
3. **儲存 hello 模型**供未來取用的 Blob 儲存體中。
4. **計分 hello 模型**針對測試資料。
5. **繪製 hello 結果**使用接收器操作特徵 (ROC) 曲線。

這些程序的 「 hello 」 程式碼如下：

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON hello TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE hello MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

載入、 評分，以及儲存 hello 結果。

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD hello SAVED MODEL AND SCORE hello TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON hello TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` tooCOMPUTE hello TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC RESULTS
    println("ROC on test data = " + ROC)


**輸出：**

測試資料的 ROC = 0.9827381497557599

使用 Python 本機熊資料框架 tooplot hello ROC 曲線上。

    # QUERY hello RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT hello ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT hello ROC CURVE
    plt.figure(figsize=(5,5))
    plt.plot(fpr, tpr, label='ROC curve (area = %0.2f)' % roc_auc)
    plt.plot([0, 1], [0, 1], 'k--')
    plt.xlim([0.0, 1.0])
    plt.ylim([0.0, 1.05])
    plt.xlabel('False Positive Rate')
    plt.ylabel('True Positive Rate')
    plt.title('ROC Curve')
    plt.legend(loc="lower right")
    plt.show()


**輸出：**

![小費或沒有小費的 ROC 曲線](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a>建立隨機樹系分類模型
接下來，建立隨機樹系分類模型使用 hello Spark ML`RandomForestClassifier()`函式，並評估 hello 模型測試資料上的。

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE hello RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT hello MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE hello MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


**輸出：**

測試資料的 ROC = 0.9847103571552683

### <a name="create-a-gbt-classification-model"></a>建立 GBT 分類模型
接下來，建立 GBT 分類模型使用 MLlib 的`GradientBoostedTrees()`函式，並評估 hello 模型測試資料上的。

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN hello MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE hello MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE hello MODEL ON TEST INSTANCES AND hello COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS tooEVALUATE hello MODEL ON hello TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


**輸出：**

ROC 曲線夏的領域 = 0.9846895479241554

## <a name="regression-model-predict-tip-amount"></a>迴歸模型：預測小費金額
在本節中，您可以建立兩種類型的迴歸模型 toopredict hello 提示量：

* A**正則化的線性迴歸模型**使用 hello Spark ML`LinearRegression()`函式。 將儲存 hello 模型，並評估 hello 模型測試資料。
* A**漸層來提升樹迴歸模型**使用 hello Spark ML`GBTRegressor()`函式。

### <a name="create-a-regularized-linear-regression-model"></a>建立正則化線性迴歸模型
    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING hello SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT hello MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE hello MODEL OVER hello TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE hello MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT hello COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**輸出：**

儲存格-toorun hello 時間： 13 的秒數。

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE hello MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE hello MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("R-sqr on test data = " + r2)


**輸出：**

測試資料的 R-sqr = 0.5960320470835743

接下來，查詢 hello 測試結果為資料框架和 AutoVizWidget 和 matplotlib toovisualize 使用它。

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

hello 程式碼會建立從 hello 查詢輸出的本機資料框架，並繪製 hello 資料。 hello `%%local` magic 會建立本機資料框架， `sqlResults`，而您可以使用 matplotlib tooplot。

> [!NOTE]
> 本文中會多次使用此 Spark magic。 如果 hello 資料量很大，您應該取樣 toocreate 本機記憶體內可容納的資料框架。
> 
> 

使用 Python matplotlib 建立繪圖。

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT hello RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

**輸出：**

![小費金額︰實際與預測](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a>建立 GBT 迴歸模型
建立 GBT 迴歸模型使用 hello Spark ML`GBTRegressor()`函式，並評估 hello 模型測試資料上的。

[梯度推進樹](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) 集合了所有決策樹。 GBTs 定型決策樹反覆 toominimize 損失函數。 您可以使用 GBT 進行迴歸和分類。 GBT 可以處理分類特徵、不需要調整特徵，而且可以擷取非線性和特徵互動。 您也可以在多類別分類設定中使用 GBT。

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    # PRINT hello RESULTS
    println("Test R-sqr is: " + Test_R2);


**輸出：**

測試 R-sqr：0.7655383534596654

## <a name="advanced-modeling-utilities-for-optimization"></a>可供最佳化的進階模型化公用程式
在本節中，您將使用開發人員經常使用的機器學習公用程式來最佳化模型。 具體來說，您可以使用參數掃掠和交叉驗證，以三種不同的方式來最佳化機器學習模型︰

* Hello 資料分割成定型和驗證設定、 充分運用 hello 模型透過超參數牽涉上定型集，並評估上驗證設定 （線性迴歸）
* 最佳化 hello 模型使用交叉驗證和超參數掃掠利用 Spark ML CrossValidator 函式 （二元分類）
* 最佳化 hello 模型使用自訂交叉驗證 」 和 「 參數掃掠的程式碼 toouse 任何機器學習服務函數與參數集 （線性迴歸）

**交叉驗證**是評估如何在一組已知的資料上定型的模型將一般化 toopredict hello 功能所在它尚未定型資料集的技術。 hello 大概了解這項技術後面是已知的資料的資料集上定型模型，並接著 hello 其預測精確度的測試，之後根據獨立的資料集。 常見的實作是 toodivide 資料集分成*k*-摺疊，並再 hello 中定型模型，只留下其中一個 hello 摺疊所有以循環配置資源的方式。

**Hyper-v 參數最佳化**hello 問題選擇一組超參數學習演算法，通常以 hello 目標最佳化 hello 演算法的效能，在獨立的資料集上的量值。 值，您必須指定 hello 模型定型程序之外超參數。 Hello 彈性與 hello 模型的精確度，可能會影響超參數值的相關假設。 決策樹，例如有超參數，例如 hello 預期深度和 hello 樹狀目錄中的分葉數目。 您必須為支援向量機器 (SVM) 設定分類誤判損失詞彙。

常見的方式 tooperform 超參數最佳化是 toouse 方格搜尋，也稱為**參數掃掠**。 方格搜尋時，是徹底搜索經過 hello 值指定學習演算法的 hello 超參數空間的子集。 交叉驗證可以提供的效能度量 toosort 出 hello 所 hello 方格搜尋演算法產生最佳的結果。 如果您使用交叉驗證超參數牽涉，可協助限制問題，例如過度配適模型 tootraining 資料。 如此一來，hello 模型會保留 hello 容量 tooapply toohello 一般的資料集從哪些 hello 擷取定型資料。

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a>利用超參數掃掠來最佳化線性迴歸模型
接下來，將資料分割成定型和驗證設定，參數使用超集上定型掃掠設定 toooptimize hello 模型，並評估驗證組 （線性迴歸） 上。

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE hello ESTIMATOR FUNCTION: `hello LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE hello PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET), AND THEN hello SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


**輸出：**

測試 R-sqr：0.6226484708501209

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a>使用交叉驗證和超參數牽涉最佳化 hello 二元分類模型
本節說明如何 toooptimize 二元分類模型使用交叉驗證和超參數掃掠。 這會使用 hello Spark ML`CrossValidator`函式。

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS tooUSE WITH hello TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE hello ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE hello PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY hello NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE hello TRAIN/TEST VALIDATION SPLIT (75% IN hello TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN hello TRAIN VALIDATION SPLIT AND CHOOSE hello BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON hello TEST DATA BY USING hello MODEL WITH hello COMBINATION OF PARAMETERS THAT PERFORMS hello BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE hello TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


**輸出：**

時間 toorun hello 資料格： 33 秒。

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a>使用自訂交叉驗證 」 和 「 參數掃掠的程式碼最佳化 hello 線性迴歸模型
接下來，使用自訂程式碼、 最佳化 hello 模型，並使用最高精確度的 hello 準則來識別 hello 最佳模型參數。 接著，建立 hello 最終模型、 評估 hello 模型測試資料和 Blob 儲存體中儲存 hello 模型。 最後，載入 hello 模型、 評分測試資料和評估精確度。

    # RECORD hello START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE hello PARAMETER GRID AND hello NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY hello NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
    val categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    var maxDepth = -1
    var numTrees = -1
    var param = ""
    var paramval = -1
    var validateLB = -1.0
    var validateUB = -1.0
    val h = 1.0 / nFolds;
    val RMSE  = Array.fill(numModels)(0.0)

    # CREATE K-FOLDS
    val splits = MLUtils.kFold(indexedTRAINbinary, numFolds = nFolds, seed=1234)


    # LOOP THROUGH K-FOLDS AND hello PARAMETER GRID tooGET AND IDENTIFY hello BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 too(nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 too(numModels-1)) {
            for (nParams <- 0 too(numParamsinGrid-1)) {
                param = paramGrid(nParamSets).toSeq(nParams).param.toString.split("__")(1)
                paramval = paramGrid(nParamSets).toSeq(nParams).value.toString.toInt
                if (param == "maxDepth") {maxDepth = paramval}
                if (param == "numTrees") {numTrees = paramval}
            }
            val rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=numTrees, maxDepth=maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)
            val labelAndPreds = validationLabPt.map { point =>
                                                     val prediction = rfModel.predict(point.features)
                                                     ( prediction, point.label )
                                                    }
            val validMetrics = new RegressionMetrics(labelAndPreds)
            val rmse = validMetrics.rootMeanSquaredError
            RMSE(nParamSets) += rmse
        }
        validationLabPt.unpersist();
        trainCVLabPt.unpersist();
    }
    val minRMSEindex = RMSE.indexOf(RMSE.min)

    # GET hello BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 too(numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE hello BEST MODEL WITH hello BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE hello BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON hello TRAINING SET WITH hello BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET hello TIME tooRUN hello CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken toorun hello above cell: " + elapsedtime + " seconds.");


    # LOAD hello MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST hello MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


**輸出：**

時間 toorun hello 資料格： 61 秒。

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a>透過 Scala 自動取用 Spark 建置的機器學習模型
如需這些主題會逐步引導您完成組成 hello 資料科學程序，在 Azure 中的 hello 工作的概觀，請參閱[資料科學的小組流程](http://aka.ms/datascienceprocess)。

[小組資料科學程序的逐步解說](data-science-process-walkthroughs.md)描述其他端對端逐步解說示範如何針對特定案例的 hello 小組資料科學程序中的 hello 步驟。 hello 逐步解說也說明如何 toocombine 雲端和內部部署工具和服務至工作流程或管線 toocreate 智慧型應用程式。

[評分 Spark 建立機器學習模型](machine-learning-data-science-spark-model-consumption.md)示範 toouse Scala 程式碼 tooautomatically 如何載入及內建的 Spark，儲存在 Azure Blob 儲存體的機器學習模型評分新資料集。 您可以遵循 hello 指示，提供，並只將 hello Python 程式碼取代 Scala 自動化耗用量的這篇文章中的程式碼。

