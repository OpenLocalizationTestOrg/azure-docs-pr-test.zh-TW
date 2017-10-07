---
title: "aaaOperationalize Spark 建立機器學習模型 |Microsoft 文件"
description: "如何 tooload 和分數學習模型儲存在 Azure Blob 儲存體 (WASB) 使用 Python。"
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
ms.openlocfilehash: c5fadcb13257b94dcb28a522be454f6e03dfa991
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="operationalize-spark-built-machine-learning-models"></a><span data-ttu-id="da43d-103">實作 Spark 建置機器學習模型</span><span class="sxs-lookup"><span data-stu-id="da43d-103">Operationalize Spark-built machine learning models</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="da43d-104">本主題說明如何 toooperationalize HDInsight Spark 上使用 Python 的已儲存的機器學習模型 (ML) 叢集。</span><span class="sxs-lookup"><span data-stu-id="da43d-104">This topic shows how toooperationalize a saved machine learning model (ML) using Python on HDInsight Spark clusters.</span></span> <span data-ttu-id="da43d-105">它說明如何 tooload 機器學習模型，可使用 Spark MLlib 建置並儲存在 Azure Blob 儲存體 (WASB)，以及如何 tooscore 它們也已儲存在 WASB 的資料集。</span><span class="sxs-lookup"><span data-stu-id="da43d-105">It describes how tooload machine learning models that have been built using Spark MLlib and stored in Azure Blob Storage (WASB), and how tooscore them with datasets that have also been stored in WASB.</span></span> <span data-ttu-id="da43d-106">它會顯示 hello 輸入的資料時，如何 toopre 程序，使用轉換功能 hello hello MLlib 工具組，以及如何 toocreate 加上標籤的點資料物件，可用來當做輸入計分 hello ML 模型中的索引和編碼方式函式。</span><span class="sxs-lookup"><span data-stu-id="da43d-106">It shows how toopre-process hello input data, transform features using hello indexing and encoding functions in hello MLlib toolkit, and how toocreate a labeled point data object that can be used as input for scoring with hello ML models.</span></span> <span data-ttu-id="da43d-107">用於計分的 hello 模型包含線性迴歸、 羅吉斯迴歸、 隨機樹系模型和梯度促進式樹狀模型。</span><span class="sxs-lookup"><span data-stu-id="da43d-107">hello models used for scoring include Linear Regression, Logistic Regression, Random Forest Models, and Gradient Boosting Tree Models.</span></span>

## <a name="spark-clusters-and-jupyter-notebooks"></a><span data-ttu-id="da43d-108">Spark 叢集和 Jupyter Notebook</span><span class="sxs-lookup"><span data-stu-id="da43d-108">Spark clusters and Jupyter notebooks</span></span>
<span data-ttu-id="da43d-109">安裝程式步驟和 hello 程式碼 toooperationalize ML 模型在本逐步解說提供使用 HDInsight Spark 1.6 叢集，以及 Spark 2.0 叢集的動作。</span><span class="sxs-lookup"><span data-stu-id="da43d-109">Setup steps and hello code toooperationalize an ML model are provided in this walkthrough for using an HDInsight Spark 1.6 cluster as well as a Spark 2.0 cluster.</span></span> <span data-ttu-id="da43d-110">Jupyter 筆記本中，也會提供這些程序的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="da43d-110">hello code for these procedures is also provided in Jupyter notebooks.</span></span>

### <a name="notebook-for-spark-16"></a><span data-ttu-id="da43d-111">Notebook for Spark 1.6</span><span class="sxs-lookup"><span data-stu-id="da43d-111">Notebook for Spark 1.6</span></span>
<span data-ttu-id="da43d-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter 筆記本會顯示如何 toooperationalize 已儲存的模型使用 Python HDInsight 上的叢集。</span><span class="sxs-lookup"><span data-stu-id="da43d-112">hello [pySpark-machine-learning-data-science-spark-model-consumption.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-model-consumption.ipynb) Jupyter notebook shows how toooperationalize a saved model using Python on HDInsight clusters.</span></span> 

### <a name="notebook-for-spark-20"></a><span data-ttu-id="da43d-113">Notebook for Spark 2.0</span><span class="sxs-lookup"><span data-stu-id="da43d-113">Notebook for Spark 2.0</span></span>
<span data-ttu-id="da43d-114">HDInsight Spark 2.0 叢集後，Spark 1.6 toouse toomodify hello Jupyter 筆記本取代 hello Python 程式碼包含檔案[這個檔案](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py)。</span><span class="sxs-lookup"><span data-stu-id="da43d-114">toomodify hello Jupyter notebook for Spark 1.6 toouse with an HDInsight Spark 2.0 cluster, replace hello Python code file with [this file](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Python/Spark2.0_ConsumeRFCV_NYCReg.py).</span></span> <span data-ttu-id="da43d-115">此程式碼會顯示如何在 Spark 2.0 建立 tooconsume hello 模型。</span><span class="sxs-lookup"><span data-stu-id="da43d-115">This code shows how tooconsume hello models created in Spark 2.0.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="da43d-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="da43d-116">Prerequisites</span></span>

1. <span data-ttu-id="da43d-117">您需要 Azure 帳戶和 Spark 1.6 （或 Spark 2.0） HDInsight 叢集 toocomplete 本逐步解說。</span><span class="sxs-lookup"><span data-stu-id="da43d-117">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster toocomplete this walkthrough.</span></span> <span data-ttu-id="da43d-118">請參閱 hello[概觀的資料科學使用 Azure HDInsight 上的 Spark](machine-learning-data-science-spark-overview.md)如需有關指示 toosatisfy 這些需求。</span><span class="sxs-lookup"><span data-stu-id="da43d-118">See hello [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how toosatisfy these requirements.</span></span> <span data-ttu-id="da43d-119">該主題也包含描述 hello NYC 2013 計程車這裡使用的資料以及 tooexecute 來自 Jupyter 筆記本 hello Spark 叢集上的程式碼的相關指示。</span><span class="sxs-lookup"><span data-stu-id="da43d-119">That topic also contains a description of hello NYC 2013 Taxi data used here and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster.</span></span> 
2. <span data-ttu-id="da43d-120">您也必須建立 hello 機器學習模型 toobe 這裡計分工作透過 hello[資料探索和模型使用 Spark](machine-learning-data-science-spark-data-exploration-modeling.md) hello Spark 1.6 叢集或 hello Spark 2.0 筆記型電腦 」 主題。</span><span class="sxs-lookup"><span data-stu-id="da43d-120">You must also create hello machine learning models toobe scored here by working through hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic for hello Spark 1.6 cluster or hello Spark 2.0 notebooks.</span></span> 
3. <span data-ttu-id="da43d-121">hello Spark 2.0 筆記本 hello 分類工作 hello 已知 Airline 準時出發，資料集從 2011年和 2012年的使用額外的資料集。</span><span class="sxs-lookup"><span data-stu-id="da43d-121">hello Spark 2.0 notebooks use an additional data set for hello classification task, hello well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="da43d-122">Hello 中提供的 hello 筆記本與連結 toothem 描述[Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello GitHub 儲存機制包含它們。</span><span class="sxs-lookup"><span data-stu-id="da43d-122">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="da43d-123">此外，hello 程式碼及連結的 hello 筆記本為泛型，應該在任何 Spark 叢集上運作。</span><span class="sxs-lookup"><span data-stu-id="da43d-123">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="da43d-124">如果您未使用 HDInsight Spark，hello 叢集中設定和管理步驟可能稍有不同於這裡所顯示。</span><span class="sxs-lookup"><span data-stu-id="da43d-124">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> 

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="da43d-125">安裝程式： 儲存位置、 程式庫，與 hello 預設 Spark 內容</span><span class="sxs-lookup"><span data-stu-id="da43d-125">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="da43d-126">Spark 是無法 tooread 」 和 「 寫入 tooan Azure 儲存體 Blob (WASB)。</span><span class="sxs-lookup"><span data-stu-id="da43d-126">Spark is able tooread and write tooan Azure Storage Blob (WASB).</span></span> <span data-ttu-id="da43d-127">因此，任何現有的資料儲存於該處可處理使用的 Spark，hello 結果儲存一次在 WASB。</span><span class="sxs-lookup"><span data-stu-id="da43d-127">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="da43d-128">hello 路徑需要正確地指定 toobe toosave 模型或 WASB 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="da43d-128">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="da43d-129">hello 預設容器附加 toohello Spark 叢集，可以使用來參考路徑，開頭： *"wasb / /"*。</span><span class="sxs-lookup"><span data-stu-id="da43d-129">hello default container attached toohello Spark cluster can be referenced using a path beginning with: *"wasb//"*.</span></span> <span data-ttu-id="da43d-130">hello 下列程式碼範例指定 hello 位置 hello 資料 toobe 讀取，並儲存 hello hello 模型儲存體目錄 toowhich hello 模型輸出路徑。</span><span class="sxs-lookup"><span data-stu-id="da43d-130">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved.</span></span> 

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="da43d-131">在 WASB 中設定儲存位置的目錄路徑</span><span class="sxs-lookup"><span data-stu-id="da43d-131">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="da43d-132">模型會儲存在：「wasb:///user/remoteuser/NYCTaxi/Models」。</span><span class="sxs-lookup"><span data-stu-id="da43d-132">Models are saved in: "wasb:///user/remoteuser/NYCTaxi/Models".</span></span> <span data-ttu-id="da43d-133">如果未正確設定此路徑，不會載入模型進行評分。</span><span class="sxs-lookup"><span data-stu-id="da43d-133">If this path is not set properly, models are not loaded for scoring.</span></span>

<span data-ttu-id="da43d-134">hello 計分的結果儲存在:"wasb: / 使用者/remoteuser/NYCTaxi/ScoredResults"。</span><span class="sxs-lookup"><span data-stu-id="da43d-134">hello scored results have been saved in: "wasb:///user/remoteuser/NYCTaxi/ScoredResults".</span></span> <span data-ttu-id="da43d-135">如果 hello 路徑 toofolder 不正確，並不會將結果儲存在該資料夾中。</span><span class="sxs-lookup"><span data-stu-id="da43d-135">If hello path toofolder is incorrect, results are not saved in that folder.</span></span>   

> [!NOTE]
> <span data-ttu-id="da43d-136">hello 檔案路徑位置可以複製及貼上這段程式碼從 hello hello 最後一個儲存格的 hello 輸出中的 hello 預留位置**machine-learning-data-science-spark-data-exploration-modeling.ipynb**筆記型電腦。</span><span class="sxs-lookup"><span data-stu-id="da43d-136">hello file path locations can be copied and pasted into hello placeholders in this code from hello output of hello last cell of hello **machine-learning-data-science-spark-data-exploration-modeling.ipynb** notebook.</span></span>   
> 
> 

<span data-ttu-id="da43d-137">以下是 hello 程式碼 tooset 目錄路徑：</span><span class="sxs-lookup"><span data-stu-id="da43d-137">Here is hello code tooset directory paths:</span></span> 

    # LOCATION OF DATA tooBE SCORED (TEST DATA)
    taxi_test_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Test.tsv";

    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 

    # SET SCORDED RESULT DIRECTORY PATH
    # NOTE hello LAST BACKSLASH IN THIS PATH IS NEEDED
    scoredResultDir = "wasb:///user/remoteuser/NYCTaxi/ScoredResults/"; 

    # FILE LOCATIONS FOR hello MODELS tooBE SCORED
    logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-04-1817_40_35.796789"
    linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-04-1817_44_00.993832"
    randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-04-1817_42_58.899412"
    randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-04-1817_44_27.204734"
    BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-04-1817_43_16.354770"
    BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-04-1817_44_46.206262"

    # RECORD START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="da43d-138">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="da43d-138">**OUTPUT:**</span></span>

<span data-ttu-id="da43d-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span><span class="sxs-lookup"><span data-stu-id="da43d-139">datetime.datetime(2016, 4, 25, 23, 56, 19, 229403)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="da43d-140">匯入程式庫</span><span class="sxs-lookup"><span data-stu-id="da43d-140">Import libraries</span></span>
<span data-ttu-id="da43d-141">設定 spark 內容，並以下列程式碼的 hello 匯入必要的程式庫</span><span class="sxs-lookup"><span data-stu-id="da43d-141">Set spark context and import necessary libraries with hello following code</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="da43d-142">預設 Spark 內容及 PySpark magic</span><span class="sxs-lookup"><span data-stu-id="da43d-142">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="da43d-143">所提供的 Jupyter 筆記本 hello PySpark 核心有預設的內容。</span><span class="sxs-lookup"><span data-stu-id="da43d-143">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="da43d-144">因此您不需要 tooset hello Spark 或登錄區內容明確之前您開始使用您所開發的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="da43d-144">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="da43d-145">依預設會將這些內容提供給您使用。</span><span class="sxs-lookup"><span data-stu-id="da43d-145">These are available for you by default.</span></span> <span data-ttu-id="da43d-146">這些內容包括：</span><span class="sxs-lookup"><span data-stu-id="da43d-146">These contexts are:</span></span>

* <span data-ttu-id="da43d-147">sc - 代表 Spark</span><span class="sxs-lookup"><span data-stu-id="da43d-147">sc - for Spark</span></span> 
* <span data-ttu-id="da43d-148">sqlContext - 代表 Hive</span><span class="sxs-lookup"><span data-stu-id="da43d-148">sqlContext - for Hive</span></span>

<span data-ttu-id="da43d-149">hello PySpark 核心提供一些預先定義 「 我們"，這是特殊的命令，您可以呼叫具有 %%。</span><span class="sxs-lookup"><span data-stu-id="da43d-149">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="da43d-150">在這些程式碼範例中，就使用了兩個此類型的命令。</span><span class="sxs-lookup"><span data-stu-id="da43d-150">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="da43d-151">**%%本機**指定 hello 下來幾行中的程式碼在本機執行。</span><span class="sxs-lookup"><span data-stu-id="da43d-151">**%%local** Specified that hello code in subsequent lines is executed locally.</span></span> <span data-ttu-id="da43d-152">程式碼必須是有效的 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="da43d-152">Code must be valid Python code.</span></span>
* <span data-ttu-id="da43d-153">**%%sql -o <variable name>**</span><span class="sxs-lookup"><span data-stu-id="da43d-153">**%%sql -o <variable name>**</span></span> 
* <span data-ttu-id="da43d-154">執行 Hive 查詢針對 hello sqlContext。</span><span class="sxs-lookup"><span data-stu-id="da43d-154">Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="da43d-155">如果傳遞 hello-o 參數，則 hello hello 查詢結果會持續保留在 hello %%熊資料框架的本機 Python 環境。</span><span class="sxs-lookup"><span data-stu-id="da43d-155">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas dataframe.</span></span>

<span data-ttu-id="da43d-156">針對 Jupyter 筆記本和預先定義的 hello hello 核心上的詳細資訊 」 magics 」，它們提供，請參閱[HDInsight 上的叢集與 HDInsight Spark Linux Jupyter 筆記本的可用的核心](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="da43d-156">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="ingest-data-and-create-a-cleaned-data-frame"></a><span data-ttu-id="da43d-157">擷取資料並建立已清除的資料框架</span><span class="sxs-lookup"><span data-stu-id="da43d-157">Ingest data and create a cleaned data frame</span></span>
<span data-ttu-id="da43d-158">本節包含一系列的工作需要的 tooingest hello 資料 toobe 計分的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="da43d-158">This section contains hello code for a series of tasks required tooingest hello data toobe scored.</span></span> <span data-ttu-id="da43d-159">閱讀聯結 0.1 %hello 計程車行程及價位檔範例 （儲存為.tsv 檔案），將資料格式化 hello，並接著會建立全新的資料框架。</span><span class="sxs-lookup"><span data-stu-id="da43d-159">Read in a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file), format hello data, and then creates a clean data frame.</span></span>

<span data-ttu-id="da43d-160">hello 計程車行程及價位檔案中提供的 hello 程序上聯結基礎: [hello 動作中的資料科學的小組流程： 使用 HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-walkthrough.md)主題。</span><span class="sxs-lookup"><span data-stu-id="da43d-160">hello taxi trip and fare files were joined based on hello procedure provided in the: [hello Team Data Science Process in action: using HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) topic.</span></span>

    # INGEST DATA AND CREATE A CLEANED DATA FRAME

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_test_file = sc.textFile(taxi_test_file_loc)

    # GET SCHEMA OF hello FILE FROM HEADER
    taxi_header = taxi_test_file.filter(lambda l: "medallion" in l)

    # PARSE FIELDS AND CONVERT DATA TYPE FOR SOME FIELDS
    taxi_temp = taxi_test_file.subtract(taxi_header).map(lambda k: k.split("\t"))\
            .map(lambda p: (p[0],p[1],p[2],p[3],p[4],p[5],p[6],int(p[7]),int(p[8]),int(p[9]),int(p[10]),
                            float(p[11]),float(p[12]),p[13],p[14],p[15],p[16],p[17],p[18],float(p[19]),
                            float(p[20]),float(p[21]),float(p[22]),float(p[23]),float(p[24]),int(p[25]),int(p[26])))

    # GET SCHEMA OF hello FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="da43d-161">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="da43d-161">**OUTPUT:**</span></span>

<span data-ttu-id="da43d-162">時間 tooexecute 儲存格上方： 46.37 秒</span><span class="sxs-lookup"><span data-stu-id="da43d-162">Time taken tooexecute above cell: 46.37 seconds</span></span>

## <a name="prepare-data-for-scoring-in-spark"></a><span data-ttu-id="da43d-163">準備資料在 Spark 中評分</span><span class="sxs-lookup"><span data-stu-id="da43d-163">Prepare data for scoring in Spark</span></span>
<span data-ttu-id="da43d-164">本節說明如何 tooindex，編碼，及縮放的用於分類和迴歸 MLlib 監督式學習演算法的類別特徵 tooprepare。</span><span class="sxs-lookup"><span data-stu-id="da43d-164">This section shows how tooindex, encode, and scale categorical features tooprepare them for use in MLlib supervised learning algorithms for classification and regression.</span></span>

### <a name="feature-transformation-index-and-encode-categorical-features-for-input-into-models-for-scoring"></a><span data-ttu-id="da43d-165">功能轉換：索引並編碼分類功能以輸入至模型進行評分。</span><span class="sxs-lookup"><span data-stu-id="da43d-165">Feature transformation: index and encode categorical features for input into models for scoring</span></span>
<span data-ttu-id="da43d-166">此區段會顯示如何 tooindex 類別資料使用`StringIndexer`，並將編碼的功能`OneHotEncoder`輸入 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="da43d-166">This section shows how tooindex categorical data using a `StringIndexer` and encode features with `OneHotEncoder` input into hello models.</span></span>

<span data-ttu-id="da43d-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer)編碼字串資料行標籤 tooa 資料行的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="da43d-167">hello [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) encodes a string column of labels tooa column of label indices.</span></span> <span data-ttu-id="da43d-168">hello 索引標籤的頻率會依據排序。</span><span class="sxs-lookup"><span data-stu-id="da43d-168">hello indices are ordered by label frequencies.</span></span> 

<span data-ttu-id="da43d-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder)標籤索引 tooa 資料行的二進位的向量，使用最多為單一其中一個值的資料行對應。</span><span class="sxs-lookup"><span data-stu-id="da43d-169">hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="da43d-170">這種編碼方式可讓演算法所預期的連續值的功能，例如羅吉斯迴歸，套用 toobe toocategorical 功能。</span><span class="sxs-lookup"><span data-stu-id="da43d-170">This encoding allows algorithms that expect continuous valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

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
    model = stringIndexer.fit(taxi_df_test_with_newFeatures) # Input data-frame is hello cleaned one from above
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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="da43d-171">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="da43d-171">**OUTPUT:**</span></span>

<span data-ttu-id="da43d-172">時間 tooexecute 儲存格上方： 5.37 秒</span><span class="sxs-lookup"><span data-stu-id="da43d-172">Time taken tooexecute above cell: 5.37 seconds</span></span>

### <a name="create-rdd-objects-with-feature-arrays-for-input-into-models"></a><span data-ttu-id="da43d-173">使用功能陣列建立 RDD 物件以輸入至模型</span><span class="sxs-lookup"><span data-stu-id="da43d-173">Create RDD objects with feature arrays for input into models</span></span>
<span data-ttu-id="da43d-174">本章節包含程式碼，說明如何為 RDD tooindex 類別的文字資料物件和一個熱它進行編碼，以便能夠使用的 tootrain 和測試 MLlib 羅吉斯迴歸和樹狀結構為基礎的模型。</span><span class="sxs-lookup"><span data-stu-id="da43d-174">This section contains code that shows how tooindex categorical text data as an RDD object and one-hot encode it so it can be used tootrain and test MLlib logistic regression and tree-based models.</span></span> <span data-ttu-id="da43d-175">hello 索引的資料會儲存在[彈性分散式資料集 (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html)物件。</span><span class="sxs-lookup"><span data-stu-id="da43d-175">hello indexed data is stored in [Resilient Distributed Dataset (RDD)](http://spark.apache.org/docs/latest/api/java/org/apache/spark/rdd/RDD.html) objects.</span></span> <span data-ttu-id="da43d-176">這些是 hello Spark 中的基本抽象概念。</span><span class="sxs-lookup"><span data-stu-id="da43d-176">These are hello basic abstraction in Spark.</span></span> <span data-ttu-id="da43d-177">RDD 物件代表不可變、資料分割、可與 Spark 平行操作的元素集合。</span><span class="sxs-lookup"><span data-stu-id="da43d-177">An RDD object represents an immutable, partitioned collection of elements that can be operated on in parallel with Spark.</span></span>

<span data-ttu-id="da43d-178">它也包含程式碼，示範如何使用 tooscale 資料 hello `StandardScalar` MLlib 所提供用於線性迴歸與隨機梯度下降 (SGD)，常用的演算法來定型各種不同的機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="da43d-178">It also contains code that shows how tooscale data with hello `StandardScalar` provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of machine learning models.</span></span> <span data-ttu-id="da43d-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler)是使用的 tooscale hello 功能 toounit 變異數。</span><span class="sxs-lookup"><span data-stu-id="da43d-179">hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) is used tooscale hello features toounit variance.</span></span> <span data-ttu-id="da43d-180">調整功能，也稱為資料正規化，以確保，功能與廣泛分散的值未授與過多權衡 hello 目標函式。</span><span class="sxs-lookup"><span data-stu-id="da43d-180">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> 

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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="da43d-181">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="da43d-181">**OUTPUT:**</span></span>

<span data-ttu-id="da43d-182">時間 tooexecute 儲存格上方： 11.72 秒</span><span class="sxs-lookup"><span data-stu-id="da43d-182">Time taken tooexecute above cell: 11.72 seconds</span></span>

## <a name="score-with-hello-logistic-regression-model-and-save-output-tooblob"></a><span data-ttu-id="da43d-183">計分以 hello 羅吉斯迴歸模型，並儲存輸出 tooblob</span><span class="sxs-lookup"><span data-stu-id="da43d-183">Score with hello Logistic Regression Model and save output tooblob</span></span>
<span data-ttu-id="da43d-184">本節中的 hello 程式碼顯示如何 tooload 羅吉斯迴歸模型，就已經儲存在 Azure blob 儲存體及在趕赴路線上使用的 toopredict 提示須付費，分數的標準分類度量，然後儲存並繪製 hello 結果 tooblob儲存體。</span><span class="sxs-lookup"><span data-stu-id="da43d-184">hello code in this section shows how tooload a Logistic Regression Model that has been saved in Azure blob storage and use it toopredict whether or not a tip is paid on a taxi trip, score it with standard classification metrics, and then save and plot hello results tooblob storage.</span></span> <span data-ttu-id="da43d-185">hello 計分結果會儲存在 RDD 物件。</span><span class="sxs-lookup"><span data-stu-id="da43d-185">hello scored results are stored in RDD objects.</span></span> 

    # SCORE AND EVALUATE LOGISTIC REGRESSION MODEL

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT LIBRARIES
    from pyspark.mllib.classification import LogisticRegressionModel

    ## LOAD SAVED MODEL
    savedModel = LogisticRegressionModel.load(sc, logisticRegFileLoc)
    predictions = oneHotTESTbinary.map(lambda features: (float(savedModel.predict(features))))

    ## SAVE SCORED RESULTS (RDD) tooBLOB
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    logisticregressionfilename = "LogisticRegressionWithLBFGS_" + datestamp + ".txt";
    dirfilename = scoredResultDir + logisticregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="da43d-186">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="da43d-186">**OUTPUT:**</span></span>

<span data-ttu-id="da43d-187">時間 tooexecute 儲存格上方： 19.22 秒</span><span class="sxs-lookup"><span data-stu-id="da43d-187">Time taken tooexecute above cell: 19.22 seconds</span></span>

## <a name="score-a-linear-regression-model"></a><span data-ttu-id="da43d-188">評分線性迴歸模型</span><span class="sxs-lookup"><span data-stu-id="da43d-188">Score a Linear Regression Model</span></span>
<span data-ttu-id="da43d-189">我們使用[LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain 線性迴歸模型使用隨機梯度下降 (SGD) 的最佳化 toopredict hello 提示數量付費。</span><span class="sxs-lookup"><span data-stu-id="da43d-189">We used [LinearRegressionWithSGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) tootrain a linear regression model using Stochastic Gradient Descent (SGD) for optimization toopredict hello amount of tip paid.</span></span> 

<span data-ttu-id="da43d-190">本節中的 hello 程式碼會示範 tooload 從 Azure blob 儲存體，線性迴歸模型評分使用縮放的變數，然後將儲存 hello 結果後 toohello blob 的方式。</span><span class="sxs-lookup"><span data-stu-id="da43d-190">hello code in this section shows how tooload a Linear Regression Model from Azure blob storage, score using scaled variables, and then save hello results back toohello blob.</span></span>

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

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="da43d-191">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="da43d-191">**OUTPUT:**</span></span>

<span data-ttu-id="da43d-192">時間 tooexecute 儲存格上方： 16.63 秒</span><span class="sxs-lookup"><span data-stu-id="da43d-192">Time taken tooexecute above cell: 16.63 seconds</span></span>

## <a name="score-classification-and-regression-random-forest-models"></a><span data-ttu-id="da43d-193">評分分類和迴歸的隨機樹系模型</span><span class="sxs-lookup"><span data-stu-id="da43d-193">Score classification and regression Random Forest Models</span></span>
<span data-ttu-id="da43d-194">本節中的 hello 程式碼會示範如何 tooload hello 儲存分類和迴歸會儲存 Azure blob 儲存體，隨機樹系模型評分標準的分類和迴歸量值中，其效能，然後將儲存 hello 結果後 tooblob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="da43d-194">hello code in this section shows how tooload hello saved classification and regression Random Forest Models saved in Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span>

<span data-ttu-id="da43d-195">[隨機樹系](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 是整體的決策樹。</span><span class="sxs-lookup"><span data-stu-id="da43d-195">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="da43d-196">結合許多決策樹 tooreduce hello 的風險過度配適。</span><span class="sxs-lookup"><span data-stu-id="da43d-196">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="da43d-197">隨機樹系可以處理類別的功能，擴充 toohello 多級分類設定、 是否需要調整功能，以及可以 toocapture 非線性互動的功能。</span><span class="sxs-lookup"><span data-stu-id="da43d-197">Random forests can handle categorical features, extend toohello multiclass classification setting, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="da43d-198">隨機樹系是其中一種 hello 可以最順利機器學習的分類和迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="da43d-198">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>

<span data-ttu-id="da43d-199">[spark.mllib](http://spark.apache.org/mllib/) 使用連續和分類特徵來支援二元和多元分類和迴歸的隨機樹系。</span><span class="sxs-lookup"><span data-stu-id="da43d-199">[spark.mllib](http://spark.apache.org/mllib/) supports random forests for binary and multiclass classification and for regression, using both continuous and categorical features.</span></span> 

    # SCORE RANDOM FOREST MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES    
    from pyspark.mllib.tree import RandomForest, RandomForestModel


    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfclassificationfilename = "RandomForestClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB
    savedModel = RandomForestModel.load(sc, randomForestRegFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    rfregressionfilename = "RandomForestRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + rfregressionfilename;
    predictions.saveAsTextFile(dirfilename)

    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="da43d-200">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="da43d-200">**OUTPUT:**</span></span>

<span data-ttu-id="da43d-201">時間 tooexecute 儲存格上方： 31.07 秒</span><span class="sxs-lookup"><span data-stu-id="da43d-201">Time taken tooexecute above cell: 31.07 seconds</span></span>

## <a name="score-classification-and-regression-gradient-boosting-tree-models"></a><span data-ttu-id="da43d-202">評分分類和迴歸的漸層停駐提升樹狀結構模型</span><span class="sxs-lookup"><span data-stu-id="da43d-202">Score classification and regression Gradient Boosting Tree Models</span></span>
<span data-ttu-id="da43d-203">本節中的 hello 程式碼顯示如何 tooload 分類和迴歸梯度促進式樹狀模型從 Azure blob 儲存體，評分標準的分類和迴歸量值中，其效能，然後儲存 hello 結果後 tooblob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="da43d-203">hello code in this section shows how tooload classification and regression Gradient Boosting Tree Models from Azure blob storage, score their performance with standard classifier and regression measures, and then save hello results back tooblob storage.</span></span> 

<span data-ttu-id="da43d-204">**spark.mllib** 使用連續和分類特徵來支援二元分類和迴歸的 GBT。</span><span class="sxs-lookup"><span data-stu-id="da43d-204">**spark.mllib** supports GBTs for binary classification and for regression, using both continuous and categorical features.</span></span> 

<span data-ttu-id="da43d-205">[漸層停駐提升樹狀結構](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) 是整體的決策樹。</span><span class="sxs-lookup"><span data-stu-id="da43d-205">[Gradient Boosting Trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="da43d-206">GBTs 定型決策樹反覆 toominimize 損失函數。</span><span class="sxs-lookup"><span data-stu-id="da43d-206">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="da43d-207">GBTs 可以處理類別特徵，不需要調整功能，而且可以 toocapture 非線性互動的功能。</span><span class="sxs-lookup"><span data-stu-id="da43d-207">GBTs can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="da43d-208">它們也可用於多類別分類設定。</span><span class="sxs-lookup"><span data-stu-id="da43d-208">They can also be used in a multiclass-classification setting.</span></span>

    # SCORE GRADIENT BOOSTING TREE MODELS FOR CLASSIFICATION AND REGRESSION

    # RECORD START TIME
    timestart = datetime.datetime.now()

    #IMPORT MLLIB LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # CLASSIFICATION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    #LOAD AND SCORE hello MODEL
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeClassificationFileLoc)
    predictions = savedModel.predict(indexedTESTbinary)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btclassificationfilename = "GradientBoostingTreeClassification_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btclassificationfilename;
    predictions.saveAsTextFile(dirfilename)


    # REGRESSION: LOAD SAVED MODEL, SCORE AND SAVE RESULTS BACK tooBLOB

    # LOAD AND SCORE MODEL 
    savedModel = GradientBoostedTreesModel.load(sc, BoostedTreeRegressionFileLoc)
    predictions = savedModel.predict(indexedTESTreg)

    # SAVE RESULTS
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    btregressionfilename = "GradientBoostingTreeRegression_" + datestamp + ".txt";
    dirfilename = scoredResultDir + btregressionfilename;
    predictions.saveAsTextFile(dirfilename)


    # PRINT HOW MUCH TIME IT TOOK tooRUN hello CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken tooexecute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="da43d-209">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="da43d-209">**OUTPUT:**</span></span>

<span data-ttu-id="da43d-210">時間 tooexecute 儲存格上方： 14.6 秒</span><span class="sxs-lookup"><span data-stu-id="da43d-210">Time taken tooexecute above cell: 14.6 seconds</span></span>

## <a name="clean-up-objects-from-memory-and-print-scored-file-locations"></a><span data-ttu-id="da43d-211">從記憶體清除物件並列印計分的檔案位置</span><span class="sxs-lookup"><span data-stu-id="da43d-211">Clean up objects from memory and print scored file locations</span></span>
    # UNPERSIST OBJECTS CACHED IN MEMORY
    taxi_df_test_cleaned.unpersist()
    indexedTESTbinary.unpersist();
    oneHotTESTbinary.unpersist();
    indexedTESTreg.unpersist();
    oneHotTESTreg.unpersist();
    oneHotTESTregScaled.unpersist();


    # PRINT OUT PATH tooSCORED OUTPUT FILES
    print "logisticRegFileLoc: " + logisticregressionfilename;
    print "linearRegFileLoc: " + linearregressionfilename;
    print "randomForestClassificationFileLoc: " + rfclassificationfilename;
    print "randomForestRegFileLoc: " + rfregressionfilename;
    print "BoostedTreeClassificationFileLoc: " + btclassificationfilename;
    print "BoostedTreeRegressionFileLoc: " + btregressionfilename;


<span data-ttu-id="da43d-212">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="da43d-212">**OUTPUT:**</span></span>

<span data-ttu-id="da43d-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span><span class="sxs-lookup"><span data-stu-id="da43d-213">logisticRegFileLoc: LogisticRegressionWithLBFGS_2016-05-0317_22_38.953814.txt</span></span>

<span data-ttu-id="da43d-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span><span class="sxs-lookup"><span data-stu-id="da43d-214">linearRegFileLoc: LinearRegressionWithSGD_2016-05-0317_22_58.878949</span></span>

<span data-ttu-id="da43d-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span><span class="sxs-lookup"><span data-stu-id="da43d-215">randomForestClassificationFileLoc: RandomForestClassification_2016-05-0317_23_15.939247.txt</span></span>

<span data-ttu-id="da43d-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span><span class="sxs-lookup"><span data-stu-id="da43d-216">randomForestRegFileLoc: RandomForestRegression_2016-05-0317_23_31.459140.txt</span></span>

<span data-ttu-id="da43d-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span><span class="sxs-lookup"><span data-stu-id="da43d-217">BoostedTreeClassificationFileLoc: GradientBoostingTreeClassification_2016-05-0317_23_49.648334.txt</span></span>

<span data-ttu-id="da43d-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span><span class="sxs-lookup"><span data-stu-id="da43d-218">BoostedTreeRegressionFileLoc: GradientBoostingTreeRegression_2016-05-0317_23_56.860740.txt</span></span>

## <a name="consume-spark-models-through-a-web-interface"></a><span data-ttu-id="da43d-219">透過 Web 介面使用 Spark 模型</span><span class="sxs-lookup"><span data-stu-id="da43d-219">Consume Spark Models through a web interface</span></span>
<span data-ttu-id="da43d-220">Spark 提供一個機制，tooremotely 提交批次作業或執行其餘的互動式查詢介面具有名為晚總的元件。</span><span class="sxs-lookup"><span data-stu-id="da43d-220">Spark provides a mechanism tooremotely submit batch jobs or interactive queries through a REST interface with a component called Livy.</span></span> <span data-ttu-id="da43d-221">Livy 預設在 HDInsight Spark 叢集上啟用。</span><span class="sxs-lookup"><span data-stu-id="da43d-221">Livy is enabled by default on your HDInsight Spark cluster.</span></span> <span data-ttu-id="da43d-222">如需 Livy 的詳細資訊，請參閱 [使用 Livy 遠端提交 Spark 作業](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md)。</span><span class="sxs-lookup"><span data-stu-id="da43d-222">For more information on Livy, see: [Submit Spark jobs remotely using Livy](../hdinsight/hdinsight-apache-spark-livy-rest-interface.md).</span></span> 

<span data-ttu-id="da43d-223">您可以使用晚總 tooremotely 提交的批次分數的工作檔案儲存在 Azure blob，然後將 hello 結果 tooanother blob。</span><span class="sxs-lookup"><span data-stu-id="da43d-223">You can use Livy tooremotely submit a job that batch scores a file that is stored in an Azure blob and then writes hello results tooanother blob.</span></span> <span data-ttu-id="da43d-224">toodo，您上傳從 hello Python 指令碼</span><span class="sxs-lookup"><span data-stu-id="da43d-224">toodo this, you upload hello Python script from</span></span>  
<span data-ttu-id="da43d-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob 的 hello Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="da43d-225">[GitHub](https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/Spark/Python/ConsumeGBNYCReg.py) toohello blob of hello Spark cluster.</span></span> <span data-ttu-id="da43d-226">您可以使用這類工具**Microsoft Azure 儲存體總管**或**AzCopy** toocopy hello 指令碼 toohello 叢集 blob。</span><span class="sxs-lookup"><span data-stu-id="da43d-226">You can use a tool like **Microsoft Azure Storage Explorer** or **AzCopy** toocopy hello script toohello cluster blob.</span></span> <span data-ttu-id="da43d-227">在我們的案例我們上傳 hello 指令碼太***wasb:///example/python/ConsumeGBNYCReg.py***。</span><span class="sxs-lookup"><span data-stu-id="da43d-227">In our case we uploaded hello script too***wasb:///example/python/ConsumeGBNYCReg.py***.</span></span>   

> [!NOTE]
> <span data-ttu-id="da43d-228">hello 您需要可以找到 hello 與 hello Spark 叢集相關聯的儲存體帳戶的 hello 入口網站的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="da43d-228">hello access keys that you need can be found on hello portal for hello storage account associated with hello Spark cluster.</span></span> 
> 
> 

<span data-ttu-id="da43d-229">一旦上傳 toothis 位置，則會在分散式的內容中的 hello Spark 叢集內執行這個指令碼。</span><span class="sxs-lookup"><span data-stu-id="da43d-229">Once uploaded toothis location, this script runs within hello Spark cluster in a distributed context.</span></span> <span data-ttu-id="da43d-230">它會載入 hello 模型，並輸入 hello 模型為基礎的檔案上執行預測。</span><span class="sxs-lookup"><span data-stu-id="da43d-230">It loads hello model and runs predictions on input files based on hello model.</span></span>  

<span data-ttu-id="da43d-231">您可以在 Livy 上進行簡單的 HTTPS/REST 要求，從遠端叫用此指令碼。</span><span class="sxs-lookup"><span data-stu-id="da43d-231">You can invoke this script remotely by making a simple HTTPS/REST request on Livy.</span></span>  <span data-ttu-id="da43d-232">以下是從遠端 curl 命令 tooconstruct hello HTTP 要求 tooinvoke hello Python 指令碼。</span><span class="sxs-lookup"><span data-stu-id="da43d-232">Here is a curl command tooconstruct hello HTTP request tooinvoke hello Python script remotely.</span></span> <span data-ttu-id="da43d-233">CLUSTERLOGIN、 CLUSTERPASSWORD、 CLUSTERNAME 取代 hello 適當的值，為您的 Spark 叢集。</span><span class="sxs-lookup"><span data-stu-id="da43d-233">Replace CLUSTERLOGIN, CLUSTERPASSWORD, CLUSTERNAME with hello appropriate values for your Spark cluster.</span></span>

    # CURL COMMAND tooINVOKE PYTHON SCRIPT WITH HTTP REQUEST

    curl -k --user "CLUSTERLOGIN:CLUSTERPASSWORD" -X POST --data "{\"file\": \"wasb:///example/python/ConsumeGBNYCReg.py\"}" -H "Content-Type: application/json" https://CLUSTERNAME.azurehdinsight.net/livy/batches

<span data-ttu-id="da43d-234">您可以使用 hello 遠端系統 tooinvoke hello Spark 作業透過晚總上的任何語言進行簡單的 HTTPS 呼叫以基本驗證。</span><span class="sxs-lookup"><span data-stu-id="da43d-234">You can use any language on hello remote system tooinvoke hello Spark job through Livy by making a simple HTTPS call with Basic Authentication.</span></span>   

> [!NOTE]
> <span data-ttu-id="da43d-235">很方便 toouse hello Python 要求程式庫時進行這個 HTTP 呼叫，但是它目前未安裝預設會在 Azure 函式。</span><span class="sxs-lookup"><span data-stu-id="da43d-235">It would be convenient toouse hello Python Requests library when making this HTTP call, but it is not currently installed by default in Azure Functions.</span></span> <span data-ttu-id="da43d-236">因此會改用較舊的 HTTP 程式庫。</span><span class="sxs-lookup"><span data-stu-id="da43d-236">So older HTTP libraries are used instead.</span></span>   
> 
> 

<span data-ttu-id="da43d-237">Hello HTTP 呼叫的 hello Python 程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="da43d-237">Here is hello Python code for hello HTTP call:</span></span>

    #MAKE AN HTTPS CALL ON LIVY. 

    import os

    # OLDER HTTP LIBRARIES USED HERE INSTEAD OF hello REQUEST LIBRARY AS THEY ARE AVAILBLE BY DEFAULT
    import httplib, urllib, base64

    # REPLACE VALUE WITH ONES FOR YOUR SPARK CLUSTER
    host = '<spark cluster name>.azurehdinsight.net:443'
    username='<username>'
    password='<password>'

    #AUTHORIZATION
    conn = httplib.HTTPSConnection(host)
    auth = base64.encodestring('%s:%s' % (username, password)).replace('\n', '')
    headers = {'Content-Type': 'application/json', 'Authorization': 'Basic %s' % auth}

    # SPECIFY hello PYTHON SCRIPT tooRUN ON hello SPARK CLUSTER
    # IN hello FILE PARAMETER OF hello JSON POST REQUEST BODY
    r=conn.request("POST", '/livy/batches', '{"file": "wasb:///example/python/ConsumeGBNYCReg.py"}', headers )
    response = conn.getresponse().read()
    print(response)
    conn.close()


<span data-ttu-id="da43d-238">您也可以過加入此 Python 程式碼[Azure 函式](https://azure.microsoft.com/documentation/services/functions/)tootrigger 分數 blob Spark 工作提交根據各種事件，像是計時器、 建立或更新的 blob。</span><span class="sxs-lookup"><span data-stu-id="da43d-238">You can also add this Python code too[Azure Functions](https://azure.microsoft.com/documentation/services/functions/) tootrigger a Spark job submission that scores a blob based on various events like a timer, creation, or update of a blob.</span></span> 

<span data-ttu-id="da43d-239">如果您偏好的程式碼可用的用戶端體驗，請使用 hello [Azure 邏輯應用程式](https://azure.microsoft.com/documentation/services/app-service/logic/)tooinvoke hello Spark 批次計分藉由定義 HTTP 動作上 hello**邏輯應用程式設計師**並設定它的參數。</span><span class="sxs-lookup"><span data-stu-id="da43d-239">If you prefer a code free client experience, use hello [Azure Logic Apps](https://azure.microsoft.com/documentation/services/app-service/logic/) tooinvoke hello Spark batch scoring by defining an HTTP action on hello **Logic Apps Designer** and setting its parameters.</span></span> 

* <span data-ttu-id="da43d-240">在 Azure 入口網站中，選取 [+ 新增]  ->  [Web + 行動 ]  ->  [邏輯應用程式] 來建立新的邏輯應用程式。</span><span class="sxs-lookup"><span data-stu-id="da43d-240">From Azure portal, create a new Logic App by selecting **+New** -> **Web + Mobile** -> **Logic App**.</span></span> 
* <span data-ttu-id="da43d-241">向上 hello toobring**邏輯應用程式設計師**，輸入 hello hello 邏輯應用程式名稱和應用程式服務方案。</span><span class="sxs-lookup"><span data-stu-id="da43d-241">toobring up hello **Logic Apps Designer**, enter hello name of hello Logic App and App Service Plan.</span></span>
* <span data-ttu-id="da43d-242">選取 HTTP 動作，然後輸入 hello 參數 hello 遵循圖所示：</span><span class="sxs-lookup"><span data-stu-id="da43d-242">Select an HTTP action and enter hello parameters shown in hello following figure:</span></span>

![Logic Apps 設計工具](./media/machine-learning-data-science-spark-model-consumption/spark-logica-app-client.png)

## <a name="whats-next"></a><span data-ttu-id="da43d-244">後續步驟</span><span class="sxs-lookup"><span data-stu-id="da43d-244">What's next?</span></span>
<span data-ttu-id="da43d-245">**交叉驗證和超參數掃掠**：如需如何使用交叉驗證和超參數掃掠訓練模型的相關資訊，請參閱 [使用 Spark 進階資料探索和模型化](machine-learning-data-science-spark-advanced-data-exploration-modeling.md)</span><span class="sxs-lookup"><span data-stu-id="da43d-245">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>

