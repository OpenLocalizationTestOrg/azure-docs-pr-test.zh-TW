---
title: "複製機器學習服務範例實驗 - Azure | Microsoft Docs"
description: "了解如何透過 Cortana 智慧資源庫和 Microsoft Azure Machine Learning 使用範例機器學習服務實驗來建立新的實驗。"
keywords: "機器學習服務範例, 範例實驗, 機器學習服務範例"
services: machine-learning
documentationcenter: 
author: cjgronlund
manager: jhubbard
editor: cgronlun
ms.assetid: 81e6c1d8-682c-4db3-bfd5-d7bfb1150ff3
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: cgronlun
ms.openlocfilehash: 55f9bd2ed0d555a14d31bf3d262707d65bd70244
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="copy-example-experiments-to-create-new-machine-learning-experiments"></a><span data-ttu-id="4f514-104">複製範例實驗來建立新的機器學習服務實驗</span><span class="sxs-lookup"><span data-stu-id="4f514-104">Copy example experiments to create new machine learning experiments</span></span>
<span data-ttu-id="4f514-105">了解如何從 [Cortana 智慧資源庫](https://gallery.cortanaintelligence.com/) 的範例實驗開始，而不是從頭建立機器學習服務實驗。</span><span class="sxs-lookup"><span data-stu-id="4f514-105">Learn how to start with example experiments from [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com/) instead of creating machine learning experiments from scratch.</span></span> <span data-ttu-id="4f514-106">您可以使用範例來建立自己的機器學習服務解決方案。</span><span class="sxs-lookup"><span data-stu-id="4f514-106">You can use the examples to build your own machine learning solution.</span></span>

<span data-ttu-id="4f514-107">資源庫有 Microsoft Azure Machine Learning 小組的範例實驗，以及由 Machine Learning 社群共用的範例。</span><span class="sxs-lookup"><span data-stu-id="4f514-107">The gallery has example experiments by the Microsoft Azure Machine Learning team as well as examples shared by the Machine Learning community.</span></span> <span data-ttu-id="4f514-108">您也可以提出有關實驗的問題或張貼意見。</span><span class="sxs-lookup"><span data-stu-id="4f514-108">You also can ask questions or post comments about experiments.</span></span>

<span data-ttu-id="4f514-109">若要查看如何使用資源庫，請觀看[初學者的資料科學](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)系列中的 3 分鐘影片[複製其他人的工作來進行資料科學](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md)。</span><span class="sxs-lookup"><span data-stu-id="4f514-109">To see how to use the gallery, watch the 3-minute video [Copy other people's work to do data science](machine-learning-data-science-for-beginners-copy-other-peoples-work-to-do-data-science.md) from the series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="find-an-experiment-to-copy-in-cortana-intelligence-gallery"></a><span data-ttu-id="4f514-110">在 Cortana 智慧資源庫中尋找要複製的實驗</span><span class="sxs-lookup"><span data-stu-id="4f514-110">Find an experiment to copy in Cortana Intelligence Gallery</span></span>
<span data-ttu-id="4f514-111">若要查看有哪些可用的實驗，請移至[資源庫](https://gallery.cortanaintelligence.com/)，然後按一下頁面頂端的 [實驗]。</span><span class="sxs-lookup"><span data-stu-id="4f514-111">To see what experiments are available, go to the [Gallery](https://gallery.cortanaintelligence.com/) and click **Experiments** at the top of the page.</span></span>

### <a name="find-the-newest-or-most-popular-experiments"></a><span data-ttu-id="4f514-112">尋找最新或最受歡迎的實驗</span><span class="sxs-lookup"><span data-stu-id="4f514-112">Find the newest or most popular experiments</span></span>
<span data-ttu-id="4f514-113">在此頁面上，您可以查看 [最近新增] 實驗，或往下捲動查看 [熱門項目] 或最新的 [熱門的 Microsoft 實驗]。</span><span class="sxs-lookup"><span data-stu-id="4f514-113">On this page, you can see **Recently added** experiments, or scroll down to look at **What's popular** or the latest **Popular Microsoft experiments**.</span></span>

### <a name="look-for-an-experiment-that-meets-specific-requirements"></a><span data-ttu-id="4f514-114">尋找符合特定需求的實驗</span><span class="sxs-lookup"><span data-stu-id="4f514-114">Look for an experiment that meets specific requirements</span></span>
<span data-ttu-id="4f514-115">若要瀏覽所有實驗︰</span><span class="sxs-lookup"><span data-stu-id="4f514-115">To browse all experiments:</span></span>

1. <span data-ttu-id="4f514-116">按一下頁面頂端的 [全部瀏覽]  。</span><span class="sxs-lookup"><span data-stu-id="4f514-116">Click **Browse all** at the top of the page.</span></span>
2. <span data-ttu-id="4f514-117">在左側 [類別] 區段的 [精簡依據] 之下，選取 [實驗] 以查看資源庫中的所有實驗。</span><span class="sxs-lookup"><span data-stu-id="4f514-117">On the left-hand side, under **Refine by** in the **Categories** section, select **Experiment** to see all the experiments in the Gallery.</span></span>
3. <span data-ttu-id="4f514-118">有幾種不同方式可以找到符合您需求的實驗︰</span><span class="sxs-lookup"><span data-stu-id="4f514-118">You can find experiments that meet your requirements a couple different ways:</span></span>
   * <span data-ttu-id="4f514-119">**選取左邊的篩選。**</span><span class="sxs-lookup"><span data-stu-id="4f514-119">**Select filters on the left.**</span></span> <span data-ttu-id="4f514-120">例如，若要瀏覽使用以 PCA 為基礎之異常偵測演算法的實驗，請選取 [類別] 之下的 [實驗]，然後按一下 [全部顯示]。</span><span class="sxs-lookup"><span data-stu-id="4f514-120">For example, to browse experiments that use a PCA-based anomaly detection algorithm: With **Experiment** selected under **Categories**, click **Show all**.</span></span> <span data-ttu-id="4f514-121">然後，在 [使用的演算法] 之下，選擇 [以 PCA 為基礎的異常偵測]。</span><span class="sxs-lookup"><span data-stu-id="4f514-121">Then, under **Algorithms Used**, choose **PCA-Based Anomaly Detection**.</span></span> <br></br><span data-ttu-id="4f514-122">
     ![選取篩選器](./media/machine-learning-sample-experiments/refine-the-view.png)</span><span class="sxs-lookup"><span data-stu-id="4f514-122">
![Select filters](./media/machine-learning-sample-experiments/refine-the-view.png)</span></span>
   * <span data-ttu-id="4f514-123">**使用 [搜尋] 方塊。**</span><span class="sxs-lookup"><span data-stu-id="4f514-123">**Use the search box.**</span></span> <span data-ttu-id="4f514-124">例如，若要尋找 Microsoft 所提出並使用二級支援向量機器演算法的數字辨識相關實驗，請在 [搜尋] 方塊中輸入「數字辨識」。</span><span class="sxs-lookup"><span data-stu-id="4f514-124">For example, to find experiments contributed by Microsoft related to digit recognition that use a two-class support vector machine algorithm, enter "digit recognition" in the search box.</span></span> <span data-ttu-id="4f514-125">然後選取篩選器 [實驗]、[僅包含 Microsoft 內容] 和 [二級支援向量機器]：</span><span class="sxs-lookup"><span data-stu-id="4f514-125">Then, select the filters **Experiment**, **Microsoft content only**, and **Two-Class Support Vector Machine**:</span></span><br></br><span data-ttu-id="4f514-126">
     ![使用搜尋方塊](./media/machine-learning-sample-experiments/search-for-experiments.png)</span><span class="sxs-lookup"><span data-stu-id="4f514-126">
![Use the search box](./media/machine-learning-sample-experiments/search-for-experiments.png)</span></span>
4. <span data-ttu-id="4f514-127">按一下實驗，以深入了解相關資訊。</span><span class="sxs-lookup"><span data-stu-id="4f514-127">Click an experiment to learn more about it.</span></span>
5. <span data-ttu-id="4f514-128">若要執行和 (或) 修改實驗，請按一下實驗頁面上的 [在 Studio 中開啟]  。</span><span class="sxs-lookup"><span data-stu-id="4f514-128">To run and/or modify the experiment, click **Open in Studio** on the experiment's page.</span></span> <br></br>

    ![範例實驗](./media/machine-learning-sample-experiments/example-experiment.png)

    > [!NOTE]
    > <span data-ttu-id="4f514-130">當您在 Machine Learning Studio 中第一次開啟實驗時，您可以免費試用或購買 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="4f514-130">When you open an experiment in Machine Learning Studio for the first time, you can try it for free or buy an Azure subscription.</span></span> [<span data-ttu-id="4f514-131">了解 Machine Learning Studio 免費試用版與付費服務</span><span class="sxs-lookup"><span data-stu-id="4f514-131">Learn about the Machine Learning Studio free trial vs. paid service</span></span>](https://azure.microsoft.com/pricing/details/machine-learning/)
    >
    >

## <a name="create-a-new-experiment-using-an-example-as-a-template"></a><span data-ttu-id="4f514-132">使用範例作為範本來建立新實驗</span><span class="sxs-lookup"><span data-stu-id="4f514-132">Create a new experiment using an example as a template</span></span>
<span data-ttu-id="4f514-133">您也可以使用資源庫範例作為範本，在 Machine Learning Studio 中建立新實驗。</span><span class="sxs-lookup"><span data-stu-id="4f514-133">You also can create a new experiment in Machine Learning Studio using a Gallery example as a template.</span></span>

1. <span data-ttu-id="4f514-134">用您的 Microsoft 帳戶認證登入 [Studio](https://studio.azureml.net)，然後按一下 [新增] 以建立實驗。</span><span class="sxs-lookup"><span data-stu-id="4f514-134">Sign in with your Microsoft account credentials to the [Studio](https://studio.azureml.net), and then click **New** to create an experiment.</span></span>
2. <span data-ttu-id="4f514-135">瀏覽範例內容，然後按一下其中一個。</span><span class="sxs-lookup"><span data-stu-id="4f514-135">Browse through the example content and click one.</span></span>

<span data-ttu-id="4f514-136">隨即以範例實驗作為範本，在您的 Machine Learning Studio 工作區中建立新的實驗。</span><span class="sxs-lookup"><span data-stu-id="4f514-136">A new experiment is created in your Machine Learning Studio workspace using the example experiment as a template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f514-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4f514-137">Next steps</span></span>
* [<span data-ttu-id="4f514-138">從各種資源匯入資料</span><span class="sxs-lookup"><span data-stu-id="4f514-138">Import data from various sources</span></span>](machine-learning-data-science-import-data.md)
* [<span data-ttu-id="4f514-139">Machine Learning 中的 R 語言所適用的快速入門教學課程</span><span class="sxs-lookup"><span data-stu-id="4f514-139">Quickstart tutorial for the R language in Machine Learning</span></span>](machine-learning-r-quickstart.md)
* [<span data-ttu-id="4f514-140">部署 Machine Learning Web 服務</span><span class="sxs-lookup"><span data-stu-id="4f514-140">Deploy a Machine Learning web service</span></span>](machine-learning-publish-a-machine-learning-web-service.md)
