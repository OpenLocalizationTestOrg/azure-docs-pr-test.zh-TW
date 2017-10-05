---
title: "在 Azure 上使用 PySpark 和 Scala 的 HDInsight Spark 逐步解說 | Microsoft Docs"
description: "以 Team Data Science Process 為例，逐步解說如何在 Azure HDInsight Spark 上使用 PySpark 和 Scala 來執行預測性分析。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev
ms.openlocfilehash: 27065c3437c4617ed035623b48aa1a1a31a7094f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a><span data-ttu-id="f962c-103">在 Azure 上使用 PySpark 和 Scala 的 HDInsight Spark 資料科學逐步解說</span><span class="sxs-lookup"><span data-stu-id="f962c-103">HDInsight Spark data science walkthroughs using PySpark and Scala on Azure</span></span>

<span data-ttu-id="f962c-104">這些逐步解說會在 Azure Spark 叢集上使用 PySpark 和 Scala 來執行預測性分析。</span><span class="sxs-lookup"><span data-stu-id="f962c-104">These walkthroughs use PySpark and Scala on an Azure Spark cluster to do predictive analytics.</span></span> <span data-ttu-id="f962c-105">其遵循 Team Data Science Process 中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="f962c-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="f962c-106">如需 Team Data Science Process 的概觀，請參閱 [Data Science Process](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f962c-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="f962c-107">如需 Spark on HDInsight 的概觀，請參閱 [Spark on HDInsight 簡介](../hdinsight/hdinsight-apache-spark-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f962c-107">For an overview of Spark on HDInsight, see [Introduction to Spark on HDInsight](../hdinsight/hdinsight-apache-spark-overview.md).</span></span>

<span data-ttu-id="f962c-108">執行 Team Data Science Process 的其他資料科學逐步解說是依據它們使用的**平台**歸納整理：</span><span class="sxs-lookup"><span data-stu-id="f962c-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a><span data-ttu-id="f962c-109">在 Azure Spark 上使用 PySpark 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="f962c-109">Predict taxi tips using PySpark on Azure Spark</span></span>

<span data-ttu-id="f962c-110">[在 Azure HDInsight 上使用 Spark](machine-learning-data-science-spark-overview.md) 逐步解說會使用紐約計程車的資料來預測乘客是否會付小費，以及預期會給予的金額範圍。</span><span class="sxs-lookup"><span data-stu-id="f962c-110">The [Use Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) walkthrough uses data from New York taxis to predict whether a tip is paid and the range of amounts expected to be paid.</span></span> <span data-ttu-id="f962c-111">它會在採用 [Azure HDInsight Spark 叢集](https://azure.microsoft.com/services/hdinsight/)的案例中使用 Team Data Science Process，以對公開提供使用的 NYC 計程車車程和車資資料集的資料進行儲存、探索和特徵工程設計。</span><span class="sxs-lookup"><span data-stu-id="f962c-111">It uses the Team Data Science Process in a scenario using an [Azure HDInsight Spark cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, and feature engineer data from the publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="f962c-112">此概觀主題會為您設定本逐步解說的其餘部分所使用的 HDInsight Spark 叢集和 Jupyter PySpark Notebook。</span><span class="sxs-lookup"><span data-stu-id="f962c-112">This overview topic sets you up with an HDInsight Spark cluster and the Jupyter  PySpark notebooks used in the rest of the walkthrough.</span></span> <span data-ttu-id="f962c-113">這些 Notebook 會示範如何瀏覽資料、建立和取用模型。</span><span class="sxs-lookup"><span data-stu-id="f962c-113">These notebooks show you how to explore your data and then how to create and consume models.</span></span> <span data-ttu-id="f962c-114">進階的資料探索和模型化 Notebook 顯示如何包括交叉驗證、超參數清除和模型評估。</span><span class="sxs-lookup"><span data-stu-id="f962c-114">The advanced data exploration and modeling notebook shows how to include cross-validation, hyper-parameter sweeping, and model evaluation.</span></span>

### <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="f962c-115">使用 Spark 進行資料探索和模型化</span><span class="sxs-lookup"><span data-stu-id="f962c-115">Data Exploration and modeling with Spark</span></span> 
<span data-ttu-id="f962c-116">遵循[使用 Spark MLlib 工具組來建立資料的二進位分類和迴歸模型](machine-learning-data-science-spark-data-exploration-modeling.md)主題的內容，來探索資料集，以及建立、評分、評估 Machine Learning 模型。</span><span class="sxs-lookup"><span data-stu-id="f962c-116">Explore the dataset and create, score, and evaluate the machine learning models by working through the [Create binary classification and regression models for data with the Spark MLlib toolkit](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span>

### <a name="model-consumption"></a><span data-ttu-id="f962c-117">模型耗用量</span><span class="sxs-lookup"><span data-stu-id="f962c-117">Model consumption</span></span>
<span data-ttu-id="f962c-118">若要瞭解如何評分本主題中所建立的分類和迴歸模型，請參閱[評分及評估 Spark 建置機器學習服務模型](machine-learning-data-science-spark-model-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="f962c-118">To learn how to score the classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

### <a name="cross-validation-and-hyperparameter-sweeping"></a><span data-ttu-id="f962c-119">交叉驗證和超參數掃掠</span><span class="sxs-lookup"><span data-stu-id="f962c-119">Cross-validation and hyperparameter sweeping</span></span>
<span data-ttu-id="f962c-120">如需如何使用交叉驗證和超參數掃掠訓練模型的相關資訊，請參閱[使用 Spark 進階資料探索和模型化](machine-learning-data-science-spark-advanced-data-exploration-modeling.md)。</span><span class="sxs-lookup"><span data-stu-id="f962c-120">See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a><span data-ttu-id="f962c-121">在 Azure Spark 上使用 Scala 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="f962c-121">Predict taxi tips using Scala on Azure Spark</span></span>

<span data-ttu-id="f962c-122">[在 Azure 上使用 Scala 與 Spark](machine-learning-data-science-process-scala-walkthrough.md) 逐步解說會使用紐約計程車的資料來預測乘客是否會付小費，以及預期會給予的金額範圍。</span><span class="sxs-lookup"><span data-stu-id="f962c-122">The [Use Scala with Spark on Azure](machine-learning-data-science-process-scala-walkthrough.md) walkthrough uses data from New York taxis to predict whether a tip is paid and the range of amounts expected to be paid.</span></span> <span data-ttu-id="f962c-123">它會說明如何使用 Scala 搭配 Spark 機器學習程式庫 (MLlib) 和 Azure HDInsight Spark 叢集上的 SparkML 套件，處理受監督的機器學習工作。</span><span class="sxs-lookup"><span data-stu-id="f962c-123">It shows how to use Scala for supervised machine learning tasks with the Spark machine learning library (MLlib) and SparkML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="f962c-124">它會引導您進行構成 [資料科學程序](http://aka.ms/datascienceprocess)的各項工作︰資料擷取和探索、視覺化、特徵設計、模型化和模型取用。</span><span class="sxs-lookup"><span data-stu-id="f962c-124">It walks you through the tasks that constitute the [Data Science Process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="f962c-125">建立的模型包括羅吉斯和線性迴歸、隨機樹系和漸層停駐推進式決策樹。</span><span class="sxs-lookup"><span data-stu-id="f962c-125">The models built include logistic and linear regression, random forests, and gradient boosted trees.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f962c-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f962c-126">Next steps</span></span>

<span data-ttu-id="f962c-127">如需組成 Team Data Science Process 之主要元件的討論，請參閱 [Team Data Science Process 概觀](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f962c-127">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="f962c-128">如需您可以用來結構化資料科學專案之 Team Data Science Process 生命週期的討論，請參閱 [Team Data Science Process 生命週期](data-science-process-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="f962c-128">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="f962c-129">生命週期會概述專案在執行時通常會遵循之從開始到完成的步驟。</span><span class="sxs-lookup"><span data-stu-id="f962c-129">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 

