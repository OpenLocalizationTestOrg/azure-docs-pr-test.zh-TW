---
title: "aaaHDInsight Hadoop 資料科學逐步解說在 Azure 上使用 Hive |Microsoft 文件"
description: "Hello 小組資料科學程序的逐步解說的 Hive hello 使用 Azure HDInsight Hadoop toodo 預測分析的範例。"
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
ms.openlocfilehash: 77efbe4ea6377f309987849d9f44e8b2b859ae9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="hdinsight-hadoop-data-science-walkthroughs-using-hive-on-azure"></a><span data-ttu-id="82b16-103">在 Azure 上使用 Hive 的 HDInsight Hadoop 資料科學逐步解說</span><span class="sxs-lookup"><span data-stu-id="82b16-103">HDInsight Hadoop data science walkthroughs using Hive on Azure</span></span> 

<span data-ttu-id="82b16-104">這些逐步解說會使用 HDInsight Hadoop 叢集 toodo 預測性分析登錄區。</span><span class="sxs-lookup"><span data-stu-id="82b16-104">These walkthroughs use Hive with an HDInsight Hadoop cluster toodo predictive analytics.</span></span> <span data-ttu-id="82b16-105">它們遵循下列 hello hello 小組資料科學程序中所述的步驟。</span><span class="sxs-lookup"><span data-stu-id="82b16-105">They follow hello steps outlined in hello Team Data Science Process.</span></span> <span data-ttu-id="82b16-106">如需 hello 小組資料科學程序的概觀，請參閱[資料科學程序](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="82b16-106">For an overview of hello Team Data Science Process, see [Data Science Process](data-science-process-overview.md).</span></span> <span data-ttu-id="82b16-107">如簡介 tooAzure HDInsight，請參閱[簡介 tooAzure HDInsight hello Hadoop 技術堆疊和 Hadoop 叢集](../hdinsight/hdinsight-hadoop-introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="82b16-107">For an introduction tooAzure HDInsight, see [Introduction tooAzure HDInsight, hello Hadoop technology stack, and Hadoop clusters](../hdinsight/hdinsight-hadoop-introduction.md).</span></span>

<span data-ttu-id="82b16-108">執行 hello 資料科學的小組流程的其他資料科學逐步解說會依照 hello**平台**它們使用：</span><span class="sxs-lookup"><span data-stu-id="82b16-108">Additional data science walkthroughs that execute hello Team Data Science Process are grouped by hello **platform** that they use:</span></span> 

[!INCLUDE [tdsp-walkthroughs-by-platform](../../includes/tdsp-walkthroughs-by-platform.md)]


## <a name="predict-taxi-tips-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="82b16-109">使用 Hive 搭配 HDInsight Hadoop 來預測計程車小費</span><span class="sxs-lookup"><span data-stu-id="82b16-109">Predict taxi tips using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="82b16-110">hello[使用 HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-walkthrough.md)逐步解說會使用從紐約 taxis toopredict 資料：</span><span class="sxs-lookup"><span data-stu-id="82b16-110">hello [Use HDInsight Hadoop clusters](machine-learning-data-science-process-hive-walkthrough.md) walkthrough uses data from New York taxis toopredict:</span></span> 

- <span data-ttu-id="82b16-111">是否給予小費</span><span class="sxs-lookup"><span data-stu-id="82b16-111">Whether a tip is paid</span></span> 
- <span data-ttu-id="82b16-112">提示數量的 hello 分佈</span><span class="sxs-lookup"><span data-stu-id="82b16-112">hello distribution of tip amounts</span></span>

<span data-ttu-id="82b16-113">使用 Hive 與實作 hello 案例[Azure HDInsight Hadoop 叢集](https://azure.microsoft.com/services/hdinsight/)。</span><span class="sxs-lookup"><span data-stu-id="82b16-113">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/).</span></span> <span data-ttu-id="82b16-114">您了解 toostore，瀏覽和功能從公開可用的 NYC 計程車路線工程資料及再見資料集的方式。</span><span class="sxs-lookup"><span data-stu-id="82b16-114">You learn how toostore, explore, and feature engineer data from a publicly available NYC taxi trip and fare dataset.</span></span> <span data-ttu-id="82b16-115">您也會使用 Azure Machine Learning toobuild，並將部署 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="82b16-115">You also use Azure Machine Learning toobuild and deploy hello models.</span></span>

## <a name="predict-advertisement-clicks-using-hive-with-hdinsight-hadoop"></a><span data-ttu-id="82b16-116">使用 Hive 搭配 HDInsight Hadoop 來預測廣告點擊數</span><span class="sxs-lookup"><span data-stu-id="82b16-116">Predict advertisement clicks using Hive with HDInsight Hadoop</span></span>

<span data-ttu-id="82b16-117">hello [1 TB 的資料集上使用 Azure HDInsight Hadoop 叢集](machine-learning-data-science-process-hive-criteo-walkthrough.md)逐步解說會使用可公開使用[Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/)按一下資料集 toopredict 是否秘訣付費和 hello 量預期的範圍。</span><span class="sxs-lookup"><span data-stu-id="82b16-117">hello [Use Azure HDInsight Hadoop Clusters on a 1-TB dataset](machine-learning-data-science-process-hive-criteo-walkthrough.md) walkthrough uses a publicly available [Criteo](http://labs.criteo.com/downloads/download-terabyte-click-logs/) click dataset toopredict whether a tip is paid and hello range of amounts expected.</span></span> <span data-ttu-id="82b16-118">使用 Hive 與實作 hello 案例[Azure HDInsight Hadoop 叢集](https://azure.microsoft.com/services/hdinsight/)toostore，瀏覽、 功能工程師編寫，並向下範例資料。</span><span class="sxs-lookup"><span data-stu-id="82b16-118">hello scenario is implemented using Hive with an [Azure HDInsight Hadoop cluster](https://azure.microsoft.com/services/hdinsight/) toostore, explore, feature engineer, and down sample data.</span></span> <span data-ttu-id="82b16-119">它會使用 Azure Machine Learning toobuild、 定型和計分二元分類模型預測是否在使用者按一下廣告。</span><span class="sxs-lookup"><span data-stu-id="82b16-119">It uses Azure Machine Learning toobuild, train, and score a binary classification model predicting whether a user clicks on an advertisement.</span></span> <span data-ttu-id="82b16-120">hello 逐步解說結束時，顯示如何 toopublish 下列其中一種模型做為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="82b16-120">hello walkthrough concludes showing how toopublish one of these models as a Web service.</span></span>


## <a name="next-steps"></a><span data-ttu-id="82b16-121">後續步驟</span><span class="sxs-lookup"><span data-stu-id="82b16-121">Next steps</span></span>

<span data-ttu-id="82b16-122">Hello 主要元件組成 hello 資料科學的小組流程的討論，請參閱[小組資料科學程序概觀](data-science-process-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="82b16-122">For a discussion of hello key components that comprise hello Team Data Science Process, see [Team Data Science Process overview](data-science-process-overview.md).</span></span>

<span data-ttu-id="82b16-123">如需您可以使用 toostructure hello 小組資料科學程序生命週期的討論資料科學專案，請參閱[小組資料科學程序生命週期](data-science-process-lifecycle.md)。</span><span class="sxs-lookup"><span data-stu-id="82b16-123">For a discussion of hello Team Data Science Process lifecycle that you can use toostructure your data science projects, see [Team Data Science Process lifecycle](data-science-process-lifecycle.md).</span></span> <span data-ttu-id="82b16-124">hello 生命週期概述 hello 步驟，從開始 toofinish 專案通常會遵循在執行時。</span><span class="sxs-lookup"><span data-stu-id="82b16-124">hello lifecycle outlines hello steps, from start toofinish, that projects usually follow when they are executed.</span></span> 

