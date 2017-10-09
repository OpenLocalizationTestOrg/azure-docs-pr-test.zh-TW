---
title: "aaa(deprecated) 機器學習 web 服務範例使用 R-Azure 建置 |Microsoft 文件"
description: "（已被取代）尋找一組實用 web 服務範例 R 程式碼與 Machine Learning 中，建立和發行 toohello Azure Marketplace。"
keywords: "csharp,r 程式碼,web 服務範例"
services: machine-learning
documentationcenter: 
author: jaymathe
manager: jhubbard
editor: cgronlun
ms.assetid: 97d66cb7-6a84-4ae9-8095-0b5f5ba82d7f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/06/2017
ms.author: jaymathe
ROBOTS: NOINDEX
redirect_url: https://gallery.cortanaintelligence.com/
redirect_document_id: True
ms.openlocfilehash: 20b074d38e65aed907d40549bb61f124cb5dfe1d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-toomicrosoft-azure-marketplace"></a><span data-ttu-id="bbeed-104">（已被取代）Web 服務使用 Azure Machine Learning 和已發行的 tooMicrosoft Azure Marketplace 上的 R 程式碼範例</span><span class="sxs-lookup"><span data-stu-id="bbeed-104">(deprecated) Web services examples using R code on Azure Machine Learning and published tooMicrosoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="bbeed-105">淘汰 hello Microsoft DataMarket，這些應用程式開發介面已被取代。</span><span class="sxs-lookup"><span data-stu-id="bbeed-105">hello Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="bbeed-106">您可以在 hello 找到許多有用的範例實驗和應用程式開發介面[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="bbeed-106">You can find many useful example experiments and APIs in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="bbeed-107">如需 hello 組件庫的詳細資訊，請參閱[共用及探索 hello Cortana 智慧組件庫中的資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="bbeed-107">For more information about hello Gallery, see [Share and discover resources in hello Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="bbeed-108">本文章中是以範例 web 服務使用 Azure Machine Learning 所建立和發行 toohello Azure Marketplace。</span><span class="sxs-lookup"><span data-stu-id="bbeed-108">In this article are example web services were created using Azure Machine Learning and published toohello Azure Marketplace.</span></span> <span data-ttu-id="bbeed-109">每個 web 服務範例具有附加，內嵌測試 hello 服務，並說明如何 hello 使用者可以建立類似服務本身的取樣資料集的完整文件。</span><span class="sxs-lookup"><span data-stu-id="bbeed-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing hello services and explaining how hello user can create a similar service themselves.</span></span> 

<span data-ttu-id="bbeed-110">在 Azure Machine Learning Studio 中，使用者可以撰寫 R 程式碼，並按幾下，將其發行為 web 服務的應用程式和裝置 tooconsume hello 世界各地。</span><span class="sxs-lookup"><span data-stu-id="bbeed-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices tooconsume around hello world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="bbeed-111">從來產生自訂的文字採礦情緒分析預測工具提供統計功能 toocreating 的簡單計算器，全新與有經驗的 R 使用者可獲得 hello 輕鬆與 Azure Machine Learning 的使用者可以實施 R程式碼。</span><span class="sxs-lookup"><span data-stu-id="bbeed-111">From producing simple calculators that provide statistical functionality toocreating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from hello ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="bbeed-112">雖然這些 web 服務無法供使用者，可能會透過行動裝置應用程式或網站，這些範例是機器學習如何可以實施的 tooshow 的 web 服務的 hello 目的 R 用於分析之指令碼和是使用的 toocreate web 服務上R 程式碼的頂端。</span><span class="sxs-lookup"><span data-stu-id="bbeed-112">While these web services could be consumed by users, potentially through a mobile app or a website, hello purpose of these web services examples is tooshow how Machine Learning can operationalize R scripts for analytical purposes and be used toocreate web services on top of R code.</span></span>

<span data-ttu-id="bbeed-113">每個範例包含取用 Web 服務的 C# 範例。</span><span class="sxs-lookup"><span data-stu-id="bbeed-113">Each example includes a C# example for web service consumption.</span></span>

![Azure Machine Learning 中的 R 程式碼的圖表： 專屬的使用或已發行的 toohello Azure Marketplace 的 R 解決方案。][1]

<span data-ttu-id="bbeed-115">請考慮下列案例的 hello。</span><span class="sxs-lookup"><span data-stu-id="bbeed-115">Consider hello following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="bbeed-116">案例 1：泛型模型</span><span class="sxs-lookup"><span data-stu-id="bbeed-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="bbeed-117">使用者會搭配一般模型可以套用的 tooa 新使用者的資料，例如基本預測的時間序列資料或自建 R 方法與進階分析。</span><span class="sxs-lookup"><span data-stu-id="bbeed-117">A user works with a generic model that can be applied tooa new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="bbeed-118">此使用者發行 hello 模型做為 web 服務，供其他人 tooconsume 其資料。</span><span class="sxs-lookup"><span data-stu-id="bbeed-118">This user publishes hello model as a web service for others tooconsume with their data.</span></span>

* [<span data-ttu-id="bbeed-119">二元分類器</span><span class="sxs-lookup"><span data-stu-id="bbeed-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="bbeed-120">叢集模型</span><span class="sxs-lookup"><span data-stu-id="bbeed-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="bbeed-121">多變量線性迴歸</span><span class="sxs-lookup"><span data-stu-id="bbeed-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="bbeed-122">預測 - 指數平滑法</span><span class="sxs-lookup"><span data-stu-id="bbeed-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="bbeed-123">ETS + STL 預測</span><span class="sxs-lookup"><span data-stu-id="bbeed-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="bbeed-124">預測 - 自動迴歸整合式移動平均 (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="bbeed-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="bbeed-125">存活分析</span><span class="sxs-lookup"><span data-stu-id="bbeed-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="bbeed-126">案例 2：定型模型 - 特定資料</span><span class="sxs-lookup"><span data-stu-id="bbeed-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="bbeed-127">使用者具有提供有用的預測執行 R 程式碼，例如特質問卷大型範例叢集透過的 k-means 演算法 toopredict hello 使用者的特質類型，或健全狀況問卷資料可能是使用的 toopredict 個別的資料lung cancer 求生分析 R 封裝的風險。</span><span class="sxs-lookup"><span data-stu-id="bbeed-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm toopredict hello user’s personality type, or health survey data that can be used toopredict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="bbeed-128">hello 使用者發行 hello 資料透過 web 服務來預測新使用者的結果。</span><span class="sxs-lookup"><span data-stu-id="bbeed-128">hello user publishes hello data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="bbeed-129">案例 3：定型模型 - 泛型資料</span><span class="sxs-lookup"><span data-stu-id="bbeed-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="bbeed-130">使用者具有泛用資料 （例如文字主體分類），可讓 web 服務 toobe 建立和套用以一般方式跨不同類型的使用案例和案例。</span><span class="sxs-lookup"><span data-stu-id="bbeed-130">A user has generic data (such as a text corpus) that allows a web service toobe built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="bbeed-131">語彙型情感分析</span><span class="sxs-lookup"><span data-stu-id="bbeed-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="bbeed-132">案例 4：進階計算機</span><span class="sxs-lookup"><span data-stu-id="bbeed-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="bbeed-133">使用者提供進階的計算或模擬不需要任何定型的模型或模型 toohello 使用者的資料調整。</span><span class="sxs-lookup"><span data-stu-id="bbeed-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model toohello user’s data.</span></span>

* [<span data-ttu-id="bbeed-134">比例差異測試</span><span class="sxs-lookup"><span data-stu-id="bbeed-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="bbeed-135">常態分佈套件</span><span class="sxs-lookup"><span data-stu-id="bbeed-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="bbeed-136">二項分配套件</span><span class="sxs-lookup"><span data-stu-id="bbeed-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="bbeed-137">常見問題集</span><span class="sxs-lookup"><span data-stu-id="bbeed-137">FAQ</span></span>
<span data-ttu-id="bbeed-138">常見問題集 hello web 服務或發行 toohello Marketplace 耗用量問題，請參閱[這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="bbeed-138">For frequently asked questions on consumption of hello web service or publishing toohello Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



