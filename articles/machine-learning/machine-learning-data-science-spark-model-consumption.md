---
title: "實作 Spark 建置機器學習模型 | Microsoft Docs"
description: "如何使用 Python 載入及評分儲存在 Azure Blob 儲存體 (WASB) 中的學習模型。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 626305a2-0abf-4642-afb0-dad0f6bd24e9
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/15/2017
ms.author: deguhath;bradsev;gokuma
ms.openlocfilehash: 00fec675bed0137473f7e3c5ddfe9c3c0e8344c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="101b5-103">實作 Spark 建置機器學習模型</span><span class="sxs-lookup"><span data-stu-id="101b5-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="101b5-104">本主題說明如何使用 HDInsight Spark 叢集上的 Python 實作已儲存的機器學習模型 (ML)。</span><span class="sxs-lookup"><span data-stu-id="101b5-104">This topic shows how to operationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="101b5-105">它說明如何載入已使用 Spark MLlib 建立並儲存於 Azure Blob 儲存體 (WASB) 的機器學習服務模型，以及如何使用已儲存在 WASB 的資料集加以評分。</span><span class="sxs-lookup"><span data-stu-id="101b5-105">It describes how to load machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how to score them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="101b5-106">它會顯示如何前置處理輸入資料、使用 MLlib 工具組中的索引和編碼函式來轉換功能，以及如何建立可做為輸入的標示點資料物件，以便使用 ML 模型加以評分。</span><span class="sxs-lookup"><span data-stu-id="101b5-106">It shows how to pre-process the input data, transform features using the indexing and encoding functions in the MLlib toolkit, and how to create a labeled point data object that can be used as input for scoring with the ML models.</span></span> <span data-ttu-id="101b5-107">用於評分的模型包含線性迴歸、羅吉斯迴歸、隨機樹系模型和漸層停駐提升樹狀結構模型。</span><span class="sxs-lookup"><span data-stu-id="101b5-107">The models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="101b5-108">Spark 叢集和 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="101b5-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="101b5-109">在本逐步解說中提供實作 ML 模型的設定步驟和程式碼，供您使用 HDInsight Spark 1.6 叢集以及 Spark 2.0 叢集。</span><span class="sxs-lookup"><span data-stu-id="101b5-109">Setup steps and the code to operationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="101b5-110">Jupyter notebook 中也會提供這些程序的程式碼。</span><span class="sxs-lookup"><span data-stu-id="101b5-110">The code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="101b5-111">Notebook for Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="101b5-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="101b5-112">[pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter Notebook 示範如何在 HDInsight 叢集上，使用 Python 讓儲存的模型能夠運作。</span><span class="sxs-lookup"><span data-stu-id="101b5-112">The [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how to operationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="101b5-113">Notebook for Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="101b5-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="101b5-114">若要修改此 Jupyter Notebook for Spark 1.6 來與 HDInsight Spark 2.0 叢集搭配使用，請使用[這個檔案](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py)來取代 Python 程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="101b5-114">To modify the Jupyter notebook for Spark 1.6 to use with an HDInsight Spark 2.0 cluster, replace the Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="101b5-115">此程式碼示範如何使用 Spark 2.0 中所建立的模型。</span><span class="sxs-lookup"><span data-stu-id="101b5-115">This code shows how to consume the models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="101b5-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="101b5-116">Prerequisites</span></span>

1. <span data-ttu-id="101b5-117">您需要 Azure 帳戶和 Spark 1.6 (或 Spark 2.0) HDInsight 叢集，才能完成此逐步解說。</span><span class="sxs-lookup"><span data-stu-id="101b5-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="101b5-118">請參閱[使用 Azure HDInsight 上的 Spark 的資料科學概觀](machine-learning-data-science-spark-overview.md)以取得這些需求。</span><span class="sxs-lookup"><span data-stu-id="101b5-118">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="101b5-119">此主題也包括這裡使用的 NYC 2013 計程車資料的描述，以及如何從 Spark 叢集的 Jupyter Notebook 執行程式碼的指示。</span><span class="sxs-lookup"><span data-stu-id="101b5-119">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 
2. <span data-ttu-id="101b5-120">您也必須針對 Spark 1.6 叢集或 Spark 2.0 Notebook，透過[使用 Spark 資料探索和模型化](machine-learning-data-science-spark-data-exploration-modeling.md)主題運作，在這裡建立要評分的機器學習服務模型。</span><span class="sxs-lookup"><span data-stu-id="101b5-120">You must also create the machine learning models to be scored here by working through the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for the Spark 1.6 cluster or the Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="101b5-121">Spark 2.0 Notebook 會針對分類工作使用額外的資料集，即 2011 年和 2012 年知名航空公司準時起飛的資料集。</span><span class="sxs-lookup"><span data-stu-id="101b5-121">The Spark 2.0 notebooks use an additional data set for the classification task, the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="101b5-122">Notebook 的描述及它們的連結已在包含它們的 GitHub 儲存機制的 [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) 中提供。</span><span class="sxs-lookup"><span data-stu-id="101b5-122">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="101b5-123">此外，此處及連結的 Notebook 內的程式碼皆屬泛型程式碼，而且應該能在任何 Spark 叢集上運作。</span><span class="sxs-lookup"><span data-stu-id="101b5-123">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="101b5-124">若您不是使用 HDInsight Spark，叢集設定和管理步驟可能與這裡顯示的稍有不同。</span><span class="sxs-lookup"><span data-stu-id="101b5-124">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="101b5-125">安裝程式︰儲存體位置、程式庫和預設 Spark 內容</span><span class="sxs-lookup"><span data-stu-id="101b5-125">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="101b5-126">Spark 也可以讀取和寫入 Azure 儲存體 Blob (WASB)。</span><span class="sxs-lookup"><span data-stu-id="101b5-126">Spark is able to read and write to an Azure Storage Blob (WASB).</span></span> <span data-ttu-id="101b5-127">如此可使用 Spark 處理該處儲存的任何現有資料，並在 WASB 中再次儲存結果。</span><span class="sxs-lookup"><span data-stu-id="101b5-127">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="101b5-128">若要在 WASB 中儲存模型或檔案，必須正確指定路徑。</span><span class="sxs-lookup"><span data-stu-id="101b5-128">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="101b5-129">可以使用以「wasb//」 開頭的路徑，參考連接到 Spark 叢集的預設容器。</span><span class="sxs-lookup"><span data-stu-id="101b5-129">The default container attached to the Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="101b5-130">下列程式碼範例會指定要讀取資料的位置，和將儲存模型輸出的模型儲存體目錄的路徑。</span><span class="sxs-lookup"><span data-stu-id="101b5-130">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="101b5-131">在 WASB 中設定儲存位置的目錄路徑</span><span class="sxs-lookup"><span data-stu-id="101b5-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="101b5-132">模型會儲存在：「wasb:///user/remoteuser/NYCTaxi/Models」。</span><span class="sxs-lookup"><span data-stu-id="101b5-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="101b5-133">如果未正確設定此路徑，不會載入模型進行評分。</span><span class="sxs-lookup"><span data-stu-id="101b5-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="101b5-134">評分的結果儲存在：「wasb:///user/remoteuser/NYCTaxi/ScoredResults」。</span><span class="sxs-lookup"><span data-stu-id="101b5-134">The scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="101b5-135">如果資料夾的路徑不正確，不會將結果儲存在該資料夾中。</span><span class="sxs-lookup"><span data-stu-id="101b5-135">If the path to folder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="101b5-136">可從 **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook 的最後一個儲存格的輸出，將檔案路徑位置複製並貼至此程式碼的預留位置。</span><span class="sxs-lookup"><span data-stu-id="101b5-136">The file path locations can be copied and pasted into the placeholders in this code from the output of the last cell of the **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="101b5-137">以下是設定目錄路徑的程式碼：</span><span class="sxs-lookup"><span data-stu-id="101b5-137">Here is the code to set directory paths:</span></span> 

    # LOCATION OF DATA TO BE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE THE LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR THE MODELS TO BE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="101b5-138">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="101b5-138">**OUTPUT:**</span></span>

<span data-ttu-id="101b5-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="101b5-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="101b5-140">匯入程式庫</span><span class="sxs-lookup"><span data-stu-id="101b5-140">Import libraries</span></span>
<span data-ttu-id="101b5-141">使用下列程式碼設定 Spark 內容並匯入必要的程式庫</span><span class="sxs-lookup"><span data-stu-id="101b5-141">Set spark context and import necessary libraries with the following code</span></span>

    #IMPORT LIBRARIES
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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="101b5-142">預設 Spark 內容及 PySpark magic</span><span class="sxs-lookup"><span data-stu-id="101b5-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="101b5-143">Jupyter Notebook 所提供的 PySpark 核心有預設的內容。</span><span class="sxs-lookup"><span data-stu-id="101b5-143">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="101b5-144">因此您不必明確設定 Spark 或 Hive 內容，就能開始使用您所開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="101b5-144">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="101b5-145">依預設會將這些內容提供給您使用。</span><span class="sxs-lookup"><span data-stu-id="101b5-145">These are available for you by default.</span></span> <span data-ttu-id="101b5-146">這些內容包括：</span><span class="sxs-lookup"><span data-stu-id="101b5-146">These contexts are:</span></span>

* <span data-ttu-id="101b5-147">sc - 代表 Spark</span><span class="sxs-lookup"><span data-stu-id="101b5-147">sc - for Spark</span></span> 
* <span data-ttu-id="101b5-148">sqlContext - 代表 Hive</span><span class="sxs-lookup"><span data-stu-id="101b5-148">sqlContext - for Hive</span></span>

<span data-ttu-id="101b5-149">PySpark 核心提供一些預先定義的「magic」，這是您可以使用 %% 呼叫的特殊命令。</span><span class="sxs-lookup"><span data-stu-id="101b5-149">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="101b5-150">在這些程式碼範例中，就使用了兩個此類型的命令。</span><span class="sxs-lookup"><span data-stu-id="101b5-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="101b5-151">**%%local** 指定後續行所列的程式碼要在本機執行。</span><span class="sxs-lookup"><span data-stu-id="101b5-151">**%%local** Specified that the code in subsequent lines is executed locally.</span></span> <span data-ttu-id="101b5-152">程式碼必須是有效的 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="101b5-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="101b5-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="101b5-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="101b5-154">針對 sqlContext 執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="101b5-154">Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="101b5-155">如果傳遞 -o 參數，則查詢的結果會當做 Pandas 資料框架，保存在 %%local Python 內容中。</span><span class="sxs-lookup"><span data-stu-id="101b5-155">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="101b5-156">如需關於 Jupyter Notebook 核心，以及其所提供的預先定義 "magics" 的詳細資訊，請參閱 [HDInsight 上的 HDInsight Spark Linux 叢集可供 Jupyter Notebook 使用的核心](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="101b5-156">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="101b5-157">擷取資料並建立已清除的資料框架</span><span class="sxs-lookup"><span data-stu-id="101b5-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="101b5-158">本節包含一系列工作的程式碼，為擷取要評分的資料所必需。</span><span class="sxs-lookup"><span data-stu-id="101b5-158">This section contains the code for a series of tasks required to ingest the data to be scored.</span></span> <span data-ttu-id="101b5-159">在聯結的 0.1% 取樣的計程車車程和費用檔案中讀取 (儲存為 .tsv 檔案)、格式化資料，然後建立清空的資料框架。</span><span class="sxs-lookup"><span data-stu-id="101b5-159">Read in a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file), format the data, and then creates a clean data frame.</span></span>

<span data-ttu-id="101b5-160">已根據 [Team Data Science Process 實務：使用 HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-walkthrough.md) 主題提供的程序來聯結計程車車程和費用檔案。</span><span class="sxs-lookup"><span data-stu-id="101b5-160">The taxi trip and fare files were joined based on the procedure provided in the: [The Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF THE FILE FROM HEADER
    schema_string = taxi_test_file.first()
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

    # CREATE DATA FRAME
    taxi_df_test = sqlContext.createDataFrame(taxi_temp, taxi_schema)

    # CREATE A CLEANED DATA-FRAME BY DROPPING SOME UN-NECESSARY COLUMNS & FILTERING FOR UNDESIRED VALUES OR OUTLIERS
    taxi_df_test_cleaned = taxi_df_test.drop('medallion').drop('hack_license').drop('store_and_fwd_flag').drop('pickup_datetime')\
        .drop('dropoff_datetime').drop('pickup_longitude').drop('pickup_latitude').drop('dropoff_latitude')\
        .drop('dropoff_longitude').drop('tip_class').drop('total_amount').drop('tolls_amount').drop('mta_tax')\
        .drop('direct_distance').drop('surcharge')\
        .filter("passenger_count > 0 and passenger_count < 8 AND payment_type in ('CSH', 'CRD') AND tip_amount >= 0 AND tip_amount < 30 AND fare_amount >= 1 AND fare_amount < 150 AND trip_distance > 0 AND trip_distance < 100 AND trip_time_in_secs > 30 AND trip_time_in_secs < 7200" )

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_cleaned.cache()
    taxi_df_test_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_test_cleaned.registerTempTable("taxi_test")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="101b5-161">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="101b5-161">**OUTPUT:**</span></span>

<span data-ttu-id="101b5-162">執行上述儲存格所花費的時間︰46.37 秒</span><span class="sxs-lookup"><span data-stu-id="101b5-162">Time taken to execute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="101b5-163">準備資料在 Spark 中評分</span><span class="sxs-lookup"><span data-stu-id="101b5-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="101b5-164">本節說明如何索引、編碼及調整分類功能，準備將它們用於分類和迴歸的 MLlib 監督式學習演算法中。</span><span class="sxs-lookup"><span data-stu-id="101b5-164">This section shows how to index, encode, and scale categorical features to prepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="101b5-165">功能轉換：索引並編碼分類功能以輸入至模型進行評分。</span><span class="sxs-lookup"><span data-stu-id="101b5-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="101b5-166">本節說明如何使用 `StringIndexer` 來為分類資料編製索引，並利用 `OneHotEncoder` 輸入將特徵編碼至模組中。</span><span class="sxs-lookup"><span data-stu-id="101b5-166">This section shows how to index categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into the models.</span></span>

<span data-ttu-id="101b5-167">[StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) 會將標籤的字串資料行編碼至標籤索引的資料行。</span><span class="sxs-lookup"><span data-stu-id="101b5-167">The [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels to a column of label indices.</span></span> <span data-ttu-id="101b5-168">索引是按標籤頻率排序。</span><span class="sxs-lookup"><span data-stu-id="101b5-168">The indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="101b5-169">[OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) 會將標籤索引資料行對應到二元向量資料行 (最多有一個單一值)。</span><span class="sxs-lookup"><span data-stu-id="101b5-169">The [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="101b5-170">這種編碼方式允許將預期連續值功能的演算法 (例如羅吉斯迴歸) 套用至分類功能。</span><span class="sxs-lookup"><span data-stu-id="101b5-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, to be applied to categorical features.</span></span>

    #INDEX AND ONE-HOT ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # CREATE FOUR BUCKETS FOR TRAFFIC TIMES
    sqlStatement = """
        SELECT *,
        CASE
         WHEN (pickup_hour <= 6 OR pickup_hour >= 20) THEN "Night" 
         WHEN (pickup_hour >= 7 AND pickup_hour <= 10) THEN "AMRush" 
         WHEN (pickup_hour >= 11 AND pickup_hour <= 15) THEN "Afternoon"
         WHEN (pickup_hour >= 16 AND pickup_hour <= 19) THEN "PMRush"
        END as TrafficTimeBins
        FROM taxi_test 
    """
    taxi_df_test_with_newFeatures = sqlContext.sql(sqlStatement)

    # CACHE DATA-FRAME IN MEMORY & MATERIALIZE DF IN MEMORY
    taxi_df_test_with_newFeatures.cache()
    taxi_df_test_with_newFeatures.count()

    # INDEX AND ONE-HOT ENCODING
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is the cleaned one from above
    indexed = model.transform(taxi_df_test_with_newFeatures)
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

    # INDEX AND ENCODE TRAFFIC TIME BINS
    stringIndexer = StringIndexer(inputCol="TrafficTimeBins", outputCol="TrafficTimeBinsIndex")
    model = stringIndexer.fit(encoded3)
    indexed = model.transform(encoded3)
    encoder = OneHotEncoder(dropLast=False, inputCol="TrafficTimeBinsIndex", outputCol="TrafficTimeBinsVec")
    encodedFinal = encoder.transform(indexed)

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="101b5-171">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="101b5-171">**OUTPUT:**</span></span>

<span data-ttu-id="101b5-172">執行上述儲存格所花費的時間︰5.37 秒</span><span class="sxs-lookup"><span data-stu-id="101b5-172">Time taken to execute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="101b5-173">使用功能陣列建立 RDD 物件以輸入至模型</span><span class="sxs-lookup"><span data-stu-id="101b5-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="101b5-174">本節包含程式碼，示範如何將分類的文字資料索引為 RDD 物件並加以單次編碼，以用來訓練及測試 MLlib 羅吉斯迴歸和樹狀結構型模型。</span><span class="sxs-lookup"><span data-stu-id="101b5-174">This section contains code that shows how to index categorical text data as an RDD object and one-hot encode it so it can be used to train and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="101b5-175">已編製索引的資料是儲存在 [彈性分散式資料集 (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) 物件中。</span><span class="sxs-lookup"><span data-stu-id="101b5-175">The indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="101b5-176">這些是 Spark 中的基本抽象概念。</span><span class="sxs-lookup"><span data-stu-id="101b5-176">These are the basic abstraction in Spark.</span></span> <span data-ttu-id="101b5-177">RDD 物件代表不可變、資料分割、可與 Spark 平行操作的元素集合。</span><span class="sxs-lookup"><span data-stu-id="101b5-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="101b5-178">它也包含程式碼，顯示如何使用 MLlib 提供的 `StandardScalar` 來調整資料，用於使用隨機梯度下降法 (SGD) 的線性迴歸，此為訓練廣泛的機器學習服務模型的常用演算法。</span><span class="sxs-lookup"><span data-stu-id="101b5-178">It also contains code that shows how to scale data with the `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="101b5-179">[StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) 是用來調整單位變異數的特徵。</span><span class="sxs-lookup"><span data-stu-id="101b5-179">The [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used to scale the features to unit variance.</span></span> <span data-ttu-id="101b5-180">調整功能，也稱為資料正規化，以確保具廣泛分散值的功能在目標函式中沒有過多權重。</span><span class="sxs-lookup"><span data-stu-id="101b5-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> 

    # CREATE RDD OBJECTS WITH FEATURE ARRAYS FOR INPUT INTO MODELS

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.linalg import Vectors
    from pyspark.mllib.feature import StandardScaler, StandardScalerModel
    from pyspark.mllib.util import MLUtils
    from numpy import array

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingBinary(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex,
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO LOGISTIC RERESSION MODELS
    def parseRowOneHotBinary(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # ONE-HOT ENCODING OF CATEGORICAL TEXT FEATURES FOR INPUT INTO TREE-BASED MODELS
    def parseRowIndexingRegression(line):
        features = np.array([line.paymentIndex, line.vendorIndex, line.rateIndex, line.TrafficTimeBinsIndex, 
                             line.pickup_hour, line.weekday, line.passenger_count, line.trip_time_in_secs, 
                             line.trip_distance, line.fare_amount])
        return  features

    # INDEXING CATEGORICAL TEXT FEATURES FOR INPUT INTO LINEAR REGRESSION MODELS
    def parseRowOneHotRegression(line):
        features = np.concatenate((np.array([line.pickup_hour, line.weekday, line.passenger_count,
                                            line.trip_time_in_secs, line.trip_distance, line.fare_amount]), 
                                            line.vendorVec.toArray(), line.rateVec.toArray(), 
                                            line.paymentVec.toArray(), line.TrafficTimeBinsVec.toArray()), axis=0)
        return  features

    # FOR BINARY CLASSIFICATION TRAINING AND TESTING
    indexedTESTbinary = encodedFinal.map(parseRowIndexingBinary)
    oneHotTESTbinary = encodedFinal.map(parseRowOneHotBinary)

    # FOR REGRESSION CLASSIFICATION TRAINING AND TESTING
    indexedTESTreg = encodedFinal.map(parseRowIndexingRegression)
    oneHotTESTreg = encodedFinal.map(parseRowOneHotRegression)

    # SCALING FEATURES FOR LINEARREGRESSIONWITHSGD MODEL
    scaler = StandardScaler(withMean=False, withStd=True).fit(oneHotTESTreg)
    oneHotTESTregScaled = scaler.transform(oneHotTESTreg)

    # CACHE RDDS IN MEMORY
    indexedTESTbinary.cache();
    oneHotTESTbinary.cache();
    indexedTESTreg.cache();
    oneHotTESTreg.cache();
    oneHotTESTregScaled.cache();

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="101b5-181">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="101b5-181">**OUTPUT:**</span></span>

<span data-ttu-id="101b5-182">執行上述儲存格所花費的時間︰11.72 秒</span><span class="sxs-lookup"><span data-stu-id="101b5-182">Time taken to execute above cell: 11.72 seconds</span></span>

## <a name="score-with-the-logistic-regression-model-and-save-output-to-blob"></a><span data-ttu-id="101b5-183">使用羅吉斯迴歸模型進行評分，並將輸出儲存至 blob</span><span class="sxs-lookup"><span data-stu-id="101b5-183">Score with the Logistic Regression Model and save output to blob</span></span>
<span data-ttu-id="101b5-184">本節的程式碼示範如何載入 Azure Blob 儲存體中已儲存的羅吉斯迴歸模型，並使用它來預測是否支付計程車車程的小費、使用標準分類度量評分，然後儲存結果並將其繪製至 Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="101b5-184">The code in this section shows how to load a Logistic Regression Model that has been saved in Azure blob storage and use it to predict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot the results to blob storage.</span></span> <span data-ttu-id="101b5-185">評分的結果會儲存在 RDD 物件。</span><span class="sxs-lookup"><span data-stu-id="101b5-185">The scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) TO BLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="101b5-186">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="101b5-186">**OUTPUT:**</span></span>

<span data-ttu-id="101b5-187">執行上述儲存格所花費的時間︰19.22 秒</span><span class="sxs-lookup"><span data-stu-id="101b5-187">Time taken to execute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="101b5-188">評分線性迴歸模型</span><span class="sxs-lookup"><span data-stu-id="101b5-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="101b5-189">我們搭配使用 [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) 與隨機梯度下降法 (SGD) 來訓練線性迴歸模型，以最佳化的方式預測支付的小費金額。</span><span class="sxs-lookup"><span data-stu-id="101b5-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) to train a linear regression model using Stochastic Gradient Descent (SGD) for optimization to predict the amount of tip paid.</span></span> 

<span data-ttu-id="101b5-190">本節的程式碼示範如何從 Azure blob 儲存體載入線性迴歸模型、使用調整變數評分，然後將結果存回 blob。</span><span class="sxs-lookup"><span data-stu-id="101b5-190">The code in this section shows how to load a Linear Regression Model from Azure blob storage, score using scaled variables, and then save the results back to the blob.</span></span>

    #SCORE LINEAR REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #LOAD LIBRARIES
    from pyspark.mllib.regression import LinearRegressionWithSGD, LinearRegressionModel

    # LOAD MODEL AND SCORE USING ** SCALED VARIABLES **
    savedModel = LinearRegressionModel.load(sc, linearRegFileLoc)
    predictions = oneHotTESTregScaled.map(lambda features: (float(savedModel.predict(features))))

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = scoredResultDir + linearregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="101b5-191">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="101b5-191">**OUTPUT:**</span></span>

<span data-ttu-id="101b5-192">執行上述儲存格所花費的時間︰16.63 秒</span><span class="sxs-lookup"><span data-stu-id="101b5-192">Time taken to execute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="101b5-193">評分分類和迴歸的隨機樹系模型</span><span class="sxs-lookup"><span data-stu-id="101b5-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="101b5-194">本節的程式碼示範如何載入已儲存的分類和迴歸的隨機樹系模型 (儲存在 Azure blob 儲存體)、使用標準分類器和迴歸措施來評分其效能，然後將結果存回 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="101b5-194">The code in this section shows how to load the saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span>

<span data-ttu-id="101b5-195">[隨機樹系](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 是整體的決策樹。</span><span class="sxs-lookup"><span data-stu-id="101b5-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="101b5-196">隨機樹系結合許多決策樹來降低風險過度膨脹。</span><span class="sxs-lookup"><span data-stu-id="101b5-196">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="101b5-197">隨機樹系可處理分類功能、擴充至多類別分類設定、不需要調整功能，而且能夠擷取非線性和功能互動。</span><span class="sxs-lookup"><span data-stu-id="101b5-197">Random forests can handle categorical features, extend to the multiclass classification setting, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="101b5-198">隨機樹系是其中一個最成功的分類和迴歸的機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="101b5-198">Random forests are one of the most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="101b5-199">[spark.mllib](http://spark.apache.org/mllib/) 使用連續和分類特徵來支援二元和多元分類和迴歸的隨機樹系。</span><span class="sxs-lookup"><span data-stu-id="101b5-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="101b5-200">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="101b5-200">**OUTPUT:**</span></span>

<span data-ttu-id="101b5-201">執行上述儲存格所花費的時間︰31.07 秒</span><span class="sxs-lookup"><span data-stu-id="101b5-201">Time taken to execute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="101b5-202">評分分類和迴歸的漸層停駐提升樹狀結構模型</span><span class="sxs-lookup"><span data-stu-id="101b5-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="101b5-203">本節的程式碼示範如何從 Azure blob 儲存體載入分類和迴歸的漸層停駐提升樹狀結構模型、使用標準分類器和迴歸措施來評分其效能，然後將結果存回 blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="101b5-203">The code in this section shows how to load classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save the results back to blob storage.</span></span> 

<span data-ttu-id="101b5-204">**spark.mllib** 使用連續和分類特徵來支援二元分類和迴歸的 GBT。</span><span class="sxs-lookup"><span data-stu-id="101b5-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="101b5-205">[漸層停駐提升樹狀結構](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) 是整體的決策樹。</span><span class="sxs-lookup"><span data-stu-id="101b5-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="101b5-206">GBT 反覆地訓練決策樹以盡可能降低遺失函式。</span><span class="sxs-lookup"><span data-stu-id="101b5-206">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="101b5-207">GBT 可處理分類功能、不需要調整功能，而且能夠擷取非線性和功能互動。</span><span class="sxs-lookup"><span data-stu-id="101b5-207">GBTs can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="101b5-208">它們也可用於多類別分類設定。</span><span class="sxs-lookup"><span data-stu-id="101b5-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    #LOAD AND SCORE THE MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK TO BLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="101b5-209">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="101b5-209">**OUTPUT:**</span></span>

<span data-ttu-id="101b5-210">執行上述儲存格所花費的時間︰14.6 秒</span><span class="sxs-lookup"><span data-stu-id="101b5-210">Time taken to execute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="101b5-211">從記憶體清除物件並列印計分的檔案位置</span><span class="sxs-lookup"><span data-stu-id="101b5-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH TO SCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="101b5-212">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="101b5-212">**OUTPUT:**</span></span>

<span data-ttu-id="101b5-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="101b5-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="101b5-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="101b5-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="101b5-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="101b5-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="101b5-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="101b5-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="101b5-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="101b5-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="101b5-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="101b5-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="101b5-219">透過 Web 介面使用 Spark 模型</span><span class="sxs-lookup"><span data-stu-id="101b5-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="101b5-220">Spark 提供一個機制，透過 REST 介面 (包含稱為 Livy 的元件) 從遠端提交批次工作或互動式查詢。</span><span class="sxs-lookup"><span data-stu-id="101b5-220">Spark provides a mechanism to remotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="101b5-221">Livy 預設在 HDInsight Spark 叢集上啟用。</span><span class="sxs-lookup"><span data-stu-id="101b5-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="101b5-222">如需 Livy 的詳細資訊，請參閱 [使用 Livy 遠端提交 Spark 作業](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="101b5-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="101b5-223">您可以使用 Livy 從遠端提交作業，其批次批分儲存在 Azure blob 中的檔案，然後將結果寫入另一個 blob。</span><span class="sxs-lookup"><span data-stu-id="101b5-223">You can use Livy to remotely submit a job that batch scores a file that is stored in an Azure blob and then writes the results to another blob.</span></span> <span data-ttu-id="101b5-224">若要這樣做，需要將 Python 指令碼從 </span><span class="sxs-lookup"><span data-stu-id="101b5-224">To do this, you upload the Python script from</span></span>  
<span data-ttu-id="101b5-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) 上傳至 Spark 叢集的 blob。</span><span class="sxs-lookup"><span data-stu-id="101b5-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) to the blob of the Spark cluster.</span></span> <span data-ttu-id="101b5-226">您可以使用類似 **Microsoft Azure 儲存體總管**或 **AzCopy** 的工具，將指令碼複製到叢集 blob。</span><span class="sxs-lookup"><span data-stu-id="101b5-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** to copy the script to the cluster blob.</span></span> <span data-ttu-id="101b5-227">在本例中，我們將指令碼上傳至 wasb:///example/python/ConsumeGBNYCReg.py。</span><span class="sxs-lookup"><span data-stu-id="101b5-227">In our case we uploaded the script to ***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="101b5-228">您可在入口網站上，為 Spark 叢集關聯的儲存體帳戶尋找需要的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="101b5-228">The access keys that you need can be found on the portal for the storage account associated with the Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="101b5-229">一旦上傳至這個位置，此指令碼會在分散式內容的 Spark 叢集內執行。</span><span class="sxs-lookup"><span data-stu-id="101b5-229">Once uploaded to this location, this script runs within the Spark cluster in a distributed context.</span></span> <span data-ttu-id="101b5-230">它會載入模型，並根據模型對輸入檔執行預測。</span><span class="sxs-lookup"><span data-stu-id="101b5-230">It loads the model and runs predictions on input files based on the model.</span></span>  

<span data-ttu-id="101b5-231">您可以在 Livy 上進行簡單的 HTTPS/REST 要求，從遠端叫用此指令碼。</span><span class="sxs-lookup"><span data-stu-id="101b5-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="101b5-232">以下是 curl 命令，可建構 HTTP 要求以遠端叫用 Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="101b5-232">Here is a curl command to construct the HTTP request to invoke the Python script remotely.</span></span> <span data-ttu-id="101b5-233">將 CLUSTERLOGIN、CLUSTERPASSWORD、CLUSTERNAME 取代為 Spark 叢集的適當值。</span><span class="sxs-lookup"><span data-stu-id="101b5-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with the appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND TO INVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="101b5-234">您可以藉由基本驗證來進行簡單 HTTPS 呼叫，使用遠端系統上的任何語言來叫用 Spark 作業。</span><span class="sxs-lookup"><span data-stu-id="101b5-234">You can use any language on the remote system to invoke the Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="101b5-235">進行此 HTTP 呼叫時可方便地使用 Python 要求程式庫，但目前預設不會在 Azure Functions 中安裝此程式庫。</span><span class="sxs-lookup"><span data-stu-id="101b5-235">It would be convenient to use the Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="101b5-236">因此會改用較舊的 HTTP 程式庫。</span><span class="sxs-lookup"><span data-stu-id="101b5-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="101b5-237">以下是 HTTP 呼叫的 Python 程式碼 ︰</span><span class="sxs-lookup"><span data-stu-id="101b5-237">Here is the Python code for the HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF THE REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY THE PYTHON SCRIPT TO RUN ON THE SPARK CLUSTER
    # IN THE FILE PARAMETER OF THE JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="101b5-238">您也可以將此 Python 程式碼新增至 [Azure Functions](https://azure.microsoft.com/documentation/services/functions/) 以觸發 Spark 作業提交，以根據各種事件 (像是計時器、建立或更新 blob) 來評分 blob。</span><span class="sxs-lookup"><span data-stu-id="101b5-238">You can also add this Python code to [Azure Functions](https://azure.microsoft.com/documentation/services/functions/) to trigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="101b5-239">如果您偏好程式碼可用的用戶端體驗，請使用 [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) 來叫用 Spark 批次評分，方法是在 **Logic Apps Designer** 上定義 HTTP 動作並設定它的參數。</span><span class="sxs-lookup"><span data-stu-id="101b5-239">If you prefer a code free client experience, use the [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) to invoke the Spark batch scoring by defining an HTTP action on the **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="101b5-240">在 Azure 入口網站中，選取 [+ 新增]  ->  [Web + 行動 ]  ->  [邏輯應用程式] 來建立新的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="101b5-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="101b5-241">若要引進 **Logic Apps Designer**，請輸入邏輯應用程式和 App Service 方案的名稱。</span><span class="sxs-lookup"><span data-stu-id="101b5-241">To bring up the **Logic Apps Designer**, enter the name of the Logic App and App Service Plan.</span></span>
* <span data-ttu-id="101b5-242">選取 HTTP 動作，然後輸入下圖顯示的參數︰</span><span class="sxs-lookup"><span data-stu-id="101b5-242">Select an HTTP action and enter the parameters shown in the following figure:</span></span>

![Logic Apps 設計工具](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="101b5-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="101b5-244">What's next?</span></span>
<span data-ttu-id="101b5-245">**交叉驗證和超參數掃掠**：如需如何使用交叉驗證和超參數掃掠訓練模型的相關資訊，請參閱 [使用 Spark 進階資料探索和模型化](machine-learning-data-science-spark-advanced-data-exploration-modeling.md)</span><span class="sxs-lookup"><span data-stu-id="101b5-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

