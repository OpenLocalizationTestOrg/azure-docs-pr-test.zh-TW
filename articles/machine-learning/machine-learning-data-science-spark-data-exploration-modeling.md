---
title: "使用 Spark 資料探索和模型化 | Microsoft Docs"
description: "展示了 Azure 上 Spark MLlib 工具組的資料探索和模型化功能。"
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
ms.openlocfilehash: 711407f7dd9e6d442e3f04a23962487f4808e8e2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="091a7-103">使用 Spark 資料探索和模型化</span><span class="sxs-lookup"><span data-stu-id="091a7-103">Data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="091a7-104">本逐步解說會使用 HDInsight Spark，在 NYC 計程車車程和費用 2013 資料集上執行資料探索和二進位分類和迴歸模型化。</span><span class="sxs-lookup"><span data-stu-id="091a7-104">This walkthrough uses HDInsight Spark to do data exploration and binary classification and regression modeling tasks on a sample of the NYC taxi trip and fare 2013 dataset.</span></span>  <span data-ttu-id="091a7-105">它將引導您逐步完成 [資料科學程序](http://aka.ms/datascienceprocess)、端對端、使用 HDInsight Spark 叢集處理，並使用 Azure blob 來儲存資料和模型。</span><span class="sxs-lookup"><span data-stu-id="091a7-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="091a7-106">程序會探索和視覺化從 Azure 儲存體 Blob 中引進的資料，然後準備資料來建立預測模型。</span><span class="sxs-lookup"><span data-stu-id="091a7-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="091a7-107">這些模型是使用 Spark MLlib 工具組來執行二進位分類和迴歸模型工作。</span><span class="sxs-lookup"><span data-stu-id="091a7-107">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span>

* <span data-ttu-id="091a7-108">**二進位分類** 工作可預測是否已支付某趟車程的小費。</span><span class="sxs-lookup"><span data-stu-id="091a7-108">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="091a7-109">**迴歸** 工作可根據其他小費功能來預測小費金額。</span><span class="sxs-lookup"><span data-stu-id="091a7-109">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="091a7-110">我們使用的模型包括羅吉斯和線性迴歸、隨機樹系和漸層停駐推進式決策樹︰</span><span class="sxs-lookup"><span data-stu-id="091a7-110">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="091a7-111">[使用 SGD 的線性迴歸](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) 是一種使用隨機梯度下降 (SGD) 方法的線性迴歸模型，並使用最佳化和功能縮放比例來預測支付的小費金額。</span><span class="sxs-lookup"><span data-stu-id="091a7-111">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="091a7-112">[使用 LBFGS 的羅吉斯迴歸](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) 或「對數優劣比」迴歸是使用相依變數來執行資料分類時，可使用的迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="091a7-112">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="091a7-113">LBFGS 是牛頓最佳化演算法，可使用有限的電腦記憶體量來逼近 Broyden–Fletcher–Goldfarb–Shanno (BFGS) 演算法，且廣泛用於機器學習中。</span><span class="sxs-lookup"><span data-stu-id="091a7-113">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="091a7-114">[隨機樹系](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 是整體的決策樹。</span><span class="sxs-lookup"><span data-stu-id="091a7-114">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="091a7-115">隨機樹系結合許多決策樹來降低風險過度膨脹。</span><span class="sxs-lookup"><span data-stu-id="091a7-115">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="091a7-116">隨機樹系適用於迴歸和分類，可處理分類功能，也可擴充至多類別分類設定。</span><span class="sxs-lookup"><span data-stu-id="091a7-116">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="091a7-117">隨機樹系不需要調整功能，而且能夠擷取非線性和功能互動。</span><span class="sxs-lookup"><span data-stu-id="091a7-117">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="091a7-118">隨機樹系是其中一個最成功的分類和迴歸的機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="091a7-118">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="091a7-119">[漸層停駐推進式決策樹](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) 是整體的決策樹。</span><span class="sxs-lookup"><span data-stu-id="091a7-119">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="091a7-120">GBT 反覆地訓練決策樹以盡可能降低遺失函式。</span><span class="sxs-lookup"><span data-stu-id="091a7-120">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="091a7-121">GBT 適用於迴歸和分類，並可處理分類功能、不需要調整功能，而且能夠擷取非線性和功能互動。</span><span class="sxs-lookup"><span data-stu-id="091a7-121">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="091a7-122">它們也可用於多類別分類設定。</span><span class="sxs-lookup"><span data-stu-id="091a7-122">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="091a7-123">模型化步驟也包含程式碼來示範如何定型、評估和儲存每類模型。</span><span class="sxs-lookup"><span data-stu-id="091a7-123">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="091a7-124">已使用 Python 來編寫解決方案程式碼，並顯示相關的繪圖。</span><span class="sxs-lookup"><span data-stu-id="091a7-124">Python has been used to code the solution and to show the relevant plots.</span></span>   

> [!NOTE]
> <span data-ttu-id="091a7-125">雖然 Spark MLlib 工具組設計成可處理大型資料集，在這裡為了簡便我們使用極小的範例 (使用 170 個資料列，原始的 NYC 資料集約 0.1%，~30 Mb)。</span><span class="sxs-lookup"><span data-stu-id="091a7-125">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="091a7-126">此處提供的練習有效地在含有 2 個背景工作節點的 HDInsight 叢集上執行 (大約 10 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="091a7-126">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="091a7-127">相同的程式碼中 (稍加修改) 可以用來處理大型資料集，適當修改的程式碼則可快取記憶體的資料以及變更叢集大小。</span><span class="sxs-lookup"><span data-stu-id="091a7-127">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="091a7-128">必要條件</span><span class="sxs-lookup"><span data-stu-id="091a7-128">Prerequisites</span></span>
<span data-ttu-id="091a7-129">您需要 Azure 帳戶和 Spark 1.6 (或 Spark 2.0) HDInsight 叢集，才能完成此逐步解說。</span><span class="sxs-lookup"><span data-stu-id="091a7-129">You need an Azure account and a Spark 1.6 (or Spark 2.0) HDInsight cluster to complete this walkthrough.</span></span> <span data-ttu-id="091a7-130">請參閱[使用 Azure HDInsight 上的 Spark 的資料科學概觀](machine-learning-data-science-spark-overview.md)以取得這些需求。</span><span class="sxs-lookup"><span data-stu-id="091a7-130">See the [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) for instructions on how to satisfy these requirements.</span></span> <span data-ttu-id="091a7-131">此主題也包括這裡使用的 NYC 2013 計程車資料的描述，以及如何從 Spark 叢集的 Jupyter Notebook 執行程式碼的指示。</span><span class="sxs-lookup"><span data-stu-id="091a7-131">That topic also contains a description of the NYC 2013 Taxi data used here and instructions on how to execute code from a Jupyter notebook on the Spark cluster.</span></span> 

## <a name="spark-clusters-and-notebooks"></a><span data-ttu-id="091a7-132">Spark 叢集和 Notebook</span><span class="sxs-lookup"><span data-stu-id="091a7-132">Spark clusters and notebooks</span></span>
<span data-ttu-id="091a7-133">此逐步解說所提供的設定步驟和程式碼適用於使用 HDInsight Spark 1.6。</span><span class="sxs-lookup"><span data-stu-id="091a7-133">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="091a7-134">不過 Jupyter Notebook 可供 HDInsight Spark 1.6 版和 Spark 2.0 叢集兩者使用。</span><span class="sxs-lookup"><span data-stu-id="091a7-134">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="091a7-135">Notebook 的描述及它們的連結已在包含它們的 GitHub 儲存機制的 [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) 中提供。</span><span class="sxs-lookup"><span data-stu-id="091a7-135">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="091a7-136">此外，此處及連結的 Notebook 內的程式碼皆屬泛型程式碼，而且應該能在任何 Spark 叢集上運作。</span><span class="sxs-lookup"><span data-stu-id="091a7-136">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="091a7-137">若您不是使用 HDInsight Spark，叢集設定和管理步驟可能與這裡顯示的稍有不同。</span><span class="sxs-lookup"><span data-stu-id="091a7-137">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="091a7-138">為了方便起見，以下是可讓 Spark 1.6 版 (在 Jupyter Notebook 伺服器的 pySpark 核心中執行) 和 Spark 2.0 版 (在 Jupyter Notebook 伺服器的 pySpark3 核心中執行) 的 Jupyter Notebook 連結：</span><span class="sxs-lookup"><span data-stu-id="091a7-138">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 (to be run in the pySpark kernel of the Jupyter Notebook server) and  Spark 2.0 (to be run in the pySpark3 kernel of the Jupyter Notebook server):</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="091a7-139">Spark 1.6 Notebook</span><span class="sxs-lookup"><span data-stu-id="091a7-139">Spark 1.6 notebooks</span></span>

<span data-ttu-id="091a7-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb)：提供如何利用數個不同的演算法來執行資料瀏覽、模型化和評分的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="091a7-140">[pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark1.6/pySpark-machine-learning-data-science-spark-data-exploration-modeling.ipynb): Provides information on how to perform data exploration, modeling, and scoring with several different algorithms.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="091a7-141">Spark 2.0 Notebook</span><span class="sxs-lookup"><span data-stu-id="091a7-141">Spark 2.0 notebooks</span></span>
<span data-ttu-id="091a7-142">使用 Spark 2.0 叢集實作的迴歸和分類工作位於不同的 Notebook，且分類 Notebook 會使用不同的資料集︰</span><span class="sxs-lookup"><span data-stu-id="091a7-142">The regression and classification tasks that are implemented using a Spark 2.0 cluster are in separate notebooks and the classification notebook uses a different data set:</span></span>

- <span data-ttu-id="091a7-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)：此檔案使用在[這裡](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data)描述的 NYC 計程車車程和費用資料集，提供如何在 Spark 2.0 叢集中執行資料瀏覽、模型化和評分的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="091a7-143">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span> <span data-ttu-id="091a7-144">Notebook 可能是很好的起點，可快速瀏覽我們針對 Spark 2.0 所提供的程式碼。</span><span class="sxs-lookup"><span data-stu-id="091a7-144">This notebook may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> <span data-ttu-id="091a7-145">如需更多分析 NYC 計程車資料的 Notebook 詳細資訊，請參閱這份清單中的下一個 Notebook。</span><span class="sxs-lookup"><span data-stu-id="091a7-145">For a more detailed notebook analyzes the NYC Taxi data, see the next notebook in this list.</span></span> <span data-ttu-id="091a7-146">請參閱此清單之後比較這些 Notebook 的附註。</span><span class="sxs-lookup"><span data-stu-id="091a7-146">See the notes following this list that compare these notebooks.</span></span> 
- <span data-ttu-id="091a7-147">[Spark2.0 pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb)：這個檔案會顯示如何使用[這裡](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data)所述的 NYC 計程車車程和費用資料集，執行資料爭議 (Spark SQL 和資料框架作業)、瀏覽、模型化和評分。</span><span class="sxs-lookup"><span data-stu-id="091a7-147">[Spark2.0-pySpark3_NYC_Taxi_Tip_Regression.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_NYC_Taxi_Tip_Regression.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the NYC Taxi trip and fare data-set described [here](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-data-science-spark-overview#the-nyc-2013-taxi-data).</span></span>
- <span data-ttu-id="091a7-148">[Spark2.0 pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb)：這個檔案會顯示如何使用已知的 2011 年和 2012 年航班準時出發資料集，執行資料爭議 (Spark SQL 和資料框架作業)、瀏覽、模型化和評分。</span><span class="sxs-lookup"><span data-stu-id="091a7-148">[Spark2.0-pySpark3_Airline_Departure_Delay_Classification.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0_pySpark3_Airline_Departure_Delay_Classification.ipynb): This file shows how to perform data wrangling (Spark SQL and dataframe operations), exploration, modeling and scoring using the well-known Airline On-time departure dataset from 2011 and 2012.</span></span> <span data-ttu-id="091a7-149">我們在模型化之前將航班資料集與機場天氣資料 (例如風速、溫度、高度等等) 整合，因此可以在模型中包含這些天氣功能。</span><span class="sxs-lookup"><span data-stu-id="091a7-149">We integrated the airline dataset with the airport weather data (e.g. windspeed, temperature, altitude etc.) prior to modeling, so these weather features can be included in the model.</span></span>

<!-- -->

> [!NOTE]
> <span data-ttu-id="091a7-150">Spark 2.0 Notebook 中新增了航班資料集，以更清楚地說明使用的分類演算法。</span><span class="sxs-lookup"><span data-stu-id="091a7-150">The airline dataset was added to the Spark 2.0 notebooks to better illustrate the use of classification algorithms.</span></span> <span data-ttu-id="091a7-151">請參閱下列連結，以取得航班準時出發資料集和天氣資料集的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="091a7-151">See the following links for information about airline on-time departure dataset and weather dataset:</span></span>

>- <span data-ttu-id="091a7-152">航班準時出發資料：[http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span><span class="sxs-lookup"><span data-stu-id="091a7-152">Airline on-time departure data: [http://www.transtats.bts.gov/ONTIME/](http://www.transtats.bts.gov/ONTIME/)</span></span>

>- <span data-ttu-id="091a7-153">機場天氣資料：[https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span><span class="sxs-lookup"><span data-stu-id="091a7-153">Airport weather data: [https://www.ncdc.noaa.gov/](https://www.ncdc.noaa.gov/)</span></span> 
> 
> 

<!-- -->

<!-- -->

> [!NOTE]
<span data-ttu-id="091a7-154">NYC 計程車和飛行航班延遲資料集上的 Spark 2.0 Notebook 需要 10 分鐘或更久 (取決於 HDI 叢集的大小) 才能執行。</span><span class="sxs-lookup"><span data-stu-id="091a7-154">The Spark 2.0 notebooks on the NYC taxi and airline flight delay data-sets can take 10 mins or more to run (depending on the size of your HDI cluster).</span></span> <span data-ttu-id="091a7-155">上述清單中的第一個 Notebook 說明 Notebook 中許多層面的資料瀏覽、視覺效果和 ML 模型訓練，會使用向下取樣 NYC 資料集以較短時間執行，其中計程車和車資檔案已預先聯結︰[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)此 Notebook 會採用較短的時間來完成 (2-3 分鐘)，並可能是快速瀏覽我們針對 Spark 2.0 所提供之程式碼的一個良好起點。</span><span class="sxs-lookup"><span data-stu-id="091a7-155">The first notebook in the above list shows many aspects of the data exploration, visualization and ML model training in a notebook that takes less time to run with down-sampled NYC data set, in which the taxi and fare files have been pre-joined: [Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb) This notebook takes a much shorter time to finish (2-3 mins) and may be a good starting point for quickly exploring the code we have provided for Spark 2.0.</span></span> 

<!-- -->

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<!-- -->

> [!NOTE]
<span data-ttu-id="091a7-156">以下說明與使用 Spark 1.6 有關。</span><span class="sxs-lookup"><span data-stu-id="091a7-156">The descriptions below are related to using Spark 1.6.</span></span> <span data-ttu-id="091a7-157">對於 Spark 2.0 版本，請使用上方說明和連結的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="091a7-157">For Spark 2.0 versions, please use the notebooks described and linked above.</span></span> 

<!-- -->

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="091a7-158">安裝程式︰儲存體位置、程式庫和預設 Spark 內容</span><span class="sxs-lookup"><span data-stu-id="091a7-158">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="091a7-159">Spark 可以讀取和寫入 Azure 儲存體 Blob (也稱為 WASB)。</span><span class="sxs-lookup"><span data-stu-id="091a7-159">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="091a7-160">如此可使用 Spark 處理該處儲存的任何現有資料，並在 WASB 中再次儲存結果。</span><span class="sxs-lookup"><span data-stu-id="091a7-160">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="091a7-161">若要在 WASB 中儲存模型或檔案，必須正確指定路徑。</span><span class="sxs-lookup"><span data-stu-id="091a7-161">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="091a7-162">可以使用以「wasb:///」開頭的路徑，參考連接到 Spark 叢集的預設容器。</span><span class="sxs-lookup"><span data-stu-id="091a7-162">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="091a7-163">其他位置由「wasb://」參考。</span><span class="sxs-lookup"><span data-stu-id="091a7-163">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="091a7-164">在 WASB 中設定儲存位置的目錄路徑</span><span class="sxs-lookup"><span data-stu-id="091a7-164">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="091a7-165">下列程式碼範例會指定要讀取資料的位置，和將儲存模型輸出的模型儲存體目錄的路徑：</span><span class="sxs-lookup"><span data-stu-id="091a7-165">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";

    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/" 


### <a name="import-libraries"></a><span data-ttu-id="091a7-166">匯入程式庫</span><span class="sxs-lookup"><span data-stu-id="091a7-166">Import libraries</span></span>
<span data-ttu-id="091a7-167">安裝程式也需要匯入必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="091a7-167">Set up also requires importing necessary libraries.</span></span> <span data-ttu-id="091a7-168">使用下列程式碼設定 Spark 內容並匯入必要的程式庫：</span><span class="sxs-lookup"><span data-stu-id="091a7-168">Set spark context and import necessary libraries with the following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="091a7-169">預設 Spark 內容及 PySpark magic</span><span class="sxs-lookup"><span data-stu-id="091a7-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="091a7-170">Jupyter Notebook 所提供的 PySpark 核心有預設的內容。</span><span class="sxs-lookup"><span data-stu-id="091a7-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="091a7-171">因此您不必明確設定 Spark 或 Hive 內容，就能開始使用您所開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="091a7-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="091a7-172">依預設會將這些內容提供給您使用。</span><span class="sxs-lookup"><span data-stu-id="091a7-172">These contexts are available for you by default.</span></span> <span data-ttu-id="091a7-173">這些內容包括：</span><span class="sxs-lookup"><span data-stu-id="091a7-173">These contexts are:</span></span>

* <span data-ttu-id="091a7-174">sc - 代表 Spark</span><span class="sxs-lookup"><span data-stu-id="091a7-174">sc - for Spark</span></span> 
* <span data-ttu-id="091a7-175">sqlContext - 代表 Hive</span><span class="sxs-lookup"><span data-stu-id="091a7-175">sqlContext - for Hive</span></span>

<span data-ttu-id="091a7-176">PySpark 核心提供一些預先定義的「magic」，這是您可以使用 %% 呼叫的特殊命令。</span><span class="sxs-lookup"><span data-stu-id="091a7-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="091a7-177">在這些程式碼範例中，就使用了兩個此類型的命令。</span><span class="sxs-lookup"><span data-stu-id="091a7-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="091a7-178">**%%local** 指定後續行所列的程式碼要在本機執行。</span><span class="sxs-lookup"><span data-stu-id="091a7-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="091a7-179">程式碼必須是有效的 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="091a7-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="091a7-180">**%%sql -o <variable name>** 會針對 sqlContext 執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="091a7-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="091a7-181">如果傳遞 -o 參數，則查詢的結果會當做 Pandas 資料框架，保存在 %%local Python 內容中。</span><span class="sxs-lookup"><span data-stu-id="091a7-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="091a7-182">如需關於 Jupyter Notebook 核心，以及其所提供的預先定義 "magics" 的詳細資訊，請參閱 [HDInsight 上的 HDInsight Spark Linux 叢集可供 Jupyter Notebook 使用的核心](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="091a7-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="091a7-183">來自公用 Blob 的資料擷取</span><span class="sxs-lookup"><span data-stu-id="091a7-183">Data ingestion from public blob</span></span>
<span data-ttu-id="091a7-184">資料科學程序的第一個步驟，是將要分析的資料從其來源位置內嵌到您的資料探索和模型化環境。</span><span class="sxs-lookup"><span data-stu-id="091a7-184">The first step in the data science process is to ingest the data to be analyzed from sources where is resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="091a7-185">在本逐步解說中環境是 Spark。</span><span class="sxs-lookup"><span data-stu-id="091a7-185">The environment is Spark in this walkthrough.</span></span> <span data-ttu-id="091a7-186">本節包含程式碼來完成一系列的工作︰</span><span class="sxs-lookup"><span data-stu-id="091a7-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="091a7-187">擷取要模型化的資料範例</span><span class="sxs-lookup"><span data-stu-id="091a7-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="091a7-188">在輸入資料集中讀取 (儲存為 .tsv 檔案)</span><span class="sxs-lookup"><span data-stu-id="091a7-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="091a7-189">格式化和清除資料</span><span class="sxs-lookup"><span data-stu-id="091a7-189">format and clean the data</span></span>
* <span data-ttu-id="091a7-190">建立並快取記憶體中的物件 (RDD 或資料框架)</span><span class="sxs-lookup"><span data-stu-id="091a7-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="091a7-191">將它註冊為 SQL 內容中的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="091a7-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="091a7-192">以下是資料擷取的程式碼。</span><span class="sxs-lookup"><span data-stu-id="091a7-192">Here is the code for data ingestion.</span></span>

    # INGEST DATA

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # IMPORT FILE FROM PUBLIC BLOB
    taxi_train_file = sc.textFile(taxi_train_file_loc)

    # GET SCHEMA OF THE FILE FROM HEADER
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

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="091a7-193">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-193">**OUTPUT:**</span></span>

<span data-ttu-id="091a7-194">執行上述儲存格所花費的時間︰51.72 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-194">Time taken to execute above cell: 51.72 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="091a7-195">資料探索和虛擬化</span><span class="sxs-lookup"><span data-stu-id="091a7-195">Data exploration & visualization</span></span>
<span data-ttu-id="091a7-196">一旦將資料引進 Spark，資料科學程序的下一個步驟是透過探索和虛擬化以更深入瞭解資料。</span><span class="sxs-lookup"><span data-stu-id="091a7-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="091a7-197">在本節中，我們會使用 SQL 查詢檢查計程車資料，並繪製目標變數和潛在功能以進行視覺檢查。</span><span class="sxs-lookup"><span data-stu-id="091a7-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="091a7-198">具體來說，我們會繪製計程車車程中的乘客計數頻率、小費金額的頻率，及小費如何隨付款金額和類型而異。</span><span class="sxs-lookup"><span data-stu-id="091a7-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="091a7-199">在計程車車程範例中繪製乘客計數頻率的長條圖</span><span class="sxs-lookup"><span data-stu-id="091a7-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="091a7-200">此程式碼與後續程式碼片段使用了 SQL magic 來查詢範例及本機 magic 以繪製資料。</span><span class="sxs-lookup"><span data-stu-id="091a7-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="091a7-201">**SQL magic (`%%sql`)** HDInsight PySpark 核心支援針對 sqlContext 進行簡單的內嵌 HiveQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="091a7-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="091a7-202">「-o VARIABLE_NAME」引數會將 SQL 查詢的輸出，保存為 Jupyter 伺服器上的 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="091a7-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="091a7-203">這代表會在本機模式中使用此引數。</span><span class="sxs-lookup"><span data-stu-id="091a7-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="091a7-204">**`%%local` magic** 是用來在 Jupyter 伺服器本機 (HDInsight 叢集的前端節點) 上執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="091a7-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="091a7-205">通常您會使用 `%%local` magic 來搭配含有 -o 參數的 `%%sql` magic。</span><span class="sxs-lookup"><span data-stu-id="091a7-205">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with -o parameter.</span></span> <span data-ttu-id="091a7-206">-o 參數會保存本機 SQL 查詢的輸出，然後 %%local magic 會針對已保存在本機上的 SQL 查詢輸出，觸發下一組要在本機上執行的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="091a7-206">The -o parameter would persist the output of the SQL query locally and then %%local magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally</span></span>

<span data-ttu-id="091a7-207">執行完程式碼後，輸出將會自動以視覺化方式呈現。</span><span class="sxs-lookup"><span data-stu-id="091a7-207">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="091a7-208">此查詢會擷取按乘客計數排列的車程。</span><span class="sxs-lookup"><span data-stu-id="091a7-208">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # HIVEQL QUERY AGAINST THE sqlContext
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts 
    FROM taxi_train 
    WHERE passenger_count > 0 and passenger_count < 7 
    GROUP BY passenger_count 

<span data-ttu-id="091a7-209">此程式碼從查詢輸出中建立了本機資料框架，以及繪製資料。</span><span class="sxs-lookup"><span data-stu-id="091a7-209">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="091a7-210">`%%local` magic 建立了本機資料框架「`sqlResults`」，可用於搭配 Matplotlib 進行繪製。</span><span class="sxs-lookup"><span data-stu-id="091a7-210">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="091a7-211">在本逐步解說中，會多次使用此 PySpark magic。</span><span class="sxs-lookup"><span data-stu-id="091a7-211">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="091a7-212">如果資料總量很大，您應該取樣以建立可容納於本機記憶體的資料框架。</span><span class="sxs-lookup"><span data-stu-id="091a7-212">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    #CREATE LOCAL DATA-FRAME AND USE FOR MATPLOTLIB PLOTTING

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="091a7-213">以下是繪製按乘客計數排列車程的程式碼</span><span class="sxs-lookup"><span data-stu-id="091a7-213">Here is the code to plot the trips by passenger counts</span></span>

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

<span data-ttu-id="091a7-214">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-214">**OUTPUT:**</span></span>

![按乘客計數排列的車程頻率](./media/machine-learning-data-science-spark-data-exploration-modeling/trip-freqency-by-passenger-count.png)

<span data-ttu-id="091a7-216">在 Notebook 內使用 [類型]  功能表按鈕，您可以選擇幾種不同類型的視覺效果 (資料表、圓形圖、折線圖、區域圖或橫條圖)。</span><span class="sxs-lookup"><span data-stu-id="091a7-216">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="091a7-217">橫條圖繪製結果會在此顯示。</span><span class="sxs-lookup"><span data-stu-id="091a7-217">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="091a7-218">繪製小費金額，和小費金額如何隨乘客計數和費用金額變化的長條圖。</span><span class="sxs-lookup"><span data-stu-id="091a7-218">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="091a7-219">使用 SQL 查詢來取樣資料。</span><span class="sxs-lookup"><span data-stu-id="091a7-219">Use a SQL query to sample data.</span></span>

    #PLOT HISTOGRAM OF TIP AMOUNTS AND VARIATION BY PASSENGER COUNT AND PAYMENT TYPE

    # HIVEQL QUERY AGAINST THE sqlContext
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


<span data-ttu-id="091a7-220">此程式碼儲存格使用 SQL 查詢來建立三種圖的資料。</span><span class="sxs-lookup"><span data-stu-id="091a7-220">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
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


<span data-ttu-id="091a7-221">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-221">**OUTPUT:**</span></span> 

![小費金額分佈](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-distribution.png)

![按乘客計數排列的小費金額](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-passenger-count.png)

![按費用金額排列的小費金額](./media/machine-learning-data-science-spark-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="091a7-225">模型化的功能工程、轉換和資料準備</span><span class="sxs-lookup"><span data-stu-id="091a7-225">Feature engineering, transformation and data preparation for modeling</span></span>
<span data-ttu-id="091a7-226">本節描述並提供程序的程式碼，可用來準備資料以供 ML 模型化使用。</span><span class="sxs-lookup"><span data-stu-id="091a7-226">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="091a7-227">它示範如何執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="091a7-227">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="091a7-228">將小時納入流量時間值區以建立新特徵</span><span class="sxs-lookup"><span data-stu-id="091a7-228">Create a new feature by binning hours into traffic time buckets</span></span>
* <span data-ttu-id="091a7-229">索引並編碼分類功能</span><span class="sxs-lookup"><span data-stu-id="091a7-229">Index and encode categorical features</span></span>
* <span data-ttu-id="091a7-230">建立輸入到 ML 函式的標示點物件</span><span class="sxs-lookup"><span data-stu-id="091a7-230">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="091a7-231">建立資料的隨機子取樣，並將它分割成訓練和測試集</span><span class="sxs-lookup"><span data-stu-id="091a7-231">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="091a7-232">調整功能</span><span class="sxs-lookup"><span data-stu-id="091a7-232">Feature scaling</span></span>
* <span data-ttu-id="091a7-233">快取記憶體中的物件</span><span class="sxs-lookup"><span data-stu-id="091a7-233">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="091a7-234">將小時納入流量時間值區以建立新特徵</span><span class="sxs-lookup"><span data-stu-id="091a7-234">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="091a7-235">此程式碼示範如何將小時納入流量時間值區以建立新功能，以及如何從記憶體快取產生的資料框架。</span><span class="sxs-lookup"><span data-stu-id="091a7-235">This code shows how to create a new feature by binning hours into traffic time buckets and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="091a7-236">在重複使用彈性分散式資料集 (RDD) 和資料框架的位置，快取可改善執行時間。</span><span class="sxs-lookup"><span data-stu-id="091a7-236">Where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="091a7-237">因此，我們會在逐步解說中的幾個階段快取 RDD 和資料框架。</span><span class="sxs-lookup"><span data-stu-id="091a7-237">Accordingly, we cache RDDs and data-frames at several stages in the walkthrough.</span></span> 

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
    # THE .COUNT() GOES THROUGH THE ENTIRE DATA-FRAME,
    # MATERIALIZES IT IN MEMORY, AND GIVES THE COUNT OF ROWS.
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()

<span data-ttu-id="091a7-238">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-238">**OUTPUT:**</span></span> 

<span data-ttu-id="091a7-239">126050</span><span class="sxs-lookup"><span data-stu-id="091a7-239">126050</span></span>

### <a name="index-and-encode-categorical-features-for-input-into-modeling-functions"></a><span data-ttu-id="091a7-240">索引並編碼分類功能以輸入模型化函式中</span><span class="sxs-lookup"><span data-stu-id="091a7-240">Index and encode categorical features for input into modeling functions</span></span>
<span data-ttu-id="091a7-241">本節說明如何索引並編碼分類功能，以輸入模型化函式中。</span><span class="sxs-lookup"><span data-stu-id="091a7-241">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="091a7-242">MLlib 的模型化和預測函式需要先執行功能來分類要索引或編碼的分類輸入資料，才能使用這些資料。</span><span class="sxs-lookup"><span data-stu-id="091a7-242">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="091a7-243">根據模型，您需要以不同方式索引或編碼它們︰</span><span class="sxs-lookup"><span data-stu-id="091a7-243">Depending on the model, you need to index or encode them in different ways:</span></span>  

* <span data-ttu-id="091a7-244">**樹狀結構型模型化** 需要將類別編碼為數值 (例如，含 3 個類別的特徵可能會使用 0、1、2 編碼)。</span><span class="sxs-lookup"><span data-stu-id="091a7-244">**Tree-based modeling** requires categories to be encoded as numerical values (for example, a feature with three categories may be encoded with 0, 1, 2).</span></span> <span data-ttu-id="091a7-245">這是由 MLlib 的 [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) 函式所提供。</span><span class="sxs-lookup"><span data-stu-id="091a7-245">This is provided by MLlib’s [StringIndexer](http://spark.apache.org/docs/latest/ml-features.html#stringindexer) function.</span></span> <span data-ttu-id="091a7-246">此函式會將標籤的字串資料行，編碼為標籤頻率所排序的標籤索引的資料行。</span><span class="sxs-lookup"><span data-stu-id="091a7-246">This function encodes a string column of labels to a column of label indices that are ordered by label frequencies.</span></span> <span data-ttu-id="091a7-247">雖然使用輸入和資料處理的數值編製索引，仍可指定樹狀結構型演算法，將它們視為類別適當地處理。</span><span class="sxs-lookup"><span data-stu-id="091a7-247">Although indexed with numerical values for input and data handling, the tree-based algorithms can be specified to treat them appropriately as categories.</span></span> 
* <span data-ttu-id="091a7-248">**羅吉斯和線性迴歸模型**需要一個有效編碼方式，例如，含 3 個類別的一個功能可擴充至 3 個功能資料行，根據觀察的類別，每個資料行包含 0 或 1。</span><span class="sxs-lookup"><span data-stu-id="091a7-248">**Logistic and Linear Regression models** require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="091a7-249">MLlib 提供 [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) 函式以執行 one-hot 編碼。</span><span class="sxs-lookup"><span data-stu-id="091a7-249">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="091a7-250">此編碼器會將標籤索引資料行對應到二進位向量資料行 (最多有一個單一值)。</span><span class="sxs-lookup"><span data-stu-id="091a7-250">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="091a7-251">這種編碼方式允許將預期數值功能的演算法 (例如羅吉斯迴歸) 套用至分類功能。</span><span class="sxs-lookup"><span data-stu-id="091a7-251">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="091a7-252">以下是要索引及編碼分類功能的程式碼︰</span><span class="sxs-lookup"><span data-stu-id="091a7-252">Here is the code to index and encode categorical features:</span></span>

    # INDEX AND ENCODE CATEGORICAL FEATURES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES    
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, VectorIndexer

    # INDEX AND ENCODE VENDOR_ID
    stringIndexer = StringIndexer(inputCol="vendor_id", outputCol="vendorIndex")
    model = stringIndexer.fit(taxi_df_train_with_newFeatures) # Input data-frame is the cleaned one from above
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="091a7-253">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-253">**OUTPUT:**</span></span>

<span data-ttu-id="091a7-254">執行上述儲存格所花費的時間︰1.28 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-254">Time taken to execute above cell: 1.28 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="091a7-255">建立輸入到 ML 函式的標示點物件</span><span class="sxs-lookup"><span data-stu-id="091a7-255">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="091a7-256">本節包含程式碼，示範如何將分類的文字資料索引為標示點資料類型並加以編碼，以用來訓練及測試 MLlib 羅吉斯迴歸和其他分類模型。</span><span class="sxs-lookup"><span data-stu-id="091a7-256">This section contains code that shows how to index categorical text data as a labeled point data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="091a7-257">標示點物件是彈性分散式資料集 (RDD)，其格式化成適合 MLlib 中大部分的 ML 演算法的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="091a7-257">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="091a7-258">[標示點](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 是本機向量 (密集或疏鬆)，與標籤/回應相關聯。</span><span class="sxs-lookup"><span data-stu-id="091a7-258">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>  

<span data-ttu-id="091a7-259">本節所包含的程式碼會示範如何以 [標示點](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 資料類型來為分類的文字資料編製索引並加以編碼，以用來訓練及測試 MLlib 羅吉斯迴歸和其他分類模型。</span><span class="sxs-lookup"><span data-stu-id="091a7-259">This section contains code that shows how to index categorical text data as a [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) data type and encode it so that it can be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="091a7-260">標示點物件是彈性分散式資料集 (RDD)，由標籤 (目標/回應變數) 和功能變數組成。</span><span class="sxs-lookup"><span data-stu-id="091a7-260">Labeled point objects are Resilient Distributed Datasets (RDD) consisting of a label (target/response variable) and feature vector.</span></span> <span data-ttu-id="091a7-261">這是 MLlib 中許多 ML 演算法輸入時的所需格式。</span><span class="sxs-lookup"><span data-stu-id="091a7-261">This format is needed as input by many ML algorithms in MLlib.</span></span>

<span data-ttu-id="091a7-262">以下是要為二進位分類進行索引及編碼文字功能的程式碼。</span><span class="sxs-lookup"><span data-stu-id="091a7-262">Here is the code to index and encode text features for binary classification.</span></span>

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


<span data-ttu-id="091a7-263">以下是要為線性迴歸分析進行編碼及建立類別文字功能的程式碼。</span><span class="sxs-lookup"><span data-stu-id="091a7-263">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="091a7-264">建立資料的隨機子取樣，並將它分割成訓練和測試集</span><span class="sxs-lookup"><span data-stu-id="091a7-264">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="091a7-265">此程式碼會建立隨機取樣資料 (這裡使用 25%)。</span><span class="sxs-lookup"><span data-stu-id="091a7-265">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="091a7-266">雖然您不需要這個範例 (因為資料集的大小)，我們將在這裡示範如何取樣，讓您了解如何在需要時使用它來自行解決問題。</span><span class="sxs-lookup"><span data-stu-id="091a7-266">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample here so you know how to use it for your own problem when needed.</span></span> <span data-ttu-id="091a7-267">在大型範例中，如此可在訓練模型時節省大量時間。</span><span class="sxs-lookup"><span data-stu-id="091a7-267">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="091a7-268">接下來我們將範例分割成訓練部分 (這裡為 75%) 和測試部分 (這裡為 25%)，以便在分類和迴歸模型化中使用。</span><span class="sxs-lookup"><span data-stu-id="091a7-268">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="091a7-269">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-269">**OUTPUT:**</span></span>

<span data-ttu-id="091a7-270">執行上述儲存格所花費的時間︰0.24 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-270">Time taken to execute above cell: 0.24 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="091a7-271">調整功能</span><span class="sxs-lookup"><span data-stu-id="091a7-271">Feature scaling</span></span>
<span data-ttu-id="091a7-272">調整功能，也稱為資料正規化，以確保具廣泛分散值的功能在目標函式中沒有過多權重。</span><span class="sxs-lookup"><span data-stu-id="091a7-272">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="091a7-273">用於調整功能的程式碼會使用 [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) ，將功能調整至單位變異數。</span><span class="sxs-lookup"><span data-stu-id="091a7-273">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="091a7-274">這是由 MLlib 提供，用於使用隨機梯度下降 (SGD) 的線性迴歸，為訓練廣泛的其他機器學習模型的常用演算法，例如正則化迴歸或支援向量機器 (SVM)。</span><span class="sxs-lookup"><span data-stu-id="091a7-274">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD), a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>

> [!NOTE]
> <span data-ttu-id="091a7-275">我們找到了適用於調整功能的 LinearRegressionWithSGD 演算法。</span><span class="sxs-lookup"><span data-stu-id="091a7-275">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>
> 
> 

<span data-ttu-id="091a7-276">以下是要用於正規化線性 SGD 演算法的比例調整變數的程式碼。</span><span class="sxs-lookup"><span data-stu-id="091a7-276">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="091a7-277">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-277">**OUTPUT:**</span></span>

<span data-ttu-id="091a7-278">執行上述儲存格所花費的時間︰13.17 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-278">Time taken to execute above cell: 13.17 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="091a7-279">快取記憶體中的物件</span><span class="sxs-lookup"><span data-stu-id="091a7-279">Cache objects in memory</span></span>
<span data-ttu-id="091a7-280">快取用於分類、迴歸和縮放功能的輸入資料框架物件，可降低訓練和測試 ML 演算法所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="091a7-280">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression, and scaled features.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="091a7-281">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-281">**OUTPUT:**</span></span> 

<span data-ttu-id="091a7-282">執行上述儲存格所花費的時間︰0.15 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-282">Time taken to execute above cell: 0.15 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="091a7-283">使用二進位分類模型來預測是否支付小費</span><span class="sxs-lookup"><span data-stu-id="091a7-283">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="091a7-284">本節說明如何為二進位分類工作使用三個模型，預測是否支付計程車車程的小費。</span><span class="sxs-lookup"><span data-stu-id="091a7-284">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="091a7-285">顯示模型如下︰</span><span class="sxs-lookup"><span data-stu-id="091a7-285">The models presented are:</span></span>

* <span data-ttu-id="091a7-286">正規化羅吉斯迴歸</span><span class="sxs-lookup"><span data-stu-id="091a7-286">Regularized logistic regression</span></span> 
* <span data-ttu-id="091a7-287">隨機樹系模型</span><span class="sxs-lookup"><span data-stu-id="091a7-287">Random forest model</span></span>
* <span data-ttu-id="091a7-288">漸層停駐提升樹狀結構</span><span class="sxs-lookup"><span data-stu-id="091a7-288">Gradient Boosting Trees</span></span>

<span data-ttu-id="091a7-289">每個模型建置程式碼區段會分成幾個步驟︰</span><span class="sxs-lookup"><span data-stu-id="091a7-289">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="091a7-290">**模型定型** 資料</span><span class="sxs-lookup"><span data-stu-id="091a7-290">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="091a7-291">**模型評估** </span><span class="sxs-lookup"><span data-stu-id="091a7-291">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="091a7-292">**儲存模型** </span><span class="sxs-lookup"><span data-stu-id="091a7-292">**Saving model** in blob for future consumption</span></span>

### <a name="classification-using-logistic-regression"></a><span data-ttu-id="091a7-293">使用羅吉斯迴歸分類</span><span class="sxs-lookup"><span data-stu-id="091a7-293">Classification using logistic regression</span></span>
<span data-ttu-id="091a7-294">本節的程式碼顯示如何定型、評估及使用 [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) 來儲存羅吉斯迴歸模型，可預測是否針對 NYC 計程車車程和費用資料集的某趟車程支付小費。</span><span class="sxs-lookup"><span data-stu-id="091a7-294">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

<span data-ttu-id="091a7-295">**使用 CV 及超參數掃掠來定型羅吉斯迴歸模型**</span><span class="sxs-lookup"><span data-stu-id="091a7-295">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitModel.weights))
    print("Intercept: " + str(logitModel.intercept))

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="091a7-296">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-296">**OUTPUT:**</span></span> 

<span data-ttu-id="091a7-297">係數：[0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="091a7-297">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="091a7-298">截距：-0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="091a7-298">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="091a7-299">執行上述儲存格所花費的時間︰14.43 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-299">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="091a7-300">**使用標準度量評估二進位分類模型**</span><span class="sxs-lookup"><span data-stu-id="091a7-300">**Evaluate the binary classification model with standard metrics**</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="091a7-301">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-301">**OUTPUT:**</span></span> 

<span data-ttu-id="091a7-302">PR 下的領域 = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="091a7-302">Area under PR = 0.985297691373</span></span>

<span data-ttu-id="091a7-303">ROC 下的領域 = 0.983714670256</span><span class="sxs-lookup"><span data-stu-id="091a7-303">Area under ROC = 0.983714670256</span></span>

<span data-ttu-id="091a7-304">摘要狀態</span><span class="sxs-lookup"><span data-stu-id="091a7-304">Summary Stats</span></span>

<span data-ttu-id="091a7-305">精確度 = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="091a7-305">Precision = 0.984304060189</span></span>

<span data-ttu-id="091a7-306">回收 = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="091a7-306">Recall = 0.984304060189</span></span>

<span data-ttu-id="091a7-307">F1 分數 = 0.984304060189</span><span class="sxs-lookup"><span data-stu-id="091a7-307">F1 Score = 0.984304060189</span></span>

<span data-ttu-id="091a7-308">執行上述儲存格所花費的時間︰57.61 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-308">Time taken to execute above cell: 57.61 seconds</span></span>

<span data-ttu-id="091a7-309">**繪製 ROC 曲線。**</span><span class="sxs-lookup"><span data-stu-id="091a7-309">**Plot the ROC curve.**</span></span>

<span data-ttu-id="091a7-310">predictionAndLabelsDF 已在先前的儲存格中已註冊為 tmp_results 資料表。</span><span class="sxs-lookup"><span data-stu-id="091a7-310">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="091a7-311">tmp_results 可用來執行查詢，並將結果輸出至 sqlResults 資料框架供繪製之用。</span><span class="sxs-lookup"><span data-stu-id="091a7-311">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="091a7-312">程式碼如下。</span><span class="sxs-lookup"><span data-stu-id="091a7-312">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="091a7-313">以下是建立預測和繪製 ROC 曲線的程式碼。</span><span class="sxs-lookup"><span data-stu-id="091a7-313">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="091a7-314">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-314">**OUTPUT:**</span></span>

![羅吉斯迴歸 ROC curve.png](./media/machine-learning-data-science-spark-data-exploration-modeling/logistic-regression-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="091a7-316">隨機樹系分類</span><span class="sxs-lookup"><span data-stu-id="091a7-316">Random forest classification</span></span>
<span data-ttu-id="091a7-317">本節的程式碼顯示如何訓練評估及儲存隨機樹系模型，可預測是否針對 NYC 計程車車程和費用資料集的某趟車程支付小費。</span><span class="sxs-lookup"><span data-stu-id="091a7-317">The code in this section shows how to train, evaluate, and save a random forest model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRINT TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="091a7-318">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-318">**OUTPUT:**</span></span>

<span data-ttu-id="091a7-319">ROC 下的領域 = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="091a7-319">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="091a7-320">執行上述儲存格所花費的時間︰31.09 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-320">Time taken to execute above cell: 31.09 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="091a7-321">漸層停駐提升樹狀結構類別</span><span class="sxs-lookup"><span data-stu-id="091a7-321">Gradient boosting trees classification</span></span>
<span data-ttu-id="091a7-322">本節的程式碼顯示如何訓練評估及儲存漸層停駐提升樹狀結構模型，可預測是否針對 NYC 計程車車程和費用資料集的某趟車程支付小費。</span><span class="sxs-lookup"><span data-stu-id="091a7-322">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    #PREDICT WHETHER A TIP IS PAID OR NOT USING GRADIENT BOOSTING TREES

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo, numIterations=5)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="091a7-323">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-323">**OUTPUT:**</span></span>

<span data-ttu-id="091a7-324">ROC 下的領域 = 0.985297691373</span><span class="sxs-lookup"><span data-stu-id="091a7-324">Area under ROC = 0.985297691373</span></span>

<span data-ttu-id="091a7-325">執行上述儲存格所花費的時間︰19.76 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-325">Time taken to execute above cell: 19.76 seconds</span></span>

## <a name="predict-tip-amounts-for-taxi-trips-with-regression-models"></a><span data-ttu-id="091a7-326">使用迴歸模型預測計程車車程的小費金額</span><span class="sxs-lookup"><span data-stu-id="091a7-326">Predict tip amounts for taxi trips with regression models</span></span>
<span data-ttu-id="091a7-327">本節說明如何使用三種迴歸工作模型，根據其他小費功能預測支付的計程車車程的小費金額。</span><span class="sxs-lookup"><span data-stu-id="091a7-327">This section shows how use three models for the regression task of predicting the amount of the tip paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="091a7-328">顯示模型如下︰</span><span class="sxs-lookup"><span data-stu-id="091a7-328">The models presented are:</span></span>

* <span data-ttu-id="091a7-329">正規化線性迴歸</span><span class="sxs-lookup"><span data-stu-id="091a7-329">Regularized linear regression</span></span>
* <span data-ttu-id="091a7-330">隨機樹系</span><span class="sxs-lookup"><span data-stu-id="091a7-330">Random forest</span></span>
* <span data-ttu-id="091a7-331">漸層停駐提升樹狀結構</span><span class="sxs-lookup"><span data-stu-id="091a7-331">Gradient Boosting Trees</span></span>

<span data-ttu-id="091a7-332">這些模型將在簡介中說明。</span><span class="sxs-lookup"><span data-stu-id="091a7-332">These models were described in the introduction.</span></span> <span data-ttu-id="091a7-333">每個模型建置程式碼區段會分成幾個步驟︰</span><span class="sxs-lookup"><span data-stu-id="091a7-333">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="091a7-334">**模型定型** 資料</span><span class="sxs-lookup"><span data-stu-id="091a7-334">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="091a7-335">**模型評估** </span><span class="sxs-lookup"><span data-stu-id="091a7-335">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="091a7-336">**儲存模型** </span><span class="sxs-lookup"><span data-stu-id="091a7-336">**Saving model** in blob for future consumption</span></span>

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="091a7-337">使用 SGD 的線性迴歸</span><span class="sxs-lookup"><span data-stu-id="091a7-337">Linear regression with SGD</span></span>
<span data-ttu-id="091a7-338">本節的程式碼示範如何使用縮放功能來訓練線性迴歸 (使用隨機梯度下降 (SGD) 以最佳化)，以及如何評分、評估並將模型儲存在 Azure Blob 儲存體 (WASB)。</span><span class="sxs-lookup"><span data-stu-id="091a7-338">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="091a7-339">在我們的經驗中，交集的 LinearRegressionWithSGD 模型可能會發生問題，且必須小心變更/最佳化參數以取得有效的模型。</span><span class="sxs-lookup"><span data-stu-id="091a7-339">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="091a7-340">調整變數對於聚合很有用。</span><span class="sxs-lookup"><span data-stu-id="091a7-340">Scaling of variables significantly helps with convergence.</span></span> 
> 
> 

    #PREDICT TIP AMOUNTS USING LINEAR REGRESSION WITH SGD

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD LIBRARIES
    from pyspark.mllib.regression import LabeledPoint, LinearRegressionWithSGD, LinearRegressionModel
    from pyspark.mllib.evaluation import RegressionMetrics
    from scipy import stats

    # USE SCALED FEATURES TO TRAIN MODEL
    linearModel = LinearRegressionWithSGD.train(oneHotTRAINregScaled, iterations=100, step = 0.1, regType='l2', regParam=0.1, intercept = True)

    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(linearModel.weights))
    print("Intercept: " + str(linearModel.intercept))

    # SCORE ON SCALED TEST DATA-SET & EVALUATE
    predictionAndLabels = oneHotTESTregScaled.map(lambda lp: (float(linearModel.predict(lp.features)), lp.label))
    testMetrics = RegressionMetrics(predictionAndLabels)

    # PRINT TEST METRICS
    print("RMSE = %s" % testMetrics.rootMeanSquaredError)
    print("R-sqr = %s" % testMetrics.r2)

    # SAVE MODEL WITH DATE-STAMP IN THE DEFAULT BLOB FOR THE CLUSTER
    datestamp = unicode(datetime.datetime.now()).replace(' ','').replace(':','_');
    linearregressionfilename = "LinearRegressionWithSGD_" + datestamp;
    dirfilename = modelDir + linearregressionfilename;

    linearModel.save(sc, dirfilename)

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="091a7-341">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-341">**OUTPUT:**</span></span>

<span data-ttu-id="091a7-342">係數：[0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span><span class="sxs-lookup"><span data-stu-id="091a7-342">Coefficients: [0.00457675809917, -0.0226314167349, -0.0191910355236, 0.246793409578, 0.312047890459, 0.359634405999, 0.00928692253981, -0.000987181489428, -0.0888306617845, 0.0569376211553, 0.115519551711, 0.149250164995, -0.00990211159703, -0.00637410344522, 0.545083566179, -0.536756072402, 0.0105762393099, -0.0130117577055, 0.0129304737772, -0.00171065945959]</span></span>

<span data-ttu-id="091a7-343">截距：0.853872718283</span><span class="sxs-lookup"><span data-stu-id="091a7-343">Intercept: 0.853872718283</span></span>

<span data-ttu-id="091a7-344">RMSE = 1.24190115863</span><span class="sxs-lookup"><span data-stu-id="091a7-344">RMSE = 1.24190115863</span></span>

<span data-ttu-id="091a7-345">R-sqr = 0.608017146081</span><span class="sxs-lookup"><span data-stu-id="091a7-345">R-sqr = 0.608017146081</span></span>

<span data-ttu-id="091a7-346">執行上述儲存格所花費的時間︰58.42 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-346">Time taken to execute above cell: 58.42 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="091a7-347">隨機樹系迴歸</span><span class="sxs-lookup"><span data-stu-id="091a7-347">Random Forest regression</span></span>
<span data-ttu-id="091a7-348">本節的程式碼會顯示如何訓練評估及儲存隨機樹系迴歸，可預測 NYC 計程車車程資料的小費金額。</span><span class="sxs-lookup"><span data-stu-id="091a7-348">The code in this section shows how to train, evaluate, and save a random forest regression that predicts tip amount for the NYC taxi trip data.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRING TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="091a7-349">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-349">**OUTPUT:**</span></span>

<span data-ttu-id="091a7-350">RMSE = 0.891209218139</span><span class="sxs-lookup"><span data-stu-id="091a7-350">RMSE = 0.891209218139</span></span>

<span data-ttu-id="091a7-351">R-sqr = 0.759661334921</span><span class="sxs-lookup"><span data-stu-id="091a7-351">R-sqr = 0.759661334921</span></span>

<span data-ttu-id="091a7-352">執行上述儲存格所花費的時間︰49.21 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-352">Time taken to execute above cell: 49.21 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="091a7-353">漸層停駐提升樹狀結構迴歸</span><span class="sxs-lookup"><span data-stu-id="091a7-353">Gradient boosting trees regression</span></span>
<span data-ttu-id="091a7-354">本節的程式碼顯示如何訓練評估及儲存漸層停駐提升樹狀結構模型，可預測 NYC 計程車車程資料的小費金額。</span><span class="sxs-lookup"><span data-stu-id="091a7-354">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="091a7-355">* * 來定型及評估 * *</span><span class="sxs-lookup"><span data-stu-id="091a7-355">**Train and evaluate **</span></span>

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

    # CONVER RESULTS TO DF AND REGISER TEMP TABLE
    test_predictions = sqlContext.createDataFrame(predictionAndLabels)
    test_predictions.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="091a7-356">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-356">**OUTPUT:**</span></span>

<span data-ttu-id="091a7-357">RMSE = 0.908473148639</span><span class="sxs-lookup"><span data-stu-id="091a7-357">RMSE = 0.908473148639</span></span>

<span data-ttu-id="091a7-358">R-sqr = 0.753835096681</span><span class="sxs-lookup"><span data-stu-id="091a7-358">R-sqr = 0.753835096681</span></span>

<span data-ttu-id="091a7-359">執行上述儲存格所花費的時間︰34.52 秒</span><span class="sxs-lookup"><span data-stu-id="091a7-359">Time taken to execute above cell: 34.52 seconds</span></span>

<span data-ttu-id="091a7-360">**圖**</span><span class="sxs-lookup"><span data-stu-id="091a7-360">**Plot**</span></span>

<span data-ttu-id="091a7-361">tmp_results 已在先前的儲存格中註冊為 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="091a7-361">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="091a7-362">來自資料表的結果已輸出至 sqlResults  資料框架以供繪製之用。</span><span class="sxs-lookup"><span data-stu-id="091a7-362">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="091a7-363">程式碼如下</span><span class="sxs-lookup"><span data-stu-id="091a7-363">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results

<span data-ttu-id="091a7-364">以下是使用 Jupyter 伺服器繪製資料的程式碼。</span><span class="sxs-lookup"><span data-stu-id="091a7-364">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="091a7-365">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="091a7-365">**OUTPUT:**</span></span>

![Actual-vs-predicted-tip-amounts](./media/machine-learning-data-science-spark-data-exploration-modeling/actual-vs-predicted-tips.png)

## <a name="clean-up-objects-from-memory"></a><span data-ttu-id="091a7-367">從記憶體清除物件</span><span class="sxs-lookup"><span data-stu-id="091a7-367">Clean up objects from memory</span></span>
<span data-ttu-id="091a7-368">使用 `unpersist()` 刪除記憶體中快取的物件。</span><span class="sxs-lookup"><span data-stu-id="091a7-368">Use `unpersist()` to delete objects cached in memory.</span></span>

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


## <a name="record-storage-locations-of-the-models-for-consumption-and-scoring"></a><span data-ttu-id="091a7-369">記錄模型的儲存位置供耗用和評分</span><span class="sxs-lookup"><span data-stu-id="091a7-369">Record storage locations of the models for consumption and scoring</span></span>
<span data-ttu-id="091a7-370">若要依[評分及評估 Spark 建置 Machine Learning 模型](machine-learning-data-science-spark-model-consumption.md)主題中所述的耗用和評分獨立資料集，您必須將在這裡所建立之儲存模型的檔案名稱，複製並貼到 Consumption Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="091a7-370">To consume and score an independent dataset described in the [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) topic, you need to copy and paste these file names containing the saved models created here into the Consumption Jupyter notebook.</span></span> <span data-ttu-id="091a7-371">以下程式碼可將路徑列印到您在該處所需要的模型檔案。</span><span class="sxs-lookup"><span data-stu-id="091a7-371">Here is the code to print out the paths to model files you need there.</span></span>

    # MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="091a7-372">**輸出**</span><span class="sxs-lookup"><span data-stu-id="091a7-372">**OUTPUT**</span></span>

<span data-ttu-id="091a7-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span><span class="sxs-lookup"><span data-stu-id="091a7-373">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0317_03_23.516568"</span></span>

<span data-ttu-id="091a7-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span><span class="sxs-lookup"><span data-stu-id="091a7-374">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0317_05_21.577773"</span></span>

<span data-ttu-id="091a7-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span><span class="sxs-lookup"><span data-stu-id="091a7-375">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0317_04_11.950206"</span></span>

<span data-ttu-id="091a7-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span><span class="sxs-lookup"><span data-stu-id="091a7-376">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0317_06_08.723736"</span></span>

<span data-ttu-id="091a7-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span><span class="sxs-lookup"><span data-stu-id="091a7-377">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0317_04_36.346583"</span></span>

<span data-ttu-id="091a7-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span><span class="sxs-lookup"><span data-stu-id="091a7-378">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0317_06_51.737282"</span></span>

## <a name="whats-next"></a><span data-ttu-id="091a7-379">後續步驟</span><span class="sxs-lookup"><span data-stu-id="091a7-379">What's next?</span></span>
<span data-ttu-id="091a7-380">現在已使用 Spark MlLib 建立迴歸和分類模型，您已瞭解如何評分及評估這些模型。</span><span class="sxs-lookup"><span data-stu-id="091a7-380">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span> <span data-ttu-id="091a7-381">進階資料探索和模型化筆記本深入探討到包括交叉驗證、超參數清除和模型評估。</span><span class="sxs-lookup"><span data-stu-id="091a7-381">The advanced data exploration and modeling notebook dives deeper into including cross-validation, hyper-parameter sweeping, and model evaluation.</span></span> 

<span data-ttu-id="091a7-382">**模型耗用量︰** 若要瞭解如何評分及評估本主題中所建立的分類和迴歸模型，請參閱 [評分及評估 Spark 建置機器學習服務模型](machine-learning-data-science-spark-model-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="091a7-382">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

<span data-ttu-id="091a7-383">**交叉驗證和超參數掃掠**：如需如何使用交叉驗證和超參數掃掠訓練模型的相關資訊，請參閱 [使用 Spark 進階資料探索和模型化](machine-learning-data-science-spark-advanced-data-exploration-modeling.md)</span><span class="sxs-lookup"><span data-stu-id="091a7-383">**Cross-validation and hyperparameter sweeping**: See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping</span></span>

