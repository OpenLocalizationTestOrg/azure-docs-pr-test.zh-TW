---
title: "aaaAdvanced 資料瀏覽和模型使用 Spark |Microsoft 文件"
description: "使用 HDInsight Spark toodo 資料瀏覽和定型二元分類和迴歸模型使用交叉驗證和 hyperparameter 最佳化。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: f90d9a80-4eaf-437b-a914-23514390cd60
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 055c342857fd732633cec9810de69cee61db973d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a>使用 Spark 進階資料探索和模型化
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

本逐步解說會使用 HDInsight Spark toodo 資料瀏覽及定型二元分類和迴歸模型使用交叉驗證和範例的 hello NYC hyperparameter 最佳化計程車路線再見 2013年資料集。 它將引導您完成 hello 步驟的 hello[資料科學程序](http://aka.ms/datascienceprocess)、 端對端，使用 HDInsight Spark 叢集以進行處理和 Azure blob toostore hello 資料和 hello 模型。 hello 程序探索和視覺化資料從 Azure 儲存體 Blob，並準備 hello 資料 toobuild 預測模型。 Python 已使用的 toocode hello 方案和 tooshow hello 相關繪圖。 這些模型是使用 hello Spark MLlib toolkit toodo 二元分類和迴歸模型工作的組建。 

* hello**二元分類**工作是 toopredict 不論是否在提示支付 hello 路線。 
* hello**迴歸**工作是根據其他提示功能 hello 提示 toopredict hello 數量。 

hello 模型步驟也包含程式碼示範如何 tootrain，評估並儲存每種模型類型。 hello 主題涵蓋一些 hello 相同地面為 hello[資料探索和模型使用 Spark](machine-learning-data-science-spark-data-exploration-modeling.md)主題。 但是，它一個 「 進階 」，它也與 hyperparameter 清除 tootrain 以最佳方式精確的分類和迴歸模型使用交叉驗證。 

**交叉驗證 (CV)**是評估如何在一組已知的資料上定型模型一般化所在它尚未定型資料集 toopredicting hello 功能的技術。  這裡使用的一般實作是 toodivide 成 K 摺疊的資料集，並再 hello 中定型模型，只留下其中一個 hello 摺疊所有以循環配置資源方式。 評估 hello 模型 tooprediction 經過測試，在此模型中未使用的摺疊 tootrain hello hello 獨立的資料集時，精確地 hello 能力。

**Hyperparameter 最佳化**hello 問題的選擇通常會有 hello 目標最佳化 hello 演算法的效能，在獨立的資料集上的量值的學習演算法的超集。 **超**hello 模型定型程序之外，必須指定的值。 假設這些值可能會影響 hello 彈性及 hello 模型的精確度。 決策樹有超參數，例如例如 hello 預期深度和 hello 樹狀目錄中的分葉數目。 支援向量機器 (SVM) 需要設定分類誤判損失詞彙。 

這裡使用的常見方式 tooperform hyperparameter 最佳化是方格搜尋，或**參數掃掠**。 這包含學習演算法執行徹底搜尋透過 hello 值指定的 hello hyperparameter 空間的子集。 交叉驗證可以提供的效能度量 toosort 出 hello 所 hello 方格搜尋演算法產生最佳的結果。 CV 搭配 hyperparameter 審慎有助於限制問題，例如使 hello 模型會保留 hello 容量 tooapply toohello 一般的資料集從哪些 hello 擷取定型資料，過度配適模型 tootraining 資料。

我們使用 hello 模型包括羅吉斯和線性迴歸、 隨機樹系和梯度促進式樹狀結構：

* [線性迴歸與 SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD)的線性迴歸模型，會使用隨機梯度下降 (SGD) 的方法和最佳化和功能的縮放比例 toopredict hello 提示數量付費。 
* [羅吉斯迴歸與 LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS)或 「 logit"迴歸是一種迴歸模型，hello 相依變數是類別 toodo 資料分類時才能使用。 LBFGS 是記憶體的 odd Newton 最佳化演算法的近似於使用電腦數量有限的 hello Broyden – Fletcher – Goldfarb – Shanno (BFGS) 演算法和可廣泛用於機器學習。
* [隨機樹系](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 是整體的決策樹。  結合許多決策樹 tooreduce hello 的風險過度配適。 隨機樹系用於迴歸和分類和可以處理類別的功能，可以擴充 toohello 多級分類設定。 它們不需要功能縮放比例和都能 toocapture 非線性和功能互動。 隨機樹系是其中一種 hello 可以最順利機器學習的分類和迴歸模型。
* [漸層停駐推進式決策樹](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) 是整體的決策樹。 GBTs 定型決策樹反覆 toominimize 損失函數。 GBTs 用於迴歸和分類和可以處理類別的功能，不需要調整功能，而是可以 toocapture 非線性互動的功能。 它們也可用於多類別分類設定。

模型使用 CV 和 Hyperparameter 範例會顯示 hello 二元分類問題掃掠。 （不含參數掃掠） 的簡單範例會顯示 hello 主要主題中的迴歸工作。 但也顯示 hello 附錄中使用參數掃掠隨機樹系迴歸，線性迴歸和 CV 使用彈性的網路驗證。 hello**彈性 net**是正則化的迴歸方法的調整線性迴歸模型，以線性方式結合 hello L1 與 L2 度量處罰下 hello[套索](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29)和[立體浮凸](https://en.wikipedia.org/wiki/Tikhonov_regularization)方法。   

> [!NOTE]
> 雖然 hello Spark MLlib toolkit 設計的 toowork 大型資料集，是此處為了方便起見使用相對較小的範例 (使用 170 K 資料列，約 0.1%的 hello 原始 NYC 資料集 ~ 30 Mb)。 在 HDInsight 叢集上具有 2 個背景工作節點，有效率地 （在約 10 分鐘） 執行此處指定的 hello 練習。 hello 相同程式碼，稍加修改，可以使用的 tooprocess 較大資料集，以適當的修改快取記憶體中的資料和變更 hello 叢集大小。
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a>設定：Spark 叢集和 Notebook
此逐步解說所提供的設定步驟和程式碼適用於使用 HDInsight Spark 1.6。 不過 Jupyter Notebook 可供 HDInsight Spark 1.6 版和 Spark 2.0 叢集兩者使用。 Hello 中提供的 hello 筆記本與連結 toothem 描述[Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello GitHub 儲存機制包含它們。 此外，hello 程式碼及連結的 hello 筆記本為泛型，應該在任何 Spark 叢集上運作。 如果您未使用 HDInsight Spark，hello 叢集中設定和管理步驟可能稍有不同於這裡所顯示。 為了方便起見，以下是 hello 的 hello 連結 toohello Jupyter 筆記本 Spark 1.6 版和 2.0 toobe Jupyter 筆記本伺服器 hello pyspark 核心中執行：

### <a name="spark-16-notebooks"></a>Spark 1.6 Notebook

[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)：包含Notebook #1 中的主題，以及使用超參數微調和交叉驗證的模型開發。

### <a name="spark-20-notebooks"></a>Spark 2.0 Notebook

[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)： 這個檔案提供如何 tooperform 資料瀏覽、 建立模型及計分 Spark 2.0 叢集資訊。

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a>安裝程式： 儲存位置、 程式庫，與 hello 預設 Spark 內容
Spark 是無法 tooread 」 和 「 寫入 tooAzure (也稱為 WASB) 的儲存體 Blob。 因此，任何現有的資料儲存於該處可處理使用的 Spark，hello 結果儲存一次在 WASB。

hello 路徑需要正確地指定 toobe toosave 模型或 WASB 中的檔案。 hello 預設容器附加 toohello Spark 叢集，可以使用來參考以開頭的路徑:"wasb: / /"。 其他位置由「wasb://」參考。

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a>在 WASB 中設定儲存位置的目錄路徑
hello 下列程式碼範例指定 hello 位置 hello 資料 toobe 讀取，並儲存 hello hello 模型儲存體目錄 toowhich hello 模型輸出路徑：

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

**輸出**

datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)

### <a name="import-libraries"></a>匯入程式庫
匯入必要的程式庫，以下列程式碼的 hello:

    # LOAD PYSPARK LIBRARIES
    import pyspark
    from pyspark import SparkConf
    from pyspark import SparkContext
    from pyspark.sql import SQLContext
    import matplotlib
    import matplotlib.pyplot as plt
    from pyspark.sql import Row
    from pyspark.sql.functions import UserDefinedFunction
    from pyspark.sql.types import *
    import atexit
    from numpy import array
    import numpy as np
    import datetime


### <a name="preset-spark-context-and-pyspark-magics"></a>預設 Spark 內容及 PySpark magic
所提供的 Jupyter 筆記本 hello PySpark 核心有預設的內容。 因此您不需要 tooset hello Spark 或登錄區內容明確之前您開始使用您所開發的 hello 應用程式。 依預設會將這些內容提供給您使用。 這些內容包括：

* sc - 代表 Spark 
* sqlContext - 代表 Hive

hello PySpark 核心提供一些預先定義 「 我們"，這是特殊的命令，您可以呼叫具有 %%。 在這些程式碼範例中，就使用了兩個此類型的命令。

* **%%本機**指定 hello 下來幾行中的程式碼是 toobe 以本機方式執行。 程式碼必須是有效的 Python 程式碼。
* **%%sql o <variable name>** 執行針對 hello sqlContext Hive 查詢。 如果傳遞 hello-o 參數，則 hello hello 查詢結果會持續保留在 hello %%熊資料框架的本機 Python 環境。

針對 Jupyter 筆記本和預先定義的 hello hello 核心上的詳細資訊 」 magics 」，它們提供，請參閱[HDInsight 上的叢集與 HDInsight Spark Linux Jupyter 筆記本的可用的核心](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)。

## <a name="data-ingestion-from-public-blob"></a>來自公用 Blob 的資料擷取：
hello hello 資料科學程序的第一個步驟是 tooingest hello 資料 toobe 分析從來源到您的資料探索和模型環境的所在位置。 這種環境在本逐步解說中是 Spark。 本節包含 hello 程式碼 toocomplete 一系列的工作：

* 內嵌 hello 資料範例 toobe 模型化
* 讀取輸入資料集中 hello （儲存為.tsv 檔案）
* 格式和全新 hello 資料
* 建立並快取記憶體中的物件 (RDD 或資料框架)
* 將它註冊為 SQL 內容中的暫存資料表。

擷取資料的 hello 程式碼如下。

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    schema_string = taxi_train_file.first()
    fields = [StructField(field_name, StringType(), True) for field_name in schema_string.split('\t')]
    fields[7].dataType = IntegerType() #Pickup hour
    fields[8].dataType = IntegerType() # Pickup week
    fields[9].dataType = IntegerType() # Weekday
    fields[10].dataType = IntegerType() # Passenger count
    fields[11].dataType = FloatType() # Trip time in secs
    fields[12].dataType = FloatType() # Trip distance
    fields[19].dataType = FloatType() # Fare amount
    fields[20].dataType = FloatType() # Surcharge
    fields[21].dataType = FloatType() # Mta_tax
    fields[22].dataType = FloatType() # Tip amount
    fields[23].dataType = FloatType() # Tolls amount
    fields[24].dataType = FloatType() # Total amount
    fields[25].dataType = IntegerType() # Tipped or not
    fields[26].dataType = IntegerType() # Tip class
    taxi_schema = StructType(fields)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_header = taxi_train_file.filter(lambda l: "medallion" in l)
    taxi_temp = taxi_train_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))


    # CREATE DATA FRAME
    taxi_train_df = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_train_cleaned = taxi_train_df.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES hello DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**輸出**

時間 tooexecute 儲存格上方： 276.62 秒

## <a name="data-exploration--visualization"></a>資料探索和虛擬化
一旦 hello 資料已放入 Spark，hello hello 資料科學程序中的下一個步驟是 toogain hello 資料探索和視覺效果的更深入了解。 在本節中，我們會檢查 hello 計程車資料使用 SQL 查詢和繪圖 hello 目標變數與潛在功能視覺化進行檢查。 具體來說，我們會繪製旅客計數計程車往返、 hello 頻率的提示數量和如何提示因付款金額和型別中的 hello 頻率。

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>繪製旅客計數頻率的計程車行程 hello 範例中的長條圖
這個程式碼和後續的程式碼片段，請使用 SQL magic tooquery hello 範例資料和本機 magic tooplot hello 資料。

* **SQL magic (`%%sql`)** hello HDInsight PySpark 核心支援 hello sqlContext 輕鬆內嵌 HiveQL 查詢。 hello (-o VARIABLE_NAME) 引數會保存 hello 的 hello SQL 查詢的輸出為熊資料框架 hello Jupyter 伺服器上。 這表示在 hello 本機模式中使用。
* hello  **`%%local` magic**是 hello Jupyter 伺服器，也就是 hello 的 hello HDInsight 叢集的前端節點上在本機使用 toorun 程式碼。 通常，您會使用`%%local`magic 之後 hello `%%sql -o` magic 是使用的 toorun 查詢。 hello-o 參數會保存在本機 hello SQL 查詢的 hello 輸出。 然後 hello `%%local` magic 觸發程序 hello 下一組程式碼片段 toorun 在本機憑藉已在本機保存的 hello 輸出的 hello SQL 查詢。 執行 hello 程式碼之後，會自動視覺化 hello 輸出。

此查詢會擷取 hello 往返依旅客計數。 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


此程式碼建立 hello 查詢輸出的本機資料框架，並繪製 hello 資料。 hello `%%local` magic 建立本機資料框架， `sqlResults`，可以用來與 matplotlib 繪製。 

> [!NOTE]
> 在本逐步解說中，會多次使用此 PySpark magic。 如果 hello 資料量很大，您應該取樣 toocreate 本機記憶體內可容納資料框架。
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

以下是 hello 程式碼 tooplot hello 往返旅客計數

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    # PLOT PASSENGER NUMBER VS TRIP COUNTS
    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**輸出**

![按乘客計數排列的車程頻率](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

您可以在多種不同類型的視覺效果 （資料表、 圓形圖、 線條、 區域或列） 之間使用選取 hello**類型**hello 筆記本中的功能表按鈕。 以下顯示 hello 橫條圖。

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>繪製小費金額，和小費金額如何隨乘客計數和費用金額變化的長條圖。
使用 SQL 查詢 toosample 資料...

    # SQL SQUERY
    %%sql -q -o sqlResults
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train 
        WHERE passenger_count > 0 
        AND passenger_count < 7
        AND fare_amount > 0 
        AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 
        AND tip_amount < 25


此資料格，程式碼會使用 hello SQL 查詢 toocreate 三種繪圖 hello 資料。

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline

    # TIP BY PAYMENT TYPE AND PASSENGER COUNT
    ax1 = resultsPDDF[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = resultsPDDF.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount ($) by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = resultsPDDF.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(resultsPDDF.passenger_count))
    ax.set_title('Tip amount by Fare amount ($)')
    ax.set_xlabel('Fare Amount')
    ax.set_ylabel('Tip Amount')
    plt.axis([-2, 120, -2, 30])
    plt.show()


**輸出：** 

![小費金額分佈](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![按乘客計數排列的小費金額](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![按費用金額排列的小費金額](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>模型化的功能工程、轉換和資料準備
本章節描述，並提供用於 ML 模型使用 tooprepare 資料的程序的 hello 程式碼。 它會顯示影響 toodo hello 下列工作：

* 將小時分割到流量時間分類區以建立新功能
* 索引和 on-hot 編碼分類功能
* 建立輸入到 ML 函式的標示點物件
* 建立 hello 資料的隨機子取樣和分割成定型集和測試集
* 調整功能
* 快取記憶體中的物件

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a>將流量時間分割到分類區以建立新功能
此程式碼顯示如何 toocreate 的新功能，藉由分割流量時間分組然後 toocache hello 產生資料框架，在記憶體中的方式。 快取，會導致 tooimproved 執行時間，彈性分散式資料集 (RDDs) 和資料框架會重複使用。 因此，我們會在逐步解說中的幾個階段快取 RDD 和資料框架。

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_train 
    """
    taxi_df_train_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    # hello .COUNT() GOES THROUGH hello ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES hello COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

**輸出**

126050

### <a name="index-and-one-hot-encode-categorical-features"></a>索引和 one-hot 編碼分類功能
此區段會顯示如何 tooindex 或編碼的輸入 hello 模型函式的類別特徵。 hello 模型和預測的 MLlib 函式需要與類別的輸入資料的功能會編製索引，或編碼先前 toouse。 

視 hello 模型而定，您需要 tooindex 或將它們以不同方式編碼。 例如，羅吉斯和線性迴歸模型需要一個熱門的編碼，其中，具有三個類別的功能，例如才可擴充到三個特徵資料行，與每個包含 0 或 1，視所觀察 hello 分類。 提供 MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder)函式 toodo 一個熱編碼方式。 此編碼器將對應的二進位的向量，使用最多為單一其中一個值的標籤索引 tooa 資料行的資料行。 這種編碼方式可讓演算法所預期的數字的重要的功能，例如羅吉斯迴歸，套用 toobe toocategorical 功能。

以下是 hello tooindex 程式碼，並將編碼類別特徵：

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is hello cleaned one from above
    indexed = model.transform(taxi_df_train_with_newFeatures)
    encoder = OneHotEncoder(dropLast=False, inputCol="vendorIndex", outputCol="vendorVec")
    encoded1 = encoder.transform(indexed)

    # INDEX AND ENCODE RATE_CODE
    stringIndexer = StringIndexer(inputCol="rate_code", outputCol="rateIndex")
    model = stringIndexer.fit(encoded1)
    indexed = model.transform(encoded1)
    encoder = OneHotEncoder(dropLast=False, inputCol="rateIndex", outputCol="rateVec")
    encoded2 = encoder.transform(indexed)

    # INDEX AND ENCODE PAYMENT_TYPE
    stringIndexer = StringIndexer(inputCol="payment_type", outputCol="paymentIndex")
    model = stringIndexer.fit(encoded2)
    indexed = model.transform(encoded2)
    encoder = OneHotEncoder(dropLast=False, inputCol="paymentIndex", outputCol="paymentVec")
    encoded3 = encoder.transform(indexed)

    # INDEX AND TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**輸出**

時間 tooexecute 儲存格上方： 3.14 秒

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>建立輸入到 ML 函式的標示點物件
此章節包含程式碼，說明如何為標記的點資料 tooindex 類別的文字資料類型以及如何 tooencode 它。 這準備好使用 toobe tootrain 和測試 MLlib 羅吉斯迴歸和其他分類模型。 標示點物件是彈性分散式資料集 (RDD)，其格式化成適合 MLlib 中大部分的 ML 演算法的輸入資料。 [標示點](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 是本機向量 (密集或疏鬆)，與標籤/回應相關聯。

以下是 hello tooindex 程式碼，並將編碼的二元分類的文字功能。

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.pickup_hour, line.weekday,
                             line.passenger_count, line.trip_time_in_secs, line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                   line.vendorVec.toArray(), line.rateVec.toArray(), line.paymentVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tipped, features)
        return  labPt


以下是 hello 程式碼的線性迴歸分析的 tooencode 和索引類別文字功能。

    # FUNCTIONS FOR REGRESSION WITH TIP AMOUNT AS TARGET VARIABLE

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        labPt = LabeledPoint(line.tip_amount, features)
        return  labPt


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a>建立 hello 資料的隨機子取樣和分割成定型集和測試集
此程式碼會建立隨機取樣的 hello 資料 （在這裡使用 25%）。 雖然您不需要這個到期 toohello 大小的 hello 資料集的範例，我們將示範如何您也可以取樣 hello 資料。 您就知道如何 toouse 它視您的問題。 在大型範例中，如此可在訓練模型時節省大量時間。 接下來我們將 hello 範例分割成定型一部分 （這裡 75%) 和測試的一部分 （這裡 25%) toouse 分類和迴歸模型中。

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    from pyspark.sql.functions import rand

    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST, WITH A RANDOM COLUMN ADDED FOR DOING CV (SHOWN LATER)
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

    # CACHE TRAIN AND TEST DATA
    trainData.cache()
    testData.cache()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary = trainData.map(parseRowIndexingBinary)
    indexedTESTbinary = testData.map(parseRowIndexingBinary)
    oneHotTRAINbinary = trainData.map(parseRowOneHotBinary)
    oneHotTESTbinary = testData.map(parseRowOneHotBinary)

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg = trainData.map(parseRowIndexingRegression)
    indexedTESTreg = testData.map(parseRowIndexingRegression)
    oneHotTRAINreg = trainData.map(parseRowOneHotRegression)
    oneHotTESTreg = testData.map(parseRowOneHotRegression)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**輸出**

時間 tooexecute 儲存格上方： 0.31 秒

### <a name="feature-scaling"></a>調整功能
調整功能，也稱為資料正規化，以確保，功能與廣泛分散的值未授與過多權衡 hello 目標函式。 hello 功能縮放比例的程式碼會使用 hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello 功能 toounit 變異數。 這是由 MLlib 提供，用於使用隨機梯度下降 (SGD) 的線性迴歸。 SGD 為訓練廣泛的其他機器學習模型的常用演算法，例如正則化迴歸或支援向量機器 (SVM)。   

> [!TIP]
> 我們發現 hello LinearRegressionWithSGD 演算法 toobe 機密 toofeature 縮放比例。   
> 
> 

以下是用於正則化的 hello 線性 SGD 演算法 hello 程式碼 tooscale 變數。

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils

    # SCALE VARIABLES FOR REGULARIZED LINEAR SGD ALGORITHM
    label = oneHotTRAINreg.map(lambda x: x.label)
    features = oneHotTRAINreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTRAINregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    label = oneHotTESTreg.map(lambda x: x.label)
    features = oneHotTESTreg.map(lambda x: x.features)
    scaler = StandardScaler(withMean=False, withStd=True).fit(features)
    dataTMP = label.zip(scaler.transform(features.map(lambda x: Vectors.dense(x.toArray()))))
    oneHotTESTregScaled = dataTMP.map(lambda x: LabeledPoint(x[0], x[1]))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**輸出**

時間 tooexecute 儲存格上方： 11.67 秒

### <a name="cache-objects-in-memory"></a>快取記憶體中的物件
caching hello 輸入的資料框架物件會用於迴歸、 分類，以及縮放功能，可以降低 hello 時間進行定型和測試的 ML 演算法。

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.cache()
    indexedTESTbinary.cache()
    oneHotTRAINbinary.cache()
    oneHotTESTbinary.cache()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.cache()
    indexedTESTreg.cache()
    oneHotTRAINreg.cache()
    oneHotTESTreg.cache()

    # SCALED FEATURES
    oneHotTRAINregScaled.cache()
    oneHotTESTregScaled.cache()

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**輸出** 

時間 tooexecute 儲存格上方： 0.13 秒

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>使用二進位分類模型來預測是否支付小費
本節說明如何使用三個模型的預測的 hello 二元分類工作在提示支付計程車路線。 呈現的 hello 模型如下：

* 羅吉斯迴歸 
* 隨機樹系
* 漸層停駐提升樹狀結構

每個模型建置程式碼區段會分成幾個步驟︰ 

1. **模型定型** 資料
2. **模型評估** 
3. **儲存模型** 

我們會示範如何 toodo 交叉驗證 (CV) 與參數掃掠兩種方式：

1. 使用**泛型**自訂程式碼可以套用的 tooany 演算法 MLlib 和 tooany 參數中設定的演算法中。 
2. 使用 hello **pySpark CrossValidator 管線函式**。 請注意，CrossValidator 對 Spark 1.5.0 有幾項限制︰ 
   
   * 管線模型無法儲存/保存供未來取用。
   * 無法用於模型中的每個參數。
   * 無法用於每個 MLlib 演算法。

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a>交叉驗證和 hyperparameter 掃掠搭配 hello 羅吉斯迴歸演算法使用二元分類的泛型
本節中的 hello 程式碼顯示如何 tootrain，評估及儲存與羅吉斯迴歸模型[LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm)的預測是否付費的行程 hello NYC 計程車行程及價位資料集中的提示。 hello 模型已定型使用交叉驗證 (CV) 和實作自訂程式碼可以套用的學習演算法中 MLlib hello tooany hyperparameter 掃掠。   

> [!NOTE]
> hello 執行此自訂的 CV 程式碼可能需要幾分鐘的時間。
> 
> 

**使用 CV 和 hyperparameter 掃掠 hello 羅吉斯迴歸模型定型**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from pyspark.mllib.evaluation import BinaryClassificationMetrics

    # CREATE PARAMETER GRID FOR LOGISTIC REGRESSION PARAMETER SWEEP
    from sklearn.grid_search import ParameterGrid
    grid = [{'regParam': [0.01, 0.1], 'iterations': [5, 10], 'regType': ["l1", "l2"], 'tolerance': [1e-3, 1e-4]}]
    paramGrid = list(ParameterGrid(grid))
    numModels = len(paramGrid)

    # SET NUM FOLDS AND NUM PARAMETER SETS tooSWEEP ON
    nFolds = 3;
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    # BEGIN CV WITH PARAMETER SWEEP
    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create LabeledPoints from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowOneHotBinary)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowOneHotBinary)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            regt = paramGrid[j]['regType']
            regp = paramGrid[j]['regParam']
            iters = paramGrid[j]['iterations']
            tol = paramGrid[j]['tolerance']
            # Train logistic regression model with hypermarameter set
            model = LogisticRegressionWithLBFGS.train(trainCVLabPt, regType=regt, iterations=iters,  
                                                      regParam=regp, tolerance = tol, intercept=True)
            predictionAndLabels = validationLabPt.map(lambda lp: (float(model.predict(lp.features)), lp.label))
            # Use ROC-AUC as accuracy metrics
            validMetrics = BinaryClassificationMetrics(predictionAndLabels)
            metric = validMetrics.areaUnderROC
            metricSum[j] += metric

    avgAcc = metricSum / nFolds;
    bestParam = paramGrid[np.argmax(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    # TRAIN ON FULL TRAIING SET USING BEST PARAMETERS FROM CV/PARAMETER SWEEP
    logitBest = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, regType=bestParam['regType'], 
                                                  iterations=bestParam['iterations'], 
                                                  regParam=bestParam['regParam'], tolerance = bestParam['tolerance'], 
                                                  intercept=True)


    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**輸出**

係數：[0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]

截距：-0.0111216486893

時間 tooexecute 儲存格上方： 14.43 秒

**評估具有標準度量的 hello 二元分類模型**

本節中的 hello 程式碼會示範如何 tooevaluate 羅吉斯迴歸模型針對測試資料集，包括 hello ROC 曲線的繪圖。

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT LIBRARIES
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # PREDICT ON TEST DATA WITH BEST/FINAL MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitBest.predict(lp.features)), lp.label))

    # INSTANTIATE METRICS OBJECT
    metrics = BinaryClassificationMetrics(predictionAndLabels)

    # AREA UNDER PRECISION-RECALL CURVE
    print("Area under PR = %s" % metrics.areaUnderPR)

    # AREA UNDER ROC CURVE
    print("Area under ROC = %s" % metrics.areaUnderROC)
    metrics = MulticlassMetrics(predictionAndLabels)

    # OVERALL STATISTICS
    precision = metrics.precision()
    recall = metrics.recall()
    f1Score = metrics.fMeasure()
    print("Summary Stats")
    print("Precision = %s" % precision)
    print("Recall = %s" % recall)
    print("F1 Score = %s" % f1Score)

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitBest.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**輸出**

PR 下的領域 = 0.985336538462

ROC 下的領域 = 0.983383274312

摘要狀態

精確度 = 0.984174341679

回收 = 0.984174341679

F1 分數 = 0.984174341679

時間 tooexecute 儲存格上方： 2.67 秒

**繪製 hello ROC 曲線。**

hello *predictionAndLabelsDF*註冊為資料表， *tmp_results*，在 hello 上一個儲存格。 *tmp_results*可以使用的 toodo 查詢和 hello sqlResults 資料框架來繪製至輸出結果。 Hello 程式碼如下。

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


以下是 hello 程式碼 toomake 預測及繪圖 hello ROC 曲線。

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES                              
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    #PREDICTIONS
    predictions_pddf = sqlResults.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVES
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


**輸出**

![泛型方法的羅吉斯迴歸 ROC 曲線](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

**blob 中供未來取用的保留模型**

本節中的 hello 程式碼會示範如何 toosave hello 羅吉斯迴歸模型的耗用量。

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    # PERSIST MODEL
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;

    logitBest.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";


**輸出**

時間 tooexecute 儲存格上方： 34.57 秒

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a>搭配使用 MLlib 的 CrossValidator 管線函式與 LogisticRegression (彈性迴歸) 模型
本節中的 hello 程式碼顯示如何 tootrain，評估及儲存與羅吉斯迴歸模型[LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm)的預測是否付費的行程 hello NYC 計程車行程及價位資料集中的提示。 hello 模型使用交叉驗證 (CV) 來定型和 hyperparameter 掃掠實作以 hello MLlib CrossValidator 管線函式的 CV 參數掃掠。   

> [!NOTE]
> hello 執行此 MLlib CV 程式碼可能需要幾分鐘的時間。
> 
> 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.classification import LogisticRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import BinaryClassificationEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder
    from sklearn.metrics import roc_curve,auc

    # DEFINE ALGORITHM / MODEL
    lr = LogisticRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build()

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=BinaryClassificationEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA-FRAME: THIS DOES NOT RUN ON RDDs
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINbinary, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    ## PREDICT AND EVALUATE ON TEST DATA-SET

    # USE TEST DATASET FOR PREDICTION
    testDataFrame = sqlContext.createDataFrame(oneHotTESTbinary, ["features", "label"])
    test_predictions = cv_model.transform(testDataFrame)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**輸出**

時間 tooexecute 儲存格上方： 107.98 秒

**繪製 hello ROC 曲線。**

hello *predictionAndLabelsDF*註冊為資料表， *tmp_results*，在 hello 上一個儲存格。 *tmp_results*可以使用的 toodo 查詢和 hello sqlResults 資料框架來繪製至輸出結果。 Hello 程式碼如下。

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

以下是 hello 程式碼 tooplot hello ROC 曲線。

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES 
    %%local
    from sklearn.metrics import roc_curve,auc

    # ROC CURVE
    prob = [x["values"][1] for x in sqlResults["probability"]]
    fpr, tpr, thresholds = roc_curve(sqlResults['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    #PLOT
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


**輸出**

![使用 MLlib 的 CrossValidator 的羅吉斯迴歸 ROC 曲線](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a>隨機樹系分類
本節中的 hello 程式碼會示範如何 tootrain，評估及儲存預測提示支付路線 hello NYC 計程車行程及價位資料集內的隨機樹系迴歸。

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # TRAIN RANDOMFOREST MODEL
    rfModel = RandomForest.trainClassifier(indexedTRAINbinary, numClasses=2, 
                                           categoricalFeaturesInfo=categoricalFeaturesInfo,
                                           numTrees=25, featureSubsetStrategy="auto",
                                           impurity='gini', maxDepth=5, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = rfModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp;
    dirfilename = modelDir + rfclassificationfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**輸出**

ROC 下的領域 = 0.985336538462

時間 tooexecute 儲存格上方： 26.72 秒

### <a name="gradient-boosting-trees-classification"></a>漸層停駐提升樹狀結構類別
本節中的 hello 程式碼會示範 tootrain，如何評估及儲存預測提示支付 hello NYC 計程車行程及價位資料集中的行程的漸層停駐提升樹模型。

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # Area under ROC curve
    metrics = BinaryClassificationMetrics(predictionAndLabels)
    print("Area under ROC = %s" % metrics.areaUnderROC)

    # PERSIST MODEL IN A BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp;
    dirfilename = modelDir + btclassificationfilename;

    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**輸出**

ROC 下的領域 = 0.985336538462

時間 tooexecute 儲存格上方： 28.13 秒

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a>使用迴歸模型預測小費金額 (非使用 CV)
本節說明如何使用三個模型 hello 迴歸工作： 預測支付其他提示功能為基礎的計程車行程 hello 提示數量。 呈現的 hello 模型如下：

* 正規化線性迴歸
* 隨機樹系
* 漸層停駐提升樹狀結構

這些模型是以 hello 簡介所述。 每個模型建置程式碼區段會分成幾個步驟︰ 

1. **模型定型** 資料
2. **模型評估** 
3. **儲存模型**    

> AZURE 的附註： 交叉驗證未搭配使用 hello 三種迴歸模型在本節中，因為這顯示 hello 羅吉斯迴歸模型的詳細資料。 範例顯示 hello 這個主題的 < 附錄中提供 toouse 與彈性 Net CV 線性迴歸的方式。
> 
> AZURE 的附註： 我們的經驗，可能有問題有 LinearRegressionWithSGD 模型的交集，參數必須 toobe 變更/最佳化仔細取得有效的模型。 調整變數對於聚合很有用。 Net 迴歸彈性，顯示在 hello 附錄 toothis 主題中，也可以代替 LinearRegressionWithSGD。
> 
> 

### <a name="linear-regression-with-sgd"></a>使用 SGD 的線性迴歸
hello 本節中的程式碼會示範如何 toouse 會縮放功能 tootrain 最佳化，使用隨機梯度下降 (SGD) 線性迴歸以及 tooscore，如何評估，並將 hello 模型儲存在 Azure Blob 儲存體 (WASB)。

> [!TIP]
> 在我們的經驗，可能有問題的 hello 交集的 LinearRegressionWithSGD 模型，而參數需要 toobe 變更/最佳化仔細取得有效的模型。 調整變數對於聚合很有用。
> 
> 

    # LINEAR REGRESSION WITH SGD 

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES tooTRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**輸出**

係數：[0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]

截距：0.854507624459

RMSE = 1.23485131376

R-sqr = 0.597963951127

時間 tooexecute 儲存格上方： 38.62 秒

### <a name="random-forest-regression"></a>隨機樹系迴歸
本節中的 hello 程式碼會示範如何 tootrain，評估及儲存預測 hello NYC 計程車路線資料的提示數量的隨機樹系模型。   

> [!NOTE]
> 交叉驗證參數掃掠使用自訂程式碼與 hello 附錄中提供。
> 
> 

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    # UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    # PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp;
    dirfilename = modelDir + rfregressionfilename;

    rfModel.save(sc, dirfilename);

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**輸出**

RMSE = 0.931981967875

R-sqr = 0.733445485802

時間 tooexecute 儲存格上方： 25.98 秒

### <a name="gradient-boosting-trees-regression"></a>漸層停駐提升樹狀結構迴歸
本節中的 hello 程式碼會示範 tootrain，如何評估及儲存預測 hello NYC 計程車路線資料的提示數量的漸層停駐提升樹模型。

**訓練及評估 **

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    # TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    # EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES
    test_predictions= sqlContext.createDataFrame(predictionAndLabels)
    test_predictions_pddf = test_predictions.toPandas()

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**輸出**

RMSE = 0.928172197114

R-sqr = 0.732680354389

時間 tooexecute 儲存格上方： 20.9 秒

**圖**

*tmp_results*註冊為 hello 前一個資料格集中的 Hive 資料表。 來自 hello 資料表的結果會輸出到 hello *sqlResults*來繪製資料框架。 以下是 hello 程式碼

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


以下是使用 hello Jupyter 伺服器 hello 程式碼 tooplot hello 資料。

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    import numpy as np

    # PLOT
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['_1'], sqlResults['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(sqlResults['_1'], fit[0] * sqlResults['_1'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 15])
    plt.show(ax)

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a>附錄︰使用交叉驗證與參數掃掠的額外迴歸工作
本附錄包含程式碼顯示如何使用線性迴歸和如何 toodo CV 參數掃掠隨機樹系迴歸中使用自訂程式碼的彈性 net toodo CV。

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a>針對線性迴歸使用彈性 net 進行交叉驗證
本節中的 hello 程式碼會示範 toodo 交叉驗證使用線性迴歸 net 彈性的方式，以及如何 tooevaluate hello 針對測試資料的模型。

    ###  CV USING ELASTIC NET FOR LINEAR REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.regression import LinearRegression
    from pyspark.ml import Pipeline
    from pyspark.ml.evaluation import RegressionEvaluator
    from pyspark.ml.tuning import CrossValidator, ParamGridBuilder

    # DEFINE ALGORITHM/MODEL
    lr = LinearRegression()

    # DEFINE GRID PARAMETERS
    paramGrid = ParamGridBuilder().addGrid(lr.regParam, (0.01, 0.1))\
                                  .addGrid(lr.maxIter, (5, 10))\
                                  .addGrid(lr.tol, (1e-4, 1e-5))\
                                  .addGrid(lr.elasticNetParam, (0.25,0.75))\
                                  .build() 

    # DEFINE PIPELINE 
    # SIMPLY hello MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT tooDATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses hello best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT tooDF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**輸出**

時間 tooexecute 儲存格上方： 161.21 秒

**使用 R-SQR 度量進行評估**

*tmp_results*註冊為 hello 前一個資料格集中的 Hive 資料表。 來自 hello 資料表的結果會輸出到 hello *sqlResults*來繪製資料框架。 以下是 hello 程式碼

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


以下是 hello 程式碼 toocalculate R sqr。

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


**輸出**

R-sqr = 0.619184907088

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a>針對隨機樹系迴歸使用自訂程式碼以參數掃掠進行交叉驗證。
本節中的 hello 程式碼會示範 toodo 參數掃掠隨機樹系迴歸中使用自訂程式碼使用交叉驗證的方式和 tooevaluate hello 模型測試資料的方式。

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    # GET ACCURARY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics
    from sklearn.grid_search import ParameterGrid

    ## CREATE PARAMETER GRID
    grid = [{'maxDepth': [5,10], 'numTrees': [25,50]}]
    paramGrid = list(ParameterGrid(grid))

    ## SPECIFY LEVELS OF CATEGORICAL VARIBLES
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    # SPECIFY NUMFOLDS AND ARRAY tooHOLD METRICS
    nFolds = 3;
    numModels = len(paramGrid)
    h = 1.0 / nFolds;
    metricSum = np.zeros(numModels);

    for i in range(nFolds):
        # Create training and x-validation sets
        validateLB = i * h
        validateUB = (i + 1) * h
        condition = (trainData["rand"] >= validateLB) & (trainData["rand"] < validateUB)
        validation = trainData.filter(condition)
        # Create labeled points from data-frames
        if i > 0:
            trainCVLabPt.unpersist()
            validationLabPt.unpersist()
        trainCV = trainData.filter(~condition)
        trainCVLabPt = trainCV.map(parseRowIndexingRegression)
        trainCVLabPt.cache()
        validationLabPt = validation.map(parseRowIndexingRegression)
        validationLabPt.cache()
        # For parameter sets compute metrics from x-validation
        for j in range(numModels):
            maxD = paramGrid[j]['maxDepth']
            numT = paramGrid[j]['numTrees']
            # Train logistic regression model with hypermarameter set
            rfModel = RandomForest.trainRegressor(trainCVLabPt, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=numT, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=maxD, maxBins=32)
            predictions = rfModel.predict(validationLabPt.map(lambda x: x.features))
            predictionAndLabels = validationLabPt.map(lambda lp: lp.label).zip(predictions)
            # Use ROC-AUC as accuracy metrics
            validMetrics = RegressionMetrics(predictionAndLabels)
            metric = validMetrics.rootMeanSquaredError
            metricSum[j] += metric

    avgAcc = metricSum/nFolds;
    bestParam = paramGrid[np.argmin(avgAcc)];

    # UNPERSIST OBJECTS
    trainCVLabPt.unpersist()
    validationLabPt.unpersist()

    ## TRAIN FINAL MODL WIHT BEST PARAMETERS
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=bestParam['numTrees'], featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=bestParam['maxDepth'], maxBins=32)

    # EVALUATE MODEL ON TEST DATA
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    #PRINT TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**輸出**

RMSE = 0.906972198262

R-sqr = 0.740751197012

時間 tooexecute 儲存格上方： 69.17 秒

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a>從記憶體清除物件並列印模型位置
使用`unpersist()`toodelete 物件在記憶體中快取。

    # UNPERSIST OBJECTS CACHED IN MEMORY

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()
    trainData.unpersist()
    trainData.unpersist()

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTRAINbinary.unpersist()
    indexedTESTbinary.unpersist()
    oneHotTRAINbinary.unpersist()
    oneHotTESTbinary.unpersist()

    # FOR REGRESSION TRAINING AND TESTING
    indexedTRAINreg.unpersist()
    indexedTESTreg.unpersist()
    oneHotTRAINreg.unpersist()
    oneHotTESTreg.unpersist()

    # SCALED FEATURES
    oneHotTRAINregScaled.unpersist()
    oneHotTESTregScaled.unpersist()


**輸出**

PythonRDD[122] at RDD at PythonRDD.scala: 43

* * 列印輸出路徑 toomodel 檔案 toobe hello 耗用量筆記本中使用。 * * tooconsume 和分數不受影響的資料集，您需要 toocopy 並將這些檔案名稱貼入 hello"耗用量筆記型電腦 」 中。

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**輸出**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"

## <a name="whats-next"></a>後續步驟
現在您已經以 hello Spark MlLib 建立迴歸和分類的模型，您就準備好 toolearn 如何 tooscore 和評估這些模型。

**模型耗用量：** toolearn 如何 tooscore 和評估建立本主題中的 hello 分類和迴歸模型，請參閱[分數及評估 Spark 建立機器學習模型](machine-learning-data-science-spark-model-consumption.md)。

