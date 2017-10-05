---
title: "使用 Machine Learning 建立的信用風險預測解決方案 | Microsoft Docs"
description: "詳細的逐步解說說明如何在 Azure Machine Learning 中為信用風險評估建立預測分析解決方案。"
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
ms.openlocfilehash: e1af999b2fde8ffa2a0ffd1b88230f0aaab32b37
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="walkthrough-develop-a-predictive-analytics-solution-for-credit-risk-assessment-in-azure-machine-learning"></a><span data-ttu-id="1f8a4-104">逐步解說：在 Azure Machine Learning 中為信用風險評估開發預測分析解決方案</span><span class="sxs-lookup"><span data-stu-id="1f8a4-104">Walkthrough: Develop a predictive analytics solution for credit risk assessment in Azure Machine Learning</span></span>

<span data-ttu-id="1f8a4-105">在本逐步解說中，我們將進一步了解在 Machine Learning Studio 中開發預測性分析解決方案的程序。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-105">In this walkthrough, we take an extended look at the process of developing a predictive analytics solution in Machine Learning Studio.</span></span> <span data-ttu-id="1f8a4-106">我們會在 Machine Learning Studio 中開發一個簡單的模型，然後將它部署為 Azure Machine Learning Web 服務，其中模型將可使用新資料來進行預測。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-106">We develop a simple model in Machine Learning Studio, and then deploy it as an Azure Machine Learning web service where the model can make predictions using new data.</span></span> 

<span data-ttu-id="1f8a4-107">本逐步解說會假設您之前已至少使用過一次 Machine Learning Studio，而且對機器學習服務概念有一些了解。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-107">This walkthrough assumes that you've used Machine Learning Studio at least once before, and that you have some understanding of machine learning concepts.</span></span> <span data-ttu-id="1f8a4-108">但不會假設您對上述任一方面有所專精。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-108">But it doesn't assume you're an expert in either.</span></span>

<span data-ttu-id="1f8a4-109">如果您未曾使用過 **Azure Machine Learning Studio**，您可以從[在 Azure Machine Learning Studio 中建立您的第一個資料科學實驗](machine-learning-create-experiment.md)教學課程著手。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-109">If you've never used **Azure Machine Learning Studio** before, you might want to start with the tutorial, [Create your first data science experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md).</span></span> <span data-ttu-id="1f8a4-110">該教學課程會引導您完成第一次使用 Machine Learning Studio 的程序。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-110">That tutorial takes you through Machine Learning Studio for the first time.</span></span> <span data-ttu-id="1f8a4-111">它會說明基本概念，讓您了解如何將模組拖放到您的實驗、將它們連接在一起、執行實驗及檢視結果。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-111">It shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="1f8a4-112">另一個可協助您開始使用的工具是一張圖，此圖提供 Machine Learning Studio 的功能概觀。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-112">Another tool that may be helpful for getting started is a diagram that gives an overview of the capabilities of Machine Learning Studio.</span></span> <span data-ttu-id="1f8a4-113">您可以從這裡下載並列印它：[Azure Machine Learning Studio 功能的概觀圖](machine-learning-studio-overview-diagram.md)。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-113">You can download and print it from here: [Overview diagram of Azure Machine Learning Studio capabilities](machine-learning-studio-overview-diagram.md).</span></span>
 
<span data-ttu-id="1f8a4-114">如果您大致上算是機器學習服務的新手，有一系列影片可為您提供協助。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-114">If you're new to the field of machine learning in general, there's a video series that might be helpful to you.</span></span> <span data-ttu-id="1f8a4-115">此系列稱為[適用於初學者的資料科學](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)，它可透過使用日常語言和概念，為您提供機器學習服務的絕佳簡介。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-115">It's called [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) and it can give you a great introduction to machine learning using everyday language and concepts.</span></span>


[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]
 

## <a name="the-problem"></a><span data-ttu-id="1f8a4-116">問題</span><span class="sxs-lookup"><span data-stu-id="1f8a4-116">The problem</span></span>

<span data-ttu-id="1f8a4-117">假設您必須根據某個人在信用申請書上提供的資訊預測其信用風險。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-117">Suppose you need to predict an individual's credit risk based on the information they gave on a credit application.</span></span>  

<span data-ttu-id="1f8a4-118">信用風險評估是一個複雜的問題，但是我們可以針對這個逐步解說將它稍微簡化。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-118">Credit risk assessment is a complex problem, but we can simplify it a bit for this walkthrough.</span></span> <span data-ttu-id="1f8a4-119">我們將使用它作為一個範例，以說明您如何使用 Microsoft Azure Machine Learning 來建立預測性分析解決方案。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-119">We'll use it as an example of how you can create a predictive analytics solution using Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="1f8a4-120">為了這麼做，我們將使用 Azure Machine Learning Studio 和 Machine Learning Web 服務。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-120">To do this, we use Azure Machine Learning Studio and a Machine Learning web service.</span></span>  

## <a name="the-solution"></a><span data-ttu-id="1f8a4-121">解決方案</span><span class="sxs-lookup"><span data-stu-id="1f8a4-121">The solution</span></span>

<span data-ttu-id="1f8a4-122">在這個詳細的逐步解說中，我們將從可公開取得的信用風險資料開始著手，然後根據該資料來開發並訓練預測性模型。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-122">In this detailed walkthrough, we start with publicly available credit risk data and develop and train a predictive model based on that data.</span></span> <span data-ttu-id="1f8a4-123">接著，我們會將該模型部署為 Web 服務，以便供其他人用來評估信用風險。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-123">Then we deploy the model as a web service so it can be used by others for credit risk assessment.</span></span>

<span data-ttu-id="1f8a4-124">為了建立此信用風險評估解決方案，我們將依照下列步驟操作：</span><span class="sxs-lookup"><span data-stu-id="1f8a4-124">To create this credit risk assessment solution, we follow these steps:</span></span>  

1. [<span data-ttu-id="1f8a4-125">建立機器學習服務工作區</span><span class="sxs-lookup"><span data-stu-id="1f8a4-125">Create a Machine Learning workspace</span></span>](machine-learning-walkthrough-1-create-ml-workspace.md)
2. [<span data-ttu-id="1f8a4-126">上傳現有資料</span><span class="sxs-lookup"><span data-stu-id="1f8a4-126">Upload existing data</span></span>](machine-learning-walkthrough-2-upload-data.md)
3. [<span data-ttu-id="1f8a4-127">建立實驗</span><span class="sxs-lookup"><span data-stu-id="1f8a4-127">Create an experiment</span></span>](machine-learning-walkthrough-3-create-new-experiment.md)
4. [<span data-ttu-id="1f8a4-128">訓練及評估模型</span><span class="sxs-lookup"><span data-stu-id="1f8a4-128">Train and evaluate the models</span></span>](machine-learning-walkthrough-4-train-and-evaluate-models.md)
5. [<span data-ttu-id="1f8a4-129">部署 Web 服務</span><span class="sxs-lookup"><span data-stu-id="1f8a4-129">Deploy the web service</span></span>](machine-learning-walkthrough-5-publish-web-service.md)
6. [<span data-ttu-id="1f8a4-130">存取 Web 服務</span><span class="sxs-lookup"><span data-stu-id="1f8a4-130">Access the web service</span></span>](machine-learning-walkthrough-6-access-web-service.md)

> [!TIP] 
> <span data-ttu-id="1f8a4-131">您可以在 [Cortana Intelligence 資源庫 (英文)](https://gallery.cortanaintelligence.com) 中，找到我們在這個逐步解說中所開發實驗的工作複本。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-131">You can find a working copy of the experiment that we develop in this walkthrough in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="1f8a4-132">移至 **[逐步解說 - 信用風險預測 (英文)](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)**，然後按一下 [Open in Studio] \(在 Studio 中開啟)，以將實驗的複本下載到您的 Machine Learning Studio 工作區。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-132">Go to **[Walkthrough - Credit risk prediction](https://gallery.cortanaintelligence.com/Experiment/Walkthrough-Credit-risk-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>
> 
> <span data-ttu-id="1f8a4-133">此逐步解說是以簡化版的[二進位分類：信用風險預測 (英文)](http://go.microsoft.com/fwlink/?LinkID=525270) 範例實驗為基礎，[資源庫](http://gallery.cortanaintelligence.com/)中也有提供此實驗。</span><span class="sxs-lookup"><span data-stu-id="1f8a4-133">This walkthrough is based on a simplified version of the sample experiment, [Binary Classification: Credit risk prediction](http://go.microsoft.com/fwlink/?LinkID=525270), also available in the [Gallery](http://gallery.cortanaintelligence.com/).</span></span>
