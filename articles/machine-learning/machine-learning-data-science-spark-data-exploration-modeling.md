---
title: "aaaData 瀏覽和模型使用 Spark |Microsoft 文件"
description: "Showcases hello 資料探索和模型化功能 hello Azure 上的 Spark MLlib 工具組。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b989b918-5ba5-4696-b8d0-76ae510a23f4
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: cf5cee4575053f5954b08ca659dfc39c53798371
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a>使用 Spark 資料探索和模型化
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

本逐步解說會使用 HDInsight Spark toodo 資料瀏覽和二進位的分類和迴歸模型上的 hello NYC 範例工作計程車路線再見 2013年資料集。  它將引導您完成 hello 步驟的 hello[資料科學程序](http://aka.ms/datascienceprocess)、 端對端，使用 HDInsight Spark 叢集以進行處理和 Azure blob toostore hello 資料和 hello 模型。 hello 程序探索和視覺化資料從 Azure 儲存體 Blob，並準備 hello 資料 toobuild 預測模型。 這些模型是使用 hello Spark MLlib toolkit toodo 二元分類和迴歸模型工作的組建。

* hello**二元分類**工作是 toopredict 不論是否在提示支付 hello 路線。 
* hello**迴歸**工作是根據其他提示功能 hello 提示 toopredict hello 數量。 

我們使用 hello 模型包括羅吉斯和線性迴歸、 隨機樹系和梯度促進式樹狀結構：

* [線性迴歸與 SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD)的線性迴歸模型，會使用隨機梯度下降 (SGD) 的方法和最佳化和功能的縮放比例 toopredict hello 提示數量付費。 
* [羅吉斯迴歸與 LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS)或 「 logit"迴歸是一種迴歸模型，hello 相依變數是類別 toodo 資料分類時才能使用。 LBFGS 是記憶體的 odd Newton 最佳化演算法的近似於使用電腦數量有限的 hello Broyden – Fletcher – Goldfarb – Shanno (BFGS) 演算法和可廣泛用於機器學習。
* [隨機樹系](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 是整體的決策樹。  結合許多決策樹 tooreduce hello 的風險過度配適。 隨機樹系用於迴歸和分類和可以處理類別的功能，可以擴充 toohello 多級分類設定。 它們不需要功能縮放比例和都能 toocapture 非線性和功能互動。 隨機樹系是其中一種 hello 可以最順利機器學習的分類和迴歸模型。
* [漸層停駐推進式決策樹](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) 是整體的決策樹。 GBTs 定型決策樹反覆 toominimize 損失函數。 GBTs 用於迴歸和分類和可以處理類別的功能，不需要調整功能，而是可以 toocapture 非線性互動的功能。 它們也可用於多類別分類設定。

hello 模型步驟也包含程式碼示範如何 tootrain，評估並儲存每種模型類型。 Python 已使用的 toocode hello 方案和 tooshow hello 相關繪圖。   

> [!NOTE]
> 雖然 hello Spark MLlib toolkit 設計的 toowork 大型資料集，是此處為了方便起見使用相對較小的範例 (使用 170 K 資料列，約 0.1%的 hello 原始 NYC 資料集 ~ 30 Mb)。 在 HDInsight 叢集上具有 2 個背景工作節點，有效率地 （在約 10 分鐘） 執行此處指定的 hello 練習。 hello 相同程式碼，稍加修改，可以使用的 tooprocess 較大資料集，以適當的修改快取記憶體中的資料和變更 hello 叢集大小。
> 
> 

## <a name="prerequisites"></a>必要條件
您需要 Azure 帳戶和 Spark 1.6 （或 Spark 2.0） HDInsight 叢集 toocomplete 本逐步解說。 請參閱 hello[概觀的資料科學使用 Azure HDInsight 上的 Spark](machine-learning-data-science-spark-overview.md)如需有關指示 toosatisfy 這些需求。 該主題也包含描述 hello NYC 2013 計程車這裡使用的資料以及 tooexecute 來自 Jupyter 筆記本 hello Spark 叢集上的程式碼的相關指示。 

## <a name="spark-clusters-and-notebooks"></a>Spark 叢集和 Notebook
此逐步解說所提供的設定步驟和程式碼適用於使用 HDInsight Spark 1.6。 不過 Jupyter Notebook 可供 HDInsight Spark 1.6 版和 Spark 2.0 叢集兩者使用。 Hello 中提供的 hello 筆記本與連結 toothem 描述[Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello GitHub 儲存機制包含它們。 此外，hello 程式碼及連結的 hello 筆記本為泛型，應該在任何 Spark 叢集上運作。 如果您未使用 HDInsight Spark，hello 叢集中設定和管理步驟可能稍有不同於這裡所顯示。 為了方便起見，以下是 hello 的 hello 的 hello 連結 toohello Jupyter 筆記本 Spark 1.6 (執行中 Jupyter 筆記本伺服器 hello pySpark 核心 toobe) 和 Spark 2.0 (執行中 Jupyter 筆記本伺服器 hello pySpark3 核心 toobe):

### <a name="spark-16-notebooks"></a>Spark 1.6 Notebook

[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb)： 提供有關如何 tooperform 資料瀏覽、 建立模型及計分具有數個不同的演算法。

### <a name="spark-20-notebooks"></a>Spark 2.0 Notebook
hello 迴歸和分類工作使用 Spark 2.0 叢集實作位於個別的筆記本和 hello 分類筆記本會使用不同的資料集：

- [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)： 這個檔案提供如何 tooperform 資料瀏覽、 建立模型及計分 Spark 2.0 中使用叢集 hello NYC 計程車路線資訊和價位資料集描述[這裡](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data)。 筆記本可能會快速瀏覽我們的 Spark 2.0 所提供的 hello 程式碼很好的起點。 更詳細的筆記本分析 hello NYC 計程車資料時，請參閱這份清單中的 hello 下一步筆記型電腦。 請參閱此清單後面，比較這些筆記本 hello 備註。 
- [Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb)： 此檔案會顯示如何 tooperform 資料 wrangling （Spark SQL 和資料框架作業），瀏覽模型及計分使用 hello NYC 計程車行程及價位資料集描述[這裡](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data)。
- [Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb)： 此檔案會顯示如何 tooperform 資料 wrangling （Spark SQL 和資料框架作業），瀏覽模型及計分使用 hello 已知 Airline 準時離開從 2011年和 2012年的資料集。 我們整合 hello airline 資料集與 hello 機場天氣資料 （例如 windspeed、 溫度、 海拔高度等） 之前 toomodeling，因此這些天氣功能可以包含在 hello 模型中。

<!-- -->

> [!NOTE]
> hello airline 資料集加入 toohello Spark 2.0 筆記本 toobetter 說明 hello 使用分類演算法。 請參閱下列連結查看有關 airline 準時出發，資料集和天氣資料集的 hello:

>- 航班準時出發資料：[http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)

>- 機場天氣資料：[https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/) 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
在 hello NYC 計程車的 hello Spark 2.0 筆記本與 airline 飛行延遲資料集可能需要 10 分鐘或更多 toorun （取決於 hello HDI 叢集大小）。 hello hello 上述清單中的第一個筆記本會顯示 hello 資料瀏覽的許多層面，視覺效果和 ML 模型定型中採用較少的時間 toorun 下取樣 NYC 資料集中的 hello 計程車行程及價位檔案都已預先已加入的筆記本： [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)筆記本會採用更短時間 toofinish （2-3 分鐘為單位），並可能不錯的起點快速瀏覽 hello 程式碼我們有提供 Spark 2.0。 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
下列的 hello 描述是相關的 toousing Spark 1.6。 如需 Spark 2.0 版本中，請使用 hello 筆記本說明和連結上方。 

<!-- -->

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
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a>匯入程式庫
安裝程式也需要匯入必要的程式庫。 設定 spark 內容，並以下列程式碼的 hello 匯入必要的程式庫：

    # IMPORT LIBRARIES
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

## <a name="data-ingestion-from-public-blob"></a>來自公用 Blob 的資料擷取
hello hello 資料科學程序中的第一個步驟是 tooingest hello 資料 toobe 分析從來源位置是位於資料探索和模型環境中。 hello 環境是在這個逐步解說中的 Spark。 本節包含 hello 程式碼 toocomplete 一系列的工作：

* 內嵌 hello 資料範例 toobe 模型化
* 讀取輸入資料集中 hello （儲存為.tsv 檔案）
* 格式和全新 hello 資料
* 建立並快取記憶體中的物件 (RDD 或資料框架)
* 將它註冊為 SQL 內容中的暫存資料表。

擷取資料的 hello 程式碼如下。

    # INGEST DATA

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


    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**輸出：**

時間 tooexecute 儲存格上方： 51.72 秒

## <a name="data-exploration--visualization"></a>資料探索和虛擬化
一旦 hello 資料已放入 Spark，hello hello 資料科學程序中的下一個步驟是 toogain hello 資料探索和視覺效果的更深入了解。 在本節中，我們會檢查 hello 計程車資料使用 SQL 查詢和繪圖 hello 目標變數與潛在功能視覺化進行檢查。 具體來說，我們會繪製旅客計數計程車往返、 hello 頻率的提示數量和如何提示因付款金額和型別中的 hello 頻率。

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a>繪製旅客計數頻率的計程車行程 hello 範例中的長條圖
這個程式碼和後續的程式碼片段，請使用 SQL magic tooquery hello 範例資料和本機 magic tooplot hello 資料。

* **SQL magic (`%%sql`)** hello HDInsight PySpark 核心支援 hello sqlContext 輕鬆內嵌 HiveQL 查詢。 hello (-o VARIABLE_NAME) 引數會保存 hello 的 hello SQL 查詢的輸出為熊資料框架 hello Jupyter 伺服器上。 這表示在 hello 本機模式中使用。
* hello  **`%%local` magic**是 hello Jupyter 伺服器，也就是 hello 的 hello HDInsight 叢集的前端節點上在本機使用 toorun 程式碼。 通常，您會使用`%%local`magic 搭配 hello`%%sql`魔法與-o 參數。 hello-o 參數會保存在本機 hello SQL 查詢的 hello 輸出，然後 %%本機 magic 會觸發 hello 下一組程式碼片段 toorun 在本機憑藉保存在本機上的 hello 輸出的 hello SQL 查詢

執行 hello 程式碼之後，會自動視覺化 hello 輸出。

此查詢會擷取 hello 往返依旅客計數。 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST hello sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

此程式碼建立 hello 查詢輸出的本機資料框架，並繪製 hello 資料。 hello `%%local` magic 建立本機資料框架， `sqlResults`，可以用來與 matplotlib 繪製。 

> [!NOTE]
> 在本逐步解說中，會多次使用此 PySpark magic。 如果 hello 資料量很大，您應該取樣 toocreate 本機記憶體內可容納資料框架。
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

以下是 hello 程式碼 tooplot hello 往返旅客計數

    # PLOT PASSENGER NUMBER VS. TRIP COUNTS
    %%local
    import matplotlib.pyplot as plt
    %matplotlib inline

    x_labels = sqlResults['passenger_count'].values
    fig = sqlResults[['trip_counts']].plot(kind='bar', facecolor='lightblue')
    fig.set_xticklabels(x_labels)
    fig.set_title('Counts of trips by passenger count')
    fig.set_xlabel('Passenger count in trips')
    fig.set_ylabel('Trip counts')
    plt.show()

**輸出：**

![按乘客計數排列的車程頻率](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

您可以在多種不同類型的視覺效果 （資料表、 圓形圖、 線條、 區域或列） 之間使用選取 hello**類型**hello 筆記本中的功能表按鈕。 以下顯示 hello 橫條圖。

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a>繪製小費金額，和小費金額如何隨乘客計數和費用金額變化的長條圖。
使用 SQL 查詢 toosample 資料。

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST hello sqlContext
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

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # HISTOGRAM OF TIP AMOUNTS AND PASSENGER COUNT
    ax1 = sqlResults[['tip_amount']].plot(kind='hist', bins=25, facecolor='lightblue')
    ax1.set_title('Tip amount distribution')
    ax1.set_xlabel('Tip Amount ($)')
    ax1.set_ylabel('Counts')
    plt.suptitle('')
    plt.show()

    # TIP BY PASSENGER COUNT
    ax2 = sqlResults.boxplot(column=['tip_amount'], by=['passenger_count'])
    ax2.set_title('Tip amount by Passenger count')
    ax2.set_xlabel('Passenger count')
    ax2.set_ylabel('Tip Amount ($)')
    plt.suptitle('')
    plt.show()

    # TIP AMOUNT BY FARE AMOUNT, POINTS ARE SCALED BY PASSENGER COUNT
    ax = sqlResults.plot(kind='scatter', x= 'fare_amount', y = 'tip_amount', c='blue', alpha = 0.10, s=5*(sqlResults.passenger_count))
    ax.set_title('Tip amount by Fare amount')
    ax.set_xlabel('Fare Amount ($)')
    ax.set_ylabel('Tip Amount ($)')
    plt.axis([-2, 100, -2, 20])
    plt.show()


**輸出：** 

![小費金額分佈](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![按乘客計數排列的小費金額](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![按費用金額排列的小費金額](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a>模型化的功能工程、轉換和資料準備
本章節描述，並提供用於 ML 模型使用 tooprepare 資料的程序的 hello 程式碼。 它會顯示影響 toodo hello 下列工作：

* 將小時納入流量時間值區以建立新特徵
* 索引並編碼分類功能
* 建立輸入到 ML 函式的標示點物件
* 建立 hello 資料的隨機子取樣和分割成定型集和測試集
* 調整功能
* 快取記憶體中的物件

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a>將小時納入流量時間值區以建立新特徵
此程式碼會示範 toocreate 的新功能的分類收納成流量時間的小時的值區，然後如何 toocache hello 產生資料框架，在記憶體中。 具有恢復功能分散式資料集 (RDDs) 和資料框架會重複使用，快取會導致 tooimproved 執行時間。 因此，我們快取 RDDs 和資料框架 hello 逐步解說中的數個階段。 

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

**輸出：** 

126050

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a>索引並編碼分類功能以輸入模型化函式中
此區段會顯示如何 tooindex 或編碼的輸入 hello 模型函式的類別特徵。 hello 模型和預測的 MLlib 函式需要功能與類別的輸入的資料 toobe 編製索引，或編碼先前 toouse。 根據 hello 模型中，您需要 tooindex，或將其編碼方式不同：  

* **樹狀結構為基礎的模型化**需要類別 toobe 編碼成數值 （例如，具有三個類別的功能可能編碼 0、 1、 2）。 這是由 MLlib 的 [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) 函式所提供。 此函式會將編碼標籤 tooa 資料行標籤索引標籤的頻率依彼此排序的字串資料的行。 使用數值輸入和資料處理編製索引，雖然 hello 樹狀結構為基礎的演算法可能會指定的 tootreat 它們適當地為類別目錄。 
* **羅吉斯和線性迴歸模型**需要一個熱編碼，例如，具有三個類別的功能才可擴充到三個特徵資料行，與每個包含 0 或 1，視所觀察 hello 分類。 提供 MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder)函式 toodo 一個熱編碼方式。 此編碼器將對應的二進位的向量，使用最多為單一其中一個值的標籤索引 tooa 資料行的資料行。 這種編碼方式可讓演算法所預期的數字的重要的功能，例如羅吉斯迴歸，套用 toobe toocategorical 功能。

以下是 hello tooindex 程式碼，並將編碼類別特徵：

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

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

**輸出：**

儲存格上方花費 tooexecute 時間： 是 1.28 秒

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a>建立輸入到 ML 函式的標示點物件
本節說明如何輸入 tooindex 類別的文字資料加上標籤的點資料，並加以編碼，讓它可以是使用的 tootrain 和測試 MLlib 羅吉斯迴歸和其他分類模型的程式碼。 標示點物件是彈性分散式資料集 (RDD)，其格式化成適合 MLlib 中大部分的 ML 演算法的輸入資料。 [標示點](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 是本機向量 (密集或疏鬆)，與標籤/回應相關聯。  

本章節包含程式碼，說明如何為 tooindex 類別的文字資料[標示為點](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point)資料類型，並使它可以使用的 tootrain 和測試 MLlib 羅吉斯迴歸和其他分類模型進行編碼。 標示點物件是彈性分散式資料集 (RDD)，由標籤 (目標/回應變數) 和功能變數組成。 這是 MLlib 中許多 ML 演算法輸入時的所需格式。

以下是 hello tooindex 程式碼，並將編碼的二元分類的文字功能。

    # FUNCTIONS FOR BINARY CLASSIFICATION

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        labPt = LabeledPoint(line.tipped, features)
        return  labPt

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
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
此程式碼會建立隨機取樣的 hello 資料 （在這裡使用 25%）。 雖然您不需要這個到期 toohello 大小的 hello 資料集的範例，我們將示範如何您可以取樣這裡以了解如何 toouse 它自己時所需的問題。 在大型範例中，如此可在訓練模型時節省大量時間。 接下來我們將 hello 範例分割成定型一部分 （這裡 75%) 和測試的一部分 （這裡 25%) toouse 分類和迴歸模型中。

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.sql.functions import rand

    # SPECIFY SAMPLING AND SPLITTING FRACTIONS
    samplingFraction = 0.25;
    trainingFraction = 0.75; testingFraction = (1-trainingFraction);
    seed = 1234;
    encodedFinalSampled = encodedFinal.sample(False, samplingFraction, seed=seed)

    # SPLIT SAMPLED DATA-FRAME INTO TRAIN/TEST
    # INCLUDE RAND COLUMN FOR CREATING CROSS-VALIDATION FOLDS (FOR USE LATER IN AN ADVANCED TOPIC)
    dfTmpRand = encodedFinalSampled.select("*", rand(0).alias("rand"));
    trainData, testData = dfTmpRand.randomSplit([trainingFraction, testingFraction], seed=seed);

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

**輸出：**

時間 tooexecute 儲存格上方： 0.24 秒

### <a name="feature-scaling"></a>調整功能
調整功能，也稱為資料正規化，以確保，功能與廣泛分散的值未授與過多權衡 hello 目標函式。 hello 功能縮放比例的程式碼會使用 hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello 功能 toounit 變異數。 這是由 MLlib 提供，用於使用隨機梯度下降 (SGD) 的線性迴歸，為訓練廣泛的其他機器學習模型的常用演算法，例如正則化迴歸或支援向量機器 (SVM)。

> [!NOTE]
> 我們發現 hello LinearRegressionWithSGD 演算法 toobe 機密 toofeature 縮放比例。
> 
> 

以下是用於正則化的 hello 線性 SGD 演算法 hello 程式碼 tooscale 變數。

    # FEATURE SCALING

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

**輸出：**

時間 tooexecute 儲存格上方： 13.17 秒

### <a name="cache-objects-in-memory"></a>快取記憶體中的物件
hello 時間的定型和測試的 ML 演算法可以降低快取用於分類，迴歸，hello 輸入的資料框架物件，因此擴充功能。

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

**輸出：** 

時間 tooexecute 儲存格上方： 0.15 k 的秒數

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a>使用二進位分類模型來預測是否支付小費
本節說明如何使用三個模型的預測的 hello 二元分類工作在提示支付計程車路線。 呈現的 hello 模型如下：

* 正規化羅吉斯迴歸 
* 隨機樹系模型
* 漸層停駐提升樹狀結構

每個模型建置程式碼區段會分成幾個步驟︰ 

1. **模型定型** 資料
2. **模型評估** 
3. **儲存模型** 

### <a name="classification-using-logistic-regression"></a>使用羅吉斯迴歸分類
本節中的 hello 程式碼顯示如何 tootrain，評估及儲存與羅吉斯迴歸模型[LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm)的預測是否付費的行程 hello NYC 計程車行程及價位資料集中的提示。

**使用 CV 和 hyperparameter 掃掠 hello 羅吉斯迴歸模型定型**

    # LOGISTIC REGRESSION CLASSIFICATION WITH CV AND HYPERPARAMETER SWEEPING

    # GET ACCURACY FOR HYPERPARAMETERS BASED ON CROSS-VALIDATION IN TRAINING DATA-SET

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionWithLBFGS 
    from sklearn.metrics import roc_curve,auc
    from pyspark.mllib.evaluation import BinaryClassificationMetrics
    from pyspark.mllib.evaluation import MulticlassMetrics


    # CREATE MODEL WITH ONE SET OF PARAMETERS
    logitModel = LogisticRegressionWithLBFGS.train(oneHotTRAINbinary, iterations=20, initialWeights=None, 
                                                   regParam=0.01, regType='l2', intercept=True, corrections=10, 
                                                   tolerance=0.0001, validateData=True, numClasses=2)

    # PRINT COEFFICIENTS AND INTERCEPT OF hello MODEL
    # NOTE: There are 20 coefficient terms for hello 10 features, 
    #       and hello different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


**輸出：** 

係數：[0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]

截距：-0.0111216486893

時間 tooexecute 儲存格上方： 14.43 秒

**評估具有標準度量的 hello 二元分類模型**

    #EVALUATE LOGISTIC REGRESSION MODEL WITH LBFGS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # PREDICT ON TEST DATA WITH MODEL
    predictionAndLabels = oneHotTESTbinary.map(lambda lp: (float(logitModel.predict(lp.features)), lp.label))

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


    ## SAVE MODEL WITH DATE-STAMP
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp;
    dirfilename = modelDir + logisticregressionfilename;
    logitModel.save(sc, dirfilename);

    # OUTPUT PROBABILITIES AND REGISTER TEMP TABLE
    logitModel.clearThreshold(); # This clears threshold for classification (0.5) and outputs probabilities
    predictionAndLabelsDF = predictionAndLabels.toDF()
    predictionAndLabelsDF.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

**輸出：** 

PR 下的領域 = 0.985297691373

ROC 下的領域 = 0.983714670256

摘要狀態

精確度 = 0.984304060189

回收 = 0.984304060189

F1 分數 = 0.984304060189

時間 tooexecute 儲存格上方： 57.61 秒

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

    # MAKE PREDICTIONS
    predictions_pddf = test_predictions.rename(columns={'_1': 'probability', '_2': 'label'})
    prob = predictions_pddf["probability"] 
    fpr, tpr, thresholds = roc_curve(predictions_pddf['label'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT ROC CURVE
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

![羅吉斯迴歸 ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a>隨機樹系分類
本節中的 hello 程式碼會示範 tootrain，如何評估及儲存預測提示支付路線 hello NYC 計程車行程及價位資料集內的隨機樹系模型。

    #PREDICT WHETHER A TIP IS PAID OR NOT USING RANDOM FOREST

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
    ## UN-COMMENT IF YOU WANT tooPRINT TREES
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

**輸出：**

ROC 下的領域 = 0.985297691373

時間 tooexecute 儲存格上方： 31.09 秒

### <a name="gradient-boosting-trees-classification"></a>漸層停駐提升樹狀結構類別
本節中的 hello 程式碼會示範 tootrain，如何評估及儲存預測提示支付 hello NYC 計程車行程及價位資料集中的行程的漸層停駐提升樹模型。

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT tooPRINT TREE DETAILS
    #print('Learned classification GBT model:')
    #print(bgtModel.toDebugString())

    # PREDICT ON TEST DATA AND EVALUATE
    predictions = gbtModel.predict(indexedTESTbinary.map(lambda x: x.features))
    predictionAndLabels = indexedTESTbinary.map(lambda lp: lp.label).zip(predictions)

    # AREA UNDER ROC CURVE
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


**輸出：**

ROC 下的領域 = 0.985297691373

時間 tooexecute 儲存格上方： 19.76 秒

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a>使用迴歸模型預測計程車車程的小費金額
本節說明如何使用三個模型的預測 hello 數量支付其他提示功能為基礎的計程車行程 hello 提示 hello 迴歸工作。 呈現的 hello 模型如下：

* 正規化線性迴歸
* 隨機樹系
* 漸層停駐提升樹狀結構

這些模型是以 hello 簡介所述。 每個模型建置程式碼區段會分成幾個步驟︰ 

1. **模型定型** 資料
2. **模型評估** 
3. **儲存模型** 

### <a name="linear-regression-with-sgd"></a>使用 SGD 的線性迴歸
hello 本節中的程式碼會示範如何 toouse 會縮放功能 tootrain 最佳化，使用隨機梯度下降 (SGD) 線性迴歸以及 tooscore，如何評估，並將 hello 模型儲存在 Azure Blob 儲存體 (WASB)。

> [!TIP]
> 在我們的經驗，可能有問題的 hello 交集的 LinearRegressionWithSGD 模型，而參數需要 toobe 變更/最佳化仔細取得有效的模型。 調整變數對於聚合很有用。 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

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

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN hello DEFAULT BLOB FOR hello CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**輸出：**

係數：[0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]

截距：0.853872718283

RMSE = 1.24190115863

R-sqr = 0.608017146081

時間 tooexecute 儲存格上方： 58.42 秒

### <a name="random-forest-regression"></a>隨機樹系迴歸
本節中的 hello 程式碼會示範如何 tootrain，評估及儲存預測 hello NYC 計程車路線資料的提示數量的隨機樹系迴歸。

    #PREDICT TIP AMOUNTS USING RANDOM FOREST

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import RandomForest, RandomForestModel
    from pyspark.mllib.util import MLUtils
    from pyspark.mllib.evaluation import RegressionMetrics


    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                        numTrees=25, featureSubsetStrategy="auto",
                                        impurity='variance', maxDepth=10, maxBins=32)
    ## UN-COMMENT IF YOU WANT tooPRING TREES
    #print('Learned classification forest model:')
    #print(rfModel.toDebugString())

    ## PREDICT AND EVALUATE ON TEST DATA-SET
    predictions = rfModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = oneHotTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
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

**輸出：**

RMSE = 0.891209218139

R-sqr = 0.759661334921

時間 tooexecute 儲存格上方： 49.21 秒

### <a name="gradient-boosting-trees-regression"></a>漸層停駐提升樹狀結構迴歸
本節中的 hello 程式碼會示範 tootrain，如何評估及儲存預測 hello NYC 計程車路線資料的提示數量的漸層停駐提升樹模型。

**訓練及評估 **

    #PREDICT TIP AMOUNTS USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart= datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel
    from pyspark.mllib.util import MLUtils

    ## TRAIN MODEL
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}
    gbtModel = GradientBoostedTrees.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo, 
                                                    numIterations=10, maxBins=32, maxDepth = 4, learningRate=0.1)

    ## EVALUATE A TEST DATA-SET
    predictions = gbtModel.predict(indexedTESTreg.map(lambda x: x.features))
    predictionAndLabels = indexedTESTreg.map(lambda lp: lp.label).zip(predictions)

    # TEST METRICS
    testMetrics = RegressionMetrics(predictionAndLabels)
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL IN BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp;
    dirfilename = modelDir + btregressionfilename;
    gbtModel.save(sc, dirfilename)

    # CONVER RESULTS tooDF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

**輸出：**

RMSE = 0.908473148639

R-sqr = 0.753835096681

時間 tooexecute 儲存格上方： 34.52 秒

**圖**

*tmp_results*註冊為 hello 前一個資料格集中的 Hive 資料表。 來自 hello 資料表的結果會輸出到 hello *sqlResults*來繪製資料框架。 以下是 hello 程式碼

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

以下是使用 hello Jupyter 伺服器 hello 程式碼 tooplot hello 資料。

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    import numpy as np

    # PLOT 
    ax = test_predictions_pddf.plot(kind='scatter', figsize = (6,6), x='_1', y='_2', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(test_predictions_pddf['_1'], test_predictions_pddf['_2'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    ax.plot(test_predictions_pddf['_1'], fit[0] * test_predictions_pddf['_1'] + fit[1], color='magenta')
    plt.axis([-1, 20, -1, 20])
    plt.show(ax)


**輸出：**

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a>從記憶體清除物件
使用`unpersist()`toodelete 物件在記憶體中快取。

    # REMOVE ORIGINAL DFs
    taxi_df_train_cleaned.unpersist()
    taxi_df_train_with_newFeatures.unpersist()

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


## <a name="record-storage-locations-of-hello-models-for-consumption-and-scoring"></a>記錄儲存體位置的耗用量和計分的 hello 模型
獨立的資料集 tooconsume 和分數述 hello[分數及評估 Spark 建立機器學習模型](machine-learning-data-science-spark-model-consumption.md)主題中，您需要 toocopy 和這些檔案名稱包含以下建立 hello 的 hello 儲存模型的貼上耗用量 Jupyter 筆記本。 以下是將程式碼 tooprint hello 出 hello 路徑 toomodel 檔案，您需要有。

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


**輸出**

logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"

linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"

randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"

randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"

BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"

BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"

## <a name="whats-next"></a>後續步驟
現在您已經以 hello Spark MlLib 建立迴歸和分類的模型，您就準備好 toolearn 如何 tooscore 和評估這些模型。 hello 進階資料探索和模型化筆記本磁碟機 e:\ 更深入到包括交叉驗證，超參數清除，並建立模型評估。 

**模型耗用量：** toolearn 如何 tooscore 和評估建立本主題中的 hello 分類和迴歸模型，請參閱[分數及評估 Spark 建立機器學習模型](machine-learning-data-science-spark-model-consumption.md)。

**交叉驗證和超參數掃掠**：如需如何使用交叉驗證和超參數掃掠訓練模型的相關資訊，請參閱 [使用 Spark 進階資料探索和模型化](machine-learning-data-science-spark-advanced-data-exploration-modeling.md)

