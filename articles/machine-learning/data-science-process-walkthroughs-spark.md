---
title: "在 Azure 上使用 PySpark 和 Scala aaaHDInsight Spark 逐步解說 |Microsoft 文件"
description: "逐步解說 hello hello 小組資料科學程序的範例使用 PySpark 和 Scala Azure HDInsight Spark toodo 預測分析。"
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
ms.openlocfilehash: f8b41a8cae414586570761ba4b4eb4c239cbb981
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-spark-data-science-walkthroughs-using-pyspark-and-scala-on-azure"></a><span data-ttu-id="d049f-103">在 Azure 上使用 PySpark 和 Scala 的 HDInsight Spark 資料科學逐步解說</span><span class="sxs-lookup"><span data-stu-id="d049f-103">HDInsight Spark data science walkthroughs using PySpark and Scala on Azure</span></span>

<span data-ttu-id="d049f-104">這些逐步解說會使用 PySpark 和 Scala Azure Spark 叢集 toodo 預測分析。</span><span class="sxs-lookup"><span data-stu-id="d049f-104">These walkthroughs use PySpark and Scala on an Azure Spark cluster toodo predictive analytics.</span></span> <span data-ttu-id="d049f-105">它們遵循下列 hello hello 小組資料科學程序中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="d049f-105">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="d049f-106">如需 hello 小組資料科學程序的概觀，請參閱[資料科學程序](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d049f-106">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="d049f-107">如需 HDInsight 上的 Spark 的概觀，請參閱[HDInsight 上的簡介 tooSpark](../hdinsight/hdinsight-apache-spark-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d049f-107">For an overview of Spark on HDInsight, see [Introduction tooSpark on HDInsight](../hdinsight/hdinsight-apache-spark-overview.md).</span></span>

<span data-ttu-id="d049f-108">執行 hello 資料科學的小組流程的其他資料科學逐步解說會依照 hello**平台**它們使用：</span><span class="sxs-lookup"><span data-stu-id="d049f-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]

## <a name="predict-taxi-tips-using-pyspark-on-azure-spark"></a><span data-ttu-id="d049f-109">在 Azure Spark 上使用 PySpark 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="d049f-109">Predict taxi tips using PySpark on Azure Spark</span></span>

<span data-ttu-id="d049f-110">hello[使用 Azure HDInsight 上的 Spark](machine-learning-data-science-spark-overview.md)逐步解說會使用從紐約 taxis toopredict 資料是否付費的秘訣和金額的 hello 範圍應 toobe 付費。</span><span class="sxs-lookup"><span data-stu-id="d049f-110">hello [Use Spark on Azure HDInsight](machine-learning-data-science-spark-overview.md) walkthrough uses data from New York taxis toopredict whether a tip is paid and hello range of amounts expected toobe paid.</span></span> <span data-ttu-id="d049f-111">它會使用案例，使用中的 hello 資料科學的小組流程[Azure HDInsight Spark 叢集](https://azure.microsoft.com/services/hdinsight/)toostore，瀏覽和功能從 hello 公開可用 NYC 計程車路線工程資料及再見資料集。</span><span class="sxs-lookup"><span data-stu-id="d049f-111">It uses hello Team Data Science Process in a scenario using an [Azure HDInsight Spark cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, and feature engineer data from hello publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="d049f-112">這個概觀主題會設定您 HDInsight Spark 叢集與 hello Jupyter PySpark 筆記本中的 hello 逐步解說的 hello 其餘部分使用。</span><span class="sxs-lookup"><span data-stu-id="d049f-112">This overview topic sets you up with an HDInsight Spark cluster and hello Jupyter  PySpark notebooks used in hello rest of hello walkthrough.</span></span> <span data-ttu-id="d049f-113">這些筆記本告訴您如何 tooexplore 您的資料，然後如何 toocreate 和取用模型。</span><span class="sxs-lookup"><span data-stu-id="d049f-113">These notebooks show you how tooexplore your data and then how toocreate and consume models.</span></span> <span data-ttu-id="d049f-114">進階資料瀏覽以及如何模型化筆記本顯示 hello tooinclude 交叉驗證，超參數牽涉和模型評估。</span><span class="sxs-lookup"><span data-stu-id="d049f-114">hello advanced data exploration and modeling notebook shows how tooinclude cross-validation, hyper-parameter sweeping, and model evaluation.</span></span>

### <a name="data-exploration-and-modeling-with-spark"></a><span data-ttu-id="d049f-115">使用 Spark 進行資料探索和模型化</span><span class="sxs-lookup"><span data-stu-id="d049f-115">Data Exploration and modeling with Spark</span></span> 
<span data-ttu-id="d049f-116">瀏覽 hello 資料集以及建立、 計分，和透過 hello 工作來評估 hello 機器學習模型[建立資料的二元分類和迴歸模型使用 hello Spark MLlib toolkit](machine-learning-data-science-spark-data-exploration-modeling.md)主題。</span><span class="sxs-lookup"><span data-stu-id="d049f-116">Explore hello dataset and create, score, and evaluate hello machine learning models by working through hello [Create binary classification and regression models for data with hello Spark MLlib toolkit](machine-learning-data-science-spark-data-exploration-modeling.md) topic.</span></span>

### <a name="model-consumption"></a><span data-ttu-id="d049f-117">模型耗用量</span><span class="sxs-lookup"><span data-stu-id="d049f-117">Model consumption</span></span>
<span data-ttu-id="d049f-118">toolearn 如何 tooscore hello 分類和迴歸模型建立本主題中，請參閱[分數及評估 Spark 建立機器學習模型](machine-learning-data-science-spark-model-consumption.md)。</span><span class="sxs-lookup"><span data-stu-id="d049f-118">toolearn how tooscore hello classification and regression models created in this topic, see [Score and evaluate Spark-built machine learning models](machine-learning-data-science-spark-model-consumption.md).</span></span>

### <a name="cross-validation-and-hyperparameter-sweeping"></a><span data-ttu-id="d049f-119">交叉驗證和超參數掃掠</span><span class="sxs-lookup"><span data-stu-id="d049f-119">Cross-validation and hyperparameter sweeping</span></span>
<span data-ttu-id="d049f-120">如需如何使用交叉驗證和超參數掃掠訓練模型的相關資訊，請參閱[使用 Spark 進階資料探索和模型化](machine-learning-data-science-spark-advanced-data-exploration-modeling.md)。</span><span class="sxs-lookup"><span data-stu-id="d049f-120">See [Advanced data exploration and modeling with Spark](machine-learning-data-science-spark-advanced-data-exploration-modeling.md) on how models can be trained using cross-validation and hyper-parameter sweeping.</span></span>


## <a name="predict-taxi-tips-using-scala-on-azure-spark"></a><span data-ttu-id="d049f-121">在 Azure Spark 上使用 Scala 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="d049f-121">Predict taxi tips using Scala on Azure Spark</span></span>

<span data-ttu-id="d049f-122">hello[與 Azure 上的 Spark 使用 Scala](machine-learning-data-science-process-scala-walkthrough.md)逐步解說會使用從紐約 taxis toopredict 資料是否付費的秘訣和金額的 hello 範圍應 toobe 付費。</span><span class="sxs-lookup"><span data-stu-id="d049f-122">hello [Use Scala with Spark on Azure](machine-learning-data-science-process-scala-walkthrough.md) walkthrough uses data from New York taxis toopredict whether a tip is paid and hello range of amounts expected toobe paid.</span></span> <span data-ttu-id="d049f-123">它會顯示為受監督的機器學習工作 hello Spark 機器學習程式庫 (MLlib) 與 SparkML toouse Scala Azure HDInsight Spark 叢集上的封裝。</span><span class="sxs-lookup"><span data-stu-id="d049f-123">It shows how toouse Scala for supervised machine learning tasks with hello Spark machine learning library (MLlib) and SparkML packages on an Azure HDInsight Spark cluster.</span></span> <span data-ttu-id="d049f-124">它會引導您完成 hello 工作構成 hello[資料科學程序](http://aka.ms/datascienceprocess)： 擷取資料並探索、 視覺效果、 功能工程、 模型和模型耗用量。</span><span class="sxs-lookup"><span data-stu-id="d049f-124">It walks you through hello tasks that constitute hello [Data Science Process](http://aka.ms/datascienceprocess): data ingestion and exploration, visualization, feature engineering, modeling, and model consumption.</span></span> <span data-ttu-id="d049f-125">內建的 hello 模型包括羅吉斯和線性迴歸、 隨機樹系和梯度促進式樹狀結構。</span><span class="sxs-lookup"><span data-stu-id="d049f-125">hello models built include logistic and linear regression, random forests, and gradient boosted trees.</span></span>


## <a name="next-steps"></a><span data-ttu-id="d049f-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d049f-126">Next steps</span></span>

<span data-ttu-id="d049f-127">Hello 主要元件組成 hello 資料科學的小組流程的討論，請參閱[小組資料科學程序概觀](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d049f-127">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="d049f-128">如需您可以使用 toostructure hello 小組資料科學程序生命週期的討論資料科學專案，請參閱[小組資料科學程序生命週期](data-science-process-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="d049f-128">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="d049f-129">hello 生命週期概述 hello 步驟，從開始 toofinish 專案通常會遵循在執行時。</span><span class="sxs-lookup"><span data-stu-id="d049f-129">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

