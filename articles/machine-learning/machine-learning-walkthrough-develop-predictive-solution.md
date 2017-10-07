---
title: "aaaA 預測使用機器學習的信用風險解決方案 |Microsoft 文件"
description: "詳細的逐步解說，示範如何 toocreate 信用額度的預測分析解決方案將風險評定 Azure Machine Learning Studio 中。"
keywords: "信用風險, 預測性分析解決方案, 風險評估"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 43300854-a14e-4cd2-9bb1-c55c779e0e93
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/23/2017
ms.author: garye
ms.openlocfilehash: 00ed39081e6952b8d03b37a8285d8dc3ddff2cb4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="89050-104">逐步解說：在 Azure Machine Learning 中為信用風險評估開發預測分析解決方案</span><span class="sxs-lookup"><span data-stu-id="89050-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="89050-105">在本逐步解說中，我們查看擴充開發預測分析解決方案 Machine Learning Studio 中的 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="89050-105">In this walkthrough, we take an extended look at hello process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="89050-106">我們開發在機器學習 Studio 中，簡單的模型，然後將其部署為其中 hello 模型可以使用資料做出預測新的 Azure Machine Learning web 服務。</span><span class="sxs-lookup"><span data-stu-id="89050-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where hello model can make predictions using new data.</span></span> 

<span data-ttu-id="89050-107">本逐步解說會假設您之前已至少使用過一次 Machine Learning Studio，而且對機器學習服務概念有一些了解。</span><span class="sxs-lookup"><span data-stu-id="89050-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="89050-108">但不會假設您對上述任一方面有所專精。</span><span class="sxs-lookup"><span data-stu-id="89050-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="89050-109">如果您從未使用過**Azure Machine Learning Studio**您可能會想 toostart hello 教學課程中，使用之前，[建立 Azure Machine Learning Studio 中的第一次的資料科學實驗](machine-learning-create-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="89050-109">If you've never used **Azure Machine Learning Studio** before, you might want toostart with hello tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="89050-110">該教學課程引導您完成 Machine Learning Studio hello 第一次。</span><span class="sxs-lookup"><span data-stu-id="89050-110">That tutorial takes you through Machine Learning Studio for hello first time.</span></span> <span data-ttu-id="89050-111">它會顯示 hello 基本概念的方式 toodrag 放模組至您的經驗，連接在一起，請執行 hello 實驗，並查看 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="89050-111">It shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="89050-112">可能會很有幫助使用者入門的另一個工具是 hello Machine Learning Studio 功能的概觀的圖表。</span><span class="sxs-lookup"><span data-stu-id="89050-112">Another tool that may be helpful for getting started is a diagram that gives an overview of hello capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="89050-113">您可以從這裡下載並列印它：[Azure Machine Learning Studio 功能的概觀圖](machine-learning-studio-overview-diagram.md)。</span><span class="sxs-lookup"><span data-stu-id="89050-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="89050-114">如果您是新 toohello 欄位的機器學習的一般情況下，沒有可能會很有幫助 tooyou 影片系列。</span><span class="sxs-lookup"><span data-stu-id="89050-114">If you're new toohello field of machine learning in general, there's a video series that might be helpful tooyou.</span></span> <span data-ttu-id="89050-115">它會呼叫[為初學者所設計的資料科學](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)和它可以提供絕佳的簡介 toomachine 學習使用日常用語和概念。</span><span class="sxs-lookup"><span data-stu-id="89050-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction toomachine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="hello-problem"></a><span data-ttu-id="89050-116">hello 問題</span><span class="sxs-lookup"><span data-stu-id="89050-116">hello problem</span></span>

<span data-ttu-id="89050-117">假設您需要的 toopredict hello 剩餘的信用應用程式所提供的資訊為基礎的個人的信用風險。</span><span class="sxs-lookup"><span data-stu-id="89050-117">Suppose you need toopredict an individual's credit risk based on hello information they gave on a credit application.</span></span>  

<span data-ttu-id="89050-118">信用風險評估是一個複雜的問題，但是我們可以針對這個逐步解說將它稍微簡化。</span><span class="sxs-lookup"><span data-stu-id="89050-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="89050-119">我們將使用它作為一個範例，以說明您如何使用 Microsoft Azure Machine Learning 來建立預測性分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="89050-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="89050-120">toodo，我們使用 Azure Machine Learning Studio 和機器學習 web 服務。</span><span class="sxs-lookup"><span data-stu-id="89050-120">toodo this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="hello-solution"></a><span data-ttu-id="89050-121">hello 方案</span><span class="sxs-lookup"><span data-stu-id="89050-121">hello solution</span></span>

<span data-ttu-id="89050-122">在這個詳細的逐步解說中，我們將從可公開取得的信用風險資料開始著手，然後根據該資料來開發並訓練預測性模型。</span><span class="sxs-lookup"><span data-stu-id="89050-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="89050-123">然後我們 hello 將模型部署為 web 服務，才能使用其他人所評估信用風險。</span><span class="sxs-lookup"><span data-stu-id="89050-123">Then we deploy hello model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="89050-124">toocreate 這個信用風險評定解決方案中，我們遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="89050-124">toocreate this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="89050-125">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="89050-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="89050-126">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="89050-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="89050-127">建立實驗</span><span class="sxs-lookup"><span data-stu-id="89050-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="89050-128">來定型及評估 hello 模型</span><span class="sxs-lookup"><span data-stu-id="89050-128">Train and evaluate hello models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="89050-129">部署 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="89050-129">Deploy hello web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="89050-130">存取 hello web 服務</span><span class="sxs-lookup"><span data-stu-id="89050-130">Access hello web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="89050-131">您可以在本逐步解說中 hello 找到我們所開發的 hello 實驗的工作副本[Cortana 智慧組件庫](https://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="89050-131">You can find a working copy of hello experiment that we develop in this walkthrough in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="89050-132">跳過**[逐步解說-信用風險預測](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**按一下**在 Studio 中開啟**toodownload hello 實驗到 Machine Learning Studio 工作區的複本。</span><span class="sxs-lookup"><span data-stu-id="89050-132">Go too**[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="89050-133">本逐步解說根據 hello 範例實驗的簡化版本[二元分類： 信用風險預測](http://go.microsoft.com/fwlink/?LinkID=525270)，也可用於 hello[圖庫](http://gallery.cortanaintelligence.com/)。</span><span class="sxs-lookup"><span data-stu-id="89050-133">This walkthrough is based on a simplified version of hello sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in hello [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
