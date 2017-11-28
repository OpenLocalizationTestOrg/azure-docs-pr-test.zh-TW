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
# <a name="advanced-data-exploration-and-modeling-with-spark"></a><span data-ttu-id="7e534-103">使用 Spark 進階資料探索和模型化</span><span class="sxs-lookup"><span data-stu-id="7e534-103">Advanced data exploration and modeling with Spark</span></span>
[!INCLUDE [machine-learning-spark-modeling](../../includes/machine-learning-spark-modeling.md)]

<span data-ttu-id="7e534-104">本逐步解說會使用 HDInsight Spark toodo 資料瀏覽及定型二元分類和迴歸模型使用交叉驗證和範例的 hello NYC hyperparameter 最佳化計程車路線再見 2013年資料集。</span><span class="sxs-lookup"><span data-stu-id="7e534-104">This walkthrough uses HDInsight Spark toodo data exploration and train binary classification and regression models using cross-validation and hyperparameter optimization on a sample of hello NYC taxi trip and fare 2013 dataset.</span></span> <span data-ttu-id="7e534-105">它將引導您完成 hello 步驟的 hello[資料科學程序](http://aka.ms/datascienceprocess)、 端對端，使用 HDInsight Spark 叢集以進行處理和 Azure blob toostore hello 資料和 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-105">It walks you through hello steps of hello [Data Science Process](http://aka.ms/datascienceprocess), end-to-end, using an HDInsight Spark cluster for processing and Azure blobs toostore hello data and hello models.</span></span> <span data-ttu-id="7e534-106">hello 程序探索和視覺化資料從 Azure 儲存體 Blob，並準備 hello 資料 toobuild 預測模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-106">hello process explores and visualizes data brought in from an Azure Storage Blob and then prepares hello data toobuild predictive models.</span></span> <span data-ttu-id="7e534-107">Python 已使用的 toocode hello 方案和 tooshow hello 相關繪圖。</span><span class="sxs-lookup"><span data-stu-id="7e534-107">Python has been used toocode hello solution and tooshow hello relevant plots.</span></span> <span data-ttu-id="7e534-108">這些模型是使用 hello Spark MLlib toolkit toodo 二元分類和迴歸模型工作的組建。</span><span class="sxs-lookup"><span data-stu-id="7e534-108">These models are build using hello Spark MLlib toolkit toodo binary classification and regression modeling tasks.</span></span> 

* <span data-ttu-id="7e534-109">hello**二元分類**工作是 toopredict 不論是否在提示支付 hello 路線。</span><span class="sxs-lookup"><span data-stu-id="7e534-109">hello **binary classification** task is toopredict whether or not a tip is paid for hello trip.</span></span> 
* <span data-ttu-id="7e534-110">hello**迴歸**工作是根據其他提示功能 hello 提示 toopredict hello 數量。</span><span class="sxs-lookup"><span data-stu-id="7e534-110">hello **regression** task is toopredict hello amount of hello tip based on other tip features.</span></span> 

<span data-ttu-id="7e534-111">hello 模型步驟也包含程式碼示範如何 tootrain，評估並儲存每種模型類型。</span><span class="sxs-lookup"><span data-stu-id="7e534-111">hello modeling steps also contain code showing how tootrain, evaluate, and save each type of model.</span></span> <span data-ttu-id="7e534-112">hello 主題涵蓋一些 hello 相同地面為 hello[資料探索和模型使用 Spark](machine-learning-data-science-spark-data-exploration-modeling.md)主題。</span><span class="sxs-lookup"><span data-stu-id="7e534-112">hello topic covers some of hello same ground as hello [Data exploration and modeling with Spark](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span> <span data-ttu-id="7e534-113">但是，它一個 「 進階 」，它也與 hyperparameter 清除 tootrain 以最佳方式精確的分類和迴歸模型使用交叉驗證。</span><span class="sxs-lookup"><span data-stu-id="7e534-113">But it is more "advanced" in that it also uses cross-validation with hyperparameter sweeping tootrain optimally accurate classification and regression models.</span></span> 

<span data-ttu-id="7e534-114">**交叉驗證 (CV)**是評估如何在一組已知的資料上定型模型一般化所在它尚未定型資料集 toopredicting hello 功能的技術。</span><span class="sxs-lookup"><span data-stu-id="7e534-114">**Cross-validation (CV)** is a technique that assesses how well a model trained on a known set of data generalizes toopredicting hello features of datasets on which it has not been trained.</span></span>  <span data-ttu-id="7e534-115">這裡使用的一般實作是 toodivide 成 K 摺疊的資料集，並再 hello 中定型模型，只留下其中一個 hello 摺疊所有以循環配置資源方式。</span><span class="sxs-lookup"><span data-stu-id="7e534-115">A common implementation used here is toodivide a dataset into K folds and then train hello model in a round-robin fashion on all but one of hello folds.</span></span> <span data-ttu-id="7e534-116">評估 hello 模型 tooprediction 經過測試，在此模型中未使用的摺疊 tootrain hello hello 獨立的資料集時，精確地 hello 能力。</span><span class="sxs-lookup"><span data-stu-id="7e534-116">hello ability of hello model tooprediction accurately when tested against hello independent dataset in this fold not used tootrain hello model is assessed.</span></span>

<span data-ttu-id="7e534-117">**Hyperparameter 最佳化**hello 問題的選擇通常會有 hello 目標最佳化 hello 演算法的效能，在獨立的資料集上的量值的學習演算法的超集。</span><span class="sxs-lookup"><span data-stu-id="7e534-117">**Hyperparameter optimization** is hello problem of choosing a set of hyperparameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="7e534-118">**超**hello 模型定型程序之外，必須指定的值。</span><span class="sxs-lookup"><span data-stu-id="7e534-118">**Hyperparameters** are values that must be specified outside of hello model training procedure.</span></span> <span data-ttu-id="7e534-119">假設這些值可能會影響 hello 彈性及 hello 模型的精確度。</span><span class="sxs-lookup"><span data-stu-id="7e534-119">Assumptions about these values can impact hello flexibility and accuracy of hello models.</span></span> <span data-ttu-id="7e534-120">決策樹有超參數，例如例如 hello 預期深度和 hello 樹狀目錄中的分葉數目。</span><span class="sxs-lookup"><span data-stu-id="7e534-120">Decision trees have hyperparameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="7e534-121">支援向量機器 (SVM) 需要設定分類誤判損失詞彙。</span><span class="sxs-lookup"><span data-stu-id="7e534-121">Support Vector Machines (SVMs) require setting a misclassification penalty term.</span></span> 

<span data-ttu-id="7e534-122">這裡使用的常見方式 tooperform hyperparameter 最佳化是方格搜尋，或**參數掃掠**。</span><span class="sxs-lookup"><span data-stu-id="7e534-122">A common way tooperform hyperparameter optimization used here is a grid search, or a **parameter sweep**.</span></span> <span data-ttu-id="7e534-123">這包含學習演算法執行徹底搜尋透過 hello 值指定的 hello hyperparameter 空間的子集。</span><span class="sxs-lookup"><span data-stu-id="7e534-123">This consists of performing an exhaustive search through hello values a specified subset of hello hyperparameter space for a learning algorithm.</span></span> <span data-ttu-id="7e534-124">交叉驗證可以提供的效能度量 toosort 出 hello 所 hello 方格搜尋演算法產生最佳的結果。</span><span class="sxs-lookup"><span data-stu-id="7e534-124">Cross validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="7e534-125">CV 搭配 hyperparameter 審慎有助於限制問題，例如使 hello 模型會保留 hello 容量 tooapply toohello 一般的資料集從哪些 hello 擷取定型資料，過度配適模型 tootraining 資料。</span><span class="sxs-lookup"><span data-stu-id="7e534-125">CV used with hyperparameter sweeping helps limit problems like overfitting a model tootraining data so that hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

<span data-ttu-id="7e534-126">我們使用 hello 模型包括羅吉斯和線性迴歸、 隨機樹系和梯度促進式樹狀結構：</span><span class="sxs-lookup"><span data-stu-id="7e534-126">hello models we use include logistic and linear regression, random forests, and gradient boosted trees:</span></span>

* <span data-ttu-id="7e534-127">[線性迴歸與 SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD)的線性迴歸模型，會使用隨機梯度下降 (SGD) 的方法和最佳化和功能的縮放比例 toopredict hello 提示數量付費。</span><span class="sxs-lookup"><span data-stu-id="7e534-127">[Linear regression with SGD](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.regression.LinearRegressionWithSGD) is a linear regression model that uses a Stochastic Gradient Descent (SGD) method and for optimization and feature scaling toopredict hello tip amounts paid.</span></span> 
* <span data-ttu-id="7e534-128">[羅吉斯迴歸與 LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS)或 「 logit"迴歸是一種迴歸模型，hello 相依變數是類別 toodo 資料分類時才能使用。</span><span class="sxs-lookup"><span data-stu-id="7e534-128">[Logistic regression with LBFGS](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.classification.LogisticRegressionWithLBFGS) or "logit" regression, is a regression model that can be used when hello dependent variable is categorical toodo data classification.</span></span> <span data-ttu-id="7e534-129">LBFGS 是記憶體的 odd Newton 最佳化演算法的近似於使用電腦數量有限的 hello Broyden – Fletcher – Goldfarb – Shanno (BFGS) 演算法和可廣泛用於機器學習。</span><span class="sxs-lookup"><span data-stu-id="7e534-129">LBFGS is a quasi-Newton optimization algorithm that approximates hello Broyden–Fletcher–Goldfarb–Shanno (BFGS) algorithm using a limited amount of computer memory and that is widely used in machine learning.</span></span>
* <span data-ttu-id="7e534-130">[隨機樹系](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) 是整體的決策樹。</span><span class="sxs-lookup"><span data-stu-id="7e534-130">[Random forests](http://spark.apache.org/docs/latest/mllib-ensembles.html#Random-Forests) are ensembles of decision trees.</span></span>  <span data-ttu-id="7e534-131">結合許多決策樹 tooreduce hello 的風險過度配適。</span><span class="sxs-lookup"><span data-stu-id="7e534-131">They combine many decision trees tooreduce hello risk of overfitting.</span></span> <span data-ttu-id="7e534-132">隨機樹系用於迴歸和分類和可以處理類別的功能，可以擴充 toohello 多級分類設定。</span><span class="sxs-lookup"><span data-stu-id="7e534-132">Random forests are used for regression and classification and can handle categorical features and can be extended toohello multiclass classification setting.</span></span> <span data-ttu-id="7e534-133">它們不需要功能縮放比例和都能 toocapture 非線性和功能互動。</span><span class="sxs-lookup"><span data-stu-id="7e534-133">They do not require feature scaling and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="7e534-134">隨機樹系是其中一種 hello 可以最順利機器學習的分類和迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-134">Random forests are one of hello most successful machine learning models for classification and regression.</span></span>
* <span data-ttu-id="7e534-135">[漸層停駐推進式決策樹](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) 是整體的決策樹。</span><span class="sxs-lookup"><span data-stu-id="7e534-135">[Gradient boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="7e534-136">GBTs 定型決策樹反覆 toominimize 損失函數。</span><span class="sxs-lookup"><span data-stu-id="7e534-136">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="7e534-137">GBTs 用於迴歸和分類和可以處理類別的功能，不需要調整功能，而是可以 toocapture 非線性互動的功能。</span><span class="sxs-lookup"><span data-stu-id="7e534-137">GBTs are used for regression and classification and can handle categorical features, do not require feature scaling, and are able toocapture non-linearities and feature interactions.</span></span> <span data-ttu-id="7e534-138">它們也可用於多類別分類設定。</span><span class="sxs-lookup"><span data-stu-id="7e534-138">They can also be used in a multiclass-classification setting.</span></span>

<span data-ttu-id="7e534-139">模型使用 CV 和 Hyperparameter 範例會顯示 hello 二元分類問題掃掠。</span><span class="sxs-lookup"><span data-stu-id="7e534-139">Modeling examples using CV and Hyperparameter sweep are shown for hello binary classification problem.</span></span> <span data-ttu-id="7e534-140">（不含參數掃掠） 的簡單範例會顯示 hello 主要主題中的迴歸工作。</span><span class="sxs-lookup"><span data-stu-id="7e534-140">Simpler examples (without parameter sweeps) are presented in hello main topic for regression tasks.</span></span> <span data-ttu-id="7e534-141">但也顯示 hello 附錄中使用參數掃掠隨機樹系迴歸，線性迴歸和 CV 使用彈性的網路驗證。</span><span class="sxs-lookup"><span data-stu-id="7e534-141">But in hello appendix, validation using elastic net for linear regression and CV with parameter sweep using for random forest regression are also presented.</span></span> <span data-ttu-id="7e534-142">hello**彈性 net**是正則化的迴歸方法的調整線性迴歸模型，以線性方式結合 hello L1 與 L2 度量處罰下 hello[套索](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29)和[立體浮凸](https://en.wikipedia.org/wiki/Tikhonov_regularization)方法。</span><span class="sxs-lookup"><span data-stu-id="7e534-142">hello **elastic net** is a regularized regression method for fitting linear regression models that linearly combines hello L1 and L2 metrics as penalties of hello [lasso](https://en.wikipedia.org/wiki/Lasso%20%28statistics%29) and [ridge](https://en.wikipedia.org/wiki/Tikhonov_regularization) methods.</span></span>   

> [!NOTE]
> <span data-ttu-id="7e534-143">雖然 hello Spark MLlib toolkit 設計的 toowork 大型資料集，是此處為了方便起見使用相對較小的範例 (使用 170 K 資料列，約 0.1%的 hello 原始 NYC 資料集 ~ 30 Mb)。</span><span class="sxs-lookup"><span data-stu-id="7e534-143">Although hello Spark MLlib toolkit is designed toowork on large datasets, a relatively small sample (~30 Mb using 170K rows, about 0.1% of hello original NYC dataset) is used here for convenience.</span></span> <span data-ttu-id="7e534-144">在 HDInsight 叢集上具有 2 個背景工作節點，有效率地 （在約 10 分鐘） 執行此處指定的 hello 練習。</span><span class="sxs-lookup"><span data-stu-id="7e534-144">hello exercise given here runs efficiently (in about 10 minutes) on an HDInsight cluster with 2 worker nodes.</span></span> <span data-ttu-id="7e534-145">hello 相同程式碼，稍加修改，可以使用的 tooprocess 較大資料集，以適當的修改快取記憶體中的資料和變更 hello 叢集大小。</span><span class="sxs-lookup"><span data-stu-id="7e534-145">hello same code, with minor modifications, can be used tooprocess larger data-sets, with appropriate modifications for caching data in memory and changing hello cluster size.</span></span>
> 
> 

## <a name="setup-spark-clusters-and-notebooks"></a><span data-ttu-id="7e534-146">設定：Spark 叢集和 Notebook</span><span class="sxs-lookup"><span data-stu-id="7e534-146">Setup: Spark clusters and notebooks</span></span>
<span data-ttu-id="7e534-147">此逐步解說所提供的設定步驟和程式碼適用於使用 HDInsight Spark 1.6。</span><span class="sxs-lookup"><span data-stu-id="7e534-147">Setup steps and code are provided in this walkthrough for using an HDInsight Spark 1.6.</span></span> <span data-ttu-id="7e534-148">不過 Jupyter Notebook 可供 HDInsight Spark 1.6 版和 Spark 2.0 叢集兩者使用。</span><span class="sxs-lookup"><span data-stu-id="7e534-148">But Jupyter notebooks are provided for both HDInsight Spark 1.6 and Spark 2.0 clusters.</span></span> <span data-ttu-id="7e534-149">Hello 中提供的 hello 筆記本與連結 toothem 描述[Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) hello GitHub 儲存機制包含它們。</span><span class="sxs-lookup"><span data-stu-id="7e534-149">A description of hello notebooks and links toothem are provided in hello [Readme.md](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Readme.md) for hello GitHub repository containing them.</span></span> <span data-ttu-id="7e534-150">此外，hello 程式碼及連結的 hello 筆記本為泛型，應該在任何 Spark 叢集上運作。</span><span class="sxs-lookup"><span data-stu-id="7e534-150">Moreover, hello code here and in hello linked notebooks is generic and should work on any Spark cluster.</span></span> <span data-ttu-id="7e534-151">如果您未使用 HDInsight Spark，hello 叢集中設定和管理步驟可能稍有不同於這裡所顯示。</span><span class="sxs-lookup"><span data-stu-id="7e534-151">If you are not using HDInsight Spark, hello cluster setup and management steps may be slightly different from what is shown here.</span></span> <span data-ttu-id="7e534-152">為了方便起見，以下是 hello 的 hello 連結 toohello Jupyter 筆記本 Spark 1.6 版和 2.0 toobe Jupyter 筆記本伺服器 hello pyspark 核心中執行：</span><span class="sxs-lookup"><span data-stu-id="7e534-152">For convenience, here are hello links toohello Jupyter notebooks for Spark 1.6 and 2.0 toobe run in hello pyspark kernel of hello Jupyter Notebook server:</span></span>

### <a name="spark-16-notebooks"></a><span data-ttu-id="7e534-153">Spark 1.6 Notebook</span><span class="sxs-lookup"><span data-stu-id="7e534-153">Spark 1.6 notebooks</span></span>

<span data-ttu-id="7e534-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)：包含Notebook #1 中的主題，以及使用超參數微調和交叉驗證的模型開發。</span><span class="sxs-lookup"><span data-stu-id="7e534-154">[pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/pySpark-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): Includes topics in notebook #1, and model development using hyperparameter tuning and cross-validation.</span></span>

### <a name="spark-20-notebooks"></a><span data-ttu-id="7e534-155">Spark 2.0 Notebook</span><span class="sxs-lookup"><span data-stu-id="7e534-155">Spark 2.0 notebooks</span></span>

<span data-ttu-id="7e534-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb)： 這個檔案提供如何 tooperform 資料瀏覽、 建立模型及計分 Spark 2.0 叢集資訊。</span><span class="sxs-lookup"><span data-stu-id="7e534-156">[Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/pySpark/Spark2.0-pySpark3-machine-learning-data-science-spark-advanced-data-exploration-modeling.ipynb): This file provides information on how tooperform data exploration, modeling, and scoring in Spark 2.0 clusters.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="setup-storage-locations-libraries-and-hello-preset-spark-context"></a><span data-ttu-id="7e534-157">安裝程式： 儲存位置、 程式庫，與 hello 預設 Spark 內容</span><span class="sxs-lookup"><span data-stu-id="7e534-157">Setup: storage locations, libraries, and hello preset Spark context</span></span>
<span data-ttu-id="7e534-158">Spark 是無法 tooread 」 和 「 寫入 tooAzure (也稱為 WASB) 的儲存體 Blob。</span><span class="sxs-lookup"><span data-stu-id="7e534-158">Spark is able tooread and write tooAzure Storage Blob (also known as WASB).</span></span> <span data-ttu-id="7e534-159">因此，任何現有的資料儲存於該處可處理使用的 Spark，hello 結果儲存一次在 WASB。</span><span class="sxs-lookup"><span data-stu-id="7e534-159">So any of your existing data stored there can be processed using Spark and hello results stored again in WASB.</span></span>

<span data-ttu-id="7e534-160">hello 路徑需要正確地指定 toobe toosave 模型或 WASB 中的檔案。</span><span class="sxs-lookup"><span data-stu-id="7e534-160">toosave models or files in WASB, hello path needs toobe specified properly.</span></span> <span data-ttu-id="7e534-161">hello 預設容器附加 toohello Spark 叢集，可以使用來參考以開頭的路徑:"wasb: / /"。</span><span class="sxs-lookup"><span data-stu-id="7e534-161">hello default container attached toohello Spark cluster can be referenced using a path beginning with: "wasb:///".</span></span> <span data-ttu-id="7e534-162">其他位置由「wasb://」參考。</span><span class="sxs-lookup"><span data-stu-id="7e534-162">Other locations are referenced by “wasb://”.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-wasb"></a><span data-ttu-id="7e534-163">在 WASB 中設定儲存位置的目錄路徑</span><span class="sxs-lookup"><span data-stu-id="7e534-163">Set directory paths for storage locations in WASB</span></span>
<span data-ttu-id="7e534-164">hello 下列程式碼範例指定 hello 位置 hello 資料 toobe 讀取，並儲存 hello hello 模型儲存體目錄 toowhich hello 模型輸出路徑：</span><span class="sxs-lookup"><span data-stu-id="7e534-164">hello following code sample specifies hello location of hello data toobe read and hello path for hello model storage directory toowhich hello model output is saved:</span></span>

    # SET PATHS tooFILE LOCATIONS: DATA AND MODEL STORAGE

    # LOCATION OF TRAINING DATA
    taxi_train_file_loc = "wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv";


    # SET hello MODEL STORAGE DIRECTORY PATH 
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS NEEDED.
    modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";

    # PRINT START TIME
    import datetime
    datetime.datetime.now()

<span data-ttu-id="7e534-165">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-165">**OUTPUT**</span></span>

<span data-ttu-id="7e534-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span><span class="sxs-lookup"><span data-stu-id="7e534-166">datetime.datetime(2016, 4, 18, 17, 36, 27, 832799)</span></span>

### <a name="import-libraries"></a><span data-ttu-id="7e534-167">匯入程式庫</span><span class="sxs-lookup"><span data-stu-id="7e534-167">Import libraries</span></span>
<span data-ttu-id="7e534-168">匯入必要的程式庫，以下列程式碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="7e534-168">Import necessary libraries with hello following code:</span></span>

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


### <a name="preset-spark-context-and-pyspark-magics"></a><span data-ttu-id="7e534-169">預設 Spark 內容及 PySpark magic</span><span class="sxs-lookup"><span data-stu-id="7e534-169">Preset Spark context and PySpark magics</span></span>
<span data-ttu-id="7e534-170">所提供的 Jupyter 筆記本 hello PySpark 核心有預設的內容。</span><span class="sxs-lookup"><span data-stu-id="7e534-170">hello PySpark kernels that are provided with Jupyter notebooks have a preset context.</span></span> <span data-ttu-id="7e534-171">因此您不需要 tooset hello Spark 或登錄區內容明確之前您開始使用您所開發的 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7e534-171">So you do not need tooset hello Spark or Hive contexts explicitly before you start working with hello application you are developing.</span></span> <span data-ttu-id="7e534-172">依預設會將這些內容提供給您使用。</span><span class="sxs-lookup"><span data-stu-id="7e534-172">These contexts are available for you by default.</span></span> <span data-ttu-id="7e534-173">這些內容包括：</span><span class="sxs-lookup"><span data-stu-id="7e534-173">These contexts are:</span></span>

* <span data-ttu-id="7e534-174">sc - 代表 Spark</span><span class="sxs-lookup"><span data-stu-id="7e534-174">sc - for Spark</span></span> 
* <span data-ttu-id="7e534-175">sqlContext - 代表 Hive</span><span class="sxs-lookup"><span data-stu-id="7e534-175">sqlContext - for Hive</span></span>

<span data-ttu-id="7e534-176">hello PySpark 核心提供一些預先定義 「 我們"，這是特殊的命令，您可以呼叫具有 %%。</span><span class="sxs-lookup"><span data-stu-id="7e534-176">hello PySpark kernel provides some predefined “magics”, which are special commands that you can call with %%.</span></span> <span data-ttu-id="7e534-177">在這些程式碼範例中，就使用了兩個此類型的命令。</span><span class="sxs-lookup"><span data-stu-id="7e534-177">There are two such commands that are used in these code samples.</span></span>

* <span data-ttu-id="7e534-178">**%%本機**指定 hello 下來幾行中的程式碼是 toobe 以本機方式執行。</span><span class="sxs-lookup"><span data-stu-id="7e534-178">**%%local** Specifies that hello code in subsequent lines is toobe executed locally.</span></span> <span data-ttu-id="7e534-179">程式碼必須是有效的 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7e534-179">Code must be valid Python code.</span></span>
* <span data-ttu-id="7e534-180">**%%sql o <variable name>** 執行針對 hello sqlContext Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="7e534-180">**%%sql -o <variable name>** Executes a Hive query against hello sqlContext.</span></span> <span data-ttu-id="7e534-181">如果傳遞 hello-o 參數，則 hello hello 查詢結果會持續保留在 hello %%熊資料框架的本機 Python 環境。</span><span class="sxs-lookup"><span data-stu-id="7e534-181">If hello -o parameter is passed, hello result of hello query is persisted in hello %%local Python context as a Pandas DataFrame.</span></span>

<span data-ttu-id="7e534-182">針對 Jupyter 筆記本和預先定義的 hello hello 核心上的詳細資訊 」 magics 」，它們提供，請參閱[HDInsight 上的叢集與 HDInsight Spark Linux Jupyter 筆記本的可用的核心](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="7e534-182">For more information on hello kernels for Jupyter notebooks and hello predefined "magics" that they provide, see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

## <a name="data-ingestion-from-public-blob"></a><span data-ttu-id="7e534-183">來自公用 Blob 的資料擷取：</span><span class="sxs-lookup"><span data-stu-id="7e534-183">Data ingestion from public blob:</span></span>
<span data-ttu-id="7e534-184">hello hello 資料科學程序的第一個步驟是 tooingest hello 資料 toobe 分析從來源到您的資料探索和模型環境的所在位置。</span><span class="sxs-lookup"><span data-stu-id="7e534-184">hello first step in hello data science process is tooingest hello data toobe analyzed from sources where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="7e534-185">這種環境在本逐步解說中是 Spark。</span><span class="sxs-lookup"><span data-stu-id="7e534-185">This environment is Spark in this walkthrough.</span></span> <span data-ttu-id="7e534-186">本節包含 hello 程式碼 toocomplete 一系列的工作：</span><span class="sxs-lookup"><span data-stu-id="7e534-186">This section contains hello code toocomplete a series of tasks:</span></span>

* <span data-ttu-id="7e534-187">內嵌 hello 資料範例 toobe 模型化</span><span class="sxs-lookup"><span data-stu-id="7e534-187">ingest hello data sample toobe modeled</span></span>
* <span data-ttu-id="7e534-188">讀取輸入資料集中 hello （儲存為.tsv 檔案）</span><span class="sxs-lookup"><span data-stu-id="7e534-188">read in hello input dataset (stored as a .tsv file)</span></span>
* <span data-ttu-id="7e534-189">格式和全新 hello 資料</span><span class="sxs-lookup"><span data-stu-id="7e534-189">format and clean hello data</span></span>
* <span data-ttu-id="7e534-190">建立並快取記憶體中的物件 (RDD 或資料框架)</span><span class="sxs-lookup"><span data-stu-id="7e534-190">create and cache objects (RDDs or data-frames) in memory</span></span>
* <span data-ttu-id="7e534-191">將它註冊為 SQL 內容中的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="7e534-191">register it as a temp-table in SQL-context.</span></span>

<span data-ttu-id="7e534-192">擷取資料的 hello 程式碼如下。</span><span class="sxs-lookup"><span data-stu-id="7e534-192">Here is hello code for data ingestion.</span></span>

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


<span data-ttu-id="7e534-193">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-193">**OUTPUT**</span></span>

<span data-ttu-id="7e534-194">時間 tooexecute 儲存格上方： 276.62 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-194">Time taken tooexecute above cell: 276.62 seconds</span></span>

## <a name="data-exploration--visualization"></a><span data-ttu-id="7e534-195">資料探索和虛擬化</span><span class="sxs-lookup"><span data-stu-id="7e534-195">Data exploration & visualization</span></span>
<span data-ttu-id="7e534-196">一旦 hello 資料已放入 Spark，hello hello 資料科學程序中的下一個步驟是 toogain hello 資料探索和視覺效果的更深入了解。</span><span class="sxs-lookup"><span data-stu-id="7e534-196">Once hello data has been brought into Spark, hello next step in hello data science process is toogain deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="7e534-197">在本節中，我們會檢查 hello 計程車資料使用 SQL 查詢和繪圖 hello 目標變數與潛在功能視覺化進行檢查。</span><span class="sxs-lookup"><span data-stu-id="7e534-197">In this section, we examine hello taxi data using SQL queries and plot hello target variables and prospective features for visual inspection.</span></span> <span data-ttu-id="7e534-198">具體來說，我們會繪製旅客計數計程車往返、 hello 頻率的提示數量和如何提示因付款金額和型別中的 hello 頻率。</span><span class="sxs-lookup"><span data-stu-id="7e534-198">Specifically, we plot hello frequency of passenger counts in taxi trips, hello frequency of tip amounts, and how tips vary by payment amount and type.</span></span>

### <a name="plot-a-histogram-of-passenger-count-frequencies-in-hello-sample-of-taxi-trips"></a><span data-ttu-id="7e534-199">繪製旅客計數頻率的計程車行程 hello 範例中的長條圖</span><span class="sxs-lookup"><span data-stu-id="7e534-199">Plot a histogram of passenger count frequencies in hello sample of taxi trips</span></span>
<span data-ttu-id="7e534-200">這個程式碼和後續的程式碼片段，請使用 SQL magic tooquery hello 範例資料和本機 magic tooplot hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7e534-200">This code and subsequent snippets use SQL magic tooquery hello sample and local magic tooplot hello data.</span></span>

* <span data-ttu-id="7e534-201">**SQL magic (`%%sql`)** hello HDInsight PySpark 核心支援 hello sqlContext 輕鬆內嵌 HiveQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="7e534-201">**SQL magic (`%%sql`)** hello HDInsight PySpark kernel supports easy inline HiveQL queries against hello sqlContext.</span></span> <span data-ttu-id="7e534-202">hello (-o VARIABLE_NAME) 引數會保存 hello 的 hello SQL 查詢的輸出為熊資料框架 hello Jupyter 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="7e534-202">hello (-o VARIABLE_NAME) argument persists hello output of hello SQL query as a Pandas DataFrame on hello Jupyter server.</span></span> <span data-ttu-id="7e534-203">這表示在 hello 本機模式中使用。</span><span class="sxs-lookup"><span data-stu-id="7e534-203">This means it is available in hello local mode.</span></span>
* <span data-ttu-id="7e534-204">hello  **`%%local` magic**是 hello Jupyter 伺服器，也就是 hello 的 hello HDInsight 叢集的前端節點上在本機使用 toorun 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7e534-204">hello **`%%local` magic** is used toorun code locally on hello Jupyter server, which is hello headnode of hello HDInsight cluster.</span></span> <span data-ttu-id="7e534-205">通常，您會使用`%%local`magic 之後 hello `%%sql -o` magic 是使用的 toorun 查詢。</span><span class="sxs-lookup"><span data-stu-id="7e534-205">Typically, you use `%%local` magic after hello `%%sql -o` magic is used toorun a query.</span></span> <span data-ttu-id="7e534-206">hello-o 參數會保存在本機 hello SQL 查詢的 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="7e534-206">hello -o parameter would persist hello output of hello SQL query locally.</span></span> <span data-ttu-id="7e534-207">然後 hello `%%local` magic 觸發程序 hello 下一組程式碼片段 toorun 在本機憑藉已在本機保存的 hello 輸出的 hello SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="7e534-207">Then hello `%%local` magic triggers hello next set of code snippets toorun locally against hello output of hello SQL queries that has been persisted locally.</span></span> <span data-ttu-id="7e534-208">執行 hello 程式碼之後，會自動視覺化 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="7e534-208">hello output is automatically visualized after you run hello code.</span></span>

<span data-ttu-id="7e534-209">此查詢會擷取 hello 往返依旅客計數。</span><span class="sxs-lookup"><span data-stu-id="7e534-209">This query retrieves hello trips by passenger count.</span></span> 

    # PLOT FREQUENCY OF PASSENGER COUNTS IN TAXI TRIPS

    # SQL QUERY
    %%sql -q -o sqlResults
    SELECT passenger_count, COUNT(*) as trip_counts FROM taxi_train WHERE passenger_count > 0 and passenger_count < 7 GROUP BY passenger_count


<span data-ttu-id="7e534-210">此程式碼建立 hello 查詢輸出的本機資料框架，並繪製 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7e534-210">This code creates a local data-frame from hello query output and plots hello data.</span></span> <span data-ttu-id="7e534-211">hello `%%local` magic 建立本機資料框架， `sqlResults`，可以用來與 matplotlib 繪製。</span><span class="sxs-lookup"><span data-stu-id="7e534-211">hello `%%local` magic creates a local data-frame, `sqlResults`, which can be used for plotting with matplotlib.</span></span> 

> [!NOTE]
> <span data-ttu-id="7e534-212">在本逐步解說中，會多次使用此 PySpark magic。</span><span class="sxs-lookup"><span data-stu-id="7e534-212">This PySpark magic is used multiple times in this walkthrough.</span></span> <span data-ttu-id="7e534-213">如果 hello 資料量很大，您應該取樣 toocreate 本機記憶體內可容納資料框架。</span><span class="sxs-lookup"><span data-stu-id="7e534-213">If hello amount of data is large, you should sample toocreate a data-frame that can fit in local memory.</span></span>
> 
> 

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES. 
    # CLICK ON hello TYPE OF PLOT tooBE GENERATED (E.G. LINE, AREA, BAR ETC.)
    sqlResults

<span data-ttu-id="7e534-214">以下是 hello 程式碼 tooplot hello 往返旅客計數</span><span class="sxs-lookup"><span data-stu-id="7e534-214">Here is hello code tooplot hello trips by passenger counts</span></span>

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

<span data-ttu-id="7e534-215">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-215">**OUTPUT**</span></span>

![按乘客計數排列的車程頻率](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/frequency-of-trips-by-passenger-count.png)

<span data-ttu-id="7e534-217">您可以在多種不同類型的視覺效果 （資料表、 圓形圖、 線條、 區域或列） 之間使用選取 hello**類型**hello 筆記本中的功能表按鈕。</span><span class="sxs-lookup"><span data-stu-id="7e534-217">You can select among several different types of visualizations (Table, Pie, Line, Area, or Bar) by using hello **Type** menu buttons in hello notebook.</span></span> <span data-ttu-id="7e534-218">以下顯示 hello 橫條圖。</span><span class="sxs-lookup"><span data-stu-id="7e534-218">hello Bar plot is shown here.</span></span>

### <a name="plot-a-histogram-of-tip-amounts-and-how-tip-amount-varies-by-passenger-count-and-fare-amounts"></a><span data-ttu-id="7e534-219">繪製小費金額，和小費金額如何隨乘客計數和費用金額變化的長條圖。</span><span class="sxs-lookup"><span data-stu-id="7e534-219">Plot a histogram of tip amounts and how tip amount varies by passenger count and fare amounts.</span></span>
<span data-ttu-id="7e534-220">使用 SQL 查詢 toosample 資料...</span><span class="sxs-lookup"><span data-stu-id="7e534-220">Use a SQL query toosample data..</span></span>

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


<span data-ttu-id="7e534-221">此資料格，程式碼會使用 hello SQL 查詢 toocreate 三種繪圖 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7e534-221">This code cell uses hello SQL query toocreate three plots hello data.</span></span>

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


<span data-ttu-id="7e534-222">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="7e534-222">**OUTPUT:**</span></span> 

![小費金額分佈](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-distribution.png)

![按乘客計數排列的小費金額](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-passenger-count.png)

![按費用金額排列的小費金額](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/tip-amount-by-fare-amount.png)

## <a name="feature-engineering-transformation-and-data-preparation-for-modeling"></a><span data-ttu-id="7e534-226">模型化的功能工程、轉換和資料準備</span><span class="sxs-lookup"><span data-stu-id="7e534-226">Feature engineering, transformation, and data preparation for modeling</span></span>
<span data-ttu-id="7e534-227">本章節描述，並提供用於 ML 模型使用 tooprepare 資料的程序的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="7e534-227">This section describes and provides hello code for procedures used tooprepare data for use in ML modeling.</span></span> <span data-ttu-id="7e534-228">它會顯示影響 toodo hello 下列工作：</span><span class="sxs-lookup"><span data-stu-id="7e534-228">It shows how toodo hello following tasks:</span></span>

* <span data-ttu-id="7e534-229">將小時分割到流量時間分類區以建立新功能</span><span class="sxs-lookup"><span data-stu-id="7e534-229">Create a new feature by partitioning hours into traffic time bins</span></span>
* <span data-ttu-id="7e534-230">索引和 on-hot 編碼分類功能</span><span class="sxs-lookup"><span data-stu-id="7e534-230">Index and on-hot encode categorical features</span></span>
* <span data-ttu-id="7e534-231">建立輸入到 ML 函式的標示點物件</span><span class="sxs-lookup"><span data-stu-id="7e534-231">Create labeled point objects for input into ML functions</span></span>
* <span data-ttu-id="7e534-232">建立 hello 資料的隨機子取樣和分割成定型集和測試集</span><span class="sxs-lookup"><span data-stu-id="7e534-232">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
* <span data-ttu-id="7e534-233">調整功能</span><span class="sxs-lookup"><span data-stu-id="7e534-233">Feature scaling</span></span>
* <span data-ttu-id="7e534-234">快取記憶體中的物件</span><span class="sxs-lookup"><span data-stu-id="7e534-234">Cache objects in memory</span></span>

### <a name="create-a-new-feature-by-partitioning-traffic-times-into-bins"></a><span data-ttu-id="7e534-235">將流量時間分割到分類區以建立新功能</span><span class="sxs-lookup"><span data-stu-id="7e534-235">Create a new feature by partitioning traffic times into bins</span></span>
<span data-ttu-id="7e534-236">此程式碼顯示如何 toocreate 的新功能，藉由分割流量時間分組然後 toocache hello 產生資料框架，在記憶體中的方式。</span><span class="sxs-lookup"><span data-stu-id="7e534-236">This code shows how toocreate a new feature by partitioning traffic times into bins and then how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="7e534-237">快取，會導致 tooimproved 執行時間，彈性分散式資料集 (RDDs) 和資料框架會重複使用。</span><span class="sxs-lookup"><span data-stu-id="7e534-237">Caching leads tooimproved execution time where Resilient Distributed Datasets (RDDs) and data-frames are used repeatedly.</span></span> <span data-ttu-id="7e534-238">因此，我們會在逐步解說中的幾個階段快取 RDD 和資料框架。</span><span class="sxs-lookup"><span data-stu-id="7e534-238">So, we cache RDDs and data-frames at several stages in this walkthrough.</span></span>

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

<span data-ttu-id="7e534-239">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-239">**OUTPUT**</span></span>

<span data-ttu-id="7e534-240">126050</span><span class="sxs-lookup"><span data-stu-id="7e534-240">126050</span></span>

### <a name="index-and-one-hot-encode-categorical-features"></a><span data-ttu-id="7e534-241">索引和 one-hot 編碼分類功能</span><span class="sxs-lookup"><span data-stu-id="7e534-241">Index and one-hot encode categorical features</span></span>
<span data-ttu-id="7e534-242">此區段會顯示如何 tooindex 或編碼的輸入 hello 模型函式的類別特徵。</span><span class="sxs-lookup"><span data-stu-id="7e534-242">This section shows how tooindex or encode categorical features for input into hello modeling functions.</span></span> <span data-ttu-id="7e534-243">hello 模型和預測的 MLlib 函式需要與類別的輸入資料的功能會編製索引，或編碼先前 toouse。</span><span class="sxs-lookup"><span data-stu-id="7e534-243">hello modeling and predict functions of MLlib require that features with categorical input data be indexed or encoded prior toouse.</span></span> 

<span data-ttu-id="7e534-244">視 hello 模型而定，您需要 tooindex 或將它們以不同方式編碼。</span><span class="sxs-lookup"><span data-stu-id="7e534-244">Depending on hello model, you need tooindex or encode them in different ways.</span></span> <span data-ttu-id="7e534-245">例如，羅吉斯和線性迴歸模型需要一個熱門的編碼，其中，具有三個類別的功能，例如才可擴充到三個特徵資料行，與每個包含 0 或 1，視所觀察 hello 分類。</span><span class="sxs-lookup"><span data-stu-id="7e534-245">For example, Logistic and Linear Regression models require one-hot encoding, where, for example, a feature with three categories can be expanded into three feature columns, with each containing 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="7e534-246">提供 MLlib [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder)函式 toodo 一個熱編碼方式。</span><span class="sxs-lookup"><span data-stu-id="7e534-246">MLlib provides [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function toodo one-hot encoding.</span></span> <span data-ttu-id="7e534-247">此編碼器將對應的二進位的向量，使用最多為單一其中一個值的標籤索引 tooa 資料行的資料行。</span><span class="sxs-lookup"><span data-stu-id="7e534-247">This encoder maps a column of label indices tooa column of binary vectors, with at most a single one-value.</span></span> <span data-ttu-id="7e534-248">這種編碼方式可讓演算法所預期的數字的重要的功能，例如羅吉斯迴歸，套用 toobe toocategorical 功能。</span><span class="sxs-lookup"><span data-stu-id="7e534-248">This encoding allows algorithms that expect numerical valued features, such as logistic regression, toobe applied toocategorical features.</span></span>

<span data-ttu-id="7e534-249">以下是 hello tooindex 程式碼，並將編碼類別特徵：</span><span class="sxs-lookup"><span data-stu-id="7e534-249">Here is hello code tooindex and encode categorical features:</span></span>

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


<span data-ttu-id="7e534-250">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-250">**OUTPUT**</span></span>

<span data-ttu-id="7e534-251">時間 tooexecute 儲存格上方： 3.14 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-251">Time taken tooexecute above cell: 3.14 seconds</span></span>

### <a name="create-labeled-point-objects-for-input-into-ml-functions"></a><span data-ttu-id="7e534-252">建立輸入到 ML 函式的標示點物件</span><span class="sxs-lookup"><span data-stu-id="7e534-252">Create labeled point objects for input into ML functions</span></span>
<span data-ttu-id="7e534-253">此章節包含程式碼，說明如何為標記的點資料 tooindex 類別的文字資料類型以及如何 tooencode 它。</span><span class="sxs-lookup"><span data-stu-id="7e534-253">This section contains code that shows how tooindex categorical text data as a labeled point data type and how tooencode it.</span></span> <span data-ttu-id="7e534-254">這準備好使用 toobe tootrain 和測試 MLlib 羅吉斯迴歸和其他分類模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-254">This prepares it toobe used tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="7e534-255">標示點物件是彈性分散式資料集 (RDD)，其格式化成適合 MLlib 中大部分的 ML 演算法的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="7e534-255">Labeled point objects are Resilient Distributed Datasets (RDD) formatted in a way that is needed as input data by most of ML algorithms in MLlib.</span></span> <span data-ttu-id="7e534-256">[標示點](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 是本機向量 (密集或疏鬆)，與標籤/回應相關聯。</span><span class="sxs-lookup"><span data-stu-id="7e534-256">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="7e534-257">以下是 hello tooindex 程式碼，並將編碼的二元分類的文字功能。</span><span class="sxs-lookup"><span data-stu-id="7e534-257">Here is hello code tooindex and encode text features for binary classification.</span></span>

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


<span data-ttu-id="7e534-258">以下是 hello 程式碼的線性迴歸分析的 tooencode 和索引類別文字功能。</span><span class="sxs-lookup"><span data-stu-id="7e534-258">Here is hello code tooencode and index categorical text features for linear regression analysis.</span></span>

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


### <a name="create-a-random-sub-sampling-of-hello-data-and-split-it-into-training-and-testing-sets"></a><span data-ttu-id="7e534-259">建立 hello 資料的隨機子取樣和分割成定型集和測試集</span><span class="sxs-lookup"><span data-stu-id="7e534-259">Create a random sub-sampling of hello data and split it into training and testing sets</span></span>
<span data-ttu-id="7e534-260">此程式碼會建立隨機取樣的 hello 資料 （在這裡使用 25%）。</span><span class="sxs-lookup"><span data-stu-id="7e534-260">This code creates a random sampling of hello data (25% is used here).</span></span> <span data-ttu-id="7e534-261">雖然您不需要這個到期 toohello 大小的 hello 資料集的範例，我們將示範如何您也可以取樣 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7e534-261">Although it is not required for this example due toohello size of hello dataset, we demonstrate how you can sample hello data here.</span></span> <span data-ttu-id="7e534-262">您就知道如何 toouse 它視您的問題。</span><span class="sxs-lookup"><span data-stu-id="7e534-262">Then you know how toouse it for your own problem if needed.</span></span> <span data-ttu-id="7e534-263">在大型範例中，如此可在訓練模型時節省大量時間。</span><span class="sxs-lookup"><span data-stu-id="7e534-263">When samples are large, this can save significant time while training models.</span></span> <span data-ttu-id="7e534-264">接下來我們將 hello 範例分割成定型一部分 （這裡 75%) 和測試的一部分 （這裡 25%) toouse 分類和迴歸模型中。</span><span class="sxs-lookup"><span data-stu-id="7e534-264">Next we split hello sample into a training part (75% here) and a testing part (25% here) toouse in classification and regression modeling.</span></span>

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

<span data-ttu-id="7e534-265">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-265">**OUTPUT**</span></span>

<span data-ttu-id="7e534-266">時間 tooexecute 儲存格上方： 0.31 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-266">Time taken tooexecute above cell: 0.31 seconds</span></span>

### <a name="feature-scaling"></a><span data-ttu-id="7e534-267">調整功能</span><span class="sxs-lookup"><span data-stu-id="7e534-267">Feature scaling</span></span>
<span data-ttu-id="7e534-268">調整功能，也稱為資料正規化，以確保，功能與廣泛分散的值未授與過多權衡 hello 目標函式。</span><span class="sxs-lookup"><span data-stu-id="7e534-268">Feature scaling, also known as data normalization, insures that features with widely disbursed values are not given excessive weigh in hello objective function.</span></span> <span data-ttu-id="7e534-269">hello 功能縮放比例的程式碼會使用 hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello 功能 toounit 變異數。</span><span class="sxs-lookup"><span data-stu-id="7e534-269">hello code for feature scaling uses hello [StandardScaler](https://spark.apache.org/docs/latest/api/python/pyspark.mllib.html#pyspark.mllib.feature.StandardScaler) tooscale hello features toounit variance.</span></span> <span data-ttu-id="7e534-270">這是由 MLlib 提供，用於使用隨機梯度下降 (SGD) 的線性迴歸。</span><span class="sxs-lookup"><span data-stu-id="7e534-270">It is provided by MLlib for use in linear regression with Stochastic Gradient Descent (SGD).</span></span> <span data-ttu-id="7e534-271">SGD 為訓練廣泛的其他機器學習模型的常用演算法，例如正則化迴歸或支援向量機器 (SVM)。</span><span class="sxs-lookup"><span data-stu-id="7e534-271">SGD is a popular algorithm for training a wide range of other machine learning models such as regularized regressions or support vector machines (SVM).</span></span>   

> [!TIP]
> <span data-ttu-id="7e534-272">我們發現 hello LinearRegressionWithSGD 演算法 toobe 機密 toofeature 縮放比例。</span><span class="sxs-lookup"><span data-stu-id="7e534-272">We have found hello LinearRegressionWithSGD algorithm toobe sensitive toofeature scaling.</span></span>   
> 
> 

<span data-ttu-id="7e534-273">以下是用於正則化的 hello 線性 SGD 演算法 hello 程式碼 tooscale 變數。</span><span class="sxs-lookup"><span data-stu-id="7e534-273">Here is hello code tooscale variables for use with hello regularized linear SGD algorithm.</span></span>

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

<span data-ttu-id="7e534-274">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-274">**OUTPUT**</span></span>

<span data-ttu-id="7e534-275">時間 tooexecute 儲存格上方： 11.67 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-275">Time taken tooexecute above cell: 11.67 seconds</span></span>

### <a name="cache-objects-in-memory"></a><span data-ttu-id="7e534-276">快取記憶體中的物件</span><span class="sxs-lookup"><span data-stu-id="7e534-276">Cache objects in memory</span></span>
<span data-ttu-id="7e534-277">caching hello 輸入的資料框架物件會用於迴歸、 分類，以及縮放功能，可以降低 hello 時間進行定型和測試的 ML 演算法。</span><span class="sxs-lookup"><span data-stu-id="7e534-277">hello time taken for training and testing of ML algorithms can be reduced by caching hello input data frame objects used for classification, regression and, scaled features.</span></span>

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

<span data-ttu-id="7e534-278">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-278">**OUTPUT**</span></span> 

<span data-ttu-id="7e534-279">時間 tooexecute 儲存格上方： 0.13 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-279">Time taken tooexecute above cell: 0.13 seconds</span></span>

## <a name="predict-whether-or-not-a-tip-is-paid-with-binary-classification-models"></a><span data-ttu-id="7e534-280">使用二進位分類模型來預測是否支付小費</span><span class="sxs-lookup"><span data-stu-id="7e534-280">Predict whether or not a tip is paid with binary classification models</span></span>
<span data-ttu-id="7e534-281">本節說明如何使用三個模型的預測的 hello 二元分類工作在提示支付計程車路線。</span><span class="sxs-lookup"><span data-stu-id="7e534-281">This section shows how use three models for hello binary classification task of predicting whether or not a tip is paid for a taxi trip.</span></span> <span data-ttu-id="7e534-282">呈現的 hello 模型如下：</span><span class="sxs-lookup"><span data-stu-id="7e534-282">hello models presented are:</span></span>

* <span data-ttu-id="7e534-283">羅吉斯迴歸</span><span class="sxs-lookup"><span data-stu-id="7e534-283">Logistic regression</span></span> 
* <span data-ttu-id="7e534-284">隨機樹系</span><span class="sxs-lookup"><span data-stu-id="7e534-284">Random forest</span></span>
* <span data-ttu-id="7e534-285">漸層停駐提升樹狀結構</span><span class="sxs-lookup"><span data-stu-id="7e534-285">Gradient Boosting Trees</span></span>

<span data-ttu-id="7e534-286">每個模型建置程式碼區段會分成幾個步驟︰</span><span class="sxs-lookup"><span data-stu-id="7e534-286">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="7e534-287">**模型定型** 資料</span><span class="sxs-lookup"><span data-stu-id="7e534-287">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="7e534-288">**模型評估** </span><span class="sxs-lookup"><span data-stu-id="7e534-288">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="7e534-289">**儲存模型** </span><span class="sxs-lookup"><span data-stu-id="7e534-289">**Saving model** in blob for future consumption</span></span>

<span data-ttu-id="7e534-290">我們會示範如何 toodo 交叉驗證 (CV) 與參數掃掠兩種方式：</span><span class="sxs-lookup"><span data-stu-id="7e534-290">We show how toodo cross-validation (CV) with parameter sweeping in two ways:</span></span>

1. <span data-ttu-id="7e534-291">使用**泛型**自訂程式碼可以套用的 tooany 演算法 MLlib 和 tooany 參數中設定的演算法中。</span><span class="sxs-lookup"><span data-stu-id="7e534-291">Using **generic** custom code which can be applied tooany algorithm in MLlib and tooany parameter sets in an algorithm.</span></span> 
2. <span data-ttu-id="7e534-292">使用 hello **pySpark CrossValidator 管線函式**。</span><span class="sxs-lookup"><span data-stu-id="7e534-292">Using hello **pySpark CrossValidator pipeline function**.</span></span> <span data-ttu-id="7e534-293">請注意，CrossValidator 對 Spark 1.5.0 有幾項限制︰</span><span class="sxs-lookup"><span data-stu-id="7e534-293">Note that CrossValidator has a few limitations for Spark 1.5.0:</span></span> 
   
   * <span data-ttu-id="7e534-294">管線模型無法儲存/保存供未來取用。</span><span class="sxs-lookup"><span data-stu-id="7e534-294">Pipeline models cannot be saved/persisted for future consumption.</span></span>
   * <span data-ttu-id="7e534-295">無法用於模型中的每個參數。</span><span class="sxs-lookup"><span data-stu-id="7e534-295">Cannot be used for every parameter in a model.</span></span>
   * <span data-ttu-id="7e534-296">無法用於每個 MLlib 演算法。</span><span class="sxs-lookup"><span data-stu-id="7e534-296">Cannot be used for every MLlib algorithm.</span></span>

### <a name="generic-cross-validation-and-hyperparameter-sweeping-used-with-hello-logistic-regression-algorithm-for-binary-classification"></a><span data-ttu-id="7e534-297">交叉驗證和 hyperparameter 掃掠搭配 hello 羅吉斯迴歸演算法使用二元分類的泛型</span><span class="sxs-lookup"><span data-stu-id="7e534-297">Generic cross validation and hyperparameter sweeping used with hello logistic regression algorithm for binary classification</span></span>
<span data-ttu-id="7e534-298">本節中的 hello 程式碼顯示如何 tootrain，評估及儲存與羅吉斯迴歸模型[LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm)的預測是否付費的行程 hello NYC 計程車行程及價位資料集中的提示。</span><span class="sxs-lookup"><span data-stu-id="7e534-298">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="7e534-299">hello 模型已定型使用交叉驗證 (CV) 和實作自訂程式碼可以套用的學習演算法中 MLlib hello tooany hyperparameter 掃掠。</span><span class="sxs-lookup"><span data-stu-id="7e534-299">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with custom code that can be applied tooany of hello learning algorithms in MLlib.</span></span>   

> [!NOTE]
> <span data-ttu-id="7e534-300">hello 執行此自訂的 CV 程式碼可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="7e534-300">hello execution of this custom CV code can take several minutes.</span></span>
> 
> 

<span data-ttu-id="7e534-301">**使用 CV 和 hyperparameter 掃掠 hello 羅吉斯迴歸模型定型**</span><span class="sxs-lookup"><span data-stu-id="7e534-301">**Train hello logistic regression model using CV and hyperparameter sweeping**</span></span>

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


<span data-ttu-id="7e534-302">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-302">**OUTPUT**</span></span>

<span data-ttu-id="7e534-303">係數：[0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span><span class="sxs-lookup"><span data-stu-id="7e534-303">Coefficients: [0.0082065285375, -0.0223675576104, -0.0183812028036, -3.48124578069e-05, -0.00247646947233, -0.00165897881503, 0.0675394837328, -0.111823113101, -0.324609912762, -0.204549780032, -1.36499216354, 0.591088507921, -0.664263411392, -1.00439726852, 3.46567827545, -3.51025855172, -0.0471341112232, -0.043521833294, 0.000243375810385, 0.054518719222]</span></span>

<span data-ttu-id="7e534-304">截距：-0.0111216486893</span><span class="sxs-lookup"><span data-stu-id="7e534-304">Intercept: -0.0111216486893</span></span>

<span data-ttu-id="7e534-305">時間 tooexecute 儲存格上方： 14.43 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-305">Time taken tooexecute above cell: 14.43 seconds</span></span>

<span data-ttu-id="7e534-306">**評估具有標準度量的 hello 二元分類模型**</span><span class="sxs-lookup"><span data-stu-id="7e534-306">**Evaluate hello binary classification model with standard metrics**</span></span>

<span data-ttu-id="7e534-307">本節中的 hello 程式碼會示範如何 tooevaluate 羅吉斯迴歸模型針對測試資料集，包括 hello ROC 曲線的繪圖。</span><span class="sxs-lookup"><span data-stu-id="7e534-307">hello code in this section shows how tooevaluate a logistic regression model against a test data-set, including a plot of hello ROC curve.</span></span>

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


<span data-ttu-id="7e534-308">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-308">**OUTPUT**</span></span>

<span data-ttu-id="7e534-309">PR 下的領域 = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="7e534-309">Area under PR = 0.985336538462</span></span>

<span data-ttu-id="7e534-310">ROC 下的領域 = 0.983383274312</span><span class="sxs-lookup"><span data-stu-id="7e534-310">Area under ROC = 0.983383274312</span></span>

<span data-ttu-id="7e534-311">摘要狀態</span><span class="sxs-lookup"><span data-stu-id="7e534-311">Summary Stats</span></span>

<span data-ttu-id="7e534-312">精確度 = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="7e534-312">Precision = 0.984174341679</span></span>

<span data-ttu-id="7e534-313">回收 = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="7e534-313">Recall = 0.984174341679</span></span>

<span data-ttu-id="7e534-314">F1 分數 = 0.984174341679</span><span class="sxs-lookup"><span data-stu-id="7e534-314">F1 Score = 0.984174341679</span></span>

<span data-ttu-id="7e534-315">時間 tooexecute 儲存格上方： 2.67 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-315">Time taken tooexecute above cell: 2.67 seconds</span></span>

<span data-ttu-id="7e534-316">**繪製 hello ROC 曲線。**</span><span class="sxs-lookup"><span data-stu-id="7e534-316">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="7e534-317">hello *predictionAndLabelsDF*註冊為資料表， *tmp_results*，在 hello 上一個儲存格。</span><span class="sxs-lookup"><span data-stu-id="7e534-317">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="7e534-318">*tmp_results*可以使用的 toodo 查詢和 hello sqlResults 資料框架來繪製至輸出結果。</span><span class="sxs-lookup"><span data-stu-id="7e534-318">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="7e534-319">Hello 程式碼如下。</span><span class="sxs-lookup"><span data-stu-id="7e534-319">Here is hello code.</span></span>

    # QUERY RESULTS                              
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="7e534-320">以下是 hello 程式碼 toomake 預測及繪圖 hello ROC 曲線。</span><span class="sxs-lookup"><span data-stu-id="7e534-320">Here is hello code toomake predictions and plot hello ROC-curve.</span></span>

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


<span data-ttu-id="7e534-321">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-321">**OUTPUT**</span></span>

![泛型方法的羅吉斯迴歸 ROC 曲線](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/logistic-regression-roc-curve.png)

<span data-ttu-id="7e534-323">**blob 中供未來取用的保留模型**</span><span class="sxs-lookup"><span data-stu-id="7e534-323">**Persist model in a blob for future consumption**</span></span>

<span data-ttu-id="7e534-324">本節中的 hello 程式碼會示範如何 toosave hello 羅吉斯迴歸模型的耗用量。</span><span class="sxs-lookup"><span data-stu-id="7e534-324">hello code in this section shows how toosave hello logistic regression model for consumption.</span></span>

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


<span data-ttu-id="7e534-325">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-325">**OUTPUT**</span></span>

<span data-ttu-id="7e534-326">時間 tooexecute 儲存格上方： 34.57 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-326">Time taken tooexecute above cell: 34.57 seconds</span></span>

### <a name="use-mllibs-crossvalidator-pipeline-function-with-logistic-regression-elastic-regression-model"></a><span data-ttu-id="7e534-327">搭配使用 MLlib 的 CrossValidator 管線函式與 LogisticRegression (彈性迴歸) 模型</span><span class="sxs-lookup"><span data-stu-id="7e534-327">Use MLlib's CrossValidator pipeline function with logistic regression (Elastic regression) model</span></span>
<span data-ttu-id="7e534-328">本節中的 hello 程式碼顯示如何 tootrain，評估及儲存與羅吉斯迴歸模型[LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm)的預測是否付費的行程 hello NYC 計程車行程及價位資料集中的提示。</span><span class="sxs-lookup"><span data-stu-id="7e534-328">hello code in this section shows how tootrain, evaluate, and save a logistic regression model with [LBFGS](https://en.wikipedia.org/wiki/Broyden%E2%80%93Fletcher%E2%80%93Goldfarb%E2%80%93Shanno_algorithm) that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="7e534-329">hello 模型使用交叉驗證 (CV) 來定型和 hyperparameter 掃掠實作以 hello MLlib CrossValidator 管線函式的 CV 參數掃掠。</span><span class="sxs-lookup"><span data-stu-id="7e534-329">hello model is trained using cross validation (CV) and hyperparameter sweeping implemented with hello MLlib CrossValidator pipeline function for CV with parameter sweep.</span></span>   

> [!NOTE]
> <span data-ttu-id="7e534-330">hello 執行此 MLlib CV 程式碼可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="7e534-330">hello execution of this MLlib CV code can take several minutes.</span></span>
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

<span data-ttu-id="7e534-331">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-331">**OUTPUT**</span></span>

<span data-ttu-id="7e534-332">時間 tooexecute 儲存格上方： 107.98 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-332">Time taken tooexecute above cell: 107.98 seconds</span></span>

<span data-ttu-id="7e534-333">**繪製 hello ROC 曲線。**</span><span class="sxs-lookup"><span data-stu-id="7e534-333">**Plot hello ROC curve.**</span></span>

<span data-ttu-id="7e534-334">hello *predictionAndLabelsDF*註冊為資料表， *tmp_results*，在 hello 上一個儲存格。</span><span class="sxs-lookup"><span data-stu-id="7e534-334">hello *predictionAndLabelsDF* is registered as a table, *tmp_results*, in hello previous cell.</span></span> <span data-ttu-id="7e534-335">*tmp_results*可以使用的 toodo 查詢和 hello sqlResults 資料框架來繪製至輸出結果。</span><span class="sxs-lookup"><span data-stu-id="7e534-335">*tmp_results* can be used toodo queries and output results into hello sqlResults data-frame for plotting.</span></span> <span data-ttu-id="7e534-336">Hello 程式碼如下。</span><span class="sxs-lookup"><span data-stu-id="7e534-336">Here is hello code.</span></span>

    # QUERY RESULTS
    %%sql -q -o sqlResults
    SELECT label, prediction, probability from tmp_results

<span data-ttu-id="7e534-337">以下是 hello 程式碼 tooplot hello ROC 曲線。</span><span class="sxs-lookup"><span data-stu-id="7e534-337">Here is hello code tooplot hello ROC curve.</span></span>

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


<span data-ttu-id="7e534-338">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-338">**OUTPUT**</span></span>

![使用 MLlib 的 CrossValidator 的羅吉斯迴歸 ROC 曲線](./media/machine-learning-data-science-spark-advanced-data-exploration-modeling/mllib-crossvalidator-roc-curve.png)

### <a name="random-forest-classification"></a><span data-ttu-id="7e534-340">隨機樹系分類</span><span class="sxs-lookup"><span data-stu-id="7e534-340">Random forest classification</span></span>
<span data-ttu-id="7e534-341">本節中的 hello 程式碼會示範如何 tootrain，評估及儲存預測提示支付路線 hello NYC 計程車行程及價位資料集內的隨機樹系迴歸。</span><span class="sxs-lookup"><span data-stu-id="7e534-341">hello code in this section shows how tootrain, evaluate, and save a random forest regression that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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


<span data-ttu-id="7e534-342">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-342">**OUTPUT**</span></span>

<span data-ttu-id="7e534-343">ROC 下的領域 = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="7e534-343">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="7e534-344">時間 tooexecute 儲存格上方： 26.72 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-344">Time taken tooexecute above cell: 26.72 seconds</span></span>

### <a name="gradient-boosting-trees-classification"></a><span data-ttu-id="7e534-345">漸層停駐提升樹狀結構類別</span><span class="sxs-lookup"><span data-stu-id="7e534-345">Gradient boosting trees classification</span></span>
<span data-ttu-id="7e534-346">本節中的 hello 程式碼會示範 tootrain，如何評估及儲存預測提示支付 hello NYC 計程車行程及價位資料集中的行程的漸層停駐提升樹模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-346">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts whether or not a tip is paid for a trip in hello NYC taxi trip and fare dataset.</span></span>

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

<span data-ttu-id="7e534-347">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-347">**OUTPUT**</span></span>

<span data-ttu-id="7e534-348">ROC 下的領域 = 0.985336538462</span><span class="sxs-lookup"><span data-stu-id="7e534-348">Area under ROC = 0.985336538462</span></span>

<span data-ttu-id="7e534-349">時間 tooexecute 儲存格上方： 28.13 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-349">Time taken tooexecute above cell: 28.13 seconds</span></span>

## <a name="predict-tip-amount-with-regression-models-not-using-cv"></a><span data-ttu-id="7e534-350">使用迴歸模型預測小費金額 (非使用 CV)</span><span class="sxs-lookup"><span data-stu-id="7e534-350">Predict tip amount with regression models (not using CV)</span></span>
<span data-ttu-id="7e534-351">本節說明如何使用三個模型 hello 迴歸工作： 預測支付其他提示功能為基礎的計程車行程 hello 提示數量。</span><span class="sxs-lookup"><span data-stu-id="7e534-351">This section shows how use three models for hello regression task: predict hello tip amount paid for a taxi trip based on other tip features.</span></span> <span data-ttu-id="7e534-352">呈現的 hello 模型如下：</span><span class="sxs-lookup"><span data-stu-id="7e534-352">hello models presented are:</span></span>

* <span data-ttu-id="7e534-353">正規化線性迴歸</span><span class="sxs-lookup"><span data-stu-id="7e534-353">Regularized linear regression</span></span>
* <span data-ttu-id="7e534-354">隨機樹系</span><span class="sxs-lookup"><span data-stu-id="7e534-354">Random forest</span></span>
* <span data-ttu-id="7e534-355">漸層停駐提升樹狀結構</span><span class="sxs-lookup"><span data-stu-id="7e534-355">Gradient Boosting Trees</span></span>

<span data-ttu-id="7e534-356">這些模型是以 hello 簡介所述。</span><span class="sxs-lookup"><span data-stu-id="7e534-356">These models were described in hello introduction.</span></span> <span data-ttu-id="7e534-357">每個模型建置程式碼區段會分成幾個步驟︰</span><span class="sxs-lookup"><span data-stu-id="7e534-357">Each model building code section is split into steps:</span></span> 

1. <span data-ttu-id="7e534-358">**模型定型** 資料</span><span class="sxs-lookup"><span data-stu-id="7e534-358">**Model training** data with one parameter set</span></span>
2. <span data-ttu-id="7e534-359">**模型評估** </span><span class="sxs-lookup"><span data-stu-id="7e534-359">**Model evaluation** on a test data set with metrics</span></span>
3. <span data-ttu-id="7e534-360">**儲存模型** </span><span class="sxs-lookup"><span data-stu-id="7e534-360">**Saving model** in blob for future consumption</span></span>   

> <span data-ttu-id="7e534-361">AZURE 的附註： 交叉驗證未搭配使用 hello 三種迴歸模型在本節中，因為這顯示 hello 羅吉斯迴歸模型的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7e534-361">AZURE NOTE: Cross-validation is not used with hello three regression models in this section, since this was shown in detail for hello logistic regression models.</span></span> <span data-ttu-id="7e534-362">範例顯示 hello 這個主題的 < 附錄中提供 toouse 與彈性 Net CV 線性迴歸的方式。</span><span class="sxs-lookup"><span data-stu-id="7e534-362">An example showing how toouse CV with Elastic Net for linear regression is provided in hello Appendix of this topic.</span></span>
> 
> <span data-ttu-id="7e534-363">AZURE 的附註： 我們的經驗，可能有問題有 LinearRegressionWithSGD 模型的交集，參數必須 toobe 變更/最佳化仔細取得有效的模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-363">AZURE NOTE: In our experience, there can be issues with convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="7e534-364">調整變數對於聚合很有用。</span><span class="sxs-lookup"><span data-stu-id="7e534-364">Scaling of variables significantly helps with convergence.</span></span> <span data-ttu-id="7e534-365">Net 迴歸彈性，顯示在 hello 附錄 toothis 主題中，也可以代替 LinearRegressionWithSGD。</span><span class="sxs-lookup"><span data-stu-id="7e534-365">Elastic net regression, shown in hello Appendix toothis topic, can also be used instead of LinearRegressionWithSGD.</span></span>
> 
> 

### <a name="linear-regression-with-sgd"></a><span data-ttu-id="7e534-366">使用 SGD 的線性迴歸</span><span class="sxs-lookup"><span data-stu-id="7e534-366">Linear regression with SGD</span></span>
<span data-ttu-id="7e534-367">hello 本節中的程式碼會示範如何 toouse 會縮放功能 tootrain 最佳化，使用隨機梯度下降 (SGD) 線性迴歸以及 tooscore，如何評估，並將 hello 模型儲存在 Azure Blob 儲存體 (WASB)。</span><span class="sxs-lookup"><span data-stu-id="7e534-367">hello code in this section shows how toouse scaled features tootrain a linear regression that uses stochastic gradient descent (SGD) for optimization, and how tooscore, evaluate, and save hello model in Azure Blob Storage (WASB).</span></span>

> [!TIP]
> <span data-ttu-id="7e534-368">在我們的經驗，可能有問題的 hello 交集的 LinearRegressionWithSGD 模型，而參數需要 toobe 變更/最佳化仔細取得有效的模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-368">In our experience, there can be issues with hello convergence of LinearRegressionWithSGD models, and parameters need toobe changed/optimized carefully for obtaining a valid model.</span></span> <span data-ttu-id="7e534-369">調整變數對於聚合很有用。</span><span class="sxs-lookup"><span data-stu-id="7e534-369">Scaling of variables significantly helps with convergence.</span></span>
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

<span data-ttu-id="7e534-370">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-370">**OUTPUT**</span></span>

<span data-ttu-id="7e534-371">係數：[0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span><span class="sxs-lookup"><span data-stu-id="7e534-371">Coefficients: [0.0141707753435, -0.0252930927087, -0.0231442517137, 0.247070902996, 0.312544147152, 0.360296120645, 0.0122079566092, -0.00456498588241, -0.0898228505177, 0.0714046248793, 0.102171263868, 0.100022455632, -0.00289545676449, -0.00791124681938, 0.54396316518, -0.536293513569, 0.0119076553369, -0.0173039244582, 0.0119632796147, 0.00146764882502]</span></span>

<span data-ttu-id="7e534-372">截距：0.854507624459</span><span class="sxs-lookup"><span data-stu-id="7e534-372">Intercept: 0.854507624459</span></span>

<span data-ttu-id="7e534-373">RMSE = 1.23485131376</span><span class="sxs-lookup"><span data-stu-id="7e534-373">RMSE = 1.23485131376</span></span>

<span data-ttu-id="7e534-374">R-sqr = 0.597963951127</span><span class="sxs-lookup"><span data-stu-id="7e534-374">R-sqr = 0.597963951127</span></span>

<span data-ttu-id="7e534-375">時間 tooexecute 儲存格上方： 38.62 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-375">Time taken tooexecute above cell: 38.62 seconds</span></span>

### <a name="random-forest-regression"></a><span data-ttu-id="7e534-376">隨機樹系迴歸</span><span class="sxs-lookup"><span data-stu-id="7e534-376">Random Forest regression</span></span>
<span data-ttu-id="7e534-377">本節中的 hello 程式碼會示範如何 tootrain，評估及儲存預測 hello NYC 計程車路線資料的提示數量的隨機樹系模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-377">hello code in this section shows how tootrain, evaluate, and save a random forest model that predicts tip amount for hello NYC taxi trip data.</span></span>   

> [!NOTE]
> <span data-ttu-id="7e534-378">交叉驗證參數掃掠使用自訂程式碼與 hello 附錄中提供。</span><span class="sxs-lookup"><span data-stu-id="7e534-378">Cross-validation with parameter sweeping using custom code is provided in hello appendix.</span></span>
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

<span data-ttu-id="7e534-379">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-379">**OUTPUT**</span></span>

<span data-ttu-id="7e534-380">RMSE = 0.931981967875</span><span class="sxs-lookup"><span data-stu-id="7e534-380">RMSE = 0.931981967875</span></span>

<span data-ttu-id="7e534-381">R-sqr = 0.733445485802</span><span class="sxs-lookup"><span data-stu-id="7e534-381">R-sqr = 0.733445485802</span></span>

<span data-ttu-id="7e534-382">時間 tooexecute 儲存格上方： 25.98 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-382">Time taken tooexecute above cell: 25.98 seconds</span></span>

### <a name="gradient-boosting-trees-regression"></a><span data-ttu-id="7e534-383">漸層停駐提升樹狀結構迴歸</span><span class="sxs-lookup"><span data-stu-id="7e534-383">Gradient boosting trees regression</span></span>
<span data-ttu-id="7e534-384">本節中的 hello 程式碼會示範 tootrain，如何評估及儲存預測 hello NYC 計程車路線資料的提示數量的漸層停駐提升樹模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-384">hello code in this section shows how tootrain, evaluate, and save a gradient boosting trees model that predicts tip amount for hello NYC taxi trip data.</span></span>

<span data-ttu-id="7e534-385">**訓練及評估 **</span><span class="sxs-lookup"><span data-stu-id="7e534-385">**Train and evaluate **</span></span>

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


<span data-ttu-id="7e534-386">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-386">**OUTPUT**</span></span>

<span data-ttu-id="7e534-387">RMSE = 0.928172197114</span><span class="sxs-lookup"><span data-stu-id="7e534-387">RMSE = 0.928172197114</span></span>

<span data-ttu-id="7e534-388">R-sqr = 0.732680354389</span><span class="sxs-lookup"><span data-stu-id="7e534-388">R-sqr = 0.732680354389</span></span>

<span data-ttu-id="7e534-389">時間 tooexecute 儲存格上方： 20.9 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-389">Time taken tooexecute above cell: 20.9 seconds</span></span>

<span data-ttu-id="7e534-390">**圖**</span><span class="sxs-lookup"><span data-stu-id="7e534-390">**Plot**</span></span>

<span data-ttu-id="7e534-391">*tmp_results*註冊為 hello 前一個資料格集中的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="7e534-391">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="7e534-392">來自 hello 資料表的結果會輸出到 hello *sqlResults*來繪製資料框架。</span><span class="sxs-lookup"><span data-stu-id="7e534-392">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="7e534-393">以下是 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="7e534-393">Here is hello code</span></span>

    # PLOT SCATTER-PLOT BETWEEN ACTUAL AND PREDICTED TIP VALUES

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT * from tmp_results


<span data-ttu-id="7e534-394">以下是使用 hello Jupyter 伺服器 hello 程式碼 tooplot hello 資料。</span><span class="sxs-lookup"><span data-stu-id="7e534-394">Here is hello code tooplot hello data using hello Jupyter server.</span></span>

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

## <a name="appendix-additional-regression-tasks-using-cross-validation-with-parameter-sweeps"></a><span data-ttu-id="7e534-396">附錄︰使用交叉驗證與參數掃掠的額外迴歸工作</span><span class="sxs-lookup"><span data-stu-id="7e534-396">Appendix: Additional regression tasks using cross validation with parameter sweeps</span></span>
<span data-ttu-id="7e534-397">本附錄包含程式碼顯示如何使用線性迴歸和如何 toodo CV 參數掃掠隨機樹系迴歸中使用自訂程式碼的彈性 net toodo CV。</span><span class="sxs-lookup"><span data-stu-id="7e534-397">This appendix contains code showing how toodo CV using Elastic net for linear regression and how toodo CV with parameter sweep using custom code for random forest regression.</span></span>

### <a name="cross-validation-using-elastic-net-for-linear-regression"></a><span data-ttu-id="7e534-398">針對線性迴歸使用彈性 net 進行交叉驗證</span><span class="sxs-lookup"><span data-stu-id="7e534-398">Cross validation using Elastic net for linear regression</span></span>
<span data-ttu-id="7e534-399">本節中的 hello 程式碼會示範 toodo 交叉驗證使用線性迴歸 net 彈性的方式，以及如何 tooevaluate hello 針對測試資料的模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-399">hello code in this section shows how toodo cross validation using Elastic net for linear regression and how tooevaluate hello model against test data.</span></span>

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


<span data-ttu-id="7e534-400">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-400">**OUTPUT**</span></span>

<span data-ttu-id="7e534-401">時間 tooexecute 儲存格上方： 161.21 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-401">Time taken tooexecute above cell: 161.21  seconds</span></span>

<span data-ttu-id="7e534-402">**使用 R-SQR 度量進行評估**</span><span class="sxs-lookup"><span data-stu-id="7e534-402">**Evaluate with R-SQR metric**</span></span>

<span data-ttu-id="7e534-403">*tmp_results*註冊為 hello 前一個資料格集中的 Hive 資料表。</span><span class="sxs-lookup"><span data-stu-id="7e534-403">*tmp_results* is registered as a Hive table in hello previous cell.</span></span> <span data-ttu-id="7e534-404">來自 hello 資料表的結果會輸出到 hello *sqlResults*來繪製資料框架。</span><span class="sxs-lookup"><span data-stu-id="7e534-404">Results from hello table are output into hello *sqlResults* data-frame for plotting.</span></span> <span data-ttu-id="7e534-405">以下是 hello 程式碼</span><span class="sxs-lookup"><span data-stu-id="7e534-405">Here is hello code</span></span>

    # SELECT RESULTS
    %%sql -q -o sqlResults
    SELECT label,prediction from tmp_results


<span data-ttu-id="7e534-406">以下是 hello 程式碼 toocalculate R sqr。</span><span class="sxs-lookup"><span data-stu-id="7e534-406">Here is hello code toocalculate R-sqr.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    from scipy import stats

    #R-SQR TEST METRIC
    corstats = stats.linregress(sqlResults['label'],sqlResults['prediction'])
    r2 = (corstats[2]*corstats[2])
    print("R-sqr = %s" % r2)


<span data-ttu-id="7e534-407">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-407">**OUTPUT**</span></span>

<span data-ttu-id="7e534-408">R-sqr = 0.619184907088</span><span class="sxs-lookup"><span data-stu-id="7e534-408">R-sqr = 0.619184907088</span></span>

### <a name="cross-validation-with-parameter-sweep-using-custom-code-for-random-forest-regression"></a><span data-ttu-id="7e534-409">針對隨機樹系迴歸使用自訂程式碼以參數掃掠進行交叉驗證。</span><span class="sxs-lookup"><span data-stu-id="7e534-409">Cross validation with parameter sweep using custom code for random forest regression</span></span>
<span data-ttu-id="7e534-410">本節中的 hello 程式碼會示範 toodo 參數掃掠隨機樹系迴歸中使用自訂程式碼使用交叉驗證的方式和 tooevaluate hello 模型測試資料的方式。</span><span class="sxs-lookup"><span data-stu-id="7e534-410">hello code in this section shows how toodo cross validation with parameter sweep using custom code for random forest regression and how tooevaluate hello model against test data.</span></span>

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


<span data-ttu-id="7e534-411">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-411">**OUTPUT**</span></span>

<span data-ttu-id="7e534-412">RMSE = 0.906972198262</span><span class="sxs-lookup"><span data-stu-id="7e534-412">RMSE = 0.906972198262</span></span>

<span data-ttu-id="7e534-413">R-sqr = 0.740751197012</span><span class="sxs-lookup"><span data-stu-id="7e534-413">R-sqr = 0.740751197012</span></span>

<span data-ttu-id="7e534-414">時間 tooexecute 儲存格上方： 69.17 秒</span><span class="sxs-lookup"><span data-stu-id="7e534-414">Time taken tooexecute above cell: 69.17 seconds</span></span>

### <a name="clean-up-objects-from-memory-and-print-model-locations"></a><span data-ttu-id="7e534-415">從記憶體清除物件並列印模型位置</span><span class="sxs-lookup"><span data-stu-id="7e534-415">Clean up objects from memory and print model locations</span></span>
<span data-ttu-id="7e534-416">使用`unpersist()`toodelete 物件在記憶體中快取。</span><span class="sxs-lookup"><span data-stu-id="7e534-416">Use `unpersist()` toodelete objects cached in memory.</span></span>

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


<span data-ttu-id="7e534-417">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-417">**OUTPUT**</span></span>

<span data-ttu-id="7e534-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span><span class="sxs-lookup"><span data-stu-id="7e534-418">PythonRDD[122] at RDD at PythonRDD.scala: 43</span></span>

<span data-ttu-id="7e534-419">* * 列印輸出路徑 toomodel 檔案 toobe hello 耗用量筆記本中使用。</span><span class="sxs-lookup"><span data-stu-id="7e534-419">**Printout path toomodel files toobe used in hello consumption notebook.</span></span> <span data-ttu-id="7e534-420">* * tooconsume 和分數不受影響的資料集，您需要 toocopy 並將這些檔案名稱貼入 hello"耗用量筆記型電腦 」 中。</span><span class="sxs-lookup"><span data-stu-id="7e534-420">** tooconsume and score an independent data-set, you need toocopy and paste these file names in hello "Consumption notebook".</span></span>

    # PRINT MODEL FILE LOCATIONS FOR CONSUMPTION
    print "logisticRegFileLoc = modelDir + \"" + logisticregressionfilename + "\"";
    print "linearRegFileLoc = modelDir + \"" + linearregressionfilename + "\"";
    print "randomForestClassificationFileLoc = modelDir + \"" + rfclassificationfilename + "\"";
    print "randomForestRegFileLoc = modelDir + \"" + rfregressionfilename + "\"";
    print "BoostedTreeClassificationFileLoc = modelDir + \"" + btclassificationfilename + "\"";
    print "BoostedTreeRegressionFileLoc = modelDir + \"" + btregressionfilename + "\"";


<span data-ttu-id="7e534-421">**輸出**</span><span class="sxs-lookup"><span data-stu-id="7e534-421">**OUTPUT**</span></span>

<span data-ttu-id="7e534-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span><span class="sxs-lookup"><span data-stu-id="7e534-422">logisticRegFileLoc = modelDir + "LogisticRegressionWithLBFGS_2016-05-0316_47_30.096528"</span></span>

<span data-ttu-id="7e534-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span><span class="sxs-lookup"><span data-stu-id="7e534-423">linearRegFileLoc = modelDir + "LinearRegressionWithSGD_2016-05-0316_51_28.433670"</span></span>

<span data-ttu-id="7e534-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span><span class="sxs-lookup"><span data-stu-id="7e534-424">randomForestClassificationFileLoc = modelDir + "RandomForestClassification_2016-05-0316_50_17.454440"</span></span>

<span data-ttu-id="7e534-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span><span class="sxs-lookup"><span data-stu-id="7e534-425">randomForestRegFileLoc = modelDir + "RandomForestRegression_2016-05-0316_51_57.331730"</span></span>

<span data-ttu-id="7e534-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span><span class="sxs-lookup"><span data-stu-id="7e534-426">BoostedTreeClassificationFileLoc = modelDir + "GradientBoostingTreeClassification_2016-05-0316_50_40.138809"</span></span>

<span data-ttu-id="7e534-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span><span class="sxs-lookup"><span data-stu-id="7e534-427">BoostedTreeRegressionFileLoc = modelDir + "GradientBoostingTreeRegression_2016-05-0316_52_18.827237"</span></span>

## <a name="whats-next"></a><span data-ttu-id="7e534-428">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e534-428">What's next?</span></span>
<span data-ttu-id="7e534-429">現在您已經以 hello Spark MlLib 建立迴歸和分類的模型，您就準備好 toolearn 如何 tooscore 和評估這些模型。</span><span class="sxs-lookup"><span data-stu-id="7e534-429">Now that you have created regression and classification models with hello Spark MlLib, you are ready toolearn how tooscore and evaluate these models.</span></span>

<span data-ttu-id="7e534-430">**模型耗用量：** toolearn 如何 tooscore 和評估建立本主題中的 hello 分類和迴歸模型，請參閱[分數及評估 Spark 建立機器學習模型](machine-learning-data-science-spark-model-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="7e534-430">**Model consumption:** toolearn how tooscore and evaluate hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

