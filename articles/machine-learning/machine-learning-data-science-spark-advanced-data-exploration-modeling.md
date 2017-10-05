---
title: "使用 Spark 進階資料探索和模型化 | Microsoft Docs"
description: "使用 HDInsight Spark 並透過交叉驗證和超參數最佳化定型模型，執行資料探索和二進位分類和迴歸模型化。"
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
ms.openlocfilehash: e6bf6bd3c905f077841ef166540337a251b91ad1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="e460a-103">使用 Spark 進階資料探索和模型化</span><span class="sxs-lookup"><span data-stu-id="e460a-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="e460a-104">本逐步解說會使用 HDInsight Spark，在 NYC 計程車車程和費用 2013 資料集的取樣上，使用交叉驗證和超參數最佳化來執行資料探索和定型二進位分類和迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-104">This walkthrough uses HDInsight Spark to do data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of the NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="e460a-105">它將引導您逐步完成 [資料科學程序](http://aka.ms/datascienceprocess)、端對端、使用 HDInsight Spark 叢集處理，並使用 Azure blob 來儲存資料和模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-105">It walks you through the steps of the [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs to store the data and the models.</span></span> <span data-ttu-id="e460a-106">程序會探索和視覺化從 Azure 儲存體 Blob 中引進的資料，然後準備資料來建立預測模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-106">The process explores and visualizes data brought in from an Azure Storage Blob and then prepares the data to build predictive models.</span></span> <span data-ttu-id="e460a-107">已使用 Python 來編寫解決方案程式碼，並顯示相關的繪圖。</span><span class="sxs-lookup"><span data-stu-id="e460a-107">Python has been used to code the solution and to show the relevant plots.</span></span> <span data-ttu-id="e460a-108">這些模型是使用 Spark MLlib 工具組來執行二進位分類和迴歸模型工作。</span><span class="sxs-lookup"><span data-stu-id="e460a-108">These models are build using the Spark MLlib toolkit to do binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="e460a-109">**二進位分類** 工作可預測是否已支付某趟車程的小費。</span><span class="sxs-lookup"><span data-stu-id="e460a-109">The **binary classification** task is to predict whether or not a tip is paid for the trip.</span></span> 
* <span data-ttu-id="e460a-110">**迴歸** 工作可根據其他小費功能來預測小費金額。</span><span class="sxs-lookup"><span data-stu-id="e460a-110">The **regression** task is to predict the amount of the tip based on other tip features.</span></span> 

<span data-ttu-id="e460a-111">模型化步驟也包含程式碼來示範如何定型、評估和儲存每類模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-111">The modeling steps also contain code showing how to train, evaluate, and save each type of model.</span></span> <span data-ttu-id="e460a-112">這個主題涵蓋一些與[使用 Spark 資料探索和模型化](machine-learning-data-science-spark-data-exploration-modeling.md)主題相同的內容，</span><span class="sxs-lookup"><span data-stu-id="e460a-112">The topic covers some of the same ground as the [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="e460a-113">但更「進階」；這是指它也會使用交叉驗證搭配超參數掃掠，以最佳方式定型精確的分類和迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping to train optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="e460a-114">**交叉驗證 (CV)** 是一種技術，評估以一組已知資料定型的模型如何一般化，以預測在其上尚未定型的資料集的功能。</span><span class="sxs-lookup"><span data-stu-id="e460a-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes to predicting the features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="e460a-115">此處所使用的通用實作是將資料集分割成 K 摺疊，然後以循環配置資源方式定型所有摺疊，只留下其中一個摺疊。</span><span class="sxs-lookup"><span data-stu-id="e460a-115">A common implementation used here is to divide a dataset into K folds and then train the model in a round-robin fashion on all but one of the folds.</span></span> <span data-ttu-id="e460a-116">評估測試未定型的此摺疊中獨立資料集時精確預測模型的能力。</span><span class="sxs-lookup"><span data-stu-id="e460a-116">The ability of the model to prediction accurately when tested against the independent dataset in this fold not used to train the model is assessed.</span></span>

<span data-ttu-id="e460a-117">**超參數最佳化** 是選擇用於學習演算法的超參數集的問題所在，通常具有最佳化獨立資料集上演算法效能的測量的目標。</span><span class="sxs-lookup"><span data-stu-id="e460a-117">**Hyperparameter optimization** is the problem of choosing a set of hyperparameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="e460a-118">**超參數** 是值，必須在模型定型程序之外指定。</span><span class="sxs-lookup"><span data-stu-id="e460a-118">**Hyperparameters** are values that must be specified outside of the model training procedure.</span></span> <span data-ttu-id="e460a-119">這些值的假設可能會影響模型的彈性和精確度。</span><span class="sxs-lookup"><span data-stu-id="e460a-119">Assumptions about these values can impact the flexibility and accuracy of the models.</span></span> <span data-ttu-id="e460a-120">決策樹有超參數，例如，想要的深度和樹狀目錄中的分葉數目等。</span><span class="sxs-lookup"><span data-stu-id="e460a-120">Decision trees have hyperparameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="e460a-121">支援向量機器 (SVM) 需要設定分類誤判損失詞彙。</span><span class="sxs-lookup"><span data-stu-id="e460a-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="e460a-122">此處所使用的執行超參數最佳化常見做法是格線搜尋，或 **參數掃掠**。</span><span class="sxs-lookup"><span data-stu-id="e460a-122">A common way to perform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="e460a-123">是透過值執行詳盡搜尋，而該值是學習演算法的超參數空間的指定子集。</span><span class="sxs-lookup"><span data-stu-id="e460a-123">This consists of performing an exhaustive search through the values a specified subset of the hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="e460a-124">交叉驗證可以提供效能度量，挑出格線搜尋演算法所產生的最佳結果。</span><span class="sxs-lookup"><span data-stu-id="e460a-124">Cross validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="e460a-125">CV 與超參數掃掠搭配使用，有助於限制問題，例如定型資料模型的過度配適，以便模型會保留容量以套用至從中擷取定型資料的一般集合。</span><span class="sxs-lookup"><span data-stu-id="e460a-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model to training data so that the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

<span data-ttu-id="e460a-126">我們使用的模型包括羅吉斯和線性迴歸、隨機樹系和漸層停駐推進式決策樹︰</span><span class="sxs-lookup"><span data-stu-id="e460a-126">The models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="e460a-127">[使用 SGD 的線性迴歸](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) 是一種使用隨機梯度下降 (SGD) 方法的線性迴歸模型，並使用最佳化和功能縮放比例來預測支付的小費金額。</span><span class="sxs-lookup"><span data-stu-id="e460a-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling to predict the tip amounts paid.</span></span> 
* <span data-ttu-id="e460a-128">[使用 LBFGS 的羅吉斯迴歸](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) 或「對數優劣比」迴歸是使用相依變數來執行資料分類時，可使用的迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when the dependent variable is categorical to do data classification.</span></span> <span data-ttu-id="e460a-129">LBFGS 是牛頓最佳化演算法，可使用有限的電腦記憶體量來逼近 Broyden–Fletcher–Goldfarb–Shanno (BFGS) 演算法，且廣泛用於機器學習中。</span><span class="sxs-lookup"><span data-stu-id="e460a-129">LBFGS is a quasi-Newton optimization algorithm that approximates the Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="e460a-130">[隨機樹系](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 是整體的決策樹。</span><span class="sxs-lookup"><span data-stu-id="e460a-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="e460a-131">隨機樹系結合許多決策樹來降低風險過度膨脹。</span><span class="sxs-lookup"><span data-stu-id="e460a-131">They combine many decision trees to reduce the risk of overfitting.</span></span> <span data-ttu-id="e460a-132">隨機樹系適用於迴歸和分類，可處理分類功能，也可擴充至多類別分類設定。</span><span class="sxs-lookup"><span data-stu-id="e460a-132">Random forests are used for regression and classification and can handle categorical features and can be extended to the multiclass classification setting.</span></span> <span data-ttu-id="e460a-133">隨機樹系不需要調整功能，而且能夠擷取非線性和功能互動。</span><span class="sxs-lookup"><span data-stu-id="e460a-133">They do not require feature scaling and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="e460a-134">隨機樹系是其中一個最成功的分類和迴歸的機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-134">Random forests are one of the most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="e460a-135">[漸層停駐推進式決策樹](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) 是整體的決策樹。</span><span class="sxs-lookup"><span data-stu-id="e460a-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="e460a-136">GBT 反覆地訓練決策樹以盡可能降低遺失函式。</span><span class="sxs-lookup"><span data-stu-id="e460a-136">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="e460a-137">GBT 適用於迴歸和分類，並可處理分類功能、不需要調整功能，而且能夠擷取非線性和功能互動。</span><span class="sxs-lookup"><span data-stu-id="e460a-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able to capture non-linearities and feature interactions.</span></span> <span data-ttu-id="e460a-138">它們也可用於多類別分類設定。</span><span class="sxs-lookup"><span data-stu-id="e460a-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="e460a-139">使用 CV 和超參數掃掠的模型化範例會針對二進位分類問題顯示。</span><span class="sxs-lookup"><span data-stu-id="e460a-139">Modeling examples using CV and Hyperparameter sweep are shown for the binary classification problem.</span></span> <span data-ttu-id="e460a-140">更簡單的範例 (不含參數掃掠) 會出現在迴歸工作的主要主題中。</span><span class="sxs-lookup"><span data-stu-id="e460a-140">Simpler examples (without parameter sweeps) are presented in the main topic for regression tasks.</span></span> <span data-ttu-id="e460a-141">但是在附錄中，另外也會提到針對線性迴歸使用彈性 net 的驗證，和針對隨機樹系迴歸使用 CV 和參數掃掠的驗證。</span><span class="sxs-lookup"><span data-stu-id="e460a-141">But in the appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="e460a-142">**彈性 net** 是正規化迴歸方法，以符合線性迴歸模型，線性結合 L1 和 L2 度量做為 [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) 和 [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) 方法的處罰。</span><span class="sxs-lookup"><span data-stu-id="e460a-142">The **elastic net** is a regularized regression method for fitting linear regression models that linearly combines the L1 and L2 metrics as penalties of the [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="e460a-143">雖然 Spark MLlib 工具組設計成可處理大型資料集，在這裡為了簡便我們使用極小的範例 (使用 170 個資料列，原始的 NYC 資料集約 0.1%，~30 Mb)。</span><span class="sxs-lookup"><span data-stu-id="e460a-143">Although the Spark MLlib toolkit is designed to work on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of the original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="e460a-144">此處提供的練習有效地在含有 2 個背景工作節點的 HDInsight 叢集上執行 (大約 10 分鐘)。</span><span class="sxs-lookup"><span data-stu-id="e460a-144">The exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="e460a-145">相同的程式碼中 (稍加修改) 可以用來處理大型資料集，適當修改的程式碼則可快取記憶體的資料以及變更叢集大小。</span><span class="sxs-lookup"><span data-stu-id="e460a-145">The same code, with minor modifications, can be used to process larger data-sets, with appropriate modifications for caching data in memory and changing the cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="e460a-146">設定：Spark 叢集和 Notebook</span><span class="sxs-lookup"><span data-stu-id="e460a-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="e460a-147">此逐步解說所提供的設定步驟和程式碼適用於使用 HDInsight Spark 1.6。</span><span class="sxs-lookup"><span data-stu-id="e460a-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="e460a-148">不過 Jupyter Notebook 可供 HDInsight Spark 1.6 版和 Spark 2.0 叢集兩者使用。</span><span class="sxs-lookup"><span data-stu-id="e460a-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="e460a-149">Notebook 的描述及它們的連結已在包含它們的 GitHub 儲存機制的 [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) 中提供。</span><span class="sxs-lookup"><span data-stu-id="e460a-149">A description of the notebooks and links to them are provided in the [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for the GitHub repository containing them.</span></span> <span data-ttu-id="e460a-150">此外，此處及連結的 Notebook 內的程式碼皆屬泛型程式碼，而且應該能在任何 Spark 叢集上運作。</span><span class="sxs-lookup"><span data-stu-id="e460a-150">Moreover, the code here and in the linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="e460a-151">若您不是使用 HDInsight Spark，叢集設定和管理步驟可能與這裡顯示的稍有不同。</span><span class="sxs-lookup"><span data-stu-id="e460a-151">If you are not using HDInsight Spark, the cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="e460a-152">為了方便起見，以下是可讓 Spark 1.6 版和 2.0 版在 Jupyter Notebook 伺服器的 pyspark 核心中執行的 Jupyter Notebook 連結：</span><span class="sxs-lookup"><span data-stu-id="e460a-152">For convenience, here are the links to the Jupyter notebooks for Spark 1.6 and 2.0 to be run in the pyspark kernel of the Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="e460a-153">Spark 1.6 Notebook</span><span class="sxs-lookup"><span data-stu-id="e460a-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="e460a-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)：包含Notebook #1 中的主題，以及使用超參數微調和交叉驗證的模型開發。</span><span class="sxs-lookup"><span data-stu-id="e460a-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="e460a-155">Spark 2.0 Notebook</span><span class="sxs-lookup"><span data-stu-id="e460a-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="e460a-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)：此檔案提供如何在 Spark 2.0 叢集中執行資料瀏覽、模型化和評分的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="e460a-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how to perform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-the-preset-spark-context"></a><span data-ttu-id="e460a-157">安裝程式︰儲存體位置、程式庫和預設 Spark 內容</span><span class="sxs-lookup"><span data-stu-id="e460a-157">Setup: storage locations, libraries, and the preset Spark context</span></span>
<span data-ttu-id="e460a-158">Spark 可以讀取和寫入 Azure 儲存體 Blob (也稱為 WASB)。</span><span class="sxs-lookup"><span data-stu-id="e460a-158">Spark is able to read and write to Azure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="e460a-159">如此可使用 Spark 處理該處儲存的任何現有資料，並在 WASB 中再次儲存結果。</span><span class="sxs-lookup"><span data-stu-id="e460a-159">So any of your existing data stored there can be processed using Spark and the results stored again in WASB.</span></span>

<span data-ttu-id="e460a-160">若要在 WASB 中儲存模型或檔案，必須正確指定路徑。</span><span class="sxs-lookup"><span data-stu-id="e460a-160">To save models or files in WASB, the path needs to be specified properly.</span></span> <span data-ttu-id="e460a-161">可以使用以「wasb:///」開頭的路徑，參考連接到 Spark 叢集的預設容器。</span><span class="sxs-lookup"><span data-stu-id="e460a-161">The default container attached to the Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="e460a-162">其他位置由「wasb://」參考。</span><span class="sxs-lookup"><span data-stu-id="e460a-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="e460a-163">在 WASB 中設定儲存位置的目錄路徑</span><span class="sxs-lookup"><span data-stu-id="e460a-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="e460a-164">下列程式碼範例會指定要讀取資料的位置，和將儲存模型輸出的模型儲存體目錄的路徑：</span><span class="sxs-lookup"><span data-stu-id="e460a-164">The following code sample specifies the location of the data to be read and the path for the model storage directory to which the model output is saved:</span></span>

    # SET PATHS TO FILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET THE MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="e460a-165">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-165">**OUTPUT**</span></span>

<span data-ttu-id="e460a-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="e460a-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="e460a-167">匯入程式庫</span><span class="sxs-lookup"><span data-stu-id="e460a-167">Import libraries</span></span>
<span data-ttu-id="e460a-168">使用下列程式碼匯入必要的程式庫：</span><span class="sxs-lookup"><span data-stu-id="e460a-168">Import necessary libraries with the following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="e460a-169">預設 Spark 內容及 PySpark magic</span><span class="sxs-lookup"><span data-stu-id="e460a-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="e460a-170">Jupyter Notebook 所提供的 PySpark 核心有預設的內容。</span><span class="sxs-lookup"><span data-stu-id="e460a-170">The PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="e460a-171">因此您不必明確設定 Spark 或 Hive 內容，就能開始使用您所開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e460a-171">So you do not need to set the Spark or Hive contexts explicitly before you start working with the application you are developing.</span></span> <span data-ttu-id="e460a-172">依預設會將這些內容提供給您使用。</span><span class="sxs-lookup"><span data-stu-id="e460a-172">These contexts are available for you by default.</span></span> <span data-ttu-id="e460a-173">這些內容包括：</span><span class="sxs-lookup"><span data-stu-id="e460a-173">These contexts are:</span></span>

* <span data-ttu-id="e460a-174">sc - 代表 Spark</span><span class="sxs-lookup"><span data-stu-id="e460a-174">sc - for Spark</span></span> 
* <span data-ttu-id="e460a-175">sqlContext - 代表 Hive</span><span class="sxs-lookup"><span data-stu-id="e460a-175">sqlContext - for Hive</span></span>

<span data-ttu-id="e460a-176">PySpark 核心提供一些預先定義的「magic」，這是您可以使用 %% 呼叫的特殊命令。</span><span class="sxs-lookup"><span data-stu-id="e460a-176">The PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="e460a-177">在這些程式碼範例中，就使用了兩個此類型的命令。</span><span class="sxs-lookup"><span data-stu-id="e460a-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="e460a-178">**%%local** 指定後續行所列的程式碼要在本機執行。</span><span class="sxs-lookup"><span data-stu-id="e460a-178">**%%local** Specifies that the code in subsequent lines is to be executed locally.</span></span> <span data-ttu-id="e460a-179">程式碼必須是有效的 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="e460a-180">**%%sql -o <variable name>** 會針對 sqlContext 執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="e460a-180">**%%sql -o <variable name>** Executes a Hive query against the sqlContext.</span></span> <span data-ttu-id="e460a-181">如果傳遞 -o 參數，則查詢的結果會當做 Pandas 資料框架，保存在 %%local Python 內容中。</span><span class="sxs-lookup"><span data-stu-id="e460a-181">If the -o parameter is passed, the result of the query is persisted in the %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="e460a-182">如需關於 Jupyter Notebook 核心，以及其所提供的預先定義 "magics" 的詳細資訊，請參閱 [HDInsight 上的 HDInsight Spark Linux 叢集可供 Jupyter Notebook 使用的核心](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="e460a-182">For more information on the kernels for Jupyter notebooks and the predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="e460a-183">來自公用 Blob 的資料擷取：</span><span class="sxs-lookup"><span data-stu-id="e460a-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="e460a-184">資料科學程序的第一個步驟，是將要分析的資料從其來源位置內嵌到您的資料探索和模型化環境。</span><span class="sxs-lookup"><span data-stu-id="e460a-184">The first step in the data science process is to ingest the data to be analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="e460a-185">這種環境在本逐步解說中是 Spark。</span><span class="sxs-lookup"><span data-stu-id="e460a-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="e460a-186">本節包含程式碼來完成一系列的工作︰</span><span class="sxs-lookup"><span data-stu-id="e460a-186">This section contains the code to complete a series of tasks:</span></span>

* <span data-ttu-id="e460a-187">擷取要模型化的資料範例</span><span class="sxs-lookup"><span data-stu-id="e460a-187">ingest the data sample to be modeled</span></span>
* <span data-ttu-id="e460a-188">在輸入資料集中讀取 (儲存為 .tsv 檔案)</span><span class="sxs-lookup"><span data-stu-id="e460a-188">read in the input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="e460a-189">格式化和清除資料</span><span class="sxs-lookup"><span data-stu-id="e460a-189">format and clean the data</span></span>
* <span data-ttu-id="e460a-190">建立並快取記憶體中的物件 (RDD 或資料框架)</span><span class="sxs-lookup"><span data-stu-id="e460a-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="e460a-191">將它註冊為 SQL 內容中的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="e460a-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="e460a-192">以下是資料擷取的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-192">Here is the code for data ingestion.</span></span>

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

    # CACHE & MATERIALIZE DATA-FRAME IN MEMORY. GOING THROUGH AND COUNTING NUMBER OF ROWS MATERIALIZES THE DATA-FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER DATA-FRAME AS A TEMP-TABLE IN SQL-CONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # PRINT HOW MUCH TIME IT TOOK TO RUN THE CELL
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="e460a-193">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-193">**OUTPUT**</span></span>

<span data-ttu-id="e460a-194">執行上述儲存格所花費的時間︰276.62 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-194">Time taken to execute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="e460a-195">資料探索和虛擬化</span><span class="sxs-lookup"><span data-stu-id="e460a-195">Data exploration & visualization</span></span>
<span data-ttu-id="e460a-196">一旦將資料引進 Spark，資料科學程序的下一個步驟是透過探索和虛擬化以更深入瞭解資料。</span><span class="sxs-lookup"><span data-stu-id="e460a-196">Once the data has been brought into Spark, the next step in the data science process is to gain deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="e460a-197">在本節中，我們會使用 SQL 查詢檢查計程車資料，並繪製目標變數和潛在功能以進行視覺檢查。</span><span class="sxs-lookup"><span data-stu-id="e460a-197">In this section, we examine the taxi data using SQL queries and plot the target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="e460a-198">具體來說，我們會繪製計程車車程中的乘客計數頻率、小費金額的頻率，及小費如何隨付款金額和類型而異。</span><span class="sxs-lookup"><span data-stu-id="e460a-198">Specifically, we plot the frequency of passenger counts in taxi trips, the frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-the-sample-of-taxi-trips"></a><span data-ttu-id="e460a-199">在計程車車程範例中繪製乘客計數頻率的長條圖</span><span class="sxs-lookup"><span data-stu-id="e460a-199">Plot a histogram of passenger count frequencies in the sample of taxi trips</span></span>
<span data-ttu-id="e460a-200">此程式碼與後續程式碼片段使用了 SQL magic 來查詢範例及本機 magic 以繪製資料。</span><span class="sxs-lookup"><span data-stu-id="e460a-200">This code and subsequent snippets use SQL magic to query the sample and local magic to plot the data.</span></span>

* <span data-ttu-id="e460a-201">**SQL magic (`%%sql`)** HDInsight PySpark 核心支援針對 sqlContext 進行簡單的內嵌 HiveQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="e460a-201">**SQL magic (`%%sql`)** The HDInsight PySpark kernel supports easy inline HiveQL queries against the sqlContext.</span></span> <span data-ttu-id="e460a-202">「-o VARIABLE_NAME」引數會將 SQL 查詢的輸出，保存為 Jupyter 伺服器上的 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="e460a-202">The (-o VARIABLE_NAME) argument persists the output of the SQL query as a Pandas DataFrame on the Jupyter server.</span></span> <span data-ttu-id="e460a-203">這代表會在本機模式中使用此引數。</span><span class="sxs-lookup"><span data-stu-id="e460a-203">This means it is available in the local mode.</span></span>
* <span data-ttu-id="e460a-204">**`%%local` magic** 是用來在 Jupyter 伺服器本機 (HDInsight 叢集的前端節點) 上執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-204">The **`%%local` magic** is used to run code locally on the Jupyter server, which is the headnode of the HDInsight cluster.</span></span> <span data-ttu-id="e460a-205">一般來說，您使用 `%%sql -o` magic 之後使用 `%%local` magic 來執行查詢。</span><span class="sxs-lookup"><span data-stu-id="e460a-205">Typically, you use `%%local` magic after the `%%sql -o` magic is used to run a query.</span></span> <span data-ttu-id="e460a-206">-o 參數會將 SQL 查詢的輸出保存在本機。</span><span class="sxs-lookup"><span data-stu-id="e460a-206">The -o parameter would persist the output of the SQL query locally.</span></span> <span data-ttu-id="e460a-207">接著 `%%local` magic 會針對保存在本機之 SQL 查詢的輸出，觸發下一組程式碼片段在本機執行。</span><span class="sxs-lookup"><span data-stu-id="e460a-207">Then the `%%local` magic triggers the next set of code snippets to run locally against the output of the SQL queries that has been persisted locally.</span></span> <span data-ttu-id="e460a-208">執行完程式碼後，輸出將會自動以視覺化方式呈現。</span><span class="sxs-lookup"><span data-stu-id="e460a-208">The output is automatically visualized after you run the code.</span></span>

<span data-ttu-id="e460a-209">此查詢會擷取按乘客計數排列的車程。</span><span class="sxs-lookup"><span data-stu-id="e460a-209">This query retrieves the trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="e460a-210">此程式碼從查詢輸出中建立了本機資料框架，以及繪製資料。</span><span class="sxs-lookup"><span data-stu-id="e460a-210">This code creates a local data-frame from the query output and plots the data.</span></span> <span data-ttu-id="e460a-211">`%%local` magic 建立了本機資料框架「`sqlResults`」，可用於搭配 Matplotlib 進行繪製。</span><span class="sxs-lookup"><span data-stu-id="e460a-211">The `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="e460a-212">在本逐步解說中，會多次使用此 PySpark magic。</span><span class="sxs-lookup"><span data-stu-id="e460a-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="e460a-213">如果資料總量很大，您應該取樣以建立可容納於本機記憶體的資料框架。</span><span class="sxs-lookup"><span data-stu-id="e460a-213">If the amount of data is large, you should sample to create a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES. 
    # CLICK ON THE TYPE OF PLOT TO BE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="e460a-214">以下是繪製按乘客計數排列車程的程式碼</span><span class="sxs-lookup"><span data-stu-id="e460a-214">Here is the code to plot the trips by passenger counts</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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

<span data-ttu-id="e460a-215">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-215">**OUTPUT**</span></span>

![按乘客計數排列的車程頻率](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="e460a-217">在 Notebook 內使用 [類型]  功能表按鈕，您可以選擇幾種不同類型的視覺效果 (資料表、圓形圖、折線圖、區域圖或橫條圖)。</span><span class="sxs-lookup"><span data-stu-id="e460a-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using the **Type** menu buttons in the notebook.</span></span> <span data-ttu-id="e460a-218">橫條圖繪製結果會在此顯示。</span><span class="sxs-lookup"><span data-stu-id="e460a-218">The Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="e460a-219">繪製小費金額，和小費金額如何隨乘客計數和費用金額變化的長條圖。</span><span class="sxs-lookup"><span data-stu-id="e460a-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="e460a-220">使用 SQL 查詢來取樣資料。</span><span class="sxs-lookup"><span data-stu-id="e460a-220">Use a SQL query to sample data..</span></span>

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


<span data-ttu-id="e460a-221">此程式碼儲存格使用 SQL 查詢來建立三種圖的資料。</span><span class="sxs-lookup"><span data-stu-id="e460a-221">This code cell uses the SQL query to create three plots the data.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="e460a-222">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="e460a-222">**OUTPUT:**</span></span> 

![小費金額分佈](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![按乘客計數排列的小費金額](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![按費用金額排列的小費金額](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="e460a-226">模型化的功能工程、轉換和資料準備</span><span class="sxs-lookup"><span data-stu-id="e460a-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="e460a-227">本節描述並提供程序的程式碼，可用來準備資料以供 ML 模型化使用。</span><span class="sxs-lookup"><span data-stu-id="e460a-227">This section describes and provides the code for procedures used to prepare data for use in ML modeling.</span></span> <span data-ttu-id="e460a-228">它示範如何執行下列工作：</span><span class="sxs-lookup"><span data-stu-id="e460a-228">It shows how to do the following tasks:</span></span>

* <span data-ttu-id="e460a-229">將小時分割到流量時間分類區以建立新功能</span><span class="sxs-lookup"><span data-stu-id="e460a-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="e460a-230">索引和 on-hot 編碼分類功能</span><span class="sxs-lookup"><span data-stu-id="e460a-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="e460a-231">建立輸入到 ML 函式的標示點物件</span><span class="sxs-lookup"><span data-stu-id="e460a-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="e460a-232">建立資料的隨機子取樣，並將它分割成訓練和測試集</span><span class="sxs-lookup"><span data-stu-id="e460a-232">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
* <span data-ttu-id="e460a-233">調整功能</span><span class="sxs-lookup"><span data-stu-id="e460a-233">Feature scaling</span></span>
* <span data-ttu-id="e460a-234">快取記憶體中的物件</span><span class="sxs-lookup"><span data-stu-id="e460a-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="e460a-235">將流量時間分割到分類區以建立新功能</span><span class="sxs-lookup"><span data-stu-id="e460a-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="e460a-236">此程式碼示範如何將流量時間分割到分類區以建立新功能，以及如何從記憶體快取產生的資料框架。</span><span class="sxs-lookup"><span data-stu-id="e460a-236">This code shows how to create a new feature by partitioning traffic times into bins and then how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="e460a-237">在重複使用彈性分散式資料集 (RDD) 和資料框架的位置，快取可改善執行時間。</span><span class="sxs-lookup"><span data-stu-id="e460a-237">Caching leads to improved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="e460a-238">因此，我們會在逐步解說中的幾個階段快取 RDD 和資料框架。</span><span class="sxs-lookup"><span data-stu-id="e460a-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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

<span data-ttu-id="e460a-239">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-239">**OUTPUT**</span></span>

<span data-ttu-id="e460a-240">126050</span><span class="sxs-lookup"><span data-stu-id="e460a-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="e460a-241">索引和 one-hot 編碼分類功能</span><span class="sxs-lookup"><span data-stu-id="e460a-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="e460a-242">本節說明如何索引並編碼分類功能，以輸入模型化函式中。</span><span class="sxs-lookup"><span data-stu-id="e460a-242">This section shows how to index or encode categorical features for input into the modeling functions.</span></span> <span data-ttu-id="e460a-243">MLlib 的模型化和預測函式需要先執行功能來分類要索引或編碼的分類輸入資料，才能使用這些資料。</span><span class="sxs-lookup"><span data-stu-id="e460a-243">The modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior to use.</span></span> 

<span data-ttu-id="e460a-244">根據模型，您需要以不同方式索引或編碼它們。</span><span class="sxs-lookup"><span data-stu-id="e460a-244">Depending on the model, you need to index or encode them in different ways.</span></span> <span data-ttu-id="e460a-245">例如，羅吉斯和線性迴歸模型需要一個有效編碼方式，例如，含 3 個類別的一個功能可擴充至 3 個功能資料行，根據觀察的類別，每個資料行包含 0 或 1。</span><span class="sxs-lookup"><span data-stu-id="e460a-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="e460a-246">MLlib 提供 [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) 函式以執行 one-hot 編碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function to do one-hot encoding.</span></span> <span data-ttu-id="e460a-247">此編碼器會將標籤索引資料行對應到二進位向量資料行 (最多有一個單一值)。</span><span class="sxs-lookup"><span data-stu-id="e460a-247">This encoder maps a column of label indices to a column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="e460a-248">這種編碼方式允許將預期數值功能的演算法 (例如羅吉斯迴歸) 套用至分類功能。</span><span class="sxs-lookup"><span data-stu-id="e460a-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, to be applied to categorical features.</span></span>

<span data-ttu-id="e460a-249">以下是要索引及編碼分類功能的程式碼︰</span><span class="sxs-lookup"><span data-stu-id="e460a-249">Here is the code to index and encode categorical features:</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler, OneHotEncoder, VectorIndexer

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


<span data-ttu-id="e460a-250">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-250">**OUTPUT**</span></span>

<span data-ttu-id="e460a-251">執行上述儲存格所花費的時間︰3.14 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-251">Time taken to execute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="e460a-252">建立輸入到 ML 函式的標示點物件</span><span class="sxs-lookup"><span data-stu-id="e460a-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="e460a-253">本節包含的程式碼示範如何將分類的文字資料索引做為標示點資料類型以及如何編碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-253">This section contains code that shows how to index categorical text data as a labeled point data type and how to encode it.</span></span> <span data-ttu-id="e460a-254">這可準備它用來訓練及測試 MLlib 羅吉斯迴歸和其他分類模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-254">This prepares it to be used to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="e460a-255">標示點物件是彈性分散式資料集 (RDD)，其格式化成適合 MLlib 中大部分的 ML 演算法的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="e460a-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="e460a-256">[標示點](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 是本機向量 (密集或疏鬆)，與標籤/回應相關聯。</span><span class="sxs-lookup"><span data-stu-id="e460a-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="e460a-257">以下是要為二進位分類進行索引及編碼文字功能的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-257">Here is the code to index and encode text features for binary classification.</span></span>

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


<span data-ttu-id="e460a-258">以下是要為線性迴歸分析進行編碼及建立類別文字功能的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-258">Here is the code to encode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-the-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="e460a-259">建立資料的隨機子取樣，並將它分割成訓練和測試集</span><span class="sxs-lookup"><span data-stu-id="e460a-259">Create a random sub-sampling of the data and split it into training and testing sets</span></span>
<span data-ttu-id="e460a-260">此程式碼會建立隨機取樣資料 (這裡使用 25%)。</span><span class="sxs-lookup"><span data-stu-id="e460a-260">This code creates a random sampling of the data (25% is used here).</span></span> <span data-ttu-id="e460a-261">雖然您不需要這個範例 (因為資料集的大小)，我們將在這裡示範如何取樣，</span><span class="sxs-lookup"><span data-stu-id="e460a-261">Although it is not required for this example due to the size of the dataset, we demonstrate how you can sample the data here.</span></span> <span data-ttu-id="e460a-262">這樣您就了解如何在需要時使用它來自行解決問題。</span><span class="sxs-lookup"><span data-stu-id="e460a-262">Then you know how to use it for your own problem if needed.</span></span> <span data-ttu-id="e460a-263">當樣本非常大時，這樣可在訓練模型時節省大量時間。</span><span class="sxs-lookup"><span data-stu-id="e460a-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="e460a-264">接下來我們將範例分割成訓練部分 (這裡為 75%) 和測試部分 (這裡為 25%)，以便在分類和迴歸模型化中使用。</span><span class="sxs-lookup"><span data-stu-id="e460a-264">Next we split the sample into a training part (75% here) and a testing part (25% here) to use in classification and regression modeling.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="e460a-265">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-265">**OUTPUT**</span></span>

<span data-ttu-id="e460a-266">執行上述儲存格所花費的時間︰0.31 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-266">Time taken to execute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="e460a-267">調整功能</span><span class="sxs-lookup"><span data-stu-id="e460a-267">Feature scaling</span></span>
<span data-ttu-id="e460a-268">調整功能，也稱為資料正規化，以確保具廣泛分散值的功能在目標函式中沒有過多權重。</span><span class="sxs-lookup"><span data-stu-id="e460a-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in the objective function.</span></span> <span data-ttu-id="e460a-269">用於調整功能的程式碼會使用 [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) ，將功能調整至單位變異數。</span><span class="sxs-lookup"><span data-stu-id="e460a-269">The code for feature scaling uses the [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) to scale the features to unit variance.</span></span> <span data-ttu-id="e460a-270">這是由 MLlib 提供，用於使用隨機梯度下降 (SGD) 的線性迴歸。</span><span class="sxs-lookup"><span data-stu-id="e460a-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="e460a-271">SGD 為訓練廣泛的其他機器學習模型的常用演算法，例如正則化迴歸或支援向量機器 (SVM)。</span><span class="sxs-lookup"><span data-stu-id="e460a-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="e460a-272">我們找到了適用於調整功能的 LinearRegressionWithSGD 演算法。</span><span class="sxs-lookup"><span data-stu-id="e460a-272">We have found the LinearRegressionWithSGD algorithm to be sensitive to feature scaling.</span></span>   
> 
> 

<span data-ttu-id="e460a-273">以下是要用於正規化線性 SGD 演算法的比例調整變數的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-273">Here is the code to scale variables for use with the regularized linear SGD algorithm.</span></span>

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

<span data-ttu-id="e460a-274">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-274">**OUTPUT**</span></span>

<span data-ttu-id="e460a-275">執行上述儲存格所花費的時間︰11.67 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-275">Time taken to execute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="e460a-276">快取記憶體中的物件</span><span class="sxs-lookup"><span data-stu-id="e460a-276">Cache objects in memory</span></span>
<span data-ttu-id="e460a-277">快取用於分類、迴歸和縮放功能的輸入資料框架物件，可降低訓練和測試 ML 演算法所花費的時間。</span><span class="sxs-lookup"><span data-stu-id="e460a-277">The time taken for training and testing of ML algorithms can be reduced by caching the input data frame objects used for classification, regression and, scaled features.</span></span>

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

<span data-ttu-id="e460a-278">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-278">**OUTPUT**</span></span> 

<span data-ttu-id="e460a-279">執行上述儲存格所花費的時間︰0.13 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-279">Time taken to execute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="e460a-280">使用二進位分類模型來預測是否支付小費</span><span class="sxs-lookup"><span data-stu-id="e460a-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="e460a-281">本節說明如何為二進位分類工作使用三個模型，預測是否支付計程車車程的小費。</span><span class="sxs-lookup"><span data-stu-id="e460a-281">This section shows how use three models for the binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="e460a-282">顯示模型如下︰</span><span class="sxs-lookup"><span data-stu-id="e460a-282">The models presented are:</span></span>

* <span data-ttu-id="e460a-283">羅吉斯迴歸</span><span class="sxs-lookup"><span data-stu-id="e460a-283">Logistic regression</span></span> 
* <span data-ttu-id="e460a-284">隨機樹系</span><span class="sxs-lookup"><span data-stu-id="e460a-284">Random forest</span></span>
* <span data-ttu-id="e460a-285">漸層停駐提升樹狀結構</span><span class="sxs-lookup"><span data-stu-id="e460a-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="e460a-286">每個模型建置程式碼區段會分成幾個步驟︰</span><span class="sxs-lookup"><span data-stu-id="e460a-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="e460a-287">**模型定型** 資料</span><span class="sxs-lookup"><span data-stu-id="e460a-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="e460a-288">**模型評估** </span><span class="sxs-lookup"><span data-stu-id="e460a-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="e460a-289">**儲存模型** </span><span class="sxs-lookup"><span data-stu-id="e460a-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="e460a-290">我們會示範如何以兩種方式使用參數掃掠執行交叉驗證 (CV)︰</span><span class="sxs-lookup"><span data-stu-id="e460a-290">We show how to do cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="e460a-291">使用 **泛型** 自訂程式碼，可以套用至 MLlib 中的任何演算法，以及套用至演算法中的任何參數集。</span><span class="sxs-lookup"><span data-stu-id="e460a-291">Using **generic** custom code which can be applied to any algorithm in MLlib and to any parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="e460a-292">使用 **pySpark CrossValidator 管線函式**。</span><span class="sxs-lookup"><span data-stu-id="e460a-292">Using the **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="e460a-293">請注意，CrossValidator 對 Spark 1.5.0 有幾項限制︰</span><span class="sxs-lookup"><span data-stu-id="e460a-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="e460a-294">管線模型無法儲存/保存供未來取用。</span><span class="sxs-lookup"><span data-stu-id="e460a-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="e460a-295">無法用於模型中的每個參數。</span><span class="sxs-lookup"><span data-stu-id="e460a-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="e460a-296">無法用於每個 MLlib 演算法。</span><span class="sxs-lookup"><span data-stu-id="e460a-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-the-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="e460a-297">針對二進位分類搭配使用一般交叉驗證和超參數掃掠與羅吉斯迴歸演算法</span><span class="sxs-lookup"><span data-stu-id="e460a-297">Generic cross validation and hyperparameter sweeping used with the logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="e460a-298">本節的程式碼顯示如何定型、評估及使用 [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) 來儲存羅吉斯迴歸模型，可預測是否針對 NYC 計程車車程和費用資料集的某趟車程支付小費。</span><span class="sxs-lookup"><span data-stu-id="e460a-298">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="e460a-299">模型是使用交叉驗證 (CV) 和超參數掃掠定型，這兩種方法是使用自訂程式碼實作，可以套用至 MLlib 中的任何學習演算法。</span><span class="sxs-lookup"><span data-stu-id="e460a-299">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied to any of the learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="e460a-300">執行此自訂 CV 程式碼可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="e460a-300">The execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="e460a-301">**使用 CV 及超參數掃掠來定型羅吉斯迴歸模型**</span><span class="sxs-lookup"><span data-stu-id="e460a-301">**Train the logistic regression model using CV and hyperparameter sweeping**</span></span>

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

    # SET NUM FOLDS AND NUM PARAMETER SETS TO SWEEP ON
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


    # PRINT COEFFICIENTS AND INTERCEPT OF THE MODEL
    # NOTE: There are 20 coefficient terms for the 10 features, 
    #       and the different categories for features: vendorVec (2), rateVec, paymentVec (6), TrafficTimeBinsVec (4)
    print("Coefficients: " + str(logitBest.weights))
    print("Intercept: " + str(logitBest.intercept))

    # PRINT ELAPSED TIME    
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="e460a-302">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-302">**OUTPUT**</span></span>

<span data-ttu-id="e460a-303">係數：[0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="e460a-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="e460a-304">截距：-0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="e460a-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="e460a-305">執行上述儲存格所花費的時間︰14.43 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-305">Time taken to execute above cell: 14.43 seconds</span></span>

<span data-ttu-id="e460a-306">**使用標準度量評估二進位分類模型**</span><span class="sxs-lookup"><span data-stu-id="e460a-306">**Evaluate the binary classification model with standard metrics**</span></span>

<span data-ttu-id="e460a-307">本章節中的程式碼示範如何針對測試資料集評估羅吉斯迴歸模型，包括 ROC 曲線的繪製。</span><span class="sxs-lookup"><span data-stu-id="e460a-307">The code in this section shows how to evaluate a logistic regression model against a test data-set, including a plot of the ROC curve.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="e460a-308">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-308">**OUTPUT**</span></span>

<span data-ttu-id="e460a-309">PR 下的領域 = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="e460a-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="e460a-310">ROC 下的領域 = 0.983383274312</span><span class="sxs-lookup"><span data-stu-id="e460a-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="e460a-311">摘要狀態</span><span class="sxs-lookup"><span data-stu-id="e460a-311">Summary Stats</span></span>

<span data-ttu-id="e460a-312">精確度 = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="e460a-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="e460a-313">回收 = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="e460a-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="e460a-314">F1 分數 = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="e460a-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="e460a-315">執行上述儲存格所花費的時間︰2.67 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-315">Time taken to execute above cell: 2.67 seconds</span></span>

<span data-ttu-id="e460a-316">**繪製 ROC 曲線。**</span><span class="sxs-lookup"><span data-stu-id="e460a-316">**Plot the ROC curve.**</span></span>

<span data-ttu-id="e460a-317">predictionAndLabelsDF 已在先前的儲存格中已註冊為 tmp_results 資料表。</span><span class="sxs-lookup"><span data-stu-id="e460a-317">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="e460a-318">tmp_results 可用來執行查詢，並將結果輸出至 sqlResults 資料框架供繪製之用。</span><span class="sxs-lookup"><span data-stu-id="e460a-318">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="e460a-319">程式碼如下。</span><span class="sxs-lookup"><span data-stu-id="e460a-319">Here is the code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="e460a-320">以下是建立預測和繪製 ROC 曲線的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-320">Here is the code to make predictions and plot the ROC-curve.</span></span>

    # MAKE PREDICTIONS AND PLOT ROC-CURVE

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES                              
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


<span data-ttu-id="e460a-321">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-321">**OUTPUT**</span></span>

![泛型方法的羅吉斯迴歸 ROC 曲線](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="e460a-323">**blob 中供未來取用的保留模型**</span><span class="sxs-lookup"><span data-stu-id="e460a-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="e460a-324">本章節中的程式碼示範如何儲存羅吉斯迴歸模型以供取用。</span><span class="sxs-lookup"><span data-stu-id="e460a-324">The code in this section shows how to save the logistic regression model for consumption.</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";


<span data-ttu-id="e460a-325">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-325">**OUTPUT**</span></span>

<span data-ttu-id="e460a-326">執行上述儲存格所花費的時間︰34.57 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-326">Time taken to execute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="e460a-327">搭配使用 MLlib 的 CrossValidator 管線函式與 LogisticRegression (彈性迴歸) 模型</span><span class="sxs-lookup"><span data-stu-id="e460a-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="e460a-328">本節的程式碼顯示如何定型、評估及使用 [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) 來儲存羅吉斯迴歸模型，可預測是否針對 NYC 計程車車程和費用資料集的某趟車程支付小費。</span><span class="sxs-lookup"><span data-stu-id="e460a-328">The code in this section shows how to train, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="e460a-329">模型是使用交叉驗證 (CV) 和超參數掃掠定型，這兩種方法是使用 CV 的 MLlib CrossValidator 管線函式和參數掃掠進行實作。</span><span class="sxs-lookup"><span data-stu-id="e460a-329">The model is trained using cross validation (CV) and hyperparameter sweeping implemented with the MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="e460a-330">執行此 MLlib CV 程式碼可能需要數分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="e460a-330">The execution of this MLlib CV code can take several minutes.</span></span>
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

    # CONVERT TO DATA-FRAME: THIS DOES NOT RUN ON RDDs
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds";

<span data-ttu-id="e460a-331">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-331">**OUTPUT**</span></span>

<span data-ttu-id="e460a-332">執行上述儲存格所花費的時間︰107.98 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-332">Time taken to execute above cell: 107.98 seconds</span></span>

<span data-ttu-id="e460a-333">**繪製 ROC 曲線。**</span><span class="sxs-lookup"><span data-stu-id="e460a-333">**Plot the ROC curve.**</span></span>

<span data-ttu-id="e460a-334">predictionAndLabelsDF 已在先前的儲存格中已註冊為 tmp_results 資料表。</span><span class="sxs-lookup"><span data-stu-id="e460a-334">The *predictionAndLabelsDF* is registered as a table, *tmp_results*, in the previous cell.</span></span> <span data-ttu-id="e460a-335">tmp_results 可用來執行查詢，並將結果輸出至 sqlResults 資料框架供繪製之用。</span><span class="sxs-lookup"><span data-stu-id="e460a-335">*tmp_results* can be used to do queries and output results into the sqlResults data-frame for plotting.</span></span> <span data-ttu-id="e460a-336">程式碼如下。</span><span class="sxs-lookup"><span data-stu-id="e460a-336">Here is the code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="e460a-337">以下是繪製 ROC 曲線的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-337">Here is the code to plot the ROC curve.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES 
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


<span data-ttu-id="e460a-338">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-338">**OUTPUT**</span></span>

![使用 MLlib 的 CrossValidator 的羅吉斯迴歸 ROC 曲線](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="e460a-340">隨機樹系分類</span><span class="sxs-lookup"><span data-stu-id="e460a-340">Random forest classification</span></span>
<span data-ttu-id="e460a-341">本節的程式碼顯示如何訓練評估及儲存隨機樹系迴歸，可預測是否針對 NYC 計程車車程和費用資料集的某趟車程支付小費。</span><span class="sxs-lookup"><span data-stu-id="e460a-341">The code in this section shows how to train, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

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
    ## UN-COMMENT IF YOU WANT TO PRING TREES
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


<span data-ttu-id="e460a-342">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-342">**OUTPUT**</span></span>

<span data-ttu-id="e460a-343">ROC 下的領域 = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="e460a-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="e460a-344">執行上述儲存格所花費的時間︰26.72 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-344">Time taken to execute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="e460a-345">漸層停駐提升樹狀結構類別</span><span class="sxs-lookup"><span data-stu-id="e460a-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="e460a-346">本節的程式碼顯示如何訓練評估及儲存漸層停駐提升樹狀結構模型，可預測是否針對 NYC 計程車車程和費用資料集的某趟車程支付小費。</span><span class="sxs-lookup"><span data-stu-id="e460a-346">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in the NYC taxi trip and fare dataset.</span></span>

    # RECORD START TIME
    timestart = datetime.datetime.now()

    # LOAD PYSPARK LIBRARIES
    from pyspark.mllib.tree import GradientBoostedTrees, GradientBoostedTreesModel

    # SPECIFY NUMBER OF CATEGORIES FOR CATEGORICAL FEATURES. FEATURE #0 HAS 2 CATEGORIES, FEATURE #2 HAS 2 CATEGORIES, AND SO ON
    categoricalFeaturesInfo={0:2, 1:2, 2:6, 3:4}

    gbtModel = GradientBoostedTrees.trainClassifier(indexedTRAINbinary, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                    numIterations=10)
    ## UNCOMMENT IF YOU WANT TO PRINT TREE DETAILS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="e460a-347">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-347">**OUTPUT**</span></span>

<span data-ttu-id="e460a-348">ROC 下的領域 = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="e460a-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="e460a-349">執行上述儲存格所花費的時間︰28.13 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-349">Time taken to execute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="e460a-350">使用迴歸模型預測小費金額 (非使用 CV)</span><span class="sxs-lookup"><span data-stu-id="e460a-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="e460a-351">本節說明如何使用三種迴歸工作模型：根據其他小費功能預測支付的計程車車程的小費金額。</span><span class="sxs-lookup"><span data-stu-id="e460a-351">This section shows how use three models for the regression task: predict the tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="e460a-352">顯示模型如下︰</span><span class="sxs-lookup"><span data-stu-id="e460a-352">The models presented are:</span></span>

* <span data-ttu-id="e460a-353">正規化線性迴歸</span><span class="sxs-lookup"><span data-stu-id="e460a-353">Regularized linear regression</span></span>
* <span data-ttu-id="e460a-354">隨機樹系</span><span class="sxs-lookup"><span data-stu-id="e460a-354">Random forest</span></span>
* <span data-ttu-id="e460a-355">漸層停駐提升樹狀結構</span><span class="sxs-lookup"><span data-stu-id="e460a-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="e460a-356">這些模型將在簡介中說明。</span><span class="sxs-lookup"><span data-stu-id="e460a-356">These models were described in the introduction.</span></span> <span data-ttu-id="e460a-357">每個模型建置程式碼區段會分成幾個步驟︰</span><span class="sxs-lookup"><span data-stu-id="e460a-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="e460a-358">**模型定型** 資料</span><span class="sxs-lookup"><span data-stu-id="e460a-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="e460a-359">**模型評估** </span><span class="sxs-lookup"><span data-stu-id="e460a-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="e460a-360">**儲存模型** </span><span class="sxs-lookup"><span data-stu-id="e460a-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="e460a-361">AZURE 附註︰交叉驗證未與本節中的三個迴歸模型搭配使用，因為這是用來顯示羅吉斯迴歸模型詳細資料的方法。</span><span class="sxs-lookup"><span data-stu-id="e460a-361">AZURE NOTE: Cross-validation is not used with the three regression models in this section, since this was shown in detail for the logistic regression models.</span></span> <span data-ttu-id="e460a-362">本主題的＜附錄＞示範如何針對線性迴歸使用 CV 與 Elastic Net。</span><span class="sxs-lookup"><span data-stu-id="e460a-362">An example showing how to use CV with Elastic Net for linear regression is provided in the Appendix of this topic.</span></span>
> 
> <span data-ttu-id="e460a-363">AZURE NOTE︰在我們的經驗中，交集的 LinearRegressionWithSGD 模型可能會發生問題，且必須小心變更/最佳化參數以取得有效的模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="e460a-364">調整變數對於聚合很有用。</span><span class="sxs-lookup"><span data-stu-id="e460a-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="e460a-365">本主題中的＜附錄＞所顯示的 Elastic Net 迴歸也可用來取代 LinearRegressionWithSGD。</span><span class="sxs-lookup"><span data-stu-id="e460a-365">Elastic net regression, shown in the Appendix to this topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="e460a-366">使用 SGD 的線性迴歸</span><span class="sxs-lookup"><span data-stu-id="e460a-366">Linear regression with SGD</span></span>
<span data-ttu-id="e460a-367">本節的程式碼示範如何使用縮放功能來訓練線性迴歸 (使用隨機梯度下降 (SGD) 以最佳化)，以及如何評分、評估並將模型儲存在 Azure Blob 儲存體 (WASB)。</span><span class="sxs-lookup"><span data-stu-id="e460a-367">The code in this section shows how to use scaled features to train a linear regression that uses stochastic gradient descent (SGD) for optimization, and how to score, evaluate, and save the model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="e460a-368">在我們的經驗中，交集的 LinearRegressionWithSGD 模型可能會發生問題，且必須小心變更/最佳化參數以取得有效的模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-368">In our experience, there can be issues with the convergence of LinearRegressionWithSGD models, and parameters need to be changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="e460a-369">調整變數對於聚合很有用。</span><span class="sxs-lookup"><span data-stu-id="e460a-369">Scaling of variables significantly helps with convergence.</span></span>
> 
> 

    # LINEAR REGRESSION WITH SGD 

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="e460a-370">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-370">**OUTPUT**</span></span>

<span data-ttu-id="e460a-371">係數：[0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span><span class="sxs-lookup"><span data-stu-id="e460a-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="e460a-372">截距：0.854507624459</span><span class="sxs-lookup"><span data-stu-id="e460a-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="e460a-373">RMSE = 1.23485131376</span><span class="sxs-lookup"><span data-stu-id="e460a-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="e460a-374">R-sqr = 0.597963951127</span><span class="sxs-lookup"><span data-stu-id="e460a-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="e460a-375">執行上述儲存格所花費的時間︰38.62 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-375">Time taken to execute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="e460a-376">隨機樹系迴歸</span><span class="sxs-lookup"><span data-stu-id="e460a-376">Random Forest regression</span></span>
<span data-ttu-id="e460a-377">本節的程式碼顯示如何訓練評估及儲存隨機樹系模型，可預測 NYC 計程車車程資料的小費金額。</span><span class="sxs-lookup"><span data-stu-id="e460a-377">The code in this section shows how to train, evaluate, and save a random forest model that predicts tip amount for the NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="e460a-378">在附錄中提供使用自訂程式碼的交叉驗證與參數掃掠。</span><span class="sxs-lookup"><span data-stu-id="e460a-378">Cross-validation with parameter sweeping using custom code is provided in the appendix.</span></span>
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
    # UN-COMMENT IF YOU WANT TO PRING TREES
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 

<span data-ttu-id="e460a-379">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-379">**OUTPUT**</span></span>

<span data-ttu-id="e460a-380">RMSE = 0.931981967875</span><span class="sxs-lookup"><span data-stu-id="e460a-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="e460a-381">R-sqr = 0.733445485802</span><span class="sxs-lookup"><span data-stu-id="e460a-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="e460a-382">執行上述儲存格所花費的時間︰25.98 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-382">Time taken to execute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="e460a-383">漸層停駐提升樹狀結構迴歸</span><span class="sxs-lookup"><span data-stu-id="e460a-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="e460a-384">本節的程式碼顯示如何訓練評估及儲存漸層停駐提升樹狀結構模型，可預測 NYC 計程車車程資料的小費金額。</span><span class="sxs-lookup"><span data-stu-id="e460a-384">The code in this section shows how to train, evaluate, and save a gradient boosting trees model that predicts tip amount for the NYC taxi trip data.</span></span>

<span data-ttu-id="e460a-385">* * 來定型及評估 * *</span><span class="sxs-lookup"><span data-stu-id="e460a-385">**Train and evaluate **</span></span>

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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="e460a-386">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-386">**OUTPUT**</span></span>

<span data-ttu-id="e460a-387">RMSE = 0.928172197114</span><span class="sxs-lookup"><span data-stu-id="e460a-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="e460a-388">R-sqr = 0.732680354389</span><span class="sxs-lookup"><span data-stu-id="e460a-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="e460a-389">執行上述儲存格所花費的時間︰20.9 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-389">Time taken to execute above cell: 20.9 seconds</span></span>

<span data-ttu-id="e460a-390">**圖**</span><span class="sxs-lookup"><span data-stu-id="e460a-390">**Plot**</span></span>

<span data-ttu-id="e460a-391">tmp_results 已在先前的儲存格中註冊為 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="e460a-391">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="e460a-392">來自資料表的結果已輸出至 sqlResults  資料框架以供繪製之用。</span><span class="sxs-lookup"><span data-stu-id="e460a-392">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="e460a-393">程式碼如下</span><span class="sxs-lookup"><span data-stu-id="e460a-393">Here is the code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="e460a-394">以下是使用 Jupyter 伺服器繪製資料的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-394">Here is the code to plot the data using the Jupyter server.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="e460a-396">附錄︰使用交叉驗證與參數掃掠的額外迴歸工作</span><span class="sxs-lookup"><span data-stu-id="e460a-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="e460a-397">本附錄包含程式碼，示範如何針對線性迴歸使用彈性 net 以執行 CV，以及如何針對隨機樹系迴歸使用自訂程式碼，以參數掃掠執行 CV。</span><span class="sxs-lookup"><span data-stu-id="e460a-397">This appendix contains code showing how to do CV using Elastic net for linear regression and how to do CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="e460a-398">針對線性迴歸使用彈性 net 進行交叉驗證</span><span class="sxs-lookup"><span data-stu-id="e460a-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="e460a-399">本章節中的程式碼示範如何針對線性迴歸使用彈性 net 進行交叉驗證，以及如何針對測試資料評估模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-399">The code in this section shows how to do cross validation using Elastic net for linear regression and how to evaluate the model against test data.</span></span>

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
    # SIMPLY THE MODEL HERE, WITHOUT TRANSFORMATIONS
    pipeline = Pipeline(stages=[lr])

    # DEFINE CV WITH PARAMETER SWEEP
    cv = CrossValidator(estimator= lr,
                        estimatorParamMaps=paramGrid,
                        evaluator=RegressionEvaluator(),
                        numFolds=3)

    # CONVERT TO DATA FRAME, AS CROSSVALIDATOR WON'T RUN ON RDDS
    trainDataFrame = sqlContext.createDataFrame(oneHotTRAINreg, ["features", "label"])

    # TRAIN WITH CROSS-VALIDATION
    cv_model = cv.fit(trainDataFrame)


    # EVALUATE MODEL ON TEST SET
    testDataFrame = sqlContext.createDataFrame(oneHotTESTreg, ["features", "label"])

    # MAKE PREDICTIONS ON TEST DOCUMENTS
    # cvModel uses the best model found (lrModel).
    predictionAndLabels = cv_model.transform(testDataFrame)

    # CONVERT TO DF AND SAVE REGISER DF AS TABLE
    predictionAndLabels.registerTempTable("tmp_results");

    # PRINT ELAPSED TIME
    timeend = datetime.datetime.now()
    timedelta = round((timeend-timestart).total_seconds(), 2) 
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="e460a-400">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-400">**OUTPUT**</span></span>

<span data-ttu-id="e460a-401">執行上述儲存格所花費的時間︰161.21 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-401">Time taken to execute above cell: 161.21  seconds</span></span>

<span data-ttu-id="e460a-402">**使用 R-SQR 度量進行評估**</span><span class="sxs-lookup"><span data-stu-id="e460a-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="e460a-403">tmp_results 已在先前的儲存格中註冊為 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="e460a-403">*tmp_results* is registered as a Hive table in the previous cell.</span></span> <span data-ttu-id="e460a-404">來自資料表的結果已輸出至 sqlResults  資料框架以供繪製之用。</span><span class="sxs-lookup"><span data-stu-id="e460a-404">Results from the table are output into the *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="e460a-405">程式碼如下</span><span class="sxs-lookup"><span data-stu-id="e460a-405">Here is the code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="e460a-406">以下是計算 R-sqr 的程式碼。</span><span class="sxs-lookup"><span data-stu-id="e460a-406">Here is the code to calculate R-sqr.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="e460a-407">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-407">**OUTPUT**</span></span>

<span data-ttu-id="e460a-408">R-sqr = 0.619184907088</span><span class="sxs-lookup"><span data-stu-id="e460a-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="e460a-409">針對隨機樹系迴歸使用自訂程式碼以參數掃掠進行交叉驗證。</span><span class="sxs-lookup"><span data-stu-id="e460a-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="e460a-410">本章節中的程式碼示範如何針對隨機樹系迴歸使用自訂程式碼以參數掃掠執行交叉驗證，以及如何針對測試資料評估模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-410">The code in this section shows how to do cross validation with parameter sweep using custom code for random forest regression and how to evaluate the model against test data.</span></span>

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

    # SPECIFY NUMFOLDS AND ARRAY TO HOLD METRICS
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
    print "Time taken to execute above cell: " + str(timedelta) + " seconds"; 


<span data-ttu-id="e460a-411">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-411">**OUTPUT**</span></span>

<span data-ttu-id="e460a-412">RMSE = 0.906972198262</span><span class="sxs-lookup"><span data-stu-id="e460a-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="e460a-413">R-sqr = 0.740751197012</span><span class="sxs-lookup"><span data-stu-id="e460a-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="e460a-414">執行上述儲存格所花費的時間︰69.17 秒</span><span class="sxs-lookup"><span data-stu-id="e460a-414">Time taken to execute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="e460a-415">從記憶體清除物件並列印模型位置</span><span class="sxs-lookup"><span data-stu-id="e460a-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="e460a-416">使用 `unpersist()` 刪除記憶體中快取的物件。</span><span class="sxs-lookup"><span data-stu-id="e460a-416">Use `unpersist()` to delete objects cached in memory.</span></span>

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


<span data-ttu-id="e460a-417">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-417">**OUTPUT**</span></span>

<span data-ttu-id="e460a-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="e460a-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="e460a-419">* * 列印輸出使用耗用量筆記本中的模型檔案的路徑。</span><span class="sxs-lookup"><span data-stu-id="e460a-419">**Printout path to model files to be used in the consumption notebook.</span></span> <span data-ttu-id="e460a-420">* * 若要取用，且分數為獨立的資料集，您需要複製和貼上 」 耗用量筆記本"中的這些檔案名稱。</span><span class="sxs-lookup"><span data-stu-id="e460a-420">** To consume and score an independent data-set, you need to copy and paste these file names in the "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="e460a-421">**輸出**</span><span class="sxs-lookup"><span data-stu-id="e460a-421">**OUTPUT**</span></span>

<span data-ttu-id="e460a-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="e460a-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="e460a-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="e460a-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="e460a-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="e460a-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="e460a-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="e460a-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="e460a-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="e460a-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="e460a-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="e460a-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="e460a-428">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e460a-428">What's next?</span></span>
<span data-ttu-id="e460a-429">現在已使用 Spark MlLib 建立迴歸和分類模型，您已瞭解如何評分及評估這些模型。</span><span class="sxs-lookup"><span data-stu-id="e460a-429">Now that you have created regression and classification models with the Spark MlLib, you are ready to learn how to score and evaluate these models.</span></span>

<span data-ttu-id="e460a-430">**模型耗用量︰** 若要瞭解如何評分及評估本主題中所建立的分類和迴歸模型，請參閱 [評分及評估 Spark 建置機器學習服務模型](machine-learning-data-science-spark-model-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="e460a-430">**Model consumption:** To learn how to score and evaluate the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

