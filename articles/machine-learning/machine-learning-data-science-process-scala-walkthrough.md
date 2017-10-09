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
# <a name="data-science-using-scala-and-spark-on-azure"></a><span data-ttu-id="53801-103">在 Azure 上使用 Scala 與 Spark 的資料科學</span><span class="sxs-lookup"><span data-stu-id="53801-103">Data Science using Scala and Spark on Azure</span></span>
<span data-ttu-id="53801-104">本文示範 toouse Scala hello Spark 可擴充 MLlib 與 Spark ML 受監督的機器學習工作的 Azure HDInsight Spark 叢集上的封裝。</span><span class="sxs-lookup"><span data-stu-id="53801-104">This article shows you how toouse Scala for supervised machine learning tasks with hello Spark scalable MLlib and Spark ML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="53801-105">它會引導您完成 hello 工作構成 hello[資料科學程序](http://aka.ms/datascienceprocess)： 擷取資料並探索、 視覺效果、 功能工程、 模型和模型耗用量。</span><span class="sxs-lookup"><span data-stu-id="53801-105">It walks you through hello tasks that constitute hello [Data Science process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="53801-106">hello 文件中的 hello 模型包括羅吉斯和線性迴歸、 隨機樹系和漸層促進式樹狀結構 (GBTs)、 tootwo 常見受監督的機器學習工作此外：</span><span class="sxs-lookup"><span data-stu-id="53801-106">hello models in hello article include logistic and linear regression, random forests, and gradient-boosted trees (GBTs), in addition tootwo common supervised machine learning tasks:</span></span>

* <span data-ttu-id="53801-107">迴歸問題： 計程車路線的 hello 提示 amount （$） 的預測</span><span class="sxs-lookup"><span data-stu-id="53801-107">Regression problem: Prediction of hello tip amount ($) for a taxi trip</span></span>
* <span data-ttu-id="53801-108">二進位分類︰計程車車程的小費或不給小費 (1/0) 預測</span><span class="sxs-lookup"><span data-stu-id="53801-108">Binary classification: Prediction of tip or no tip (1/0) for a taxi trip</span></span>

<span data-ttu-id="53801-109">hello 模型程序需要定型和測試資料集和相關的精確度標準的評估。</span><span class="sxs-lookup"><span data-stu-id="53801-109">hello modeling process requires training and evaluation on a test data set and relevant accuracy metrics.</span></span> <span data-ttu-id="53801-110">在本文中，您可以了解如何 toostore 這些模型在 Azure Blob 儲存體以及 tooscore 並評估其預測的效能。</span><span class="sxs-lookup"><span data-stu-id="53801-110">In this article, you can learn how toostore these models in Azure Blob storage and how tooscore and evaluate their predictive performance.</span></span> <span data-ttu-id="53801-111">本文亦涵蓋 hello 更進階的 toooptimize 模型使用交叉驗證和超參數牽涉的如何主題。</span><span class="sxs-lookup"><span data-stu-id="53801-111">This article also covers hello more advanced topics of how toooptimize models by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="53801-112">使用 hello 資料是範例 hello 2013 NYC 計程車行程及價位資料集可在 GitHub 上取得。</span><span class="sxs-lookup"><span data-stu-id="53801-112">hello data used is a sample of hello 2013 NYC taxi trip and fare data set available on GitHub.</span></span>

<span data-ttu-id="53801-113">[Scala](http://www.scala-lang.org/)，hello Java 虛擬機器，為基礎的語言整合物件導向與功能性語言概念。</span><span class="sxs-lookup"><span data-stu-id="53801-113">[Scala](http://www.scala-lang.org/), a language based on hello Java virtual machine, integrates object-oriented and functional language concepts.</span></span> <span data-ttu-id="53801-114">它是可擴充的語言，是很適合的 toodistributed hello 雲端中的處理，而 Azure Spark 叢集上執行。</span><span class="sxs-lookup"><span data-stu-id="53801-114">It's a scalable language that is well suited toodistributed processing in hello cloud, and runs on Azure Spark clusters.</span></span>

<span data-ttu-id="53801-115">[Spark](http://spark.apache.org/)一種開放原始碼平行處理架構支援記憶體中處理 tooboost hello 巨量資料分析應用程式效能。</span><span class="sxs-lookup"><span data-stu-id="53801-115">[Spark](http://spark.apache.org/) is an open-source parallel-processing framework that supports in-memory processing tooboost hello performance of big data analytics applications.</span></span> <span data-ttu-id="53801-116">hello Spark 處理引擎內建的速度、 容易使用，且複雜的分析。</span><span class="sxs-lookup"><span data-stu-id="53801-116">hello Spark processing engine is built for speed, ease of use, and sophisticated analytics.</span></span> <span data-ttu-id="53801-117">Spark 的記憶體內分散式計算功能，使其成為機器學習和圖表計算中反覆演算法的絕佳選擇。</span><span class="sxs-lookup"><span data-stu-id="53801-117">Spark's in-memory distributed computation capabilities make it a good choice for iterative algorithms in machine learning and graph computations.</span></span> <span data-ttu-id="53801-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html)套件提供一組一致的框架，可協助您建立及微調實際的機器學習管線中的資料之上建立高階應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="53801-118">hello [spark.ml](http://spark.apache.org/docs/latest/ml-guide.html) package provides a uniform set of high-level APIs built on top of data frames that can help you create and tune practical machine learning pipelines.</span></span> <span data-ttu-id="53801-119">[MLlib](http://spark.apache.org/mllib/)是 Spark 的可調整的機器學習文件庫，它將模型化功能 toothis 分散式的環境。</span><span class="sxs-lookup"><span data-stu-id="53801-119">[MLlib](http://spark.apache.org/mllib/) is Spark's scalable machine learning library, which brings modeling capabilities toothis distributed environment.</span></span>

<span data-ttu-id="53801-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md)是 hello Azure 託管服務的開放原始碼 Spark。</span><span class="sxs-lookup"><span data-stu-id="53801-120">[HDInsight Spark](../hdinsight/hdinsight-apache-spark-overview.md) is hello Azure-hosted offering of open-source Spark.</span></span> <span data-ttu-id="53801-121">它也包含支援 Jupyter Scala 筆記本 hello Spark 叢集，並可以執行的 Spark SQL 的互動式查詢 tootransform，篩選和 Azure Blob 儲存體中的資料視覺化。</span><span class="sxs-lookup"><span data-stu-id="53801-121">It also includes support for Jupyter Scala notebooks on hello Spark cluster, and can run Spark SQL interactive queries tootransform, filter, and visualize data stored in Azure Blob storage.</span></span> <span data-ttu-id="53801-122">hello Scala 的程式碼片段中這篇文章提供 hello 解決方案，並顯示 hello 相關繪圖 toovisualize hello 資料執行中 Jupyter 筆記本 hello Spark 叢集上安裝。</span><span class="sxs-lookup"><span data-stu-id="53801-122">hello Scala code snippets in this article that provide hello solutions and show hello relevant plots toovisualize hello data run in Jupyter notebooks installed on hello Spark clusters.</span></span> <span data-ttu-id="53801-123">這些主題中的 hello 模型步驟的程式碼您 tootrain，如何評估、 儲存和取用每一個輸入模型的該節目。</span><span class="sxs-lookup"><span data-stu-id="53801-123">hello modeling steps in these topics have code that shows you how tootrain, evaluate, save, and consume each type of model.</span></span>

<span data-ttu-id="53801-124">hello 安裝步驟與本文章中的程式碼適用於 Azure HDInsight 3.4 Spark 1.6。</span><span class="sxs-lookup"><span data-stu-id="53801-124">hello setup steps and code in this article are for Azure HDInsight 3.4 Spark 1.6.</span></span> <span data-ttu-id="53801-125">不過，hello hello 和本文中的程式碼[Scala Jupyter 筆記本](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb)泛型以及應該使用任何 Spark 叢集上。</span><span class="sxs-lookup"><span data-stu-id="53801-125">However, hello code in this article and in hello [Scala Jupyter Notebook](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration%20Modeling%20and%20Scoring%20using%20Scala.ipynb) are generic and should work on any Spark cluster.</span></span> <span data-ttu-id="53801-126">hello 叢集設定，而且管理步驟可能稍有不同如果您不想要使用 HDInsight Spark 顯示本文章中。</span><span class="sxs-lookup"><span data-stu-id="53801-126">hello cluster setup and management steps might be slightly different from what is shown in this article if you are not using HDInsight Spark.</span></span>

> [!NOTE]
> <span data-ttu-id="53801-127">顯示 toouse Python，而不是 Scala toocomplete 端對端資料科學處理程序的工作的主題，請參閱[使用 Azure HDInsight 上的 Spark 資料科學](machine-learning-data-science-spark-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="53801-127">For a topic that shows you how toouse Python rather than Scala toocomplete tasks for an end-to-end Data Science process, see [Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="53801-128">必要條件</span><span class="sxs-lookup"><span data-stu-id="53801-128">Prerequisites</span></span>
* <span data-ttu-id="53801-129">您必須擁有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="53801-129">You must have an Azure subscription.</span></span> <span data-ttu-id="53801-130">如果還沒有， [請取得 Azure 免費試用](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="53801-130">If you do not already have one, [get an Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="53801-131">您需要下列程序的 Azure HDInsight 3.4 Spark 1.6 叢集 toocomplete hello。</span><span class="sxs-lookup"><span data-stu-id="53801-131">You need an Azure HDInsight 3.4 Spark 1.6 cluster toocomplete hello following procedures.</span></span> <span data-ttu-id="53801-132">toocreate 叢集中，請參閱中的 hello 指示[快速入門： 建立 Azure HDInsight 上的 Apache Spark](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md)。</span><span class="sxs-lookup"><span data-stu-id="53801-132">toocreate a cluster, see hello instructions in [Get started: Create Apache Spark on Azure HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-spark-sql.md).</span></span> <span data-ttu-id="53801-133">Hello 叢集類型與版本設定 hello**選取叢集類型**功能表。</span><span class="sxs-lookup"><span data-stu-id="53801-133">Set hello cluster type and version on hello **Select Cluster Type** menu.</span></span>

![HDInsight 叢集類型組態](./media/machine-learning-data-science-process-scala-walkthrough/spark-cluster-on-portal.png)

> [!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]
> 
> 

<span data-ttu-id="53801-135">如需說明的 hello NYC 計程車路線資料以及 tooexecute 來自 Jupyter 筆記本 hello Spark 叢集上的程式碼的相關指示，請參閱 hello 相關章節[概觀的資料科學使用 Azure HDInsight 上的 Spark](machine-learning-data-science-spark-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="53801-135">For a description of hello NYC taxi trip data and instructions on how tooexecute code from a Jupyter notebook on hello Spark cluster, see hello relevant sections in [Overview of Data Science using Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md).</span></span>  

## <a name="execute-scala-code-from-a-jupyter-notebook-on-hello-spark-cluster"></a><span data-ttu-id="53801-136">從 Jupyter 筆記本 hello Spark 叢集上執行 Scala 程式碼</span><span class="sxs-lookup"><span data-stu-id="53801-136">Execute Scala code from a Jupyter notebook on hello Spark cluster</span></span>
<span data-ttu-id="53801-137">您可以啟動 Jupyter 筆記本從 hello Azure 入口網站。</span><span class="sxs-lookup"><span data-stu-id="53801-137">You can launch a Jupyter notebook from hello Azure portal.</span></span> <span data-ttu-id="53801-138">尋找在您的儀表板，hello Spark 叢集，並按一下它 tooenter hello 管理頁面，為您的叢集。</span><span class="sxs-lookup"><span data-stu-id="53801-138">Find hello Spark cluster on your dashboard, and then click it tooenter hello management page for your cluster.</span></span> <span data-ttu-id="53801-139">接下來，按一下**叢集儀表板**，然後按一下 **Jupyter 筆記本**tooopen hello 筆記本 hello Spark 叢集相關聯。</span><span class="sxs-lookup"><span data-stu-id="53801-139">Next, click **Cluster Dashboards**, and then click **Jupyter Notebook** tooopen hello notebook associated with hello Spark cluster.</span></span>

![叢集儀表板和 Jupyter Notebook](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-on-portal.png)

<span data-ttu-id="53801-141">您也可以在 https://&lt;clustername&gt;.azurehdinsight.net/jupyter 存取 Jupyter Notebook。</span><span class="sxs-lookup"><span data-stu-id="53801-141">You also can access Jupyter notebooks at https://&lt;clustername&gt;.azurehdinsight.net/jupyter.</span></span> <span data-ttu-id="53801-142">取代*clustername*與 hello 叢集的名稱。</span><span class="sxs-lookup"><span data-stu-id="53801-142">Replace *clustername* with hello name of your cluster.</span></span> <span data-ttu-id="53801-143">您需要您系統管理員帳戶 tooaccess hello Jupyter 筆記本 hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="53801-143">You need hello password for your administrator account tooaccess hello Jupyter notebooks.</span></span>

![經過 tooJupyter 筆記本 hello 叢集名稱](./media/machine-learning-data-science-process-scala-walkthrough/spark-jupyter-notebook.png)

<span data-ttu-id="53801-145">選取**Scala** toosee 該使用 hello PySpark API 有幾個範例的套裝筆記本目錄。</span><span class="sxs-lookup"><span data-stu-id="53801-145">Select **Scala** toosee a directory that has a few examples of prepackaged notebooks that use hello PySpark API.</span></span> <span data-ttu-id="53801-146">使用此套件的 Spark 主題位於包含 hello 程式碼範例的 Scala.ipynb 筆記本 hello 瀏覽模型及計分[GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala)。</span><span class="sxs-lookup"><span data-stu-id="53801-146">hello Exploration Modeling and Scoring using Scala.ipynb notebook that contains hello code samples for this suite of Spark topics is available on [GitHub](https://github.com/Azure/Azure-MachineLearning-DataScience/tree/master/Misc/Spark/Scala).</span></span>

<span data-ttu-id="53801-147">您可以上傳直接從 GitHub toohello Jupyter 筆記本伺服器 hello 筆記本，您的 Spark 叢集上。</span><span class="sxs-lookup"><span data-stu-id="53801-147">You can upload hello notebook directly from GitHub toohello Jupyter Notebook server on your Spark cluster.</span></span> <span data-ttu-id="53801-148">在您 Jupyter 首頁上，按一下 hello**上傳** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53801-148">On your Jupyter home page, click hello **Upload** button.</span></span> <span data-ttu-id="53801-149">在 hello 檔案總管 中，貼上 hello GitHub （未經處理的內容） URL，hello Scala 筆記本，，然後按一下**開啟**。</span><span class="sxs-lookup"><span data-stu-id="53801-149">In hello file explorer, paste hello GitHub (raw content) URL of hello Scala notebook, and then click **Open**.</span></span> <span data-ttu-id="53801-150">hello Scala 筆記本會位於下列 URL 的 hello:</span><span class="sxs-lookup"><span data-stu-id="53801-150">hello Scala notebook is available at hello following URL:</span></span>

[<span data-ttu-id="53801-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span><span class="sxs-lookup"><span data-stu-id="53801-151">Exploration-Modeling-and-Scoring-using-Scala.ipynb</span></span>](https://github.com/Azure/Azure-MachineLearning-DataScience/blob/master/Misc/Spark/Scala/Exploration-Modeling-and-Scoring-using-Scala.ipynb)

## <a name="setup-preset-spark-and-hive-contexts-spark-magics-and-spark-libraries"></a><span data-ttu-id="53801-152">安裝程式︰預設的 Spark 和 Hive 內容、Spark Magic 和 Spark 程式庫</span><span class="sxs-lookup"><span data-stu-id="53801-152">Setup: Preset Spark and Hive contexts, Spark magics, and Spark libraries</span></span>
### <a name="preset-spark-and-hive-contexts"></a><span data-ttu-id="53801-153">預設的 Spark 和 Hive 內容</span><span class="sxs-lookup"><span data-stu-id="53801-153">Preset Spark and Hive contexts</span></span>
    # SET hello START TIME
    import java.util.Calendar
    val beginningTime = Calendar.getInstance().getTime()


<span data-ttu-id="53801-154">所提供的 Jupyter 筆記本 hello Spark 核心有預設的內容。</span><span class="sxs-lookup"><span data-stu-id="53801-154">hello Spark kernels that are provided with Jupyter notebooks have preset contexts.</span></span> <span data-ttu-id="53801-155">您開始使用您所開發的 hello 應用程式之前，您不需要 tooexplicitly 組 hello Spark 或登錄區內容。</span><span class="sxs-lookup"><span data-stu-id="53801-155">You don't need tooexplicitly set hello Spark or Hive contexts before you start working with hello application you are developing.</span></span> <span data-ttu-id="53801-156">hello 預先設定的內容如下：</span><span class="sxs-lookup"><span data-stu-id="53801-156">hello preset contexts are:</span></span>

* <span data-ttu-id="53801-157">`sc` 代表 SparkContext</span><span class="sxs-lookup"><span data-stu-id="53801-157">`sc` for SparkContext</span></span>
* <span data-ttu-id="53801-158">`sqlContext` 代表 HiveContext</span><span class="sxs-lookup"><span data-stu-id="53801-158">`sqlContext` for HiveContext</span></span>

### <a name="spark-magics"></a><span data-ttu-id="53801-159">Spark Magic</span><span class="sxs-lookup"><span data-stu-id="53801-159">Spark magics</span></span>
<span data-ttu-id="53801-160">hello Spark 核心提供一些預先定義 「"我們，這是特殊的命令，您可以呼叫與`%%`。</span><span class="sxs-lookup"><span data-stu-id="53801-160">hello Spark kernel provides some predefined “magics,” which are special commands that you can call with `%%`.</span></span> <span data-ttu-id="53801-161">兩個命令會使用下列程式碼範例的 hello。</span><span class="sxs-lookup"><span data-stu-id="53801-161">Two of these commands are used in hello following code samples.</span></span>

* <span data-ttu-id="53801-162">`%%local`指定在本機執行接下來幾行中的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="53801-162">`%%local` specifies that hello code in subsequent lines will be executed locally.</span></span> <span data-ttu-id="53801-163">hello 程式碼必須是有效的 Scala 程式碼。</span><span class="sxs-lookup"><span data-stu-id="53801-163">hello code must be valid Scala code.</span></span>
* <span data-ttu-id="53801-164">`%%sql -o <variable name>` 針對 `sqlContext` 執行 Hive 查詢。</span><span class="sxs-lookup"><span data-stu-id="53801-164">`%%sql -o <variable name>` executes a Hive query against `sqlContext`.</span></span> <span data-ttu-id="53801-165">如果 hello`-o`參數傳遞，hello hello 查詢結果會持續保留在 hello `%%local` Scala 成為 Spark 資料框架的內容。</span><span class="sxs-lookup"><span data-stu-id="53801-165">If hello `-o` parameter is passed, hello result of hello query is persisted in hello `%%local` Scala context as a Spark data frame.</span></span>

<span data-ttu-id="53801-166">您的 hello 核心 Jupyter 筆記本和其預先定義的詳細資訊 」 magics"的呼叫與`%%`(比方說， `%%local`)，請參閱[與 HDInsight Spark Linux Jupyter 筆記本的可用的核心叢集上HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md)。</span><span class="sxs-lookup"><span data-stu-id="53801-166">For more information about hello kernels for Jupyter notebooks and their predefined "magics" that you call with `%%` (for example, `%%local`), see [Kernels available for Jupyter notebooks with HDInsight Spark Linux clusters on HDInsight](../hdinsight/hdinsight-apache-spark-jupyter-notebook-kernels.md).</span></span>

### <a name="import-libraries"></a><span data-ttu-id="53801-167">匯入程式庫</span><span class="sxs-lookup"><span data-stu-id="53801-167">Import libraries</span></span>
<span data-ttu-id="53801-168">匯入 hello Spark、 MLlib 和其他文件庫，您必須使用下列程式碼的 hello。</span><span class="sxs-lookup"><span data-stu-id="53801-168">Import hello Spark, MLlib, and other libraries you'll need by using hello following code.</span></span>

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


## <a name="data-ingestion"></a><span data-ttu-id="53801-169">資料擷取</span><span class="sxs-lookup"><span data-stu-id="53801-169">Data ingestion</span></span>
<span data-ttu-id="53801-170">hello hello 資料科學程序中的第一個步驟是您想 tooanalyze tooingest hello 資料。</span><span class="sxs-lookup"><span data-stu-id="53801-170">hello first step in hello Data Science process is tooingest hello data that you want tooanalyze.</span></span> <span data-ttu-id="53801-171">您將 hello 資料從外部來源或系統資料探索和模型環境的所在位置。</span><span class="sxs-lookup"><span data-stu-id="53801-171">You bring hello data from external sources or systems where it resides into your data exploration and modeling environment.</span></span> <span data-ttu-id="53801-172">在本文中，您所擷取的 hello 資料會是聯結的 0.1 %hello 計程車行程及價位檔範例 （儲存為.tsv 檔案）。</span><span class="sxs-lookup"><span data-stu-id="53801-172">In this article, hello data you ingest is a joined 0.1% sample of hello taxi trip and fare file (stored as a .tsv file).</span></span> <span data-ttu-id="53801-173">hello 資料探索和模型環境是 Spark。</span><span class="sxs-lookup"><span data-stu-id="53801-173">hello data exploration and modeling environment is Spark.</span></span> <span data-ttu-id="53801-174">本節包含一系列的工作後 hello 程式碼 toocomplete hello:</span><span class="sxs-lookup"><span data-stu-id="53801-174">This section contains hello code toocomplete hello following series of tasks:</span></span>

1. <span data-ttu-id="53801-175">設定資料和模型儲存體的目錄路徑。</span><span class="sxs-lookup"><span data-stu-id="53801-175">Set directory paths for data and model storage.</span></span>
2. <span data-ttu-id="53801-176">讀取 hello 輸入資料集中 （儲存為.tsv 檔案）。</span><span class="sxs-lookup"><span data-stu-id="53801-176">Read in hello input data set (stored as a .tsv file).</span></span>
3. <span data-ttu-id="53801-177">定義 hello 和全新 hello 資料的結構描述。</span><span class="sxs-lookup"><span data-stu-id="53801-177">Define a schema for hello data and clean hello data.</span></span>
4. <span data-ttu-id="53801-178">建立已清除的資料框架，並在記憶體中加以快取。</span><span class="sxs-lookup"><span data-stu-id="53801-178">Create a cleaned data frame and cache it in memory.</span></span>
5. <span data-ttu-id="53801-179">註冊 hello 資料 SQLContext 中的暫存資料表。</span><span class="sxs-lookup"><span data-stu-id="53801-179">Register hello data as a temporary table in SQLContext.</span></span>
6. <span data-ttu-id="53801-180">查詢 hello 資料表和 hello 結果匯入至資料框架。</span><span class="sxs-lookup"><span data-stu-id="53801-180">Query hello table and import hello results into a data frame.</span></span>

### <a name="set-directory-paths-for-storage-locations-in-azure-blob-storage"></a><span data-ttu-id="53801-181">在 Azure Blob 儲存體中設定儲存位置的目錄路徑</span><span class="sxs-lookup"><span data-stu-id="53801-181">Set directory paths for storage locations in Azure Blob storage</span></span>
<span data-ttu-id="53801-182">Spark 可讀寫 tooAzure Blob 儲存體。</span><span class="sxs-lookup"><span data-stu-id="53801-182">Spark can read and write tooAzure Blob storage.</span></span> <span data-ttu-id="53801-183">您可以使用 Spark tooprocess 任何現有的資料，並再儲存 hello 結果 Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="53801-183">You can use Spark tooprocess any of your existing data, and then store hello results again in Blob storage.</span></span>

<span data-ttu-id="53801-184">toosave 模型或 Blob 儲存體中的檔案，您需要 tooproperly 指定 hello 路徑。</span><span class="sxs-lookup"><span data-stu-id="53801-184">toosave models or files in Blob storage, you need tooproperly specify hello path.</span></span> <span data-ttu-id="53801-185">參考 hello 預設容器使用的路徑，開頭附加 toohello Spark 叢集`wasb:///`。</span><span class="sxs-lookup"><span data-stu-id="53801-185">Reference hello default container attached toohello Spark cluster by using a path that begins with `wasb:///`.</span></span> <span data-ttu-id="53801-186">使用 `wasb://`參考其他位置。</span><span class="sxs-lookup"><span data-stu-id="53801-186">Reference other locations by using `wasb://`.</span></span>

<span data-ttu-id="53801-187">hello 下列程式碼範例指定 hello hello 模型儲存的位置讀取的 hello 輸入的資料 toobe 和 hello 路徑 tooBlob 存放裝置附加的 toohello Spark 叢集的位置。</span><span class="sxs-lookup"><span data-stu-id="53801-187">hello following code sample specifies hello location of hello input data toobe read and hello path tooBlob storage that is attached toohello Spark cluster where hello model will be saved.</span></span>

    # SET PATHS tooDATA AND MODEL FILE LOCATIONS
    # INGEST DATA AND SPECIFY HEADERS FOR COLUMNS
    val taxi_train_file = sc.textFile("wasb://mllibwalkthroughs@cdspsparksamples.blob.core.windows.net/Data/NYCTaxi/JoinedTaxiTripFare.Point1Pct.Train.tsv")
    val header = taxi_train_file.first;

    # SET hello MODEL STORAGE DIRECTORY PATH
    # NOTE THAT hello FINAL BACKSLASH IN hello PATH IS REQUIRED.
    val modelDir = "wasb:///user/remoteuser/NYCTaxi/Models/";


### <a name="import-data-create-an-rdd-and-define-a-data-frame-according-toohello-schema"></a><span data-ttu-id="53801-188">匯入資料、 建立 RDD，以及定義根據 toohello 結構描述資料框架</span><span class="sxs-lookup"><span data-stu-id="53801-188">Import data, create an RDD, and define a data frame according toohello schema</span></span>
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


<span data-ttu-id="53801-189">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-189">**Output:**</span></span>

<span data-ttu-id="53801-190">時間 toorun hello 資料格： 8 秒。</span><span class="sxs-lookup"><span data-stu-id="53801-190">Time toorun hello cell: 8 seconds.</span></span>

### <a name="query-hello-table-and-import-results-in-a-data-frame"></a><span data-ttu-id="53801-191">查詢 hello 資料表，並匯入資料框架中的結果</span><span class="sxs-lookup"><span data-stu-id="53801-191">Query hello table and import results in a data frame</span></span>
<span data-ttu-id="53801-192">下一步，查詢 hello 資料表價位、 旅客，和 tip 資料;篩選出損毀且外圍的資料。也會列印數個資料列。</span><span class="sxs-lookup"><span data-stu-id="53801-192">Next, query hello table for fare, passenger, and tip data; filter out corrupt and outlying data; and print several rows.</span></span>

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

<span data-ttu-id="53801-193">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-193">**Output:**</span></span>

| <span data-ttu-id="53801-194">fare_amount</span><span class="sxs-lookup"><span data-stu-id="53801-194">fare_amount</span></span> | <span data-ttu-id="53801-195">passenger_count</span><span class="sxs-lookup"><span data-stu-id="53801-195">passenger_count</span></span> | <span data-ttu-id="53801-196">tip_amount</span><span class="sxs-lookup"><span data-stu-id="53801-196">tip_amount</span></span> | <span data-ttu-id="53801-197">tipped</span><span class="sxs-lookup"><span data-stu-id="53801-197">tipped</span></span> |
| --- | --- | --- | --- |
|        <span data-ttu-id="53801-198">13.5</span><span class="sxs-lookup"><span data-stu-id="53801-198">13.5</span></span> |<span data-ttu-id="53801-199">1.0</span><span class="sxs-lookup"><span data-stu-id="53801-199">1.0</span></span> |<span data-ttu-id="53801-200">2.9</span><span class="sxs-lookup"><span data-stu-id="53801-200">2.9</span></span> |<span data-ttu-id="53801-201">1.0</span><span class="sxs-lookup"><span data-stu-id="53801-201">1.0</span></span> |
|        <span data-ttu-id="53801-202">16.0</span><span class="sxs-lookup"><span data-stu-id="53801-202">16.0</span></span> |<span data-ttu-id="53801-203">2.0</span><span class="sxs-lookup"><span data-stu-id="53801-203">2.0</span></span> |<span data-ttu-id="53801-204">3.4</span><span class="sxs-lookup"><span data-stu-id="53801-204">3.4</span></span> |<span data-ttu-id="53801-205">1.0</span><span class="sxs-lookup"><span data-stu-id="53801-205">1.0</span></span> |
|        <span data-ttu-id="53801-206">10.5</span><span class="sxs-lookup"><span data-stu-id="53801-206">10.5</span></span> |<span data-ttu-id="53801-207">2.0</span><span class="sxs-lookup"><span data-stu-id="53801-207">2.0</span></span> |<span data-ttu-id="53801-208">1.0</span><span class="sxs-lookup"><span data-stu-id="53801-208">1.0</span></span> |<span data-ttu-id="53801-209">1.0</span><span class="sxs-lookup"><span data-stu-id="53801-209">1.0</span></span> |

## <a name="data-exploration-and-visualization"></a><span data-ttu-id="53801-210">資料探索和虛擬化</span><span class="sxs-lookup"><span data-stu-id="53801-210">Data exploration and visualization</span></span>
<span data-ttu-id="53801-211">Hello 資料帶入 Spark 之後，hello hello 資料科學程序中的下一個步驟是 toogain hello 資料探索和視覺效果的更深入了解。</span><span class="sxs-lookup"><span data-stu-id="53801-211">After you bring hello data into Spark, hello next step in hello Data Science process is toogain a deeper understanding of hello data through exploration and visualization.</span></span> <span data-ttu-id="53801-212">在本節中，您可以檢查 hello 計程車資料使用 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="53801-212">In this section, you examine hello taxi data by using SQL queries.</span></span> <span data-ttu-id="53801-213">然後，匯入資料框架 tooplot hello 結果 hello 目標變數和潛在的功能，如 visual 檢查使用 Jupyter hello 自動視覺效果功能。</span><span class="sxs-lookup"><span data-stu-id="53801-213">Then, import hello results into a data frame tooplot hello target variables and prospective features for visual inspection by using hello auto-visualization feature of Jupyter.</span></span>

### <a name="use-local-and-sql-magic-tooplot-data"></a><span data-ttu-id="53801-214">使用本機和 SQL magic tooplot 資料</span><span class="sxs-lookup"><span data-stu-id="53801-214">Use local and SQL magic tooplot data</span></span>
<span data-ttu-id="53801-215">根據預設，您從 Jupyter 筆記本執行任何程式碼片段的 hello 輸出可 hello hello 保存在 hello 背景工作節點的工作階段內容中。</span><span class="sxs-lookup"><span data-stu-id="53801-215">By default, hello output of any code snippet that you run from a Jupyter notebook is available within hello context of hello session that is persisted on hello worker nodes.</span></span> <span data-ttu-id="53801-216">如果希望 toosave 路線 toohello 背景工作角色節點的每個計算，且如果所有 hello 您需要您計算是在本機上 hello Jupyter 伺服器節點 （即 hello 前端節點） 可用的資料，您可以使用 hello `%%local` magic toorun hello 程式碼hello Jupyter 伺服器上的程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="53801-216">If you want toosave a trip toohello worker nodes for every computation, and if all hello data that you need for your computation is available locally on hello Jupyter server node (which is hello head node), you can use hello `%%local` magic toorun hello code snippet on hello Jupyter server.</span></span>

* <span data-ttu-id="53801-217">**SQL magic** (`%%sql`)。</span><span class="sxs-lookup"><span data-stu-id="53801-217">**SQL magic** (`%%sql`).</span></span> <span data-ttu-id="53801-218">hello HDInsight Spark 核心支援 SQLContext 輕鬆內嵌 HiveQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="53801-218">hello HDInsight Spark kernel supports easy inline HiveQL queries against SQLContext.</span></span> <span data-ttu-id="53801-219">hello (`-o VARIABLE_NAME`) 引數會保存 hello 的 hello SQL 查詢的輸出為熊資料框架 hello Jupyter 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="53801-219">hello (`-o VARIABLE_NAME`) argument persists hello output of hello SQL query as a Pandas data frame on hello Jupyter server.</span></span> <span data-ttu-id="53801-220">這表示，將無法在 hello 本機模式中。</span><span class="sxs-lookup"><span data-stu-id="53801-220">This means it'll be available in hello local mode.</span></span>
* <span data-ttu-id="53801-221">`%%local` **magic**。</span><span class="sxs-lookup"><span data-stu-id="53801-221">`%%local` **magic**.</span></span> <span data-ttu-id="53801-222">hello `%%local` magic hello 程式碼會在本機執行 hello Jupyter 在伺服器上，也就是 hello hello HDInsight 叢集前端節點。</span><span class="sxs-lookup"><span data-stu-id="53801-222">hello `%%local` magic runs hello code locally on hello Jupyter server, which is hello head node of hello HDInsight cluster.</span></span> <span data-ttu-id="53801-223">通常，您會使用`%%local`magic 搭配 hello`%%sql`魔法與 hello`-o`參數。</span><span class="sxs-lookup"><span data-stu-id="53801-223">Typically, you use `%%local` magic in conjunction with hello `%%sql` magic with hello `-o` parameter.</span></span> <span data-ttu-id="53801-224">hello`-o`參數會保存在本機，hello SQL 查詢的 hello 輸出，然後`%%local`magic 會觸發 hello 下在本機憑藉保存在本機上的 hello 輸出的 hello SQL 查詢的程式碼片段 toorun 一組。</span><span class="sxs-lookup"><span data-stu-id="53801-224">hello `-o` parameter would persist hello output of hello SQL query locally, and then `%%local` magic would trigger hello next set of code snippet toorun locally against hello output of hello SQL queries that is persisted locally.</span></span>

### <a name="query-hello-data-by-using-sql"></a><span data-ttu-id="53801-225">使用 SQL 查詢 hello 資料</span><span class="sxs-lookup"><span data-stu-id="53801-225">Query hello data by using SQL</span></span>
<span data-ttu-id="53801-226">此查詢會擷取 hello 計程車往返價位量、 旅客計數的提示數量。</span><span class="sxs-lookup"><span data-stu-id="53801-226">This query retrieves hello taxi trips by fare amount, passenger count, and tip amount.</span></span>

    # RUN hello SQL QUERY
    %%sql -q -o sqlResults
    SELECT fare_amount, passenger_count, tip_amount, tipped FROM taxi_train WHERE passenger_count > 0 AND passenger_count < 7 AND fare_amount > 0 AND fare_amount < 200 AND payment_type in ('CSH', 'CRD') AND tip_amount > 0 AND tip_amount < 25

<span data-ttu-id="53801-227">在下列程式碼的 hello，hello `%%local` magic 會建立本機資料框架，sqlResults。</span><span class="sxs-lookup"><span data-stu-id="53801-227">In hello following code, hello `%%local` magic creates a local data frame, sqlResults.</span></span> <span data-ttu-id="53801-228">您可以使用 sqlResults tooplot 使用 matplotlib。</span><span class="sxs-lookup"><span data-stu-id="53801-228">You can use sqlResults tooplot by using matplotlib.</span></span>

> [!TIP]
> <span data-ttu-id="53801-229">本文中會多次使用本機 magic。</span><span class="sxs-lookup"><span data-stu-id="53801-229">Local magic is used multiple times in this article.</span></span> <span data-ttu-id="53801-230">如果您的資料集很大，請範例 toocreate 本機記憶體內可容納的資料框架。</span><span class="sxs-lookup"><span data-stu-id="53801-230">If your data set is large, please sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

### <a name="plot-hello-data"></a><span data-ttu-id="53801-231">繪製 hello 的資料</span><span class="sxs-lookup"><span data-stu-id="53801-231">Plot hello data</span></span>
<span data-ttu-id="53801-232">您可以繪製後 hello 資料框架會成為資料框架，熊本機內容中使用的 Python 程式碼。</span><span class="sxs-lookup"><span data-stu-id="53801-232">You can plot by using Python code after hello data frame is in local context as a Pandas data frame.</span></span>

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES.
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, ETC.)
    sqlResults


 <span data-ttu-id="53801-233">hello Spark 核心執行 hello 程式碼之後，自動視覺化 hello 的 SQL (HiveQL) 查詢的輸出。</span><span class="sxs-lookup"><span data-stu-id="53801-233">hello Spark kernel automatically visualizes hello output of SQL (HiveQL) queries after you run hello code.</span></span> <span data-ttu-id="53801-234">您可以選擇數種類型的視覺效果︰</span><span class="sxs-lookup"><span data-stu-id="53801-234">You can choose between several types of visualizations:</span></span>

* <span data-ttu-id="53801-235">資料表</span><span class="sxs-lookup"><span data-stu-id="53801-235">Table</span></span>
* <span data-ttu-id="53801-236">圓形圖</span><span class="sxs-lookup"><span data-stu-id="53801-236">Pie</span></span>
* <span data-ttu-id="53801-237">折線圖</span><span class="sxs-lookup"><span data-stu-id="53801-237">Line</span></span>
* <span data-ttu-id="53801-238">領域</span><span class="sxs-lookup"><span data-stu-id="53801-238">Area</span></span>
* <span data-ttu-id="53801-239">長條圖</span><span class="sxs-lookup"><span data-stu-id="53801-239">Bar</span></span>

<span data-ttu-id="53801-240">以下是 hello 程式碼 tooplot hello 資料：</span><span class="sxs-lookup"><span data-stu-id="53801-240">Here's hello code tooplot hello data:</span></span>

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


<span data-ttu-id="53801-241">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-241">**Output:**</span></span>

![小費金額長條圖](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-histogram.png)

![按乘客計數排列的小費金額](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-passenger-count.png)

![按費用金額排列的小費金額](./media/machine-learning-data-science-process-scala-walkthrough/plot-tip-amount-by-fare-amount.png)

## <a name="create-features-and-transform-features-and-then-prep-data-for-input-into-modeling-functions"></a><span data-ttu-id="53801-245">建立特徵和轉換特徵，然後準備資料輸入模型化函式</span><span class="sxs-lookup"><span data-stu-id="53801-245">Create features and transform features, and then prep data for input into modeling functions</span></span>
<span data-ttu-id="53801-246">對於從 Spark ML 和 MLlib 樹狀結構為基礎的模型化函式，您需要 tooprepare 目標和功能使用各種不同的技術，例如分類收納、 索引、 一個熱門的編碼方式，與向量化。</span><span class="sxs-lookup"><span data-stu-id="53801-246">For tree-based modeling functions from Spark ML and MLlib, you have tooprepare target and features by using a variety of techniques, such as binning, indexing, one-hot encoding, and vectorization.</span></span> <span data-ttu-id="53801-247">以下是本節中的 hello 程序 toofollow:</span><span class="sxs-lookup"><span data-stu-id="53801-247">Here are hello procedures toofollow in this section:</span></span>

1. <span data-ttu-id="53801-248">將小時 **納入** 流量時間值區以建立新特徵。</span><span class="sxs-lookup"><span data-stu-id="53801-248">Create a new feature by **binning** hours into traffic time buckets.</span></span>
2. <span data-ttu-id="53801-249">套用**編製索引和一個熱編碼**toocategorical 功能。</span><span class="sxs-lookup"><span data-stu-id="53801-249">Apply **indexing and one-hot encoding** toocategorical features.</span></span>
3. <span data-ttu-id="53801-250">**取樣和分割 hello 資料集**成定型集和測試的分數。</span><span class="sxs-lookup"><span data-stu-id="53801-250">**Sample and split hello data set** into training and test fractions.</span></span>
4. <span data-ttu-id="53801-251">**指定訓練變數和特徵**，然後建立已編製索引或已進行 one-hot 編碼的訓練和測試輸入標示點彈性分散式資料集 (RDD) 或資料框架。</span><span class="sxs-lookup"><span data-stu-id="53801-251">**Specify training variable and features**, and then create indexed or one-hot encoded training and testing input labeled point resilient distributed datasets (RDDs) or data frames.</span></span>
5. <span data-ttu-id="53801-252">自動**分類和向量化的功能和目標**toouse 做為輸入的機器學習模型。</span><span class="sxs-lookup"><span data-stu-id="53801-252">Automatically **categorize and vectorize features and targets** toouse as inputs for machine learning models.</span></span>

### <a name="create-a-new-feature-by-binning-hours-into-traffic-time-buckets"></a><span data-ttu-id="53801-253">將小時納入流量時間值區以建立新特徵</span><span class="sxs-lookup"><span data-stu-id="53801-253">Create a new feature by binning hours into traffic time buckets</span></span>
<span data-ttu-id="53801-254">這段程式碼會示範 toocreate 的新功能的分類收納成流量時間的小時的值區及如何 toocache hello 產生資料框架，在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="53801-254">This code shows you how toocreate a new feature by binning hours into traffic time buckets and how toocache hello resulting data frame in memory.</span></span> <span data-ttu-id="53801-255">重複使用 RDDs 和資料框架，快取會導致 tooimproved 執行時間。</span><span class="sxs-lookup"><span data-stu-id="53801-255">Where RDDs and data frames are used repeatedly, caching leads tooimproved execution times.</span></span> <span data-ttu-id="53801-256">因此，您會在 hello 下列程序中的數個階段快取 RDDs 和資料框架。</span><span class="sxs-lookup"><span data-stu-id="53801-256">Accordingly, you'll cache RDDs and data frames at several stages in hello following procedures.</span></span>

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


### <a name="indexing-and-one-hot-encoding-of-categorical-features"></a><span data-ttu-id="53801-257">索引和 one-hot 編碼分類功能</span><span class="sxs-lookup"><span data-stu-id="53801-257">Indexing and one-hot encoding of categorical features</span></span>
<span data-ttu-id="53801-258">hello 模型和預測的 MLlib 函式需要功能與類別的輸入的資料 toobe 編製索引，或編碼先前 toouse。</span><span class="sxs-lookup"><span data-stu-id="53801-258">hello modeling and predict functions of MLlib require features with categorical input data toobe indexed or encoded prior toouse.</span></span> <span data-ttu-id="53801-259">這個區段會顯示如何 tooindex 或編碼的輸入 hello 模型函式的類別特徵。</span><span class="sxs-lookup"><span data-stu-id="53801-259">This section shows you how tooindex or encode categorical features for input into hello modeling functions.</span></span>

<span data-ttu-id="53801-260">您需要 tooindex 或編碼您的模型，以不同的方式，視 hello 模型而定。</span><span class="sxs-lookup"><span data-stu-id="53801-260">You need tooindex or encode your models in different ways, depending on hello model.</span></span> <span data-ttu-id="53801-261">例如，羅吉斯和線性迴歸模型需要 one-hot 編碼。</span><span class="sxs-lookup"><span data-stu-id="53801-261">For example, logistic and linear regression models require one-hot encoding.</span></span> <span data-ttu-id="53801-262">例如，有三個類別的特徵可展開成三個特徵資料行。</span><span class="sxs-lookup"><span data-stu-id="53801-262">For example, a feature with three categories can be expanded into three feature columns.</span></span> <span data-ttu-id="53801-263">每個資料行可能包含 0 或 1，視所觀察 hello 分類。</span><span class="sxs-lookup"><span data-stu-id="53801-263">Each column would contain 0 or 1 depending on hello category of an observation.</span></span> <span data-ttu-id="53801-264">MLlib 提供 hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder)函式的其中一個熱門的編碼方式。</span><span class="sxs-lookup"><span data-stu-id="53801-264">MLlib provides hello [OneHotEncoder](http://scikit-learn.org/stable/modules/generated/sklearn.preprocessing.OneHotEncoder.html#sklearn.preprocessing.OneHotEncoder) function for one-hot encoding.</span></span> <span data-ttu-id="53801-265">此編碼器將對應的二進位的向量，使用最多為單一其中一個值的標籤索引 tooa 資料行的資料行。</span><span class="sxs-lookup"><span data-stu-id="53801-265">This encoder maps a column of label indices tooa column of binary vectors with at most a single one-value.</span></span> <span data-ttu-id="53801-266">使用這種編碼方式，所預期的數字的重要的功能，例如羅吉斯迴歸演算法可以套用的 toocategorical 功能。</span><span class="sxs-lookup"><span data-stu-id="53801-266">With this encoding, algorithms that expect numerical valued features, such as logistic regression, can be applied toocategorical features.</span></span>

<span data-ttu-id="53801-267">這裡您轉換只能有四個變數 tooshow 範例是字元字串。</span><span class="sxs-lookup"><span data-stu-id="53801-267">Here you transform only four variables tooshow examples, which are character strings.</span></span> <span data-ttu-id="53801-268">您也可以將其他以數值表示的變數 (例如工作日) 編製索引為類別變數。</span><span class="sxs-lookup"><span data-stu-id="53801-268">You also can index other variables, such as weekday, represented by numerical values, as categorical variables.</span></span>

<span data-ttu-id="53801-269">如需編製索引，請使用 `StringIndexer()`，如需進行 one-hot 編碼，請使用 MLlib 中的 `OneHotEncoder()` 函式。</span><span class="sxs-lookup"><span data-stu-id="53801-269">For indexing, use `StringIndexer()`, and for one-hot encoding, use `OneHotEncoder()` functions from MLlib.</span></span> <span data-ttu-id="53801-270">以下是 hello tooindex 程式碼，並將編碼類別特徵：</span><span class="sxs-lookup"><span data-stu-id="53801-270">Here is hello code tooindex and encode categorical features:</span></span>

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


<span data-ttu-id="53801-271">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-271">**Output:**</span></span>

<span data-ttu-id="53801-272">儲存格-toorun hello 時間： 4 秒。</span><span class="sxs-lookup"><span data-stu-id="53801-272">Time toorun hello cell: 4 seconds.</span></span>

### <a name="sample-and-split-hello-data-set-into-training-and-test-fractions"></a><span data-ttu-id="53801-273">取樣和分割成定型集和測試分數中 hello 資料集</span><span class="sxs-lookup"><span data-stu-id="53801-273">Sample and split hello data set into training and test fractions</span></span>
<span data-ttu-id="53801-274">此程式碼會建立隨機取樣的 hello 資料 （在此範例中，25%)。</span><span class="sxs-lookup"><span data-stu-id="53801-274">This code creates a random sampling of hello data (25%, in this example).</span></span> <span data-ttu-id="53801-275">取樣不需要因為 toohello 大小 hello 資料集的這個範例中，雖然 hello 文章向您示範如何可以取樣，以了解如何 toouse 它自己時所需的問題。</span><span class="sxs-lookup"><span data-stu-id="53801-275">Although sampling is not required for this example due toohello size of hello data set, hello article shows you how you can sample so that you know how toouse it for your own problems when needed.</span></span> <span data-ttu-id="53801-276">如果樣本數較大，這可以在訓練模型時節省大量時間。</span><span class="sxs-lookup"><span data-stu-id="53801-276">When samples are large, this can save significant time while you train models.</span></span> <span data-ttu-id="53801-277">接下來，將 hello 範例分割成定型部分 （在此範例中，75%) 和測試組件 （在此範例中，25%) toouse 分類和迴歸模型中的。</span><span class="sxs-lookup"><span data-stu-id="53801-277">Next, split hello sample into a training part (75%, in this example) and a testing part (25%, in this example) toouse in classification and regression modeling.</span></span>

<span data-ttu-id="53801-278">加入在定型期間可使用的 tooselect 交叉驗證摺疊資料隨機數字 （介於 0 和 1） tooeach 列 （在"rand 」 資料行中）。</span><span class="sxs-lookup"><span data-stu-id="53801-278">Add a random number (between 0 and 1) tooeach row (in a "rand" column) that can be used tooselect cross-validation folds during training.</span></span>

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


<span data-ttu-id="53801-279">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-279">**Output:**</span></span>

<span data-ttu-id="53801-280">時間 toorun hello 資料格： 2 秒。</span><span class="sxs-lookup"><span data-stu-id="53801-280">Time toorun hello cell: 2 seconds.</span></span>

### <a name="specify-training-variable-and-features-and-then-create-indexed-or-one-hot-encoded-training-and-testing-input-labeled-point-rdds-or-data-frames"></a><span data-ttu-id="53801-281">指定訓練變數和特徵，然後建立已編製索引或已進行 one-hot 編碼的訓練和測試輸入標示點 RDD 或資料框架</span><span class="sxs-lookup"><span data-stu-id="53801-281">Specify training variable and features, and then create indexed or one-hot encoded training and testing input labeled point RDDs or data frames</span></span>
<span data-ttu-id="53801-282">本節包含示範如何 tooindex 類別的文字資料加上標籤與資料類型及加以編碼，因此您可以使用它 tootrain 和測試 MLlib 羅吉斯迴歸和其他分類模型的程式碼。</span><span class="sxs-lookup"><span data-stu-id="53801-282">This section contains code that shows you how tooindex categorical text data as a labeled point data type, and encode it so you can use it tootrain and test MLlib logistic regression and other classification models.</span></span> <span data-ttu-id="53801-283">標示點物件是 RDD，其格式化成適合 MLlib 中大部分機器學習演算法所需的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="53801-283">Labeled point objects are RDDs that are formatted in a way that is needed as input data by most of machine learning algorithms in MLlib.</span></span> <span data-ttu-id="53801-284">[標示點](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) 是本機向量 (密集或疏鬆)，與標籤/回應相關聯。</span><span class="sxs-lookup"><span data-stu-id="53801-284">A [labeled point](https://spark.apache.org/docs/latest/mllib-data-types.html#labeled-point) is a local vector, either dense or sparse, associated with a label/response.</span></span>

<span data-ttu-id="53801-285">在此程式碼中，您可以指定 hello 目標 （相依） 變數和 hello 功能 toouse tootrain 模型。</span><span class="sxs-lookup"><span data-stu-id="53801-285">In this code, you specify hello target (dependent) variable and hello features toouse tootrain models.</span></span> <span data-ttu-id="53801-286">然後，建立已編製索引或已進行 one-hot 編碼的訓練和測試輸入標示點 RDD 或資料框架。</span><span class="sxs-lookup"><span data-stu-id="53801-286">Then, you create indexed or one-hot encoded training and testing input labeled point RDDs or data frames.</span></span>

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


<span data-ttu-id="53801-287">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-287">**Output:**</span></span>

<span data-ttu-id="53801-288">儲存格-toorun hello 時間： 4 秒。</span><span class="sxs-lookup"><span data-stu-id="53801-288">Time toorun hello cell: 4 seconds.</span></span>

### <a name="automatically-categorize-and-vectorize-features-and-targets-toouse-as-inputs-for-machine-learning-models"></a><span data-ttu-id="53801-289">自動分類，並做為機器學習模型的輸入向量化的功能和目標 toouse</span><span class="sxs-lookup"><span data-stu-id="53801-289">Automatically categorize and vectorize features and targets toouse as inputs for machine learning models</span></span>
<span data-ttu-id="53801-290">您可以使用 Spark ML toocategorize hello 目標和功能 toouse 中樹狀結構為基礎的模型功能。</span><span class="sxs-lookup"><span data-stu-id="53801-290">Use Spark ML toocategorize hello target and features toouse in tree-based modeling functions.</span></span> <span data-ttu-id="53801-291">hello 程式碼會完成兩項工作：</span><span class="sxs-lookup"><span data-stu-id="53801-291">hello code completes two tasks:</span></span>

* <span data-ttu-id="53801-292">藉由使用臨界值為 0.5，將指派 0 或 1 tooeach 資料點，介於 0 和 1 之間的值建立二進位分類的目標。</span><span class="sxs-lookup"><span data-stu-id="53801-292">Creates a binary target for classification by assigning a value of 0 or 1 tooeach data point between 0 and 1 by using a threshold value of 0.5.</span></span>
* <span data-ttu-id="53801-293">自動將功能分類。</span><span class="sxs-lookup"><span data-stu-id="53801-293">Automatically categorizes features.</span></span> <span data-ttu-id="53801-294">如果小於 32 hello 相異值數目的數字的任何功能，並屬於該功能。</span><span class="sxs-lookup"><span data-stu-id="53801-294">If hello number of distinct numerical values for any feature is less than 32, that feature is categorized.</span></span>

<span data-ttu-id="53801-295">以下是這兩個工作的 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="53801-295">Here's hello code for these two tasks.</span></span>

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



## <a name="binary-classification-model-predict-whether-a-tip-should-be-paid"></a><span data-ttu-id="53801-296">二進位分類模型：預測是否應支付小費</span><span class="sxs-lookup"><span data-stu-id="53801-296">Binary classification model: Predict whether a tip should be paid</span></span>
<span data-ttu-id="53801-297">在本節中，您可以建立三種類型的二元分類模型 toopredict 應該付費秘訣：</span><span class="sxs-lookup"><span data-stu-id="53801-297">In this section, you create three types of binary classification models toopredict whether or not a tip should be paid:</span></span>

* <span data-ttu-id="53801-298">A**羅吉斯迴歸模型**使用 hello Spark ML`LogisticRegression()`函式</span><span class="sxs-lookup"><span data-stu-id="53801-298">A **logistic regression model** by using hello Spark ML `LogisticRegression()` function</span></span>
* <span data-ttu-id="53801-299">A**隨機樹系分類模型**使用 hello Spark ML`RandomForestClassifier()`函式</span><span class="sxs-lookup"><span data-stu-id="53801-299">A **random forest classification model** by using hello Spark ML `RandomForestClassifier()` function</span></span>
* <span data-ttu-id="53801-300">A**漸層停駐提升樹分類模型**使用 hello MLlib`GradientBoostedTrees()`函式</span><span class="sxs-lookup"><span data-stu-id="53801-300">A **gradient boosting tree classification model** by using hello MLlib `GradientBoostedTrees()` function</span></span>

### <a name="create-a-logistic-regression-model"></a><span data-ttu-id="53801-301">建立羅吉斯迴歸模型</span><span class="sxs-lookup"><span data-stu-id="53801-301">Create a logistic regression model</span></span>
<span data-ttu-id="53801-302">接下來，建立羅吉斯迴歸模型使用 hello Spark ML`LogisticRegression()`函式。</span><span class="sxs-lookup"><span data-stu-id="53801-302">Next, create a logistic regression model by using hello Spark ML `LogisticRegression()` function.</span></span> <span data-ttu-id="53801-303">您建立 hello 模型建立一系列的步驟中的程式碼：</span><span class="sxs-lookup"><span data-stu-id="53801-303">You create hello model building code in a series of steps:</span></span>

1. <span data-ttu-id="53801-304">**定型 hello 模型**具有一個參數集的資料。</span><span class="sxs-lookup"><span data-stu-id="53801-304">**Train hello model** data with one parameter set.</span></span>
2. <span data-ttu-id="53801-305">**評估 hello 模型**上測試資料集 （包括計量）。</span><span class="sxs-lookup"><span data-stu-id="53801-305">**Evaluate hello model** on a test data set with metrics.</span></span>
3. <span data-ttu-id="53801-306">**儲存 hello 模型**供未來取用的 Blob 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="53801-306">**Save hello model** in Blob storage for future consumption.</span></span>
4. <span data-ttu-id="53801-307">**計分 hello 模型**針對測試資料。</span><span class="sxs-lookup"><span data-stu-id="53801-307">**Score hello model** against test data.</span></span>
5. <span data-ttu-id="53801-308">**繪製 hello 結果**使用接收器操作特徵 (ROC) 曲線。</span><span class="sxs-lookup"><span data-stu-id="53801-308">**Plot hello results** with receiver operating characteristic (ROC) curves.</span></span>

<span data-ttu-id="53801-309">這些程序的 「 hello 」 程式碼如下：</span><span class="sxs-lookup"><span data-stu-id="53801-309">Here's hello code for these procedures:</span></span>

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

<span data-ttu-id="53801-310">載入、 評分，以及儲存 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="53801-310">Load, score, and save hello results.</span></span>

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


<span data-ttu-id="53801-311">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-311">**Output:**</span></span>

<span data-ttu-id="53801-312">測試資料的 ROC = 0.9827381497557599</span><span class="sxs-lookup"><span data-stu-id="53801-312">ROC on test data = 0.9827381497557599</span></span>

<span data-ttu-id="53801-313">使用 Python 本機熊資料框架 tooplot hello ROC 曲線上。</span><span class="sxs-lookup"><span data-stu-id="53801-313">Use Python on local Pandas data frames tooplot hello ROC curve.</span></span>

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


<span data-ttu-id="53801-314">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-314">**Output:**</span></span>

![小費或沒有小費的 ROC 曲線](./media/machine-learning-data-science-process-scala-walkthrough/plot-roc-curve-tip-or-not.png)

### <a name="create-a-random-forest-classification-model"></a><span data-ttu-id="53801-316">建立隨機樹系分類模型</span><span class="sxs-lookup"><span data-stu-id="53801-316">Create a random forest classification model</span></span>
<span data-ttu-id="53801-317">接下來，建立隨機樹系分類模型使用 hello Spark ML`RandomForestClassifier()`函式，並評估 hello 模型測試資料上的。</span><span class="sxs-lookup"><span data-stu-id="53801-317">Next, create a random forest classification model by using hello Spark ML `RandomForestClassifier()` function, and then evaluate hello model on test data.</span></span>

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


<span data-ttu-id="53801-318">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-318">**Output:**</span></span>

<span data-ttu-id="53801-319">測試資料的 ROC = 0.9847103571552683</span><span class="sxs-lookup"><span data-stu-id="53801-319">ROC on test data = 0.9847103571552683</span></span>

### <a name="create-a-gbt-classification-model"></a><span data-ttu-id="53801-320">建立 GBT 分類模型</span><span class="sxs-lookup"><span data-stu-id="53801-320">Create a GBT classification model</span></span>
<span data-ttu-id="53801-321">接下來，建立 GBT 分類模型使用 MLlib 的`GradientBoostedTrees()`函式，並評估 hello 模型測試資料上的。</span><span class="sxs-lookup"><span data-stu-id="53801-321">Next, create a GBT classification model by using MLlib's `GradientBoostedTrees()` function, and then evaluate hello model on test data.</span></span>

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


<span data-ttu-id="53801-322">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-322">**Output:**</span></span>

<span data-ttu-id="53801-323">ROC 曲線夏的領域 = 0.9846895479241554</span><span class="sxs-lookup"><span data-stu-id="53801-323">Area under ROC curve: 0.9846895479241554</span></span>

## <a name="regression-model-predict-tip-amount"></a><span data-ttu-id="53801-324">迴歸模型：預測小費金額</span><span class="sxs-lookup"><span data-stu-id="53801-324">Regression model: Predict tip amount</span></span>
<span data-ttu-id="53801-325">在本節中，您可以建立兩種類型的迴歸模型 toopredict hello 提示量：</span><span class="sxs-lookup"><span data-stu-id="53801-325">In this section, you create two types of regression models toopredict hello tip amount:</span></span>

* <span data-ttu-id="53801-326">A**正則化的線性迴歸模型**使用 hello Spark ML`LinearRegression()`函式。</span><span class="sxs-lookup"><span data-stu-id="53801-326">A **regularized linear regression model** by using hello Spark ML `LinearRegression()` function.</span></span> <span data-ttu-id="53801-327">將儲存 hello 模型，並評估 hello 模型測試資料。</span><span class="sxs-lookup"><span data-stu-id="53801-327">You'll save hello model and evaluate hello model on test data.</span></span>
* <span data-ttu-id="53801-328">A**漸層來提升樹迴歸模型**使用 hello Spark ML`GBTRegressor()`函式。</span><span class="sxs-lookup"><span data-stu-id="53801-328">A **gradient-boosting tree regression model** by using hello Spark ML `GBTRegressor()` function.</span></span>

### <a name="create-a-regularized-linear-regression-model"></a><span data-ttu-id="53801-329">建立正則化線性迴歸模型</span><span class="sxs-lookup"><span data-stu-id="53801-329">Create a regularized linear regression model</span></span>
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


<span data-ttu-id="53801-330">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-330">**Output:**</span></span>

<span data-ttu-id="53801-331">儲存格-toorun hello 時間： 13 的秒數。</span><span class="sxs-lookup"><span data-stu-id="53801-331">Time toorun hello cell: 13 seconds.</span></span>

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


<span data-ttu-id="53801-332">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-332">**Output:**</span></span>

<span data-ttu-id="53801-333">測試資料的 R-sqr = 0.5960320470835743</span><span class="sxs-lookup"><span data-stu-id="53801-333">R-sqr on test data = 0.5960320470835743</span></span>

<span data-ttu-id="53801-334">接下來，查詢 hello 測試結果為資料框架和 AutoVizWidget 和 matplotlib toovisualize 使用它。</span><span class="sxs-lookup"><span data-stu-id="53801-334">Next, query hello test results as a data frame and use AutoVizWidget and matplotlib toovisualize it.</span></span>

    # RUN A SQL QUERY
    %%sql -q -o sqlResults
    select * from testResults

    # RUN hello CODE LOCALLY ON hello JUPYTER SERVER
    %%local

    # USE hello JUPYTER AUTO-PLOTTING FEATURE tooCREATE INTERACTIVE FIGURES
    # CLICK hello TYPE OF PLOT tooGENERATE (LINE, AREA, BAR, AND SO ON)
    sqlResults

<span data-ttu-id="53801-335">hello 程式碼會建立從 hello 查詢輸出的本機資料框架，並繪製 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="53801-335">hello code creates a local data frame from hello query output and plots hello data.</span></span> <span data-ttu-id="53801-336">hello `%%local` magic 會建立本機資料框架， `sqlResults`，而您可以使用 matplotlib tooplot。</span><span class="sxs-lookup"><span data-stu-id="53801-336">hello `%%local` magic creates a local data frame, `sqlResults`, which you can use tooplot with matplotlib.</span></span>

> [!NOTE]
> <span data-ttu-id="53801-337">本文中會多次使用此 Spark magic。</span><span class="sxs-lookup"><span data-stu-id="53801-337">This Spark magic is used multiple times in this article.</span></span> <span data-ttu-id="53801-338">如果 hello 資料量很大，您應該取樣 toocreate 本機記憶體內可容納的資料框架。</span><span class="sxs-lookup"><span data-stu-id="53801-338">If hello amount of data is large, you should sample toocreate a data frame that can fit in local memory.</span></span>
> 
> 

<span data-ttu-id="53801-339">使用 Python matplotlib 建立繪圖。</span><span class="sxs-lookup"><span data-stu-id="53801-339">Create plots by using Python matplotlib.</span></span>

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

<span data-ttu-id="53801-340">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-340">**Output:**</span></span>

![小費金額︰實際與預測](./media/machine-learning-data-science-process-scala-walkthrough/plot-actual-vs-predicted-tip-amount.png)

### <a name="create-a-gbt-regression-model"></a><span data-ttu-id="53801-342">建立 GBT 迴歸模型</span><span class="sxs-lookup"><span data-stu-id="53801-342">Create a GBT regression model</span></span>
<span data-ttu-id="53801-343">建立 GBT 迴歸模型使用 hello Spark ML`GBTRegressor()`函式，並評估 hello 模型測試資料上的。</span><span class="sxs-lookup"><span data-stu-id="53801-343">Create a GBT regression model by using hello Spark ML `GBTRegressor()` function, and then evaluate hello model on test data.</span></span>

<span data-ttu-id="53801-344">[梯度推進樹](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBT) 集合了所有決策樹。</span><span class="sxs-lookup"><span data-stu-id="53801-344">[Gradient-boosted trees](http://spark.apache.org/docs/latest/ml-classification-regression.html#gradient-boosted-trees-gbts) (GBTs) are ensembles of decision trees.</span></span> <span data-ttu-id="53801-345">GBTs 定型決策樹反覆 toominimize 損失函數。</span><span class="sxs-lookup"><span data-stu-id="53801-345">GBTs train decision trees iteratively toominimize a loss function.</span></span> <span data-ttu-id="53801-346">您可以使用 GBT 進行迴歸和分類。</span><span class="sxs-lookup"><span data-stu-id="53801-346">You can use GBTs for regression and classification.</span></span> <span data-ttu-id="53801-347">GBT 可以處理分類特徵、不需要調整特徵，而且可以擷取非線性和特徵互動。</span><span class="sxs-lookup"><span data-stu-id="53801-347">They can handle categorical features, do not require feature scaling, and can capture nonlinearities and feature interactions.</span></span> <span data-ttu-id="53801-348">您也可以在多類別分類設定中使用 GBT。</span><span class="sxs-lookup"><span data-stu-id="53801-348">You also can use them in a multiclass-classification setting.</span></span>

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


<span data-ttu-id="53801-349">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-349">**Output:**</span></span>

<span data-ttu-id="53801-350">測試 R-sqr：0.7655383534596654</span><span class="sxs-lookup"><span data-stu-id="53801-350">Test R-sqr is: 0.7655383534596654</span></span>

## <a name="advanced-modeling-utilities-for-optimization"></a><span data-ttu-id="53801-351">可供最佳化的進階模型化公用程式</span><span class="sxs-lookup"><span data-stu-id="53801-351">Advanced modeling utilities for optimization</span></span>
<span data-ttu-id="53801-352">在本節中，您將使用開發人員經常使用的機器學習公用程式來最佳化模型。</span><span class="sxs-lookup"><span data-stu-id="53801-352">In this section, you use machine learning utilities that developers frequently use for model optimization.</span></span> <span data-ttu-id="53801-353">具體來說，您可以使用參數掃掠和交叉驗證，以三種不同的方式來最佳化機器學習模型︰</span><span class="sxs-lookup"><span data-stu-id="53801-353">Specifically, you can optimize machine learning models three different ways by using parameter sweeping and cross-validation:</span></span>

* <span data-ttu-id="53801-354">Hello 資料分割成定型和驗證設定、 充分運用 hello 模型透過超參數牽涉上定型集，並評估上驗證設定 （線性迴歸）</span><span class="sxs-lookup"><span data-stu-id="53801-354">Split hello data into train and validation sets, optimize hello model by using hyper-parameter sweeping on a training set, and evaluate on a validation set (linear regression)</span></span>
* <span data-ttu-id="53801-355">最佳化 hello 模型使用交叉驗證和超參數掃掠利用 Spark ML CrossValidator 函式 （二元分類）</span><span class="sxs-lookup"><span data-stu-id="53801-355">Optimize hello model by using cross-validation and hyper-parameter sweeping by using Spark ML's CrossValidator function (binary classification)</span></span>
* <span data-ttu-id="53801-356">最佳化 hello 模型使用自訂交叉驗證 」 和 「 參數掃掠的程式碼 toouse 任何機器學習服務函數與參數集 （線性迴歸）</span><span class="sxs-lookup"><span data-stu-id="53801-356">Optimize hello model by using custom cross-validation and parameter-sweeping code toouse any machine learning function and parameter set (linear regression)</span></span>

<span data-ttu-id="53801-357">**交叉驗證**是評估如何在一組已知的資料上定型的模型將一般化 toopredict hello 功能所在它尚未定型資料集的技術。</span><span class="sxs-lookup"><span data-stu-id="53801-357">**Cross-validation** is a technique that assesses how well a model trained on a known set of data will generalize toopredict hello features of data sets on which it has not been trained.</span></span> <span data-ttu-id="53801-358">hello 大概了解這項技術後面是已知的資料的資料集上定型模型，並接著 hello 其預測精確度的測試，之後根據獨立的資料集。</span><span class="sxs-lookup"><span data-stu-id="53801-358">hello general idea behind this technique is that a model is trained on a data set of known data, and then hello accuracy of its predictions is tested against an independent data set.</span></span> <span data-ttu-id="53801-359">常見的實作是 toodivide 資料集分成*k*-摺疊，並再 hello 中定型模型，只留下其中一個 hello 摺疊所有以循環配置資源的方式。</span><span class="sxs-lookup"><span data-stu-id="53801-359">A common implementation is toodivide a data set into *k*-folds, and then train hello model in a round-robin fashion on all but one of hello folds.</span></span>

<span data-ttu-id="53801-360">**Hyper-v 參數最佳化**hello 問題選擇一組超參數學習演算法，通常以 hello 目標最佳化 hello 演算法的效能，在獨立的資料集上的量值。</span><span class="sxs-lookup"><span data-stu-id="53801-360">**Hyper-parameter optimization** is hello problem of choosing a set of hyper-parameters for a learning algorithm, usually with hello goal of optimizing a measure of hello algorithm's performance on an independent data set.</span></span> <span data-ttu-id="53801-361">值，您必須指定 hello 模型定型程序之外超參數。</span><span class="sxs-lookup"><span data-stu-id="53801-361">A hyper-parameter is a value that you must specify outside hello model training procedure.</span></span> <span data-ttu-id="53801-362">Hello 彈性與 hello 模型的精確度，可能會影響超參數值的相關假設。</span><span class="sxs-lookup"><span data-stu-id="53801-362">Assumptions about hyper-parameter values can affect hello flexibility and accuracy of hello model.</span></span> <span data-ttu-id="53801-363">決策樹，例如有超參數，例如 hello 預期深度和 hello 樹狀目錄中的分葉數目。</span><span class="sxs-lookup"><span data-stu-id="53801-363">Decision trees have hyper-parameters, for example, such as hello desired depth and number of leaves in hello tree.</span></span> <span data-ttu-id="53801-364">您必須為支援向量機器 (SVM) 設定分類誤判損失詞彙。</span><span class="sxs-lookup"><span data-stu-id="53801-364">You must set a misclassification penalty term for a support vector machine (SVM).</span></span>

<span data-ttu-id="53801-365">常見的方式 tooperform 超參數最佳化是 toouse 方格搜尋，也稱為**參數掃掠**。</span><span class="sxs-lookup"><span data-stu-id="53801-365">A common way tooperform hyper-parameter optimization is toouse a grid search, also called a **parameter sweep**.</span></span> <span data-ttu-id="53801-366">方格搜尋時，是徹底搜索經過 hello 值指定學習演算法的 hello 超參數空間的子集。</span><span class="sxs-lookup"><span data-stu-id="53801-366">In a grid search, an exhaustive search is performed through hello values of a specified subset of hello hyper-parameter space for a learning algorithm.</span></span> <span data-ttu-id="53801-367">交叉驗證可以提供的效能度量 toosort 出 hello 所 hello 方格搜尋演算法產生最佳的結果。</span><span class="sxs-lookup"><span data-stu-id="53801-367">Cross-validation can supply a performance metric toosort out hello optimal results produced by hello grid search algorithm.</span></span> <span data-ttu-id="53801-368">如果您使用交叉驗證超參數牽涉，可協助限制問題，例如過度配適模型 tootraining 資料。</span><span class="sxs-lookup"><span data-stu-id="53801-368">If you use cross-validation hyper-parameter sweeping, you can help limit problems like overfitting a model tootraining data.</span></span> <span data-ttu-id="53801-369">如此一來，hello 模型會保留 hello 容量 tooapply toohello 一般的資料集從哪些 hello 擷取定型資料。</span><span class="sxs-lookup"><span data-stu-id="53801-369">This way, hello model retains hello capacity tooapply toohello general set of data from which hello training data was extracted.</span></span>

### <a name="optimize-a-linear-regression-model-with-hyper-parameter-sweeping"></a><span data-ttu-id="53801-370">利用超參數掃掠來最佳化線性迴歸模型</span><span class="sxs-lookup"><span data-stu-id="53801-370">Optimize a linear regression model with hyper-parameter sweeping</span></span>
<span data-ttu-id="53801-371">接下來，將資料分割成定型和驗證設定，參數使用超集上定型掃掠設定 toooptimize hello 模型，並評估驗證組 （線性迴歸） 上。</span><span class="sxs-lookup"><span data-stu-id="53801-371">Next, split data into train and validation sets, use hyper-parameter sweeping on a training set toooptimize hello model, and evaluate on a validation set (linear regression).</span></span>

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


<span data-ttu-id="53801-372">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-372">**Output:**</span></span>

<span data-ttu-id="53801-373">測試 R-sqr：0.6226484708501209</span><span class="sxs-lookup"><span data-stu-id="53801-373">Test R-sqr is: 0.6226484708501209</span></span>

### <a name="optimize-hello-binary-classification-model-by-using-cross-validation-and-hyper-parameter-sweeping"></a><span data-ttu-id="53801-374">使用交叉驗證和超參數牽涉最佳化 hello 二元分類模型</span><span class="sxs-lookup"><span data-stu-id="53801-374">Optimize hello binary classification model by using cross-validation and hyper-parameter sweeping</span></span>
<span data-ttu-id="53801-375">本節說明如何 toooptimize 二元分類模型使用交叉驗證和超參數掃掠。</span><span class="sxs-lookup"><span data-stu-id="53801-375">This section shows you how toooptimize a binary classification model by using cross-validation and hyper-parameter sweeping.</span></span> <span data-ttu-id="53801-376">這會使用 hello Spark ML`CrossValidator`函式。</span><span class="sxs-lookup"><span data-stu-id="53801-376">This uses hello Spark ML `CrossValidator` function.</span></span>

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


<span data-ttu-id="53801-377">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-377">**Output:**</span></span>

<span data-ttu-id="53801-378">時間 toorun hello 資料格： 33 秒。</span><span class="sxs-lookup"><span data-stu-id="53801-378">Time toorun hello cell: 33 seconds.</span></span>

### <a name="optimize-hello-linear-regression-model-by-using-custom-cross-validation-and-parameter-sweeping-code"></a><span data-ttu-id="53801-379">使用自訂交叉驗證 」 和 「 參數掃掠的程式碼最佳化 hello 線性迴歸模型</span><span class="sxs-lookup"><span data-stu-id="53801-379">Optimize hello linear regression model by using custom cross-validation and parameter-sweeping code</span></span>
<span data-ttu-id="53801-380">接下來，使用自訂程式碼、 最佳化 hello 模型，並使用最高精確度的 hello 準則來識別 hello 最佳模型參數。</span><span class="sxs-lookup"><span data-stu-id="53801-380">Next, optimize hello model by using custom code, and identify hello best model parameters by using hello criterion of highest accuracy.</span></span> <span data-ttu-id="53801-381">接著，建立 hello 最終模型、 評估 hello 模型測試資料和 Blob 儲存體中儲存 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="53801-381">Then, create hello final model, evaluate hello model on test data, and save hello model in Blob storage.</span></span> <span data-ttu-id="53801-382">最後，載入 hello 模型、 評分測試資料和評估精確度。</span><span class="sxs-lookup"><span data-stu-id="53801-382">Finally, load hello model, score test data, and evaluate accuracy.</span></span>

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


<span data-ttu-id="53801-383">**輸出：**</span><span class="sxs-lookup"><span data-stu-id="53801-383">**Output:**</span></span>

<span data-ttu-id="53801-384">時間 toorun hello 資料格： 61 秒。</span><span class="sxs-lookup"><span data-stu-id="53801-384">Time toorun hello cell: 61 seconds.</span></span>

## <a name="consume-spark-built-machine-learning-models-automatically-with-scala"></a><span data-ttu-id="53801-385">透過 Scala 自動取用 Spark 建置的機器學習模型</span><span class="sxs-lookup"><span data-stu-id="53801-385">Consume Spark-built machine learning models automatically with Scala</span></span>
<span data-ttu-id="53801-386">如需這些主題會逐步引導您完成組成 hello 資料科學程序，在 Azure 中的 hello 工作的概觀，請參閱[資料科學的小組流程](http://aka.ms/datascienceprocess)。</span><span class="sxs-lookup"><span data-stu-id="53801-386">For an overview of topics that walk you through hello tasks that comprise hello Data Science process in Azure, see [Team Data Science Process](http://aka.ms/datascienceprocess).</span></span>

<span data-ttu-id="53801-387">[小組資料科學程序的逐步解說](data-science-process-walkthroughs.md)描述其他端對端逐步解說示範如何針對特定案例的 hello 小組資料科學程序中的 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="53801-387">[Team Data Science Process walkthroughs](data-science-process-walkthroughs.md) describes other end-to-end walkthroughs that demonstrate hello steps in hello Team Data Science Process for specific scenarios.</span></span> <span data-ttu-id="53801-388">hello 逐步解說也說明如何 toocombine 雲端和內部部署工具和服務至工作流程或管線 toocreate 智慧型應用程式。</span><span class="sxs-lookup"><span data-stu-id="53801-388">hello walkthroughs also illustrate how toocombine cloud and on-premises tools and services into a workflow or pipeline toocreate an intelligent application.</span></span>

<span data-ttu-id="53801-389">[評分 Spark 建立機器學習模型](machine-learning-data-science-spark-model-consumption.md)示範 toouse Scala 程式碼 tooautomatically 如何載入及內建的 Spark，儲存在 Azure Blob 儲存體的機器學習模型評分新資料集。</span><span class="sxs-lookup"><span data-stu-id="53801-389">[Score Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md) shows you how toouse Scala code tooautomatically load and score new data sets with machine learning models built in Spark and saved in Azure Blob storage.</span></span> <span data-ttu-id="53801-390">您可以遵循 hello 指示，提供，並只將 hello Python 程式碼取代 Scala 自動化耗用量的這篇文章中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="53801-390">You can follow hello instructions provided there, and simply replace hello Python code with Scala code in this article for automated consumption.</span></span>

