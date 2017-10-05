---
title: "(已過時) 以 R 建置的 Machine Learning Web 服務範例 - Azure | Microsoft Docs"
description: "(已過時) 尋找以 R 程式碼和 Machine Learning 建立並發佈至 Azure Marketplace 的一組實用 Web 服務範例。"
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
redirect_document_id: TRUE
ms.openlocfilehash: 9514025db6f812f9e7934ea2d1575e948d6585b0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="deprecated-web-services-examples-using-r-code-on-azure-machine-learning-and-published-to-microsoft-azure-marketplace"></a><span data-ttu-id="268ee-104">(已過時) 使用 R 程式碼在 Azure Machine Learning 上建置並發佈至 Microsoft Azure Marketplace 的 Web 服務範例</span><span class="sxs-lookup"><span data-stu-id="268ee-104">(deprecated) Web services examples using R code on Azure Machine Learning and published to Microsoft Azure Marketplace</span></span>

> [!NOTE]
> <span data-ttu-id="268ee-105">Microsoft DataMarket 已進入淘汰階段，而這些 API 已被取代。</span><span class="sxs-lookup"><span data-stu-id="268ee-105">The Microsoft DataMarket is being retired and these APIs have been deprecated.</span></span> 
> 
> <span data-ttu-id="268ee-106">您可以在 [Cortana Intelligence 資源庫](http://gallery.cortanaintelligence.com)中找到許多實用的範例實驗和 API。</span><span class="sxs-lookup"><span data-stu-id="268ee-106">You can find many useful example experiments and APIs in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="268ee-107">如需有關「資源庫」的詳細資訊，請參閱[在 Cortana Intelligence 資源庫中共用及探索資源](machine-learning-gallery-how-to-use-contribute-publish.md)。</span><span class="sxs-lookup"><span data-stu-id="268ee-107">For more information about the Gallery, see [Share and discover resources in the Cortana Intelligence Gallery](machine-learning-gallery-how-to-use-contribute-publish.md).</span></span>

<span data-ttu-id="268ee-108">本文提供使用 Azure Machine Learning 建立並發佈至 Azure Marketplace 的範例 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="268ee-108">In this article are example web services were created using Azure Machine Learning and published to the Azure Marketplace.</span></span> <span data-ttu-id="268ee-109">每個 Web 服務範例都附加完整的文件、內嵌可用於測試服務的樣本資料集，並說明使用者如何自行建立類似的服務。</span><span class="sxs-lookup"><span data-stu-id="268ee-109">Each web service example has a comprehensive document attached, embedding sample data sets for testing the services and explaining how the user can create a similar service themselves.</span></span> 

<span data-ttu-id="268ee-110">在 Azure Machine Learning Studio 中，使用者可以撰寫 R 程式碼，而且只要按幾下，就可以將其發佈為 Web 服務，以供世界各地的應用程式和裝置取用。</span><span class="sxs-lookup"><span data-stu-id="268ee-110">In Azure Machine Learning Studio, users can write R code and with a few clicks, publish it as a web service for applications and devices to consume around the world.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="268ee-111">從產生可提供統計功能的簡單計算機，到建立自訂文字採礦情感分析預測工具，由於 Azure Machine Learning 的使用者可輕鬆操作 R 程式碼，因此不論是剛接觸 R 的使用者，或是有經驗的使用者都可以從中獲益。</span><span class="sxs-lookup"><span data-stu-id="268ee-111">From producing simple calculators that provide statistical functionality to creating a custom text-mining sentiment analysis predictor, both new and experienced R users can benefit from the ease with which users of Azure Machine Learning can operationalize R code.</span></span> <span data-ttu-id="268ee-112">使用者可透過行動裝置應用程式或網站，來取用這些 Web 服務；不過，這些 Web 服務範例也可用來示範 Machine Learning 如何操作 R 指令碼進行分析，以及如何使用 Machine Learning，來建立採用 R 程式碼的 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="268ee-112">While these web services could be consumed by users, potentially through a mobile app or a website, the purpose of these web services examples is to show how Machine Learning can operationalize R scripts for analytical purposes and be used to create web services on top of R code.</span></span>

<span data-ttu-id="268ee-113">每個範例包含取用 Web 服務的 C# 範例。</span><span class="sxs-lookup"><span data-stu-id="268ee-113">Each example includes a C# example for web service consumption.</span></span>

![Azure Machine Learning 中的 R 程式碼圖表：獨佔使用 R 解決方案，或發佈至 Azure Marketplace。][1]

<span data-ttu-id="268ee-115">請考慮下列案例。</span><span class="sxs-lookup"><span data-stu-id="268ee-115">Consider the following scenarios.</span></span>

## <a name="scenario-1-generic-model"></a><span data-ttu-id="268ee-116">案例 1：泛型模型</span><span class="sxs-lookup"><span data-stu-id="268ee-116">Scenario 1: Generic model</span></span>
<span data-ttu-id="268ee-117">使用者會使用可套用至新使用者資料的泛型模型，例如時間序列資料的基本預測或具備進階分析的自建 R 方法。</span><span class="sxs-lookup"><span data-stu-id="268ee-117">A user works with a generic model that can be applied to a new user’s data, such as a basic forecasting of time series data or a custom-built R method with advanced analytics.</span></span> <span data-ttu-id="268ee-118">此使用者會將此模型發行為一項 Web 服務，以便他人取用其資料。</span><span class="sxs-lookup"><span data-stu-id="268ee-118">This user publishes the model as a web service for others to consume with their data.</span></span>

* [<span data-ttu-id="268ee-119">二元分類器</span><span class="sxs-lookup"><span data-stu-id="268ee-119">Binary Classifier</span></span>](machine-learning-r-csharp-binary-classifier.md)
* [<span data-ttu-id="268ee-120">叢集模型</span><span class="sxs-lookup"><span data-stu-id="268ee-120">Cluster Model</span></span>](machine-learning-r-csharp-cluster-model.md)
* [<span data-ttu-id="268ee-121">多變量線性迴歸</span><span class="sxs-lookup"><span data-stu-id="268ee-121">Multivariate Linear Regression</span></span>](machine-learning-r-csharp-multivariate-linear-regression.md)
* [<span data-ttu-id="268ee-122">預測 - 指數平滑法</span><span class="sxs-lookup"><span data-stu-id="268ee-122">Forecasting - Exponential Smoothing</span></span>](machine-learning-r-csharp-forecasting-exponential-smoothing.md)
* [<span data-ttu-id="268ee-123">ETS + STL 預測</span><span class="sxs-lookup"><span data-stu-id="268ee-123">ETS + STL Forecasting</span></span>](machine-learning-r-csharp-retail-demand-forecasting.md)
* [<span data-ttu-id="268ee-124">預測 - 自動迴歸整合式移動平均 (ARIMA)</span><span class="sxs-lookup"><span data-stu-id="268ee-124">Forecasting - Autoregressive Integrated Moving Average (ARIMA)</span></span>](machine-learning-r-csharp-arima.md)
* [<span data-ttu-id="268ee-125">存活分析</span><span class="sxs-lookup"><span data-stu-id="268ee-125">Survival Analysis</span></span>](machine-learning-r-csharp-survival-analysis.md)

## <a name="scenario-2-trained-model--specific-data"></a><span data-ttu-id="268ee-126">案例 2：定型模型 - 特定資料</span><span class="sxs-lookup"><span data-stu-id="268ee-126">Scenario 2: Trained model – specific data</span></span>
<span data-ttu-id="268ee-127">使用者具有可透過 R 程式碼提供實用預測的資料，例如可透過 k-means 演算法叢集以預測使用者性格類型的大型性格問卷樣本，或可透過存活分析 R 封裝預測個人罹患肺癌之風險的健康調查資料。</span><span class="sxs-lookup"><span data-stu-id="268ee-127">A user has data that provides useful predictions through R code, such as a large sample of personality questionnaires clustered through a k-means algorithm to predict the user’s personality type, or health survey data that can be used to predict an individual’s risk for lung cancer with a survival analysis R package.</span></span> <span data-ttu-id="268ee-128">使用者會透過可預測新使用者結果的 Web 服務來發行資料。</span><span class="sxs-lookup"><span data-stu-id="268ee-128">The user publishes the data through a web service that predicts a new user’s outcome.</span></span>

## <a name="scenario-3-trained-model--generic-data"></a><span data-ttu-id="268ee-129">案例 3：定型模型 - 泛型資料</span><span class="sxs-lookup"><span data-stu-id="268ee-129">Scenario 3: Trained model – generic data</span></span>
<span data-ttu-id="268ee-130">使用者具有泛型資料 (例如文字主體)，該資料可用於建置 Web 服務，並將其廣泛套用至不同類型的使用個案和案例。</span><span class="sxs-lookup"><span data-stu-id="268ee-130">A user has generic data (such as a text corpus) that allows a web service to be built and applied generically across different types of use cases and scenarios.</span></span>

* [<span data-ttu-id="268ee-131">語彙型情感分析</span><span class="sxs-lookup"><span data-stu-id="268ee-131">Lexicon Based Sentiment Analysis</span></span>](machine-learning-r-csharp-lexicon-based-sentiment-analysis.md)

## <a name="scenario-4-advanced-calculator"></a><span data-ttu-id="268ee-132">案例 4：進階計算機</span><span class="sxs-lookup"><span data-stu-id="268ee-132">Scenario 4: Advanced calculator</span></span>
<span data-ttu-id="268ee-133">使用者提供進階計算或模擬，而不需要任何定型模型或將使用者資料套入模型。</span><span class="sxs-lookup"><span data-stu-id="268ee-133">A user provides advanced calculations or simulations that don’t require any trained model or fitting of a model to the user’s data.</span></span>

* [<span data-ttu-id="268ee-134">比例差異測試</span><span class="sxs-lookup"><span data-stu-id="268ee-134">Difference in Proportions Test</span></span>](machine-learning-r-csharp-difference-in-two-proportions.md)
* [<span data-ttu-id="268ee-135">常態分佈套件</span><span class="sxs-lookup"><span data-stu-id="268ee-135">Normal Distribution Suite</span></span>](machine-learning-r-csharp-normal-distribution.md)
* [<span data-ttu-id="268ee-136">二項分配套件</span><span class="sxs-lookup"><span data-stu-id="268ee-136">Binomial Distribution Suite</span></span>](machine-learning-r-csharp-binomial-distribution.md)

## <a name="faq"></a><span data-ttu-id="268ee-137">常見問題集</span><span class="sxs-lookup"><span data-stu-id="268ee-137">FAQ</span></span>
<span data-ttu-id="268ee-138">如需取用 Web 服務或發佈至 Marketplace 的常見問題集，請參閱 [這裡](machine-learning-marketplace-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="268ee-138">For frequently asked questions on consumption of the web service or publishing to the Marketplace, see [here](machine-learning-marketplace-faq.md).</span></span>

[1]: ./media/machine-learning-r-csharp-web-service-examples/machine-learning-r-code-options-for-using-and-sharing-cloud.png



