---
title: "在 Azure 上使用 Scala 與 Spark 的資料科學 | Microsoft Docs"
description: "如何使用 Scala 搭配 Spark 可調整 MLlib 和 Azure HDInsight Spark 叢集上的 SparkML 封裝，處理受監督的機器學習工作。"
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
ms.openlocfilehash: b2419f53bdc3236d7de76b89f2a0a76704e85391
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="8232e-103">在 Azure 上使用 Scala 與 Spark 的資料科學</span><span class="sxs-lookup"><span data-stu-id="8232e-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="8232e-104">本文章說明如何使用 Scala 搭配 Spark 可調整 MLlib 和 Azure HDInsight Spark 叢集上的 SparkML 封裝，處理受監督的機器學習工作。</span><span class="sxs-lookup"><span data-stu-id="8232e-104">This article shows you how to use Scala for supervised machine learning tasks with the Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="8232e-105">它會引導您進行構成 [資料科學程序](http://aka.ms/datascienceprocess)的各項工作︰資料擷取和探索、視覺化、特徵設計、模型化和模型取用。</span><span class="sxs-lookup"><span data-stu-id="8232e-105">It walks you through the tasks that constitute the [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="8232e-106">本文中的模型除了兩個常見受監督的機器學習工作之外，還包括羅吉斯和線性迴歸、隨機樹系和梯度推進樹 (GBT)︰</span><span class="sxs-lookup"><span data-stu-id="8232e-106">The models in the article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition to two common supervised machine learning tasks:</span></span>

* <span data-ttu-id="8232e-107">迴歸問題︰計程車車程的小費金額 ($) 預測</span><span class="sxs-lookup"><span data-stu-id="8232e-107">Regression problem: Prediction of the tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="8232e-108">二進位分類︰計程車車程的小費或不給小費 (1/0) 預測</span><span class="sxs-lookup"><span data-stu-id="8232e-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="8232e-109">模型化程序需要訓練和評估測試資料集和相關精確度計量。</span><span class="sxs-lookup"><span data-stu-id="8232e-109">The modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="8232e-110">在本文中，您會了解如何在 Azure Blob 儲存體中儲存這些模型，以及如何評分及評估模型的預測效能。</span><span class="sxs-lookup"><span data-stu-id="8232e-110">In this article, you can learn how to store these models in Azure Blob storage and how to score and evaluate their predictive performance.</span></span> <span data-ttu-id="8232e-111">本文也涵蓋如何使用交叉驗證和超參數掃掠來最佳化模型等更進階的主題。</span><span class="sxs-lookup"><span data-stu-id="8232e-111">This article also covers the more advanced topics of how to optimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="8232e-112">所使用的資料是 GitHub 上 2013 年紐約市計程車車程和費用資料集的抽樣樣本。</span><span class="sxs-lookup"><span data-stu-id="8232e-112">The data used is a sample of the 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="8232e-113">[Scala](http://www.scala-lang.org/)是一種以 Java 虛擬機器為基礎的語言，整合物件導向與函式型語言的概念。</span><span class="sxs-lookup"><span data-stu-id="8232e-113">[Scala](http://www.scala-lang.org/), a language based on the Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="8232e-114">這是一種可調整的語言，非常適合用於雲端中的分散式處理以及在 Azure Spark 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="8232e-114">It's a scalable language that is well suited to distributed processing in the cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="8232e-115">[Spark](http://spark.apache.org/) 是一個開放原始碼平行處理架構，可支援記憶體內部處理，大幅提升巨量資料分析應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="8232e-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing to boost the performance of big data analytics applications.</span></span> <span data-ttu-id="8232e-116">Spark 處理引擎是專為速度、易用性及精密分析打造的產品。</span><span class="sxs-lookup"><span data-stu-id="8232e-116">The Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="8232e-117">Spark 的記憶體內分散式計算功能，使其成為機器學習和圖表計算中反覆演算法的絕佳選擇。</span><span class="sxs-lookup"><span data-stu-id="8232e-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="8232e-118">[Spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) 封裝提供一組以資料框架為基礎的統一高階 API，可協助您建立及微調實際的機器學習管線。</span><span class="sxs-lookup"><span data-stu-id="8232e-118">The [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="8232e-119">[MLlib](http://spark.apache.org/mllib/) 是 Spark 的可調整機器學習程式庫，將模型化功能引進此分散式環境。</span><span class="sxs-lookup"><span data-stu-id="8232e-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities to this distributed environment.</span></span>

<span data-ttu-id="8232e-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) 是開放原始碼 Spark 的 Azure 託管服務。</span><span class="sxs-lookup"><span data-stu-id="8232e-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is the Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="8232e-121">它也支援 Spark 叢集上的 Jupyter Scala Notebook，可執行 Spark SQL 互動式查詢以轉換、篩選和視覺化 Azure Blob 儲存體中儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="8232e-121">It also includes support for Jupyter Scala notebooks on the Spark cluster, and can run Spark SQL interactive queries to transform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="8232e-122">本文中的 Scala 程式碼片段提供解決方案，並且顯示相關的繪圖，將安裝在 Spark 叢集上的 Jupyter Notebook 資料加以視覺化。</span><span class="sxs-lookup"><span data-stu-id="8232e-122">The Scala code snippets in this article that provide the solutions and show the relevant plots to visualize the data run in Jupyter notebooks installed on the Spark clusters.</span></span> <span data-ttu-id="8232e-123">這些主題中的模型化步驟有程式碼向您示範如何訓練、評估、儲存和使用各類模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-123">The modeling steps in these topics have code that shows you how to train, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="8232e-124">本文中的設定步驟與程式碼適用於 Azure HDInsight 3.4 Spark 1.6。</span><span class="sxs-lookup"><span data-stu-id="8232e-124">The setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="8232e-125">不過，本文與 [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) 中的程式碼皆屬泛型程式碼，應該能在任何 Spark 叢集上運作。</span><span class="sxs-lookup"><span data-stu-id="8232e-125">However, the code in this article and in the [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="8232e-126">若未使用 HDInsight Spark，叢集設定和管理步驟可能與本文顯示的稍有不同。</span><span class="sxs-lookup"><span data-stu-id="8232e-126">The cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="8232e-127">如需示範如何使用 Python 而非 Scala 來完成端對端資料科學程序工作的主題，請參閱 [在 Azure HDInsight 上使用 Spark 的資料科學](machine-learning-data-science-spark-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8232e-127">For a topic that shows you how to use Python rather than Scala to complete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="8232e-128">必要條件</span><span class="sxs-lookup"><span data-stu-id="8232e-128">Prerequisites</span></span>
* <span data-ttu-id="8232e-129">您必須擁有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="8232e-129">You must have an Azure subscription.</span></span> <span data-ttu-id="8232e-130">如果還沒有， [請取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="8232e-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="8232e-131">您需要 Azure HDInsight 3.4 Spark 1.6 叢集來完成下列程序。</span><span class="sxs-lookup"><span data-stu-id="8232e-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster to complete the following procedures.</span></span> <span data-ttu-id="8232e-132">若要建立叢集，請參閱 [開始使用：在 Azure HDInsight 上建立 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)中的指示。</span><span class="sxs-lookup"><span data-stu-id="8232e-132">To create a cluster, see the instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="8232e-133">在 [選取叢集類型]  功能表上設定叢集類型和版本。</span><span class="sxs-lookup"><span data-stu-id="8232e-133">Set the cluster type and version on the **Select Cluster Type** menu.</span></span>

![HDInsight 叢集類型組態](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="8232e-135">如需紐約市計程車車程資料的說明以及如何在 Spark 叢集上從 Jupyter Notebook 執行程式碼的指示，請參閱 [在 Azure HDInsight 上使用 Spark 的資料科學概觀](machine-learning-data-science-spark-overview.md)中的相關章節。</span><span class="sxs-lookup"><span data-stu-id="8232e-135">For a description of the NYC taxi trip data and instructions on how to execute code from a Jupyter notebook on the Spark cluster, see the relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-the-spark-cluster"></a><span data-ttu-id="8232e-136">在 Spark 叢集上從 Jupyter Notebook 執行 Scala 程式碼</span><span class="sxs-lookup"><span data-stu-id="8232e-136">Execute Scala code from a Jupyter notebook on the Spark cluster</span></span>
<span data-ttu-id="8232e-137">您可以從 Azure 入口網站啟動 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="8232e-137">You can launch a Jupyter notebook from the Azure portal.</span></span> <span data-ttu-id="8232e-138">在儀表板上尋找 Spark 叢集，然後按一下該項目以進入您的叢集管理頁面。</span><span class="sxs-lookup"><span data-stu-id="8232e-138">Find the Spark cluster on your dashboard, and then click it to enter the management page for your cluster.</span></span> <span data-ttu-id="8232e-139">接著按一下 [叢集儀表板]，然後按一下 [Jupyter Notebook] 來開啟與 Spark 叢集相關聯的 Notebook。</span><span class="sxs-lookup"><span data-stu-id="8232e-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** to open the notebook associated with the Spark cluster.</span></span>

![叢集儀表板和 Jupyter Notebook](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="8232e-141">您也可以在 https://&lt;clustername&gt;.azurehdinsight.net/jupyter 存取 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="8232e-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="8232e-142">將 *clustername* 取代為您叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="8232e-142">Replace *clustername* with the name of your cluster.</span></span> <span data-ttu-id="8232e-143">您需要有系統管理員帳戶的密碼才能存取 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="8232e-143">You need the password for your administrator account to access the Jupyter notebooks.</span></span>

![使用叢集名稱移至 Jupyter Notebook](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="8232e-145">選取 [Scala]  會看到一個目錄，當中有一些使用 PySpark API 的預先封裝 Notebook 的範例。</span><span class="sxs-lookup"><span data-stu-id="8232e-145">Select **Scala** to see a directory that has a few examples of prepackaged notebooks that use the PySpark API.</span></span> <span data-ttu-id="8232e-146">[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala)上有使用 Scala.ipynb Notebook 的探勘模型化和評分，其中包含此 Spark 主題套件的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="8232e-146">The Exploration Modeling and Scoring using Scala.ipynb notebook that contains the code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="8232e-147">您可以將 Notebook 直接從 GitHub 上傳至 Spark 叢集上的 Jupyter Notebook 伺服器。</span><span class="sxs-lookup"><span data-stu-id="8232e-147">You can upload the notebook directly from GitHub to the Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="8232e-148">在 Jupyter 首頁上，按一下 [上傳]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8232e-148">On your Jupyter home page, click the **Upload** button.</span></span> <span data-ttu-id="8232e-149">在檔案總管中，貼上 Scala Notebook 的 GitHub (原始內容) URL，然後按一下 [開啟] 。</span><span class="sxs-lookup"><span data-stu-id="8232e-149">In the file explorer, paste the GitHub (raw content) URL of the Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="8232e-150">下列 URL 有 Scala Notebook 可供使用：</span><span class="sxs-lookup"><span data-stu-id="8232e-150">The Scala notebook is available at the following URL:</span></span>

[<span data-ttu-id="8232e-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="8232e-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="8232e-152">安裝程式︰預設的 Spark 和 Hive 內容、Spark Magic 和 Spark 程式庫</span><span class="sxs-lookup"><span data-stu-id="8232e-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="8232e-153">預設的 Spark 和 Hive 內容</span><span class="sxs-lookup"><span data-stu-id="8232e-153">Preset Spark and Hive contexts</span></span>
    # SET THE START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="8232e-154">Jupyter Notebook 所提供的 Spark 核心有預設的內容。</span><span class="sxs-lookup"><span data-stu-id="8232e-154">The Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="8232e-155">您不必明確設定 Spark 或 Hive 內容，就能開始使用您所開發的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8232e-155">You don't need to explicitly set the Spark or Hive contexts before you start working with the application you are developing.</span></span> <span data-ttu-id="8232e-156">預設內容為：</span><span class="sxs-lookup"><span data-stu-id="8232e-156">The preset contexts are:</span></span>

* <span data-ttu-id="8232e-157">`sc` 代表 SparkContext</span><span class="sxs-lookup"><span data-stu-id="8232e-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="8232e-158">`sqlContext` 代表 HiveContext</span><span class="sxs-lookup"><span data-stu-id="8232e-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="8232e-159">Spark Magic</span><span class="sxs-lookup"><span data-stu-id="8232e-159">Spark magics</span></span>
<span data-ttu-id="8232e-160">Spark 核心提供一些預先定義的 “Magic”，這是您可以使用 `%%`呼叫的特殊命令。</span><span class="sxs-lookup"><span data-stu-id="8232e-160">The Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="8232e-161">下列程式碼範例會使用兩個命令。</span><span class="sxs-lookup"><span data-stu-id="8232e-161">Two of these commands are used in the following code samples.</span></span>

* <span data-ttu-id="8232e-162">`%%local` 指定後續行所列的程式碼，將在本機執行。</span><span class="sxs-lookup"><span data-stu-id="8232e-162">`%%local` specifies that the code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="8232e-163">程式碼必須是有效的 Scala 程式碼。</span><span class="sxs-lookup"><span data-stu-id="8232e-163">The code must be valid Scala code.</span></span>
* <span data-ttu-id="8232e-164">`%%sql -o <variable name>` 針對 `sqlContext` 執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="8232e-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="8232e-165">如果傳遞 `-o` 參數，則查詢的結果會當做 Spark 資料框架，保存在 `%%local` Scala 內容中。</span><span class="sxs-lookup"><span data-stu-id="8232e-165">If the `-o` parameter is passed, the result of the query is persisted in the `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="8232e-166">如需關於 Jupyter Notebook 核心，以及使用 `%%` (例如 `%%local`) 呼叫其預先定義的 "Magic" 的詳細資訊，請參閱 [HDInsight 上的 HDInsight Spark Linux 叢集可供 Jupyter Notebook 使用的核心](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="8232e-166">For more information about the kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="8232e-167">匯入程式庫</span><span class="sxs-lookup"><span data-stu-id="8232e-167">Import libraries</span></span>
<span data-ttu-id="8232e-168">使用下列程式碼匯入 Spark、MLlib 和其他所需的程式庫。</span><span class="sxs-lookup"><span data-stu-id="8232e-168">Import the Spark, MLlib, and other libraries you'll need by using the following code.</span></span>

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


## <a name="data-ingestion"></a><span data-ttu-id="8232e-169">資料擷取</span><span class="sxs-lookup"><span data-stu-id="8232e-169">Data ingestion</span></span>
<span data-ttu-id="8232e-170">資料科學程序的第一步是內嵌您想要分析的資料。</span><span class="sxs-lookup"><span data-stu-id="8232e-170">The first step in the Data Science process is to ingest the data that you want to analyze.</span></span> <span data-ttu-id="8232e-171">您要從資料所在的外部來源或系統，將資料帶入資料探索和模型化環境。</span><span class="sxs-lookup"><span data-stu-id="8232e-171">You bring the data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="8232e-172">在本文中，您要內嵌的資料是聯結 0.1% 取樣的計程車車程和資費檔案 (儲存為 .tsv 檔案)。</span><span class="sxs-lookup"><span data-stu-id="8232e-172">In this article, the data you ingest is a joined 0.1% sample of the taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="8232e-173">資料探索和模型化環境為 Spark。</span><span class="sxs-lookup"><span data-stu-id="8232e-173">The data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="8232e-174">本節包含程式碼來完成下列的工作系列︰</span><span class="sxs-lookup"><span data-stu-id="8232e-174">This section contains the code to complete the following series of tasks:</span></span>

1. <span data-ttu-id="8232e-175">設定資料和模型儲存體的目錄路徑。</span><span class="sxs-lookup"><span data-stu-id="8232e-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="8232e-176">讀取輸入資料集 (儲存為 .tsv 檔案)。</span><span class="sxs-lookup"><span data-stu-id="8232e-176">Read in the input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="8232e-177">定義資料的結構描述並清除資料。</span><span class="sxs-lookup"><span data-stu-id="8232e-177">Define a schema for the data and clean the data.</span></span>
4. <span data-ttu-id="8232e-178">建立已清除的資料框架，並在記憶體中加以快取。</span><span class="sxs-lookup"><span data-stu-id="8232e-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="8232e-179">在 SQLContext 中將資料註冊為暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="8232e-179">Register the data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="8232e-180">查詢資料表並將結果匯入資料框架。</span><span class="sxs-lookup"><span data-stu-id="8232e-180">Query the table and import the results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="8232e-181">在 Azure Blob 儲存體中設定儲存位置的目錄路徑</span><span class="sxs-lookup"><span data-stu-id="8232e-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="8232e-182">Spark 可以讀取和寫入 Azure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="8232e-182">Spark can read and write to Azure Blob storage.</span></span> <span data-ttu-id="8232e-183">您可以使用 Spark 來處理任何現有的資料，然後在 Blob 儲存體中再次儲存結果。</span><span class="sxs-lookup"><span data-stu-id="8232e-183">You can use Spark to process any of your existing data, and then store the results again in Blob storage.</span></span>

<span data-ttu-id="8232e-184">若要在 Blob 儲存體中儲存模型或檔案，您必須正確指定路徑。</span><span class="sxs-lookup"><span data-stu-id="8232e-184">To save models or files in Blob storage, you need to properly specify the path.</span></span> <span data-ttu-id="8232e-185">使用以 `wasb:///`開頭的路徑，參考附加至 Spark 叢集的預設容器。</span><span class="sxs-lookup"><span data-stu-id="8232e-185">Reference the default container attached to the Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="8232e-186">使用 `wasb://`參考其他位置。</span><span class="sxs-lookup"><span data-stu-id="8232e-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="8232e-187">下列程式碼範例指定要讀取輸入資料的位置，以及附加至 Spark 叢集 (將會儲存模型) 的 Blob 儲存體路徑。</span><span class="sxs-lookup"><span data-stu-id="8232e-187">The following code sample specifies the location of the input data to be read and the path to Blob storage that is attached to the Spark cluster where the model will be saved.</span></span>

    # SET PATHS TO DATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET THE MODEL STORAGE DIRECTORY PATH
    # NOTE THAT THE FINAL BACKSLASH IN THE PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-to-the-schema"></a><span data-ttu-id="8232e-188">根據結構描述匯入資料、建立 RDD 並定義資料框架</span><span class="sxs-lookup"><span data-stu-id="8232e-188">Import data, create an RDD, and define a data frame according to the schema</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE SCHEMA BASED ON THE HEADER OF THE FILE
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

    # CAST VARIABLES ACCORDING TO THE SCHEMA
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

    # CACHE AND MATERIALIZE THE CLEANED DATA FRAME IN MEMORY
    taxi_df_train_cleaned.cache()
    taxi_df_train_cleaned.count()

    # REGISTER THE DATA FRAME AS A TEMPORARY TABLE IN SQLCONTEXT
    taxi_df_train_cleaned.registerTempTable("taxi_train")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="8232e-189">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-189">**Output:**</span></span>

<span data-ttu-id="8232e-190">執行資料格的時間︰8 秒。</span><span class="sxs-lookup"><span data-stu-id="8232e-190">Time to run the cell: 8 seconds.</span></span>

### <a name="query-the-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="8232e-191">查詢資料表並將結果匯入資料框架</span><span class="sxs-lookup"><span data-stu-id="8232e-191">Query the table and import results in a data frame</span></span>
<span data-ttu-id="8232e-192">接著，查詢資料表中的資費、乘客和小費資料，篩選出損毀和離群資料，並列印數個資料列。</span><span class="sxs-lookup"><span data-stu-id="8232e-192">Next, query the table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

    # QUERY THE DATA
    val sqlStatement = """
        SELECT fare_amount, passenger_count, tip_amount, tipped
        FROM taxi_train
        WHERE passenger_count > 0 AND passenger_count < 7
        AND fare_amount > 0 AND fare_amount < 200
        AND payment_type in ('CSH', 'CRD')
        AND tip_amount > 0 AND tip_amount < 25
    """
    val sqlResultsDF = sqlContext.sql(sqlStatement)

    # SHOW ONLY THE TOP THREE ROWS
    sqlResultsDF.show(3)

<span data-ttu-id="8232e-193">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-193">**Output:**</span></span>

| <span data-ttu-id="8232e-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="8232e-194">fare_amount</span></span> | <span data-ttu-id="8232e-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="8232e-195">passenger_count</span></span> | <span data-ttu-id="8232e-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="8232e-196">tip_amount</span></span> | <span data-ttu-id="8232e-197">tipped</span><span class="sxs-lookup"><span data-stu-id="8232e-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="8232e-198">13.5</span><span class="sxs-lookup"><span data-stu-id="8232e-198">13.5</span></span> |<span data-ttu-id="8232e-199">1.0</span><span class="sxs-lookup"><span data-stu-id="8232e-199">1.0</span></span> |<span data-ttu-id="8232e-200">2.9</span><span class="sxs-lookup"><span data-stu-id="8232e-200">2.9</span></span> |<span data-ttu-id="8232e-201">1.0</span><span class="sxs-lookup"><span data-stu-id="8232e-201">1.0</span></span> |
|        <span data-ttu-id="8232e-202">16.0</span><span class="sxs-lookup"><span data-stu-id="8232e-202">16.0</span></span> |<span data-ttu-id="8232e-203">2.0</span><span class="sxs-lookup"><span data-stu-id="8232e-203">2.0</span></span> |<span data-ttu-id="8232e-204">3.4</span><span class="sxs-lookup"><span data-stu-id="8232e-204">3.4</span></span> |<span data-ttu-id="8232e-205">1.0</span><span class="sxs-lookup"><span data-stu-id="8232e-205">1.0</span></span> |
|        <span data-ttu-id="8232e-206">10.5</span><span class="sxs-lookup"><span data-stu-id="8232e-206">10.5</span></span> |<span data-ttu-id="8232e-207">2.0</span><span class="sxs-lookup"><span data-stu-id="8232e-207">2.0</span></span> |<span data-ttu-id="8232e-208">1.0</span><span class="sxs-lookup"><span data-stu-id="8232e-208">1.0</span></span> |<span data-ttu-id="8232e-209">1.0</span><span class="sxs-lookup"><span data-stu-id="8232e-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="8232e-210">資料探索和虛擬化</span><span class="sxs-lookup"><span data-stu-id="8232e-210">Data exploration and visualization</span></span>
<span data-ttu-id="8232e-211">將資料帶入 Spark 之後，資料科學程序的下一個步驟是透過探索和視覺化以更深入瞭解資料。</span><span class="sxs-lookup"><span data-stu-id="8232e-211">After you bring the data into Spark, the next step in the Data Science process is to gain a deeper understanding of the data through exploration and visualization.</span></span> <span data-ttu-id="8232e-212">本節中，您可以使用 SQL 查詢檢查計程車資料。</span><span class="sxs-lookup"><span data-stu-id="8232e-212">In this section, you examine the taxi data by using SQL queries.</span></span> <span data-ttu-id="8232e-213">然後將結果匯入資料框架，以使用 Jupyter 的自動視覺化特徵繪製目標變數和潛在特徵以便進行視覺檢查。</span><span class="sxs-lookup"><span data-stu-id="8232e-213">Then, import the results into a data frame to plot the target variables and prospective features for visual inspection by using the auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-to-plot-data"></a><span data-ttu-id="8232e-214">使用本機和 SQL magic 來繪製資料</span><span class="sxs-lookup"><span data-stu-id="8232e-214">Use local and SQL magic to plot data</span></span>
<span data-ttu-id="8232e-215">根據預設，在背景工作節點上保存的工作階段內容中，可取得您從 Jupyter Notebook 執行之任何程式碼片段的輸出。</span><span class="sxs-lookup"><span data-stu-id="8232e-215">By default, the output of any code snippet that you run from a Jupyter notebook is available within the context of the session that is persisted on the worker nodes.</span></span> <span data-ttu-id="8232e-216">如果您想要將車程儲存至每個計算的背景工作節點，而且如果在 Jupyter 伺服器節點 (此為前端節點) 的本機上可取得計算所需的所有資料，您可以使用 `%%local` Magic 在 Jupyter 伺服器上執行程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="8232e-216">If you want to save a trip to the worker nodes for every computation, and if all the data that you need for your computation is available locally on the Jupyter server node (which is the head node), you can use the `%%local` magic to run the code snippet on the Jupyter server.</span></span>

* <span data-ttu-id="8232e-217">**SQL magic** (`%%sql`)。</span><span class="sxs-lookup"><span data-stu-id="8232e-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="8232e-218">HDInsight Spark 核心支援針對 SQLContext 進行簡單的內嵌 HiveQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="8232e-218">The HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="8232e-219">(`-o VARIABLE_NAME`) 引數會將 SQL 查詢的輸出，保存為 Jupyter 伺服器上的 Pandas 資料框架。</span><span class="sxs-lookup"><span data-stu-id="8232e-219">The (`-o VARIABLE_NAME`) argument persists the output of the SQL query as a Pandas data frame on the Jupyter server.</span></span> <span data-ttu-id="8232e-220">這代表會在本機模式中使用此引數。</span><span class="sxs-lookup"><span data-stu-id="8232e-220">This means it'll be available in the local mode.</span></span>
* <span data-ttu-id="8232e-221">`%%local` **magic**。</span><span class="sxs-lookup"><span data-stu-id="8232e-221">`%%local` **magic**.</span></span> <span data-ttu-id="8232e-222">`%%local` magic 在 Jupyter 伺服器本機 (HDInsight 叢集的前端節點) 上執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="8232e-222">The `%%local` magic runs the code locally on the Jupyter server, which is the head node of the HDInsight cluster.</span></span> <span data-ttu-id="8232e-223">一般而言，您會使用 `%%local` magic 來搭配含有 `-o` 參數的 `%%sql` magic。</span><span class="sxs-lookup"><span data-stu-id="8232e-223">Typically, you use `%%local` magic in conjunction with the `%%sql` magic with the `-o` parameter.</span></span> <span data-ttu-id="8232e-224">`-o` 參數會保存本機 SQL 查詢的輸出，然後 `%%local` magic 會針對已保存在本機上的 SQL 查詢輸出，觸發下一組要在本機上執行的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="8232e-224">The `-o` parameter would persist the output of the SQL query locally, and then `%%local` magic would trigger the next set of code snippet to run locally against the output of the SQL queries that is persisted locally.</span></span>

### <a name="query-the-data-by-using-sql"></a><span data-ttu-id="8232e-225">使用 SQL 查詢資料</span><span class="sxs-lookup"><span data-stu-id="8232e-225">Query the data by using SQL</span></span>
<span data-ttu-id="8232e-226">此查詢會依照費用金額、乘客計數和小費金額擷取計程車車程。</span><span class="sxs-lookup"><span data-stu-id="8232e-226">This query retrieves the taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN THE SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="8232e-227">在下列程式碼中， `%%local` magic 會建立本機資料框架 sqlResults。</span><span class="sxs-lookup"><span data-stu-id="8232e-227">In the following code, the `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="8232e-228">您可以使用 sqlResults 透過 matplotlib 繪圖。</span><span class="sxs-lookup"><span data-stu-id="8232e-228">You can use sqlResults to plot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="8232e-229">本文中會多次使用本機 magic。</span><span class="sxs-lookup"><span data-stu-id="8232e-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="8232e-230">如果資料集很大，請進行取樣以建立可容納於本機記憶體的資料框架。</span><span class="sxs-lookup"><span data-stu-id="8232e-230">If your data set is large, please sample to create a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-the-data"></a><span data-ttu-id="8232e-231">繪製資料</span><span class="sxs-lookup"><span data-stu-id="8232e-231">Plot the data</span></span>
<span data-ttu-id="8232e-232">資料框架以 Pandas 資料框架形式出現在本機內容之後，您就可以使用 Python 程式碼進行繪圖。</span><span class="sxs-lookup"><span data-stu-id="8232e-232">You can plot by using Python code after the data frame is in local context as a Pandas data frame.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES.
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="8232e-233">在您執行程式碼之後，Spark 核心會將 SQL (HiveQL) 查詢的輸出自動視覺化。</span><span class="sxs-lookup"><span data-stu-id="8232e-233">The Spark kernel automatically visualizes the output of SQL (HiveQL) queries after you run the code.</span></span> <span data-ttu-id="8232e-234">您可以選擇數種類型的視覺效果︰</span><span class="sxs-lookup"><span data-stu-id="8232e-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="8232e-235">資料表</span><span class="sxs-lookup"><span data-stu-id="8232e-235">Table</span></span>
* <span data-ttu-id="8232e-236">圓形圖</span><span class="sxs-lookup"><span data-stu-id="8232e-236">Pie</span></span>
* <span data-ttu-id="8232e-237">折線圖</span><span class="sxs-lookup"><span data-stu-id="8232e-237">Line</span></span>
* <span data-ttu-id="8232e-238">領域</span><span class="sxs-lookup"><span data-stu-id="8232e-238">Area</span></span>
* <span data-ttu-id="8232e-239">長條圖</span><span class="sxs-lookup"><span data-stu-id="8232e-239">Bar</span></span>

<span data-ttu-id="8232e-240">以下是繪製資料的程式碼：</span><span class="sxs-lookup"><span data-stu-id="8232e-240">Here's the code to plot the data:</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
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


<span data-ttu-id="8232e-241">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-241">**Output:**</span></span>

![小費金額長條圖](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![按乘客計數排列的小費金額](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![按費用金額排列的小費金額](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="8232e-245">建立特徵和轉換特徵，然後準備資料輸入模型化函式</span><span class="sxs-lookup"><span data-stu-id="8232e-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="8232e-246">如需 Spark ML 和 MLlib 中以樹狀結構為基礎的模型化函式，您必須使用各種技術 (例如分類收納、索引編製、one-hot 編碼和向量化) 備妥目標和特徵。</span><span class="sxs-lookup"><span data-stu-id="8232e-246">For tree-based modeling functions from Spark ML and MLlib, you have to prepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="8232e-247">以下是本節要遵循的程序︰</span><span class="sxs-lookup"><span data-stu-id="8232e-247">Here are the procedures to follow in this section:</span></span>

1. <span data-ttu-id="8232e-248">將小時 **納入** 流量時間值區以建立新特徵。</span><span class="sxs-lookup"><span data-stu-id="8232e-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="8232e-249">對分類特徵套用 **索引編製和 one-hot 編碼** 。</span><span class="sxs-lookup"><span data-stu-id="8232e-249">Apply **indexing and one-hot encoding** to categorical features.</span></span>
3. <span data-ttu-id="8232e-250">**取樣並將資料集分割** 成訓練和測試部分。</span><span class="sxs-lookup"><span data-stu-id="8232e-250">**Sample and split the data set** into training and test fractions.</span></span>
4. <span data-ttu-id="8232e-251">**指定訓練變數和特徵**，然後建立已編製索引或已進行 one-hot 編碼的訓練和測試輸入標示點彈性分散式資料集 (RDD) 或資料框架。</span><span class="sxs-lookup"><span data-stu-id="8232e-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="8232e-252">自動 **分類及向量化特徵和目標** 以做為機器學習模型的輸入。</span><span class="sxs-lookup"><span data-stu-id="8232e-252">Automatically **categorize and vectorize features and targets** to use as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="8232e-253">將小時納入流量時間值區以建立新特徵</span><span class="sxs-lookup"><span data-stu-id="8232e-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="8232e-254">此程式碼示範如何將小時納入流量時間值區以建立新特徵，以及如何從記憶體快取產生的資料框架。</span><span class="sxs-lookup"><span data-stu-id="8232e-254">This code shows you how to create a new feature by binning hours into traffic time buckets and how to cache the resulting data frame in memory.</span></span> <span data-ttu-id="8232e-255">在重複使用 RDD 和資料框架的位置，快取可改善執行時間。</span><span class="sxs-lookup"><span data-stu-id="8232e-255">Where RDDs and data frames are used repeatedly, caching leads to improved execution times.</span></span> <span data-ttu-id="8232e-256">因此，您會在下列程序中的幾個階段快取 RDD 和資料框架。</span><span class="sxs-lookup"><span data-stu-id="8232e-256">Accordingly, you'll cache RDDs and data frames at several stages in the following procedures.</span></span>

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

    # CACHE THE DATA FRAME IN MEMORY AND MATERIALIZE THE DATA FRAME IN MEMORY
    taxi_df_train_with_newFeatures.cache()
    taxi_df_train_with_newFeatures.count()


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="8232e-257">索引和 one-hot 編碼分類功能</span><span class="sxs-lookup"><span data-stu-id="8232e-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="8232e-258">MLlib 的模型化和預測函式需要先執行功能來分類要索引或編碼的分類輸入資料，才能使用這些資料。</span><span class="sxs-lookup"><span data-stu-id="8232e-258">The modeling and predict functions of MLlib require features with categorical input data to be indexed or encoded prior to use.</span></span> <span data-ttu-id="8232e-259">本節示範如何索引或編碼分類特徵，以輸入模型化函式。</span><span class="sxs-lookup"><span data-stu-id="8232e-259">This section shows you how to index or encode categorical features for input into the modeling functions.</span></span>

<span data-ttu-id="8232e-260">根據模型，您需要以不同方式索引或編碼它們。</span><span class="sxs-lookup"><span data-stu-id="8232e-260">You need to index or encode your models in different ways, depending on the model.</span></span> <span data-ttu-id="8232e-261">例如，羅吉斯和線性迴歸模型需要 one-hot 編碼。</span><span class="sxs-lookup"><span data-stu-id="8232e-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="8232e-262">例如，有三個類別的特徵可展開成三個特徵資料行。</span><span class="sxs-lookup"><span data-stu-id="8232e-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="8232e-263">根據觀察值的分類，每個資料行包含 0 或 1。</span><span class="sxs-lookup"><span data-stu-id="8232e-263">Each column would contain 0 or 1 depending on the category of an observation.</span></span> <span data-ttu-id="8232e-264">MLlib 為 one-hot 編碼提供 [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) 函式。</span><span class="sxs-lookup"><span data-stu-id="8232e-264">MLlib provides the [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="8232e-265">此編碼器會將標籤索引資料行對應到二進位向量資料行，最多有一個單一值。</span><span class="sxs-lookup"><span data-stu-id="8232e-265">This encoder maps a column of label indices to a column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="8232e-266">使用這種編碼方式，可將預期數值特徵的演算法 (例如羅吉斯迴歸) 套用至分類特徵。</span><span class="sxs-lookup"><span data-stu-id="8232e-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied to categorical features.</span></span>

<span data-ttu-id="8232e-267">您在此只會轉換四個變數 (其為字元字串) 來顯示範例。</span><span class="sxs-lookup"><span data-stu-id="8232e-267">Here you transform only four variables to show examples, which are character strings.</span></span> <span data-ttu-id="8232e-268">您也可以將其他以數值表示的變數 (例如工作日) 編製索引為類別變數。</span><span class="sxs-lookup"><span data-stu-id="8232e-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="8232e-269">如需編製索引，請使用 `StringIndexer()`，如需進行 one-hot 編碼，請使用 MLlib 中的 `OneHotEncoder()` 函式。</span><span class="sxs-lookup"><span data-stu-id="8232e-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="8232e-270">以下是要索引及編碼分類功能的程式碼︰</span><span class="sxs-lookup"><span data-stu-id="8232e-270">Here is the code to index and encode categorical features:</span></span>

    # CREATE INDEXES AND ONE-HOT ENCODED VECTORS FOR SEVERAL CATEGORICAL FEATURES

    # RECORD THE START TIME
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

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="8232e-271">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-271">**Output:**</span></span>

<span data-ttu-id="8232e-272">執行資料格的時間︰4 秒。</span><span class="sxs-lookup"><span data-stu-id="8232e-272">Time to run the cell: 4 seconds.</span></span>

### <a name="sample-and-split-the-data-set-into-training-and-test-fractions"></a><span data-ttu-id="8232e-273">取樣並將資料集分割成訓練和測試部分</span><span class="sxs-lookup"><span data-stu-id="8232e-273">Sample and split the data set into training and test fractions</span></span>
<span data-ttu-id="8232e-274">此程式碼會建立隨機取樣資料 (此範例中為 25%)。</span><span class="sxs-lookup"><span data-stu-id="8232e-274">This code creates a random sampling of the data (25%, in this example).</span></span> <span data-ttu-id="8232e-275">雖然此範例因為資料集的大小而不需要取樣，但是本文會示範如何取樣，讓您了解需要時如何使用它來自行解決問題。</span><span class="sxs-lookup"><span data-stu-id="8232e-275">Although sampling is not required for this example due to the size of the data set, the article shows you how you can sample so that you know how to use it for your own problems when needed.</span></span> <span data-ttu-id="8232e-276">如果樣本數較大，這可以在訓練模型時節省大量時間。</span><span class="sxs-lookup"><span data-stu-id="8232e-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="8232e-277">接下來將樣本數分割成訓練部分 (此範例中為 75%) 和測試部分 (此範例中為 25%)，以便在分類和迴歸模型化中使用。</span><span class="sxs-lookup"><span data-stu-id="8232e-277">Next, split the sample into a training part (75%, in this example) and a testing part (25%, in this example) to use in classification and regression modeling.</span></span>

<span data-ttu-id="8232e-278">在 ("rand" 資料行中) 的每一列加入一個隨機數字 (介於 0 與 1 之間)，可用來在訓練期間選取交叉驗證摺疊數。</span><span class="sxs-lookup"><span data-stu-id="8232e-278">Add a random number (between 0 and 1) to each row (in a "rand" column) that can be used to select cross-validation folds during training.</span></span>

    # RECORD THE START TIME
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

    # SPLIT THE SAMPLED DATA FRAME INTO TRAIN AND TEST, WITH A RANDOM COLUMN ADDED FOR DOING CROSS-VALIDATION (SHOWN LATER)
    # INCLUDE A RANDOM COLUMN FOR CREATING CROSS-VALIDATION FOLDS
    val splits = encodedFinalSampled.randomSplit(Array(trainingFraction, testingFraction), seed = seed)
    val trainData = splits(0)
    val testData = splits(1)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="8232e-279">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-279">**Output:**</span></span>

<span data-ttu-id="8232e-280">執行資料格的時間︰2 秒。</span><span class="sxs-lookup"><span data-stu-id="8232e-280">Time to run the cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="8232e-281">指定訓練變數和特徵，然後建立已編製索引或已進行 one-hot 編碼的訓練和測試輸入標示點 RDD 或資料框架</span><span class="sxs-lookup"><span data-stu-id="8232e-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="8232e-282">本節包含的程式碼示範如何將分類的文字資料索引為標示點資料類型並加以編碼，您可以用來訓練及測試 MLlib 羅吉斯迴歸和其他分類模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-282">This section contains code that shows you how to index categorical text data as a labeled point data type, and encode it so you can use it to train and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="8232e-283">標示點物件是 RDD，其格式化成適合 MLlib 中大部分機器學習演算法所需的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="8232e-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="8232e-284">[標示點](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 是本機向量 (密集或疏鬆)，與標籤/回應相關聯。</span><span class="sxs-lookup"><span data-stu-id="8232e-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="8232e-285">在此程式碼中，您指定目標 (相依) 變數和要用來訓練模型的特徵。</span><span class="sxs-lookup"><span data-stu-id="8232e-285">In this code, you specify the target (dependent) variable and the features to use to train models.</span></span> <span data-ttu-id="8232e-286">然後，建立已編製索引或已進行 one-hot 編碼的訓練和測試輸入標示點 RDD 或資料框架。</span><span class="sxs-lookup"><span data-stu-id="8232e-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # MAP NAMES OF FEATURES AND TARGETS FOR CLASSIFICATION AND REGRESSION PROBLEMS
    val featuresIndOneHot = List("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))
    val featuresIndIndex = List("paymentIndex", "vendorIndex", "rateIndex", "TrafficTimeBinsIndex", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount").map(encodedFinalSampled.columns.indexOf(_))

    # SPECIFY THE TARGET FOR CLASSIFICATION ('tipped') AND REGRESSION ('tip_amount') PROBLEMS
    val targetIndBinary = List("tipped").map(encodedFinalSampled.columns.indexOf(_))
    val targetIndRegression = List("tip_amount").map(encodedFinalSampled.columns.indexOf(_))

    # CREATE INDEXED LABELED POINT RDD OBJECTS
    val indexedTRAINbinary = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTbinary = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndBinary(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTRAINreg = trainData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))
    val indexedTESTreg = testData.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)))

    # CREATE INDEXED DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val indexedTRAINbinaryDF = indexedTRAINbinary.toDF()
    val indexedTESTbinaryDF = indexedTESTbinary.toDF()
    val indexedTRAINregDF = indexedTRAINreg.toDF()
    val indexedTESTregDF = indexedTESTreg.toDF()

    # CREATE ONE-HOT ENCODED (VECTORIZED) DATA FRAMES THAT YOU CAN USE TO TRAIN BY USING SPARK ML FUNCTIONS
    val assemblerOneHot = new VectorAssembler().setInputCols(Array("paymentVec", "vendorVec", "rateVec", "TrafficTimeBinsVec", "pickup_hour", "weekday", "passenger_count", "trip_time_in_secs", "trip_distance", "fare_amount")).setOutputCol("features")
    val OneHotTRAIN = assemblerOneHot.transform(trainData)
    val OneHotTEST = assemblerOneHot.transform(testData)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="8232e-287">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-287">**Output:**</span></span>

<span data-ttu-id="8232e-288">執行資料格的時間︰4 秒。</span><span class="sxs-lookup"><span data-stu-id="8232e-288">Time to run the cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-to-use-as-inputs-for-machine-learning-models"></a><span data-ttu-id="8232e-289">自動分類及向量化特徵和目標，以做為機器學習模型的輸入</span><span class="sxs-lookup"><span data-stu-id="8232e-289">Automatically categorize and vectorize features and targets to use as inputs for machine learning models</span></span>
<span data-ttu-id="8232e-290">使用 Spark ML 分類目標和特徵，以便在以樹狀結構為基礎的模型化函式中使用。</span><span class="sxs-lookup"><span data-stu-id="8232e-290">Use Spark ML to categorize the target and features to use in tree-based modeling functions.</span></span> <span data-ttu-id="8232e-291">程式碼會完成兩項工作︰</span><span class="sxs-lookup"><span data-stu-id="8232e-291">The code completes two tasks:</span></span>

* <span data-ttu-id="8232e-292">使用臨界值 0.5，將值 0 或 1 指派給介於 0 和 1 之間的每個資料點，以建立分類的二進位目標。</span><span class="sxs-lookup"><span data-stu-id="8232e-292">Creates a binary target for classification by assigning a value of 0 or 1 to each data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="8232e-293">自動將功能分類。</span><span class="sxs-lookup"><span data-stu-id="8232e-293">Automatically categorizes features.</span></span> <span data-ttu-id="8232e-294">如果任何特徵的相異數值的數目小於 32，該特徵就會進行分類。</span><span class="sxs-lookup"><span data-stu-id="8232e-294">If the number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="8232e-295">以下是這兩項工作的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8232e-295">Here's the code for these two tasks.</span></span>

    # CATEGORIZE FEATURES AND BINARIZE THE TARGET FOR THE BINARY CLASSIFICATION PROBLEM

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

    # CATEGORIZE FEATURES FOR THE REGRESSION PROBLEM
    # CREATE PROPERLY INDEXED AND CATEGORIZED DATA FRAMES FOR TREE-BASED MODELS

    # TRAIN DATA
    val indexer = new VectorIndexer().setInputCol("features").setOutputCol("featuresCat").setMaxCategories(32)
    val indexerModel = indexer.fit(indexedTRAINregDF)
    val indexedTRAINwithCatFeat = indexerModel.transform(indexedTRAINregDF)

    # TEST DATA
    val indexerModel = indexer.fit(indexedTESTbinaryDF)
    val indexedTESTwithCatFeat = indexerModel.transform(indexedTESTregDF)



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="8232e-296">二進位分類模型：預測是否應支付小費</span><span class="sxs-lookup"><span data-stu-id="8232e-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="8232e-297">在本節中，您會建立三種類型的二進位分類模型來預測是否應支付小費：</span><span class="sxs-lookup"><span data-stu-id="8232e-297">In this section, you create three types of binary classification models to predict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="8232e-298">使用 Spark ML `LogisticRegression()` 函式的**羅吉斯迴歸模型**</span><span class="sxs-lookup"><span data-stu-id="8232e-298">A **logistic regression model** by using the Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="8232e-299">使用 Spark ML `RandomForestClassifier()` 函式的**隨機樹系分類模型**</span><span class="sxs-lookup"><span data-stu-id="8232e-299">A **random forest classification model** by using the Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="8232e-300">使用 MLlib `GradientBoostedTrees()` 函式的**梯度推進樹分類模型**</span><span class="sxs-lookup"><span data-stu-id="8232e-300">A **gradient boosting tree classification model** by using the MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="8232e-301">建立羅吉斯迴歸模型</span><span class="sxs-lookup"><span data-stu-id="8232e-301">Create a logistic regression model</span></span>
<span data-ttu-id="8232e-302">接著，使用 Spark ML `LogisticRegression()` 函式建立羅吉斯迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-302">Next, create a logistic regression model by using the Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="8232e-303">您會在一系列步驟中建立模型建置程式碼︰</span><span class="sxs-lookup"><span data-stu-id="8232e-303">You create the model building code in a series of steps:</span></span>

1. <span data-ttu-id="8232e-304">**訓練模型** 資料。</span><span class="sxs-lookup"><span data-stu-id="8232e-304">**Train the model** data with one parameter set.</span></span>
2. <span data-ttu-id="8232e-305">**評估模型** 。</span><span class="sxs-lookup"><span data-stu-id="8232e-305">**Evaluate the model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="8232e-306">**儲存模型** 供未來取用。</span><span class="sxs-lookup"><span data-stu-id="8232e-306">**Save the model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="8232e-307">**評分模型** 。</span><span class="sxs-lookup"><span data-stu-id="8232e-307">**Score the model** against test data.</span></span>
5. <span data-ttu-id="8232e-308">**繪製結果** 。</span><span class="sxs-lookup"><span data-stu-id="8232e-308">**Plot the results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="8232e-309">以下是這些程序的程式碼：</span><span class="sxs-lookup"><span data-stu-id="8232e-309">Here's the code for these procedures:</span></span>

    # CREATE A LOGISTIC REGRESSION MODEL
    val lr = new LogisticRegression().setLabelCol("tipped").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)
    val lrModel = lr.fit(OneHotTRAIN)

    # PREDICT ON THE TEST DATA SET
    val predictions = lrModel.transform(OneHotTEST)

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)

    # SAVE THE MODEL
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LogisticRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

<span data-ttu-id="8232e-310">載入、評分以及儲存結果。</span><span class="sxs-lookup"><span data-stu-id="8232e-310">Load, score, and save the results.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD THE SAVED MODEL AND SCORE THE TEST DATA SET
    val savedModel = org.apache.spark.ml.classification.LogisticRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON THE TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tipped","probability","rawPrediction")
    predictions.registerTempTable("testResults")

    # SELECT `BinaryClassificationEvaluator()` TO COMPUTE THE TEST ERROR
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("tipped").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC RESULTS
    println("ROC on test data = " + ROC)


<span data-ttu-id="8232e-311">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-311">**Output:**</span></span>

<span data-ttu-id="8232e-312">測試資料的 ROC = 0.9827381497557599</span><span class="sxs-lookup"><span data-stu-id="8232e-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="8232e-313">在本機 Pandas 資料框架上使用 Python 來繪製 ROC 曲線。</span><span class="sxs-lookup"><span data-stu-id="8232e-313">Use Python on local Pandas data frames to plot the ROC curve.</span></span>

    # QUERY THE RESULTS
    %%sql -q -o sqlResults
    SELECT tipped, probability from testResults


    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    %matplotlib inline
    from sklearn.metrics import roc_curve,auc

    sqlResults['probFloat'] = sqlResults.apply(lambda row: row['probability'].values()[0][1], axis=1)
    predictions_pddf = sqlResults[["tipped","probFloat"]]

    # PREDICT THE ROC CURVE
    # predictions_pddf = sqlResults.rename(columns={'_1': 'probability', 'tipped': 'label'})
    prob = predictions_pddf["probFloat"]
    fpr, tpr, thresholds = roc_curve(predictions_pddf['tipped'], prob, pos_label=1);
    roc_auc = auc(fpr, tpr)

    # PLOT THE ROC CURVE
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


<span data-ttu-id="8232e-314">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-314">**Output:**</span></span>

![小費或沒有小費的 ROC 曲線](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="8232e-316">建立隨機樹系分類模型</span><span class="sxs-lookup"><span data-stu-id="8232e-316">Create a random forest classification model</span></span>
<span data-ttu-id="8232e-317">接著，使用 SparkML `RandomForestClassifier()` 函式建立隨機樹系分類模型，然後對測試資料評估模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-317">Next, create a random forest classification model by using the Spark ML `RandomForestClassifier()` function, and then evaluate the model on test data.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE THE RANDOM FOREST CLASSIFIER MODEL
    val rf = new RandomForestClassifier().setLabelCol("labelBin").setFeaturesCol("featuresCat").setNumTrees(10).setSeed(1234)

    # FIT THE MODEL
    val rfModel = rf.fit(indexedTRAINwithCatFeatBinTarget)
    val predictions = rfModel.transform(indexedTESTwithCatFeatBinTarget)

    # EVALUATE THE MODEL
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(predictions)
    println("F1 score on test data: " + Test_f1Score);

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # CALCULATE BINARY CLASSIFICATION EVALUATION METRICS
    val evaluator = new BinaryClassificationEvaluator().setLabelCol("label").setRawPredictionCol("probability").setMetricName("areaUnderROC")
    val ROC = evaluator.evaluate(predictions)
    println("ROC on test data = " + ROC)


<span data-ttu-id="8232e-318">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-318">**Output:**</span></span>

<span data-ttu-id="8232e-319">測試資料的 ROC = 0.9847103571552683</span><span class="sxs-lookup"><span data-stu-id="8232e-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="8232e-320">建立 GBT 分類模型</span><span class="sxs-lookup"><span data-stu-id="8232e-320">Create a GBT classification model</span></span>
<span data-ttu-id="8232e-321">接著，使用 MLlib 的 `GradientBoostedTrees()` 函式建立 GBT 分類模型，然後對測試資料評估模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate the model on test data.</span></span>

    # TRAIN A GBT CLASSIFICATION MODEL BY USING MLLIB AND A LABELED POINT

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE GBT CLASSIFICATION MODEL
    val boostingStrategy = BoostingStrategy.defaultParams("Classification")
    boostingStrategy.numIterations = 20
    boostingStrategy.treeStrategy.numClasses = 2
    boostingStrategy.treeStrategy.maxDepth = 5
    boostingStrategy.treeStrategy.categoricalFeaturesInfo = Map[Int, Int]((0,2),(1,2),(2,6),(3,4))

    # TRAIN THE MODEL
    val gbtModel = GradientBoostedTrees.train(indexedTRAINbinary, boostingStrategy)

    # SAVE THE MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "GBT_Classification__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    gbtModel.save(sc, filename);

    # EVALUATE THE MODEL ON TEST INSTANCES AND THE COMPUTE TEST ERROR
    val labelAndPreds = indexedTESTbinary.map { point =>
      val prediction = gbtModel.predict(point.features)
      (point.label, prediction)
    }
    val testErr = labelAndPreds.filter(r => r._1 != r._2).count.toDouble / indexedTRAINbinary.count()
    //println("Learned classification GBT model:\n" + gbtModel.toDebugString)
    println("Test Error = " + testErr)

    # USE BINARY AND MULTICLASS METRICS TO EVALUATE THE MODEL ON THE TEST DATA
    val metrics = new MulticlassMetrics(labelAndPreds)
    println(s"Precision: ${metrics.precision}")
    println(s"Recall: ${metrics.recall}")
    println(s"F1 Score: ${metrics.fMeasure}")

    val metrics = new BinaryClassificationMetrics(labelAndPreds)
    println(s"Area under PR curve: ${metrics.areaUnderPR}")
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE ROC METRIC
    println(s"Area under ROC curve: ${metrics.areaUnderROC}")


<span data-ttu-id="8232e-322">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-322">**Output:**</span></span>

<span data-ttu-id="8232e-323">ROC 曲線夏的領域 = 0.9846895479241554</span><span class="sxs-lookup"><span data-stu-id="8232e-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="8232e-324">迴歸模型：預測小費金額</span><span class="sxs-lookup"><span data-stu-id="8232e-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="8232e-325">在本節中，您會建立兩種類型的迴歸模型來預測小費金額︰</span><span class="sxs-lookup"><span data-stu-id="8232e-325">In this section, you create two types of regression models to predict the tip amount:</span></span>

* <span data-ttu-id="8232e-326">使用 Spark ML `LinearRegression()` 函式的**正規化線性迴歸模型**。</span><span class="sxs-lookup"><span data-stu-id="8232e-326">A **regularized linear regression model** by using the Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="8232e-327">您將儲存模型，並對測試資料評估模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-327">You'll save the model and evaluate the model on test data.</span></span>
* <span data-ttu-id="8232e-328">使用 Spark ML `GBTRegressor()` 函式的**梯度推進樹迴歸模型**。</span><span class="sxs-lookup"><span data-stu-id="8232e-328">A **gradient-boosting tree regression model** by using the Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="8232e-329">建立正則化線性迴歸模型</span><span class="sxs-lookup"><span data-stu-id="8232e-329">Create a regularized linear regression model</span></span>
    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE A REGULARIZED LINEAR REGRESSION MODEL BY USING THE SPARK ML FUNCTION AND DATA FRAMES
    val lr = new LinearRegression().setLabelCol("tip_amount").setFeaturesCol("features").setMaxIter(10).setRegParam(0.3).setElasticNetParam(0.8)

    # FIT THE MODEL BY USING DATA FRAMES
    val lrModel = lr.fit(OneHotTRAIN)
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SUMMARIZE THE MODEL OVER THE TRAINING SET AND PRINT METRICS
    val trainingSummary = lrModel.summary
    println(s"numIterations: ${trainingSummary.totalIterations}")
    println(s"objectiveHistory: ${trainingSummary.objectiveHistory.toList}")
    trainingSummary.residuals.show()
    println(s"RMSE: ${trainingSummary.rootMeanSquaredError}")
    println(s"r2: ${trainingSummary.r2}")

    # SAVE THE MODEL IN AZURE BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "LinearRegression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    lrModel.save(filename);

    # PRINT THE COEFFICIENTS
    println(s"Coefficients: ${lrModel.coefficients} Intercept: ${lrModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = lrModel.transform(OneHotTEST)

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="8232e-330">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-330">**Output:**</span></span>

<span data-ttu-id="8232e-331">執行資料格的時間︰13 秒。</span><span class="sxs-lookup"><span data-stu-id="8232e-331">Time to run the cell: 13 seconds.</span></span>

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM BLOB STORAGE AND SCORE A TEST DATA SET

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # LOAD A SAVED LINEAR REGRESSION MODEL FROM AZURE BLOB STORAGE
    val savedModel = org.apache.spark.ml.regression.LinearRegressionModel.load(filename)
    println(s"Coefficients: ${savedModel.coefficients} Intercept: ${savedModel.intercept}")

    # SCORE THE MODEL ON TEST DATA
    val predictions = savedModel.transform(OneHotTEST).select("tip_amount","prediction")
    predictions.registerTempTable("testResults")

    # EVALUATE THE MODEL ON TEST DATA
    val evaluator = new RegressionEvaluator().setLabelCol("tip_amount").setPredictionCol("prediction").setMetricName("r2")
    val r2 = evaluator.evaluate(predictions)
    println("R-sqr on test data = " + r2)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("R-sqr on test data = " + r2)


<span data-ttu-id="8232e-332">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-332">**Output:**</span></span>

<span data-ttu-id="8232e-333">測試資料的 R-sqr = 0.5960320470835743</span><span class="sxs-lookup"><span data-stu-id="8232e-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="8232e-334">接著，查詢測試結果做為資料框架，並使用 AutoVizWidget 和 matplotlib 將其視覺化呈現。</span><span class="sxs-lookup"><span data-stu-id="8232e-334">Next, query the test results as a data frame and use AutoVizWidget and matplotlib to visualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER
    %%local

    # USE THE JUPYTER AUTO-PLOTTING FEATURE TO CREATE INTERACTIVE FIGURES
    # CLICK THE TYPE OF PLOT TO GENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="8232e-335">此程式碼從查詢輸出中建立本機資料框架，以及繪製資料。</span><span class="sxs-lookup"><span data-stu-id="8232e-335">The code creates a local data frame from the query output and plots the data.</span></span> <span data-ttu-id="8232e-336">`%%local` magic 建立本機資料框架 `sqlResults`，您可以用來搭配 matplotlib 進行繪製。</span><span class="sxs-lookup"><span data-stu-id="8232e-336">The `%%local` magic creates a local data frame, `sqlResults`, which you can use to plot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="8232e-337">本文中會多次使用此 Spark magic。</span><span class="sxs-lookup"><span data-stu-id="8232e-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="8232e-338">如果資料總量很大，您應該取樣以建立可容納於本機記憶體的資料框架。</span><span class="sxs-lookup"><span data-stu-id="8232e-338">If the amount of data is large, you should sample to create a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="8232e-339">使用 Python matplotlib 建立繪圖。</span><span class="sxs-lookup"><span data-stu-id="8232e-339">Create plots by using Python matplotlib.</span></span>

    # RUN THE CODE LOCALLY ON THE JUPYTER SERVER AND IMPORT LIBRARIES
    %%local
    sqlResults
    %matplotlib inline
    import numpy as np

    # PLOT THE RESULTS
    ax = sqlResults.plot(kind='scatter', figsize = (6,6), x='tip_amount', y='prediction', color='blue', alpha = 0.25, label='Actual vs. predicted');
    fit = np.polyfit(sqlResults['tip_amount'], sqlResults['prediction'], deg=1)
    ax.set_title('Actual vs. Predicted Tip Amounts ($)')
    ax.set_xlabel("Actual")
    ax.set_ylabel("Predicted")
    #ax.plot(sqlResults['tip_amount'], fit[0] * sqlResults['prediction'] + fit[1], color='magenta')
    plt.axis([-1, 15, -1, 8])
    plt.show(ax)

<span data-ttu-id="8232e-340">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-340">**Output:**</span></span>

![小費金額︰實際與預測](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="8232e-342">建立 GBT 迴歸模型</span><span class="sxs-lookup"><span data-stu-id="8232e-342">Create a GBT regression model</span></span>
<span data-ttu-id="8232e-343">使用 SparkML `GBTRegressor()` 函式建立 GBT 迴歸模型，然後對測試資料評估模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-343">Create a GBT regression model by using the Spark ML `GBTRegressor()` function, and then evaluate the model on test data.</span></span>

<span data-ttu-id="8232e-344">[梯度推進樹](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) 集合了所有決策樹。</span><span class="sxs-lookup"><span data-stu-id="8232e-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="8232e-345">GBT 反覆地訓練決策樹以盡可能降低遺失函式。</span><span class="sxs-lookup"><span data-stu-id="8232e-345">GBTs train decision trees iteratively to minimize a loss function.</span></span> <span data-ttu-id="8232e-346">您可以使用 GBT 進行迴歸和分類。</span><span class="sxs-lookup"><span data-stu-id="8232e-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="8232e-347">GBT 可以處理分類特徵、不需要調整特徵，而且可以擷取非線性和特徵互動。</span><span class="sxs-lookup"><span data-stu-id="8232e-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="8232e-348">您也可以在多類別分類設定中使用 GBT。</span><span class="sxs-lookup"><span data-stu-id="8232e-348">You also can use them in a multiclass-classification setting.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # TRAIN A GBT REGRESSION MODEL
    val gbt = new GBTRegressor().setLabelCol("label").setFeaturesCol("featuresCat").setMaxIter(10)
    val gbtModel = gbt.fit(indexedTRAINwithCatFeat)

    # MAKE PREDICTIONS
    val predictions = gbtModel.transform(indexedTESTwithCatFeat)

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(predictions)


    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    # PRINT THE RESULTS
    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="8232e-349">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-349">**Output:**</span></span>

<span data-ttu-id="8232e-350">測試 R-sqr：0.7655383534596654</span><span class="sxs-lookup"><span data-stu-id="8232e-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="8232e-351">可供最佳化的進階模型化公用程式</span><span class="sxs-lookup"><span data-stu-id="8232e-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="8232e-352">在本節中，您將使用開發人員經常使用的機器學習公用程式來最佳化模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="8232e-353">具體來說，您可以使用參數掃掠和交叉驗證，以三種不同的方式來最佳化機器學習模型︰</span><span class="sxs-lookup"><span data-stu-id="8232e-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="8232e-354">將資料分為訓練集和驗證集，對訓練集使用超參數掃掠來最佳化模型，然後對驗證集進行評估 (線性迴歸)</span><span class="sxs-lookup"><span data-stu-id="8232e-354">Split the data into train and validation sets, optimize the model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="8232e-355">利用 Spark ML 的 CrossValidator 函式 (二進位分類)，使用交叉驗證和超參數掃掠來最佳化模型</span><span class="sxs-lookup"><span data-stu-id="8232e-355">Optimize the model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="8232e-356">使用自訂交叉驗證和參數掃掠程式碼，利用任何機器學習函式和參數集來最佳化模型 (線性迴歸)</span><span class="sxs-lookup"><span data-stu-id="8232e-356">Optimize the model by using custom cross-validation and parameter-sweeping code to use any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="8232e-357">**交叉驗證** 是一種技術，評估已對一組已知資料訓練過的模型將能多廣泛地預測尚未對其訓練過的資料集特徵。</span><span class="sxs-lookup"><span data-stu-id="8232e-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize to predict the features of data sets on which it has not been trained.</span></span> <span data-ttu-id="8232e-358">這種技術背後的基本概念是模型已針對已知資料的資料集訓練，然後針對獨立的資料集測試其預測的精確度。</span><span class="sxs-lookup"><span data-stu-id="8232e-358">The general idea behind this technique is that a model is trained on a data set of known data, and then the accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="8232e-359">常見的實作是將資料集分割成 *k*個摺疊，然後以循環配置資源方式對除了一個摺疊的所有摺疊訓練模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-359">A common implementation is to divide a data set into *k*-folds, and then train the model in a round-robin fashion on all but one of the folds.</span></span>

<span data-ttu-id="8232e-360">**超參數最佳化** 的問題是要選擇一組超參數來學習演算法，目標通常是要最佳化獨立資料集上演算法效能的測量。</span><span class="sxs-lookup"><span data-stu-id="8232e-360">**Hyper-parameter optimization** is the problem of choosing a set of hyper-parameters for a learning algorithm, usually with the goal of optimizing a measure of the algorithm's performance on an independent data set.</span></span> <span data-ttu-id="8232e-361">超參數是您在模型訓練程序之外必須指定的值。</span><span class="sxs-lookup"><span data-stu-id="8232e-361">A hyper-parameter is a value that you must specify outside the model training procedure.</span></span> <span data-ttu-id="8232e-362">對於超參數值的假設可能會影響模型的彈性和精確度。</span><span class="sxs-lookup"><span data-stu-id="8232e-362">Assumptions about hyper-parameter values can affect the flexibility and accuracy of the model.</span></span> <span data-ttu-id="8232e-363">決策樹有超參數，例如想要的樹深度和葉數目等。</span><span class="sxs-lookup"><span data-stu-id="8232e-363">Decision trees have hyper-parameters, for example, such as the desired depth and number of leaves in the tree.</span></span> <span data-ttu-id="8232e-364">您必須為支援向量機器 (SVM) 設定分類誤判損失詞彙。</span><span class="sxs-lookup"><span data-stu-id="8232e-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="8232e-365">執行超參數最佳化一個常見的方法是使用格線搜尋，也稱為 **參數掃掠**。</span><span class="sxs-lookup"><span data-stu-id="8232e-365">A common way to perform hyper-parameter optimization is to use a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="8232e-366">在格線搜尋中，會對某個學習演算法的超參數空間指定子集的所有值執行詳盡搜尋。</span><span class="sxs-lookup"><span data-stu-id="8232e-366">In a grid search, an exhaustive search is performed through the values of a specified subset of the hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="8232e-367">交叉驗證可以提供效能度量，挑出格線搜尋演算法所產生的最佳結果。</span><span class="sxs-lookup"><span data-stu-id="8232e-367">Cross-validation can supply a performance metric to sort out the optimal results produced by the grid search algorithm.</span></span> <span data-ttu-id="8232e-368">如果您使用交叉驗證超參數掃掠，可以協助限制例如將模型過度擬合到訓練資料的問題。</span><span class="sxs-lookup"><span data-stu-id="8232e-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model to training data.</span></span> <span data-ttu-id="8232e-369">如此一來，模型會保留空間來套用到擷取訓練資料的一般資料集。</span><span class="sxs-lookup"><span data-stu-id="8232e-369">This way, the model retains the capacity to apply to the general set of data from which the training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="8232e-370">利用超參數掃掠來最佳化線性迴歸模型</span><span class="sxs-lookup"><span data-stu-id="8232e-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="8232e-371">接著，將資料分為訓練集和驗證集，對訓練集使用超參數掃掠來最佳化模型，然後對驗證集進行評估 (線性迴歸)。</span><span class="sxs-lookup"><span data-stu-id="8232e-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set to optimize the model, and evaluate on a validation set (linear regression).</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # RENAME `tip_amount` AS A LABEL
    val OneHotTRAINLabeled = OneHotTRAIN.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    val OneHotTESTLabeled = OneHotTEST.select("tip_amount","features").withColumnRenamed(existingName="tip_amount",newName="label")
    OneHotTRAINLabeled.cache()
    OneHotTESTLabeled.cache()

    # DEFINE THE ESTIMATOR FUNCTION: `THE LinearRegression()` FUNCTION
    val lr = new LinearRegression().setLabelCol("label").setFeaturesCol("features").setMaxIter(10)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(lr.regParam, Array(0.1, 0.01, 0.001)).addGrid(lr.fitIntercept).addGrid(lr.elasticNetParam, Array(0.1, 0.5, 0.9)).build()

    # DEFINE THE PIPELINE WITH A TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET), AND THEN THE SPECIFY ESTIMATOR, EVALUATOR, AND PARAMETER GRID
    val trainPct = 0.75
    val trainValidationSplit = new TrainValidationSplit().setEstimator(lr).setEvaluator(new RegressionEvaluator).setEstimatorParamMaps(paramGrid).setTrainRatio(trainPct)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = trainValidationSplit.fit(OneHotTRAINLabeled)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(OneHotTESTLabeled).select("label", "prediction")

    # COMPUTE TEST SET R2
    val evaluator = new RegressionEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("r2")
    val Test_R2 = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");

    println("Test R-sqr is: " + Test_R2);


<span data-ttu-id="8232e-372">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-372">**Output:**</span></span>

<span data-ttu-id="8232e-373">測試 R-sqr：0.6226484708501209</span><span class="sxs-lookup"><span data-stu-id="8232e-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-the-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="8232e-374">使用交叉驗證和超參數掃掠來最佳化二進位分類模型</span><span class="sxs-lookup"><span data-stu-id="8232e-374">Optimize the binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="8232e-375">本節示範如何使用交叉驗證和超參數掃掠來最佳化二進位分類模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-375">This section shows you how to optimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="8232e-376">這會使用 Spark ML `CrossValidator` 函式。</span><span class="sxs-lookup"><span data-stu-id="8232e-376">This uses the Spark ML `CrossValidator` function.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # CREATE DATA FRAMES WITH PROPERLY LABELED COLUMNS TO USE WITH THE TRAIN AND TEST SPLIT
    val indexedTRAINwithCatFeatBinTargetRF = indexedTRAINwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    val indexedTESTwithCatFeatBinTargetRF = indexedTESTwithCatFeatBinTarget.select("labelBin","featuresCat").withColumnRenamed(existingName="labelBin",newName="label").withColumnRenamed(existingName="featuresCat",newName="features")
    indexedTRAINwithCatFeatBinTargetRF.cache()
    indexedTESTwithCatFeatBinTargetRF.cache()

    # DEFINE THE ESTIMATOR FUNCTION
    val rf = new RandomForestClassifier().setLabelCol("label").setFeaturesCol("features").setImpurity("gini").setSeed(1234).setFeatureSubsetStrategy("auto").setMaxBins(32)

    # DEFINE THE PARAMETER GRID
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(4,8)).addGrid(rf.numTrees, Array(5,10)).addGrid(rf.minInstancesPerNode, Array(100,300)).build()

    # SPECIFY THE NUMBER OF FOLDS
    val numFolds = 3

    # DEFINE THE TRAIN/TEST VALIDATION SPLIT (75% IN THE TRAINING SET)
    val CrossValidator = new CrossValidator().setEstimator(rf).setEvaluator(new BinaryClassificationEvaluator).setEstimatorParamMaps(paramGrid).setNumFolds(numFolds)

    # RUN THE TRAIN VALIDATION SPLIT AND CHOOSE THE BEST SET OF PARAMETERS
    val model = CrossValidator.fit(indexedTRAINwithCatFeatBinTargetRF)

    # MAKE PREDICTIONS ON THE TEST DATA BY USING THE MODEL WITH THE COMBINATION OF PARAMETERS THAT PERFORMS THE BEST
    val testResults = model.transform(indexedTESTwithCatFeatBinTargetRF).select("label", "prediction")

    # COMPUTE THE TEST F1 SCORE
    val evaluator = new MulticlassClassificationEvaluator().setLabelCol("label").setPredictionCol("prediction").setMetricName("f1")
    val Test_f1Score = evaluator.evaluate(testResults)

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


<span data-ttu-id="8232e-377">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-377">**Output:**</span></span>

<span data-ttu-id="8232e-378">執行資料格的時間︰33 秒。</span><span class="sxs-lookup"><span data-stu-id="8232e-378">Time to run the cell: 33 seconds.</span></span>

### <a name="optimize-the-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="8232e-379">使用自訂交叉驗證和參數掃掠程式碼來最佳化線性迴歸模型</span><span class="sxs-lookup"><span data-stu-id="8232e-379">Optimize the linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="8232e-380">接著，使用自訂程式碼來最佳化模型，並使用最精確的準則來找出最佳的模型參數。</span><span class="sxs-lookup"><span data-stu-id="8232e-380">Next, optimize the model by using custom code, and identify the best model parameters by using the criterion of highest accuracy.</span></span> <span data-ttu-id="8232e-381">然後，建立最終模型、對測試資料評估模型，以及在 Blob 儲存體中儲存模型。</span><span class="sxs-lookup"><span data-stu-id="8232e-381">Then, create the final model, evaluate the model on test data, and save the model in Blob storage.</span></span> <span data-ttu-id="8232e-382">最後，載入模型、對測試資料進行評分，以及評估精確度。</span><span class="sxs-lookup"><span data-stu-id="8232e-382">Finally, load the model, score test data, and evaluate accuracy.</span></span>

    # RECORD THE START TIME
    val starttime = Calendar.getInstance().getTime()

    # DEFINE THE PARAMETER GRID AND THE NUMBER OF FOLDS
    val paramGrid = new ParamGridBuilder().addGrid(rf.maxDepth, Array(5,10)).addGrid(rf.numTrees, Array(10,25,50)).build()

    val nFolds = 3
    val numModels = paramGrid.size
    val numParamsinGrid = 2

    # SPECIFY THE NUMBER OF CATEGORIES FOR CATEGORICAL VARIABLES
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


    # LOOP THROUGH K-FOLDS AND THE PARAMETER GRID TO GET AND IDENTIFY THE BEST PARAMETER SET BY LEVEL OF ACCURACY
    for (i <- 0 to (nFolds-1)) {
        validateLB = i * h
        validateUB = (i + 1) * h
        val validationCV = trainData.filter($"rand" >= validateLB  && $"rand" < validateUB)
        val trainCV = trainData.filter($"rand" < validateLB  || $"rand" >= validateUB)
        val validationLabPt = validationCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        val trainCVLabPt = trainCV.rdd.map(r => LabeledPoint(r.getDouble(targetIndRegression(0).toInt), Vectors.dense(featuresIndIndex.map(r.getDouble(_)).toArray)));
        validationLabPt.cache()
        trainCVLabPt.cache()

        for (nParamSets <- 0 to (numModels-1)) {
            for (nParams <- 0 to (numParamsinGrid-1)) {
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

    # GET THE BEST PARAMETERS FROM A CROSS-VALIDATION AND PARAMETER SWEEP
    var best_maxDepth = -1
    var best_numTrees = -1
    for (nParams <- 0 to (numParamsinGrid-1)) {
        param = paramGrid(minRMSEindex).toSeq(nParams).param.toString.split("__")(1)
        paramval = paramGrid(minRMSEindex).toSeq(nParams).value.toString.toInt
        if (param == "maxDepth") {best_maxDepth = paramval}
        if (param == "numTrees") {best_numTrees = paramval}
    }

    # CREATE THE BEST MODEL WITH THE BEST PARAMETERS AND A FULL TRAINING DATA SET
    val best_rfModel = RandomForest.trainRegressor(indexedTRAINreg, categoricalFeaturesInfo=categoricalFeaturesInfo,
                                                      numTrees=best_numTrees, maxDepth=best_maxDepth,
                                                      featureSubsetStrategy="auto",impurity="variance", maxBins=32)

    # SAVE THE BEST RANDOM FOREST MODEL IN BLOB STORAGE
    val datestamp = Calendar.getInstance().getTime().toString.replaceAll(" ", ".").replaceAll(":", "_");
    val modelName = "BestCV_RF_Regression__"
    val filename = modelDir.concat(modelName).concat(datestamp)
    best_rfModel.save(sc, filename);

    # PREDICT ON THE TRAINING SET WITH THE BEST MODEL AND THEN EVALUATE
    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = best_rfModel.predict(point.features)
                                            ( prediction, point.label )
                                           }

    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2

    # GET THE TIME TO RUN THE CELL
    val endtime = Calendar.getInstance().getTime()
    val elapsedtime =  ((endtime.getTime() - starttime.getTime())/1000).toString;
    println("Time taken to run the above cell: " + elapsedtime + " seconds.");


    # LOAD THE MODEL
    val savedRFModel = RandomForestModel.load(sc, filename)

    val labelAndPreds = indexedTESTreg.map { point =>
                                            val prediction = savedRFModel.predict(point.features)
                                            ( prediction, point.label )
                                           }
    # TEST THE MODEL
    val test_rmse = new RegressionMetrics(labelAndPreds).rootMeanSquaredError
    val test_rsqr = new RegressionMetrics(labelAndPreds).r2


<span data-ttu-id="8232e-383">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="8232e-383">**Output:**</span></span>

<span data-ttu-id="8232e-384">執行資料格的時間︰61 秒。</span><span class="sxs-lookup"><span data-stu-id="8232e-384">Time to run the cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="8232e-385">透過 Scala 自動取用 Spark 建置的機器學習模型</span><span class="sxs-lookup"><span data-stu-id="8232e-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="8232e-386">如需能引導您完成在 Azure 中構成資料科學程序之工作的主題概觀，請參閱 [Team Data Science Process](http://aka.ms/datascienceprocess)。</span><span class="sxs-lookup"><span data-stu-id="8232e-386">For an overview of topics that walk you through the tasks that comprise the Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="8232e-387">[Team Data Science Process 逐步解說](data-science-process-walkthroughs.md) 說明的其他端對端逐步解說示範 Team Data Science Process 針對特定案例的步驟。</span><span class="sxs-lookup"><span data-stu-id="8232e-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate the steps in the Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="8232e-388">這些逐步解說也示範如何將雲端和內部部署工具與服務組合成工作流程或管線，以建立智慧型應用程式。</span><span class="sxs-lookup"><span data-stu-id="8232e-388">The walkthroughs also illustrate how to combine cloud and on-premises tools and services into a workflow or pipeline to create an intelligent application.</span></span>

<span data-ttu-id="8232e-389">[評分 Spark 建置的機器學習模型](machine-learning-data-science-spark-model-consumption.md) 示範如何利用 Spark 內建並儲存於 Azure Blob 儲存體的機器學習模型，使用 Scala 程式碼來自動載入及評分新資料集。</span><span class="sxs-lookup"><span data-stu-id="8232e-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how to use Scala code to automatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="8232e-390">您可以遵循此處提供的指示，只要將本文中的 Python 程式碼取代為 Scala 程式碼，即可自動取用。</span><span class="sxs-lookup"><span data-stu-id="8232e-390">You can follow the instructions provided there, and simply replace the Python code with Scala code in this article for automated consumption.</span></span>

