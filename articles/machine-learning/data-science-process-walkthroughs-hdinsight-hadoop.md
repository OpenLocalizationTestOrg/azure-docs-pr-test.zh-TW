---
title: "在 Azure 上使用 Hive 的 HDInsight Hadoop 資料科學逐步解說 | Microsoft Docs"
description: "以 Team Data Science Process 為例，逐步解說如何在 Azure HDInsight Hadoop 上使用 Hive 來執行預測性分析。"
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
ms.openlocfilehash: fb06c3c1b1ae30d970a2e4d45a49e22e9d78b876
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="164be-103">在 Azure 上使用 Hive 的 HDInsight Hadoop 資料科學逐步解說</span><span class="sxs-lookup"><span data-stu-id="164be-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="164be-104">這些逐步解說會使用 Hive 搭配 HDInsight Hadoop 叢集來執行預測性分析。</span><span class="sxs-lookup"><span data-stu-id="164be-104">These walkthroughs use Hive with an HDInsight Hadoop cluster to do predictive analytics.</span></span> <span data-ttu-id="164be-105">其遵循 Team Data Science Process 中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="164be-105">They follow the steps outlined in the Team Data Science Process.</span></span> <span data-ttu-id="164be-106">如需 Team Data Science Process 的概觀，請參閱 [Data Science Process](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="164be-106">For an overview of the Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="164be-107">如需 Azure HDInsight 的簡介，請參閱 [Azure HDInsight、Hadoop 技術堆疊和 Hadoop 叢集簡介](../hdinsight/hdinsight-hadoop-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="164be-107">For an introduction to Azure HDInsight, see [Introduction to Azure HDInsight, the Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="164be-108">執行 Team Data Science Process 的其他資料科學逐步解說是依據它們使用的**平台**來歸納整理：</span><span class="sxs-lookup"><span data-stu-id="164be-108">Additional data science walkthroughs that execute the Team Data Science Process are grouped by the **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="164be-109">使用 Hive 搭配 HDInsight Hadoop 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="164be-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="164be-110">[使用 HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-walkthrough.md)逐步解說會使用紐約計程車行的資料來預測：</span><span class="sxs-lookup"><span data-stu-id="164be-110">The [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis to predict:</span></span> 

- <span data-ttu-id="164be-111">是否給予小費</span><span class="sxs-lookup"><span data-stu-id="164be-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="164be-112">小費金額的分佈</span><span class="sxs-lookup"><span data-stu-id="164be-112">The distribution of tip amounts</span></span>

<span data-ttu-id="164be-113">此案例是透過 Hive 搭配 [Azure HDInsight Hadoop 叢集](https://azure.microsoft.com/services/hdinsight/)來實作。</span><span class="sxs-lookup"><span data-stu-id="164be-113">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="164be-114">您將了解如何對公開使用之 NYC 計程車車程和車資資料集中的資料，進行儲存、探索及特性工程設計。</span><span class="sxs-lookup"><span data-stu-id="164be-114">You learn how to store, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="164be-115">您也可以使用 Azure Machine Learning 來建置及部署模型。</span><span class="sxs-lookup"><span data-stu-id="164be-115">You also use Azure Machine Learning to build and deploy the models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="164be-116">使用 Hive 搭配 HDInsight Hadoop 來預測廣告點擊數</span><span class="sxs-lookup"><span data-stu-id="164be-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="164be-117">[在 1 TB 資料集上使用 Azure HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-criteo-walkthrough.md)逐步解說會使用公開使用的 [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) 點擊資料集，來預測是否給予小費及預期的金額範圍。</span><span class="sxs-lookup"><span data-stu-id="164be-117">The [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset to predict whether a tip is paid and the range of amounts expected.</span></span> <span data-ttu-id="164be-118">此案例是透過 Hive 搭配 [Azure HDInsight Hadoop 叢集](https://azure.microsoft.com/services/hdinsight/)來實作，以對資料進行儲存、探索、特性工程設計及縮減取樣。</span><span class="sxs-lookup"><span data-stu-id="164be-118">The scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) to store, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="164be-119">它使用 Azure Machine Learning 來建立、定型二元分類模型並對其進行評分，以預測使用者是否點擊廣告。</span><span class="sxs-lookup"><span data-stu-id="164be-119">It uses Azure Machine Learning to build, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="164be-120">此逐步解說最後會示範如何將其中一個模型發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="164be-120">The walkthrough concludes showing how to publish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="164be-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="164be-121">Next steps</span></span>

<span data-ttu-id="164be-122">如需組成 Team Data Science Process 之主要元件的討論，請參閱 [Team Data Science Process 概觀](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="164be-122">For a discussion of the key components that comprise the Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="164be-123">如需您可以用來結構化資料科學專案之 Team Data Science Process 生命週期的討論，請參閱 [Team Data Science Process 生命週期](data-science-process-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="164be-123">For a discussion of the Team Data Science Process lifecycle that you can use to structure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="164be-124">生命週期會概述專案在執行時通常會遵循之從開始到完成的步驟。</span><span class="sxs-lookup"><span data-stu-id="164be-124">The lifecycle outlines the steps, from start to finish, that projects usually follow when they are executed.</span></span> 

