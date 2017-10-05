---
title: "Machine Learning Studio 中的簡易實驗 | Microsoft Docs"
description: "此機器學習服務教學課程會引導您輕鬆進行資料科學實驗。 我們將使用迴歸演算法預測汽車價格。"
keywords: "實驗、線性迴歸、機器學習服務演算法、機器學習服務教學課程、預測性模型技術、資料科學實驗"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: b6176bb2-3bb6-4ebf-84d1-3598ee6e01c6
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 0539e9d04c61d35de56a29d350c07654c095c576
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="10840-105">機器學習服務教學課程：在 Azure Machine Learning Studio 中建立您的第一個資料科學實驗</span><span class="sxs-lookup"><span data-stu-id="10840-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="10840-106">如果您從未使用過 **Azure Machine Learning Studio**，本教學課程很適合您。</span><span class="sxs-lookup"><span data-stu-id="10840-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="10840-107">在本教學課程中，我們將逐步解說第一次如何使用 Studio 建立機器學習服務實驗。</span><span class="sxs-lookup"><span data-stu-id="10840-107">In this tutorial, we'll walk through how to use Studio for the first time to create a machine learning experiment.</span></span> <span data-ttu-id="10840-108">此實驗將測試一個分析模型，該模型會根據使用製造和技術規格等不同變數，來預測汽車的價格。</span><span class="sxs-lookup"><span data-stu-id="10840-108">The experiment will test an analytical model that predicts the price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="10840-109">本教學課程說明如何拖放模組到您的實驗、將它們連接在一起、執行實驗及檢視結果的基本概念。</span><span class="sxs-lookup"><span data-stu-id="10840-109">This tutorial shows you the basics of how to drag-and-drop modules onto your experiment, connect them together, run the experiment, and look at the results.</span></span> <span data-ttu-id="10840-110">我們不討論機器學習服務或如何選取及使用 100 個以上內建的演算法和資料操作模組的一般主題。</span><span class="sxs-lookup"><span data-stu-id="10840-110">We're not going to discuss the general topic of machine learning or how to select and use the 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="10840-111">如果您是機器學習服務的新手，[初學者資料科學](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)影片系列可能是不錯的起點。</span><span class="sxs-lookup"><span data-stu-id="10840-111">If you're new to machine learning, the video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place to start.</span></span> <span data-ttu-id="10840-112">此影片系列使用日常用語和概念，是絕佳的機器學習服務介紹。</span><span class="sxs-lookup"><span data-stu-id="10840-112">This video series is a great introduction to machine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="10840-113">如果您已熟悉機器學習服務，但是想了解更多關於 Machine Learning Studio 的一般資訊及其所包含的演算法，這裡有一些不錯的資源：</span><span class="sxs-lookup"><span data-stu-id="10840-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and the machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="10840-114">什麼是 Machine Learning Studio？</span><span class="sxs-lookup"><span data-stu-id="10840-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="10840-115">- 這是 Studio 的高階概觀。</span><span class="sxs-lookup"><span data-stu-id="10840-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="10840-116">[機器學習服務基本概念 (含演算法範例)](machine-learning-basics-infographic-with-algorithm-examples.md) - 如果您想深入了解 Machine Learning Studio 包含的不同類型機器學習服務演算法，此資訊圖很有用。</span><span class="sxs-lookup"><span data-stu-id="10840-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want to learn more about the different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="10840-117">[機器學習服務指南](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - 本指南涵蓋類似上述資訊圖的資訊，但採用互動式格式。</span><span class="sxs-lookup"><span data-stu-id="10840-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as the infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="10840-118">[機器學習服務演算法小祕技](machine-learning-algorithm-cheat-sheet.md)和[如何選擇 Microsoft Azure Machine Learning 的演算法](machine-learning-algorithm-choice.md) - 這個可下載的海報和隨附的文章深入探討 Studio 演算法。</span><span class="sxs-lookup"><span data-stu-id="10840-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How to choose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss the Studio algorithms in depth.</span></span>
- <span data-ttu-id="10840-119">[Machine Learning Studio︰演算法和模組說明](https://msdn.microsoft.com/library/azure/dn905974.aspx) - 這是所有 Studio 模組的完整參考，還包括機器學習服務演算法。</span><span class="sxs-lookup"><span data-stu-id="10840-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is the complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="10840-120">Machine Learning Studio 如何協助您？</span><span class="sxs-lookup"><span data-stu-id="10840-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="10840-121">Machine Learning Studio 可讓您輕鬆地使用以預測性模型技術預先程式化的拖放模組來設定實驗。</span><span class="sxs-lookup"><span data-stu-id="10840-121">Machine Learning Studio makes it easy to set up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="10840-122">使用互動式的視覺化工作區，可以拖放***資料集***和***分析***模組到互動式畫布。</span><span class="sxs-lookup"><span data-stu-id="10840-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="10840-123">將它們連接在一起，可組成在 Machine Learning Studio 中執行的***實驗***。</span><span class="sxs-lookup"><span data-stu-id="10840-123">You connect them together to form an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="10840-124">您可以***建立模型***、***訓練模型***以及***評分與測試模型***。</span><span class="sxs-lookup"><span data-stu-id="10840-124">You ***create a model***, ***train the model***, and ***score and test the model***.</span></span>

<span data-ttu-id="10840-125">您可以逐一查看模型設計、編輯並執行實驗，直到它能提供您想要的結果。</span><span class="sxs-lookup"><span data-stu-id="10840-125">You can iterate on your model design, editing the experiment and running it until it gives you the results you're looking for.</span></span> <span data-ttu-id="10840-126">當您的模型就緒後，您可以將其發行為 ***Web 服務***，讓其他人可以傳送新資料到該服務，並取得預測結果。</span><span class="sxs-lookup"><span data-stu-id="10840-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="10840-127">開啟 Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="10840-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="10840-128">若要開始使用 Studio，請移至 [https://studio.azureml.net](https://studio.azureml.net)。</span><span class="sxs-lookup"><span data-stu-id="10840-128">To get started with Studio, go to [https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="10840-129">如果您之前已登入過 Machine Learning Studio，請按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="10840-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="10840-130">否則，請按一下 [由此註冊] 並選擇免費或付費選項。</span><span class="sxs-lookup"><span data-stu-id="10840-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="10840-131">![登入 Machine Learning Studio][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="10840-131">![Sign in to Machine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="10840-132">
***登入 Machine Learning Studio***</span><span class="sxs-lookup"><span data-stu-id="10840-132">
***Sign in to Machine Learning Studio***</span></span>

## <a name="five-steps-to-create-an-experiment"></a><span data-ttu-id="10840-133">建立實驗的五個步驟</span><span class="sxs-lookup"><span data-stu-id="10840-133">Five steps to create an experiment</span></span>

<span data-ttu-id="10840-134">在這個機器學習教學課程中，您可以遵循下列五個基本步驟，在 Machine Learning Studio 中建置實驗，來建立、訓練及評分您的模型：</span><span class="sxs-lookup"><span data-stu-id="10840-134">In this machine learning tutorial, you'll follow five basic steps to build an experiment in Machine Learning Studio to create, train, and score your model:</span></span>

- <span data-ttu-id="10840-135">**建立模型**</span><span class="sxs-lookup"><span data-stu-id="10840-135">**Create a model**</span></span>
    - <span data-ttu-id="10840-136">[步驟 1：取得資料]</span><span class="sxs-lookup"><span data-stu-id="10840-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="10840-137">[步驟 2︰ 準備資料]</span><span class="sxs-lookup"><span data-stu-id="10840-137">[Step 2: Prepare the data]</span></span>
    - <span data-ttu-id="10840-138">[步驟 3：定義功能]</span><span class="sxs-lookup"><span data-stu-id="10840-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="10840-139">**訓練模型**</span><span class="sxs-lookup"><span data-stu-id="10840-139">**Train the model**</span></span>
    - <span data-ttu-id="10840-140">[步驟 4：選擇及套用學習演算法]</span><span class="sxs-lookup"><span data-stu-id="10840-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="10840-141">**對模型評分與測試**</span><span class="sxs-lookup"><span data-stu-id="10840-141">**Score and test the model**</span></span>
    - <span data-ttu-id="10840-142">[步驟 5：預測新的汽車價格]</span><span class="sxs-lookup"><span data-stu-id="10840-142">[Step 5: Predict new automobile prices]</span></span>

<span data-ttu-id="10840-143">[步驟 1：取得資料]: #step-1-get-data</span><span class="sxs-lookup"><span data-stu-id="10840-143">[Step 1: Get data]: #step-1-get-data</span></span>
<span data-ttu-id="10840-144">[步驟 2︰ 準備資料]: #step-2-prepare-the-data</span><span class="sxs-lookup"><span data-stu-id="10840-144">[Step 2: Prepare the data]: #step-2-prepare-the-data</span></span>
<span data-ttu-id="10840-145">[步驟 3：定義功能]: #step-3-define-features</span><span class="sxs-lookup"><span data-stu-id="10840-145">[Step 3: Define features]: #step-3-define-features</span></span>
<span data-ttu-id="10840-146">[步驟 4：選擇及套用學習演算法]: #step-4-choose-and-apply-a-learning-algorithm</span><span class="sxs-lookup"><span data-stu-id="10840-146">[Step 4: Choose and apply a learning algorithm]: #step-4-choose-and-apply-a-learning-algorithm</span></span>
<span data-ttu-id="10840-147">[步驟 5：預測新的汽車價格]: #step-5-predict-new-automobile-prices</span><span class="sxs-lookup"><span data-stu-id="10840-147">[Step 5: Predict new automobile prices]: #step-5-predict-new-automobile-prices</span></span>

> [!TIP] 
> <span data-ttu-id="10840-148">您可以在 [Cortana Intelligence 資源庫](https://gallery.cortanaintelligence.com)中找到下列實驗的工作複本。</span><span class="sxs-lookup"><span data-stu-id="10840-148">You can find a working copy of the following experiment in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="10840-149">移至**[您的第一個資料科學實驗 - 汽車價格預測](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**，按一下 [在 Studio 中開啟]，以將實驗的複本下載到您的 Machine Learning Studio 工作區。</span><span class="sxs-lookup"><span data-stu-id="10840-149">Go to **[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** to download a copy of the experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="10840-150">步驟 1：取得資料</span><span class="sxs-lookup"><span data-stu-id="10840-150">Step 1: Get data</span></span>

<span data-ttu-id="10840-151">要執行機器學習服務，首先您需要的是資料。</span><span class="sxs-lookup"><span data-stu-id="10840-151">The first thing you need to perform machine learning is data.</span></span>
<span data-ttu-id="10840-152">Machine Learning Studio 隨附多個範例資料集供您使用，或者，您可以從許多來源匯入資料。</span><span class="sxs-lookup"><span data-stu-id="10840-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="10840-153">在此範例中，我們將使用您的工作區內含的範例資料集**汽車價格資料 (原始)**。</span><span class="sxs-lookup"><span data-stu-id="10840-153">For this example, we'll use the sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="10840-154">此資料集將包含許多個別汽車的項目，包括製造、模型、技術規格和價格等資訊。</span><span class="sxs-lookup"><span data-stu-id="10840-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="10840-155">以下說明如何匯入資料集到您的實驗。</span><span class="sxs-lookup"><span data-stu-id="10840-155">Here's how to get the dataset into your experiment.</span></span>

1. <span data-ttu-id="10840-156">按一下 Machine Learning Studio 視窗底部的 [+新增]，並選取 [實驗]，然後選取 [空白實驗] 以建立新的實驗。</span><span class="sxs-lookup"><span data-stu-id="10840-156">Create a new experiment by clicking **+NEW** at the bottom of the Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="10840-157">您可以在畫布頂端看到實驗的預設名稱。</span><span class="sxs-lookup"><span data-stu-id="10840-157">The experiment is given a default name that you can see at the top of the canvas.</span></span> <span data-ttu-id="10840-158">選取這段文字，然後重新命名為有意義的名稱，例如**汽車價格預測**。</span><span class="sxs-lookup"><span data-stu-id="10840-158">Select this text and rename it to something meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="10840-159">此名稱不必是唯一的。</span><span class="sxs-lookup"><span data-stu-id="10840-159">The name doesn't need to be unique.</span></span>

    ![將實驗重新命名][rename-experiment]

2. <span data-ttu-id="10840-161">實驗畫布左側是資料集和模組的調色盤。</span><span class="sxs-lookup"><span data-stu-id="10840-161">To the left of the experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="10840-162">在此調色盤頂端的 [搜尋] 方塊中輸入**汽車**，可尋找標示為**汽車價格資料 (原始)** 的資料集。</span><span class="sxs-lookup"><span data-stu-id="10840-162">Type **automobile** in the Search box at the top of this palette to find the dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="10840-163">將此資料集拖曳到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="10840-163">Drag this dataset to the experiment canvas.</span></span>

    <span data-ttu-id="10840-164">![找出汽車資料集，並將它拖曳到實驗畫布上][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="10840-164">![Find the automobile dataset and drag it onto the experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="10840-165">***尋找汽車的資料集，並將它拖曳到實驗畫布***</span><span class="sxs-lookup"><span data-stu-id="10840-165">***Find the automobile dataset and drag it onto the experiment canvas***</span></span>

<span data-ttu-id="10840-166">若想知道此資料的呈現情形，請按一下汽車資料集底部的輸出連接埠，然後選取 [視覺化] 。</span><span class="sxs-lookup"><span data-stu-id="10840-166">To see what this data looks like, click the output port at the bottom of the automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="10840-167">![按一下輸出連接埠，然後選取 [視覺化]][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="10840-167">![Click the output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="10840-168">
***按一下輸出連接埠，然後選取 [視覺化]***</span><span class="sxs-lookup"><span data-stu-id="10840-168">
***Click the output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="10840-169">資料集和模組以小圓圈代表輸入和輸出連接埠，輸入連接埠位在頂端，輸出連接埠在底端。</span><span class="sxs-lookup"><span data-stu-id="10840-169">Datasets and modules have input and output ports represented by small circles - input ports at the top, output ports at the bottom.</span></span>
<span data-ttu-id="10840-170">若要在您的實驗中建立資料流程，您要將某個模組的輸出連接埠連接到另一個模組的輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="10840-170">To create a flow of data through your experiment, you'll connect an output port of one module to an input port of another.</span></span>
<span data-ttu-id="10840-171">您隨時可以按一下資料集或模組的輸出連接埠，以查看資料於該時間點在資料流程中的型態。</span><span class="sxs-lookup"><span data-stu-id="10840-171">At any time, you can click the output port of a dataset or module to see what the data looks like at that point in the data flow.</span></span>

<span data-ttu-id="10840-172">在此範例資料集中，汽車的每個執行個體會顯示為資料列，而與每部汽車相關聯的變數會顯示為資料行。</span><span class="sxs-lookup"><span data-stu-id="10840-172">In this sample dataset, each instance of an automobile appears as a row, and the variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="10840-173">使用特定一款汽車的變數，我們要嘗試預測最右側資料行中的價格 (資料行 26，標題為「價格」)。</span><span class="sxs-lookup"><span data-stu-id="10840-173">Given the variables for a specific automobile, we're going to try to predict the price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="10840-174">![檢視資料視覺效果視窗中的汽車資料][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="10840-174">![View the automobile data in the data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="10840-175">
***檢視資料視覺效果視窗中的汽車資料***</span><span class="sxs-lookup"><span data-stu-id="10840-175">
***View the automobile data in the data visualization window***</span></span>

<span data-ttu-id="10840-176">按一下右上角的 "**x**"，以關閉視覺化視窗。</span><span class="sxs-lookup"><span data-stu-id="10840-176">Close the visualization window by clicking the "**x**" in the upper-right corner.</span></span>

## <a name="step-2-prepare-the-data"></a><span data-ttu-id="10840-177">步驟 2︰準備資料</span><span class="sxs-lookup"><span data-stu-id="10840-177">Step 2: Prepare the data</span></span>

<span data-ttu-id="10840-178">資料集通常必須先經過某些前置處理，才能進行分析。</span><span class="sxs-lookup"><span data-stu-id="10840-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="10840-179">例如，您可能已經注意到在各種不同資料列的資料行中有遺漏的值。</span><span class="sxs-lookup"><span data-stu-id="10840-179">For example, you might have noticed the missing values present in the columns of various rows.</span></span> <span data-ttu-id="10840-180">必須清除這些遺漏的值，讓模型才能正確地分析資料。</span><span class="sxs-lookup"><span data-stu-id="10840-180">These missing values need to be cleaned so the model can analyze the data correctly.</span></span> <span data-ttu-id="10840-181">在我們的案例中，我們將移除含有遺漏值的所有資料列。</span><span class="sxs-lookup"><span data-stu-id="10840-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="10840-182">此外， **自負虧損** 資料行含有比例很高的遺漏值，因此我們會將該資料行從模型中完全排除。</span><span class="sxs-lookup"><span data-stu-id="10840-182">Also, the **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from the model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="10840-183">在使用大部分的模組時，都必須從輸入資料中清除遺漏值。</span><span class="sxs-lookup"><span data-stu-id="10840-183">Cleaning the missing values from input data is a prerequisite for using most of the modules.</span></span>

<span data-ttu-id="10840-184">我們先新增一個模組以完整移除 [自負虧損] 資料行，然後再新增另一個模組以移除含有遺漏資料的任何資料列。</span><span class="sxs-lookup"><span data-stu-id="10840-184">First we add a module that removes the **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="10840-185">在模組調色盤頂端的 [搜尋] 方塊中輸入**選取資料行**以尋找[選取資料集中的資料行][select-columns]模組，然後將其拖曳到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="10840-185">Type **select columns** in the Search box at the top of the module palette to find the [Select Columns in Dataset][select-columns] module, then drag it to the experiment canvas.</span></span> <span data-ttu-id="10840-186">此模組可讓我們選取要將哪些資料行包含在模型中，或是從模型中排除。</span><span class="sxs-lookup"><span data-stu-id="10840-186">This module allows us to select which columns of data we want to include or exclude in the model.</span></span>

2. <span data-ttu-id="10840-187">將**汽車價格資料 (原始)** 資料集的輸出連接埠連接到[選取資料集中的資料行][select-columns]模組的輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="10840-187">Connect the output port of the **Automobile price data (Raw)** dataset to the input port of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="10840-188">![將 [選取資料集中的資料行] 模組新增到實驗畫布並連接它][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="10840-188">![Add the "Select Columns in Dataset" module to the experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="10840-189">***加入到實驗畫布 」 選取資料行中資料集 」 模組，其連接***</span><span class="sxs-lookup"><span data-stu-id="10840-189">***Add the "Select Columns in Dataset" module to the experiment canvas and connect it***</span></span>

3. <span data-ttu-id="10840-190">按一下 [選取資料集中的資料行][select-columns] 模組，然後按一下 [屬性] 窗格中的 [啟動資料行選取器]。</span><span class="sxs-lookup"><span data-stu-id="10840-190">Click the [Select Columns in Dataset][select-columns] module and click **Launch column selector** in the **Properties** pane.</span></span>

    - <span data-ttu-id="10840-191">在左側按一下 [套用規則] </span><span class="sxs-lookup"><span data-stu-id="10840-191">On the left, click **With rules**</span></span>
    - <span data-ttu-id="10840-192">在 [開始於] 下，按一下 [所有資料行]。</span><span class="sxs-lookup"><span data-stu-id="10840-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="10840-193">這會引導 [選取資料集中的資料行][select-columns] 通過所有資料行 (但即將排除的資料行除外)。</span><span class="sxs-lookup"><span data-stu-id="10840-193">This directs [Select Columns in Dataset][select-columns] to pass through all the columns (except those columns we're about to exclude).</span></span>
    - <span data-ttu-id="10840-194">在下拉式清單中，選取 [排除] 和 [資料行名稱]，然後按一下文字方塊內部。</span><span class="sxs-lookup"><span data-stu-id="10840-194">From the drop-downs, select **Exclude** and **column names**, and then click inside the text box.</span></span> <span data-ttu-id="10840-195">資料行清單隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="10840-195">A list of columns is displayed.</span></span> <span data-ttu-id="10840-196">選取 [自負虧損]，該資料行就會新增到文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="10840-196">Select **normalized-losses**, and it's added to the text box.</span></span>
    - <span data-ttu-id="10840-197">按一下核取記號 ([確定]) 按鈕，以關閉資料行選取器 (位於右下方)。</span><span class="sxs-lookup"><span data-stu-id="10840-197">Click the check mark (OK) button to close the column selector (on the lower-right).</span></span>

    <span data-ttu-id="10840-198">![啟動資料行選取器，並排除 [自負虧損] 資料行][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="10840-198">![Launch the column selector and exclude the "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="10840-199">***啟動資料行選取器，並排除 「 normalized-losses 」 資料行***</span><span class="sxs-lookup"><span data-stu-id="10840-199">***Launch the column selector and exclude the "normalized-losses" column***</span></span>

    <span data-ttu-id="10840-200">現在，[選取資料集中的資料行] 的屬性窗格指出它會傳遞資料集中的所有資料行，但 [自負虧損] 除外。</span><span class="sxs-lookup"><span data-stu-id="10840-200">Now the properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from the dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="10840-201">![[屬性] 窗格顯示 [自負虧損] 資料行已被排除][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="10840-201">![The properties pane shows that the "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="10840-202">***[屬性] 窗格會顯示已排除 「 normalized-losses 」 資料行***</span><span class="sxs-lookup"><span data-stu-id="10840-202">***The properties pane shows that the "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="10840-203">您可以按兩下模組並輸入文字，為模組新增註解。</span><span class="sxs-lookup"><span data-stu-id="10840-203">You can add a comment to a module by double-clicking the module and entering text.</span></span> <span data-ttu-id="10840-204">這有助於您快速檢視模組在您實驗中的執行情況。</span><span class="sxs-lookup"><span data-stu-id="10840-204">This can help you see at a glance what the module is doing in your experiment.</span></span> <span data-ttu-id="10840-205">在此案例中，按兩下 [選取資料集中的資料行][select-columns] 模組，然後輸入註解「排除自負虧損」。</span><span class="sxs-lookup"><span data-stu-id="10840-205">In this case double-click the [Select Columns in Dataset][select-columns] module and type the comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="10840-206">![按兩下模組以新增註解][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="10840-206">![Double-click a module to add a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="10840-207">***按兩下要新增註解的模組***</span><span class="sxs-lookup"><span data-stu-id="10840-207">***Double-click a module to add a comment***</span></span>

3. <span data-ttu-id="10840-208">將[清除遺漏的資料][clean-missing-data] 模組拖曳到實驗畫布，然後將其連接到 [選取資料集中的資料行][select-columns] 模組。</span><span class="sxs-lookup"><span data-stu-id="10840-208">Drag the [Clean Missing Data][clean-missing-data] module to the experiment canvas and connect it to the [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="10840-209">在 [屬性] 窗格中，選取 [清除模式] 底下的 [移除整個資料列]。</span><span class="sxs-lookup"><span data-stu-id="10840-209">In the **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="10840-210">這會指示[清除遺漏的資料][clean-missing-data]藉由移除含任何遺漏值的資料列以清除資料。</span><span class="sxs-lookup"><span data-stu-id="10840-210">This directs [Clean Missing Data][clean-missing-data] to clean the data by removing rows that have any missing values.</span></span> <span data-ttu-id="10840-211">按兩下模組，並輸入註解「移除遺漏值資料列」。</span><span class="sxs-lookup"><span data-stu-id="10840-211">Double-click the module and type the comment "Remove missing value rows."</span></span>

    <span data-ttu-id="10840-212">![將 [清除遺漏的資料] 的清除模式設為 [移除整個資料列]][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="10840-212">![Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="10840-213">***將清理模式設為 「 清除遺漏資料 」 模組的 「 移除整個資料列 」***</span><span class="sxs-lookup"><span data-stu-id="10840-213">***Set the cleaning mode to "Remove entire row" for the "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="10840-214">按一下頁面底部的 [執行]，以執行實驗。</span><span class="sxs-lookup"><span data-stu-id="10840-214">Run the experiment by clicking **RUN** at the bottom of the page.</span></span>

    <span data-ttu-id="10840-215">實驗執行完成時，所有模組都會呈現綠色核取標記，表示它們已順利完成。</span><span class="sxs-lookup"><span data-stu-id="10840-215">When the experiment has finished running, all the modules have a green check mark to indicate that they finished successfully.</span></span> <span data-ttu-id="10840-216">同時也請留意位於右上角的 **執行完成** 狀態。</span><span class="sxs-lookup"><span data-stu-id="10840-216">Notice also the **Finished running** status in the upper-right corner.</span></span>

<span data-ttu-id="10840-217">![執行後，實驗看起來應如下所示：][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="10840-217">![After running it, the experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="10840-218">
***執行後，實驗看起來應如下所示：***</span><span class="sxs-lookup"><span data-stu-id="10840-218">
***After running it, the experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="10840-219">為什麼要立即執行實驗？</span><span class="sxs-lookup"><span data-stu-id="10840-219">Why did we run the experiment now?</span></span> <span data-ttu-id="10840-220">藉由執行實驗，就會從資料集傳遞我們資料的資料行定義 (透過[選取資料集中的資料行][select-columns]模組，及透過[清除遺漏的資料][clean-missing-data]模組)。</span><span class="sxs-lookup"><span data-stu-id="10840-220">By running the experiment, the column definitions for our data pass from the dataset, through the [Select Columns in Dataset][select-columns] module, and through the [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="10840-221">這表示，我們連接到[清除遺漏的資料][clean-missing-data]的任何模組也會有相同的資訊。</span><span class="sxs-lookup"><span data-stu-id="10840-221">This means that any modules we connect to [Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="10840-222">我們的實驗到目前為止所完成的是清除資料。</span><span class="sxs-lookup"><span data-stu-id="10840-222">All we have done in the experiment up to this point is clean the data.</span></span> <span data-ttu-id="10840-223">若要檢視已清除的資料集，請按一下[清除遺漏的資料][clean-missing-data]模組的左側輸出連接埠，然後選取 [視覺化]。</span><span class="sxs-lookup"><span data-stu-id="10840-223">If you want to view the cleaned dataset, click the left output port of the [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="10840-224">請注意，此時已不包含 **自負虧損** 資料行，而且也沒有遺漏值。</span><span class="sxs-lookup"><span data-stu-id="10840-224">Notice that the **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="10840-225">現在我們已清除資料，而可以指定要在預測模型中使用哪些功能。</span><span class="sxs-lookup"><span data-stu-id="10840-225">Now that the data is clean, we're ready to specify what features we're going to use in the predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="10840-226">步驟 3：定義功能</span><span class="sxs-lookup"><span data-stu-id="10840-226">Step 3: Define features</span></span>

<span data-ttu-id="10840-227">在機器學習中， *功能* 是您感興趣的某項目的個別可測量的屬性。</span><span class="sxs-lookup"><span data-stu-id="10840-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="10840-228">在我們的資料集中，每個資料列都代表一部汽車，而每個資料行是該汽車的功能。</span><span class="sxs-lookup"><span data-stu-id="10840-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="10840-229">要找到一組理想的功能來建立預測模型，必須針對您要解決的問題進行實驗，並具備相關知識。</span><span class="sxs-lookup"><span data-stu-id="10840-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about the problem you want to solve.</span></span> <span data-ttu-id="10840-230">有些功能會比其他功能更適合用來預測目標。</span><span class="sxs-lookup"><span data-stu-id="10840-230">Some features are better for predicting the target than others.</span></span> <span data-ttu-id="10840-231">此外，某些功能與其他功能具有強相關性，而且可以移除。</span><span class="sxs-lookup"><span data-stu-id="10840-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="10840-232">例如，市區油耗和高速公路油耗密切相關，我們可以保留其中一項而移除另一項，這對預測不會有大幅影響。</span><span class="sxs-lookup"><span data-stu-id="10840-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove the other without significantly affecting the prediction.</span></span>

<span data-ttu-id="10840-233">我們將建置一個模型，並在其中使用我們資料集中的功能子集。</span><span class="sxs-lookup"><span data-stu-id="10840-233">Let's build a model that uses a subset of the features in our dataset.</span></span> <span data-ttu-id="10840-234">您稍後可以重新選取不同功能、再次執行實驗，並確認是否會有較理想的結果。</span><span class="sxs-lookup"><span data-stu-id="10840-234">You can come back later and select different features, run the experiment again, and see if you get better results.</span></span> <span data-ttu-id="10840-235">但是若要開始，讓我們試用下列功能︰</span><span class="sxs-lookup"><span data-stu-id="10840-235">But to start, let's try the following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="10840-236">將另一個[選取資料集中的資料行][select-columns]模組拖曳到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="10840-236">Drag another [Select Columns in Dataset][select-columns] module to the experiment canvas.</span></span> <span data-ttu-id="10840-237">將[清除遺漏資料][clean-missing-data]模組的左側輸出連接埠連接到[選取資料集中的資料行][select-columns]模組的輸入。</span><span class="sxs-lookup"><span data-stu-id="10840-237">Connect the left output port of the [Clean Missing Data][clean-missing-data] module to the input of the [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="10840-238">![將 [選取資料集中的資料行] 模組連接到 [清除遺漏的資料] 模組][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="10840-238">![Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="10840-239">***「 選取資料行中資料集 」 模組連接至 「 清除遺漏資料 」 模組***</span><span class="sxs-lookup"><span data-stu-id="10840-239">***Connect the "Select Columns in Dataset" module to the "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="10840-240">按兩下模組，並輸入「選取要預測的功能」。</span><span class="sxs-lookup"><span data-stu-id="10840-240">Double-click the module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="10840-241">按一下 [屬性] 窗格中的 [啟動資料行選取器]。</span><span class="sxs-lookup"><span data-stu-id="10840-241">Click **Launch column selector** in the **Properties** pane.</span></span>

3. <span data-ttu-id="10840-242">按一下 [套用規則] 。</span><span class="sxs-lookup"><span data-stu-id="10840-242">Click **With rules**.</span></span>

4. <span data-ttu-id="10840-243">在 [開始於] 下，按一下 [無資料行]。</span><span class="sxs-lookup"><span data-stu-id="10840-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="10840-244">在 [篩選] 資料列中，選取 [包含] 和 [資料行名稱]，然後在文字方塊中選取資料行名稱的清單。</span><span class="sxs-lookup"><span data-stu-id="10840-244">In the filter row, select **Include** and **column names** and select our list of column names in the text box.</span></span> <span data-ttu-id="10840-245">這會指示模組不要傳遞我們所指定以外的任何資料行 (功能)。</span><span class="sxs-lookup"><span data-stu-id="10840-245">This directs the module to not pass through any columns (features) except the ones that we specify.</span></span>

5. <span data-ttu-id="10840-246">按一下核取記號 ([確定]) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10840-246">Click the check mark (OK) button.</span></span>

    <span data-ttu-id="10840-247">![選取要包含在預測中的資料行 (功能)][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="10840-247">![Select the columns (features) to include in the prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="10840-248">***選取要包含在預測中的資料行 （功能）***</span><span class="sxs-lookup"><span data-stu-id="10840-248">***Select the columns (features) to include in the prediction***</span></span>

<span data-ttu-id="10840-249">這會產生已篩選的資料集，其中只包含我們想傳遞至下一個步驟中將使用之學習服務演算法的功能。</span><span class="sxs-lookup"><span data-stu-id="10840-249">This produces a filtered dataset containing only the features we want to pass to the learning algorithm we'll use in the next step.</span></span> <span data-ttu-id="10840-250">稍後您可以返回，並選取不同的功能重新嘗試。</span><span class="sxs-lookup"><span data-stu-id="10840-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="10840-251">步驟 4：選擇及套用學習演算法</span><span class="sxs-lookup"><span data-stu-id="10840-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="10840-252">現在，資料已備妥，訓練和測試是建構預測模型的要素。</span><span class="sxs-lookup"><span data-stu-id="10840-252">Now that the data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="10840-253">我們將使用我們的資料來訓練模型，然後測試模型，以檢驗它預測價格的精準度。</span><span class="sxs-lookup"><span data-stu-id="10840-253">We'll use our data to train the model, and then we'll test the model to see how closely it's able to predict prices.</span></span>
<!-- For now, don't worry about *why* we need to train and then test a model.-->

<span data-ttu-id="10840-254">*分類*和*迴歸*是兩種受監督的機器學習服務演算法。</span><span class="sxs-lookup"><span data-stu-id="10840-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="10840-255">「分類」可從一組已定義的類別預測答案，例如色彩 (紅色、藍色或綠色)。</span><span class="sxs-lookup"><span data-stu-id="10840-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="10840-256">「迴歸」可用來預測數字。</span><span class="sxs-lookup"><span data-stu-id="10840-256">Regression is used to predict a number.</span></span>

<span data-ttu-id="10840-257">因為要預測價格，也就是一個數字，因此我們將使用迴歸演算法。</span><span class="sxs-lookup"><span data-stu-id="10840-257">Because we want to predict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="10840-258">在此範例中，我們將使用簡單*線性迴歸*模型。</span><span class="sxs-lookup"><span data-stu-id="10840-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="10840-259">如果您想深入了解不同類型的機器學習服務演算法和使用時機，您可以檢視初學者資料科學系列中的第一部影片[資料科學解答的五個問題](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)。</span><span class="sxs-lookup"><span data-stu-id="10840-259">If you want to learn more about different types of machine learning algorithms and when to use them, you might view the first video in the Data Science for Beginners series, [The five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="10840-260">您也可以查看資訊圖[機器學習服務基本概念 (含演算法範例)](machine-learning-basics-infographic-with-algorithm-examples.md)，或查看[機器學習服務演算法小祕技](machine-learning-algorithm-cheat-sheet.md)。</span><span class="sxs-lookup"><span data-stu-id="10840-260">You might also look at the infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out the [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="10840-261">我們藉由提供一組包含價格的資料來訓練模型。</span><span class="sxs-lookup"><span data-stu-id="10840-261">We train the model by giving it a set of data that includes the price.</span></span> <span data-ttu-id="10840-262">模型會掃描的資料，然後尋找汽車功能與價格之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="10840-262">The model scans the data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="10840-263">然後，我們將測試模型 - 提供它一組我們熟悉的汽車功能，接著檢驗模型預測已知價格的精準度。</span><span class="sxs-lookup"><span data-stu-id="10840-263">Then we'll test the model - we'll give it a set of features for automobiles we're familiar with and see how close the model comes to predicting the known price.</span></span>

<span data-ttu-id="10840-264">我們將資料分割成個別的訓練和測試資料集，用來訓練和測試模型。</span><span class="sxs-lookup"><span data-stu-id="10840-264">We'll use our data for both training the model and testing it by splitting the data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="10840-265">選取 [分割資料][split] 模組並拖曳到實驗畫布，然後將其連接到最後一個 [選取資料集中的資料行][select-columns] 模組。</span><span class="sxs-lookup"><span data-stu-id="10840-265">Select and drag the [Split Data][split] module to the experiment canvas and connect it to the last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="10840-266">按一下[分割資料][split]模組以選取它。</span><span class="sxs-lookup"><span data-stu-id="10840-266">Click the [Split Data][split] module to select it.</span></span> <span data-ttu-id="10840-267">尋找 [第一個輸出資料集中的資料列分數] \(在畫布右邊的 [屬性] 窗格)，並將它設為 0.75。</span><span class="sxs-lookup"><span data-stu-id="10840-267">Find the **Fraction of rows in the first output dataset** (in the **Properties** pane to the right of the canvas) and set it to 0.75.</span></span> <span data-ttu-id="10840-268">如此，我們將使用百分之 75 的資料來訓練模型，並保留百分之 25 做為測試之用 (稍後，您可以使用不同的百分比來實驗)。</span><span class="sxs-lookup"><span data-stu-id="10840-268">This way, we'll use 75 percent of the data to train the model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="10840-269">![將 [分割資料] 模組的分割分數設為 0.75][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="10840-269">![Set the split fraction of the "Split Data" module to 0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="10840-270">***分割分數的 「 分割資料 」 的模組設 0.75***</span><span class="sxs-lookup"><span data-stu-id="10840-270">***Set the split fraction of the "Split Data" module to 0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="10840-271">變更 [ **隨機種子** ] 參數，可讓您為訓練和測試產生不同的隨機範例。</span><span class="sxs-lookup"><span data-stu-id="10840-271">By changing the **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="10840-272">此參數會控制虛擬隨機數字產生器的植入。</span><span class="sxs-lookup"><span data-stu-id="10840-272">This parameter controls the seeding of the pseudo-random number generator.</span></span>

2. <span data-ttu-id="10840-273">執行實驗。</span><span class="sxs-lookup"><span data-stu-id="10840-273">Run the experiment.</span></span> <span data-ttu-id="10840-274">執行實驗時，[選取資料集中的資料行][select-columns]和[分割資料][split]模組會將資料行定義傳遞至我們接下來要新增的模組。</span><span class="sxs-lookup"><span data-stu-id="10840-274">When the experiment is run, the [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions to the modules we'll be adding next.</span></span>  

3. <span data-ttu-id="10840-275">若要選取學習演算法，請在畫布左側的模組調色盤中展開 [機器學習服務] 類別，然後展開 [初始化模型]。</span><span class="sxs-lookup"><span data-stu-id="10840-275">To select the learning algorithm, expand the **Machine Learning** category in the module palette to the left of the canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="10840-276">這會顯示數個可用來初始化機器學習演算法的模組類別。</span><span class="sxs-lookup"><span data-stu-id="10840-276">This displays several categories of modules that can be used to initialize machine learning algorithms.</span></span> <span data-ttu-id="10840-277">在此實驗中，請選取 [迴歸] 類別下的[線性迴歸][linear-regression]模組，然後將其拖曳到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="10840-277">For this experiment, select the [Linear Regression][linear-regression] module under the **Regression** category, and drag it to the experiment canvas.</span></span>
<span data-ttu-id="10840-278">(您也可以在調色盤搜尋方塊中輸入「線性迴歸」以尋找模組。)</span><span class="sxs-lookup"><span data-stu-id="10840-278">(You can also find the module by typing "linear regression" in the palette Search box.)</span></span>

4. <span data-ttu-id="10840-279">找出[訓練模型][train-model]模組，並將其拖曳到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="10840-279">Find and drag the [Train Model][train-model] module to the experiment canvas.</span></span> <span data-ttu-id="10840-280">將[線性迴歸][linear-regression]模組的輸出連接到[訓練模型][train-model]模組的左側輸入，並將[分割資料][split]模組的訓練資料輸出 (左側連接埠) 連接到[訓練模型][train-model]模組的右側輸入。</span><span class="sxs-lookup"><span data-stu-id="10840-280">Connect the output of the [Linear Regression][linear-regression] module to the left input of the [Train Model][train-model] module, and connect the training data output (left port) of the [Split Data][split] module to the right input of the [Train Model][train-model] module.</span></span>

    <span data-ttu-id="10840-281">![將「評分模型」模組連接到「線性迴歸」和「分割資料」模組][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="10840-281">![Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="10840-282">***「 定型模型 」 模組連接至 「 線性迴歸 」 和 「 分割資料 」 模組***</span><span class="sxs-lookup"><span data-stu-id="10840-282">***Connect the "Train Model" module to both the "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="10840-283">按一下[訓練模型][train-model]模組，按一下 [屬性] 窗格中的 [啟動資料行選取器]，然後選取 [價格] 資料行。</span><span class="sxs-lookup"><span data-stu-id="10840-283">Click the [Train Model][train-model] module, click **Launch column selector** in the **Properties** pane, and then select the **price** column.</span></span> <span data-ttu-id="10840-284">這是我們的模型所將預測的值。</span><span class="sxs-lookup"><span data-stu-id="10840-284">This is the value that our model is going to predict.</span></span>

    <span data-ttu-id="10840-285">在資料行選取器中選取 [價格] 資料行 (將它從 [可用的資料行] 清單 移到 [選取的資料行] 清單)。</span><span class="sxs-lookup"><span data-stu-id="10840-285">You select the **price** column in the column selector by moving it from the **Available columns** list to the **Selected columns** list.</span></span>

    <span data-ttu-id="10840-286">![選取 [訓練模型] 模組的價格資料行][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="10840-286">![Select the price column for the "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="10840-287">***選取 「 定型模型 」 模組的價格資料行***</span><span class="sxs-lookup"><span data-stu-id="10840-287">***Select the price column for the "Train Model" module***</span></span>

6. <span data-ttu-id="10840-288">執行實驗。</span><span class="sxs-lookup"><span data-stu-id="10840-288">Run the experiment.</span></span>

<span data-ttu-id="10840-289">我們現在有經過訓練的迴歸模型可用來為新的汽車資料評分，以藉此預測價格。</span><span class="sxs-lookup"><span data-stu-id="10840-289">We now have a trained regression model that can be used to score new automobile data to make price predictions.</span></span>

<span data-ttu-id="10840-290">![執行後，實驗此時看起來應如下所示：][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="10840-290">![After running, the experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="10840-291">
***執行後，實驗此時看起來應如下所示：***</span><span class="sxs-lookup"><span data-stu-id="10840-291">
***After running, the experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="10840-292">步驟 5：預測新的汽車價格</span><span class="sxs-lookup"><span data-stu-id="10840-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="10840-293">現在已完成使用百分之 75 資料模型的訓練，我們可以用它來為其他百分之 25 的資料評分，以了解模型的運作是否理想。</span><span class="sxs-lookup"><span data-stu-id="10840-293">Now that we've trained the model using 75 percent of our data, we can use it to score the other 25 percent of the data to see how well our model functions.</span></span>

1. <span data-ttu-id="10840-294">找出[評分模型][score-model]模組，並將其拖曳到實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="10840-294">Find and drag the [Score Model][score-model] module to the experiment canvas.</span></span> <span data-ttu-id="10840-295">將[訓練模型][train-model]模組的輸出連接到[評分模型][score-model]的左側輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="10840-295">Connect the output of the [Train Model][train-model] module to the left input port of [Score Model][score-model].</span></span> <span data-ttu-id="10840-296">將[分割資料][split]模組的測試資料輸出 (右側連接埠) 連接到[評分模型][score-model]的右側輸入連接埠。</span><span class="sxs-lookup"><span data-stu-id="10840-296">Connect the test data output (right port) of the [Split Data][split] module to the right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="10840-297">![將「評分模型」模組連接到「訓練模型」和「分割資料」模組][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="10840-297">![Connect the "Score Model" module to both the "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="10840-298">***「 計分模型 」 模組連接至 「 定型模型 」 和 「 分割資料 」 模組***</span><span class="sxs-lookup"><span data-stu-id="10840-298">***Connect the "Score Model" module to both the "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="10840-299">執行實驗並檢視[評分模型][score-model]模組的輸出 (按一下[評分模型][score-model]的輸出連接埠，然後選取 [視覺化])。</span><span class="sxs-lookup"><span data-stu-id="10840-299">Run the experiment and view the output from the [Score Model][score-model] module (click the output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="10840-300">輸出會顯示價格的預測值，以及來自測試資料的已知值。</span><span class="sxs-lookup"><span data-stu-id="10840-300">The output shows the predicted values for price and the known values from the test data.</span></span>  

    <span data-ttu-id="10840-301">![「評分模型」模組的輸出][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="10840-301">![Output of the "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="10840-302">***「 計分模型 」 模組的輸出***</span><span class="sxs-lookup"><span data-stu-id="10840-302">***Output of the "Score Model" module***</span></span>

3. <span data-ttu-id="10840-303">最後，我們要測試結果的品質。</span><span class="sxs-lookup"><span data-stu-id="10840-303">Finally, we test the quality of the results.</span></span> <span data-ttu-id="10840-304">選取[評估模型][evaluate-model]模組，並將其拖曳至實驗畫布，然後將[評分模型][score-model]模組的輸出連接到[評估模型][evaluate-model]的左側輸入。</span><span class="sxs-lookup"><span data-stu-id="10840-304">Select and drag the [Evaluate Model][evaluate-model] module to the experiment canvas, and connect the output of the [Score Model][score-model] module to the left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="10840-305">[評估模型][evaluate-model]模組有兩個輸入連接埠，因為它可以並排方式來比較兩個模型。</span><span class="sxs-lookup"><span data-stu-id="10840-305">There are two input ports on the [Evaluate Model][evaluate-model] module because it can be used to compare two models side by side.</span></span> <span data-ttu-id="10840-306">稍後，您可以在實驗中新增其他演算法，並使用[評估模型][evaluate-model]查看哪一個提供更好的結果。</span><span class="sxs-lookup"><span data-stu-id="10840-306">Later, you can add another algorithm to the experiment and use [Evaluate Model][evaluate-model] to see which one gives better results.</span></span>

4. <span data-ttu-id="10840-307">執行實驗。</span><span class="sxs-lookup"><span data-stu-id="10840-307">Run the experiment.</span></span>

<span data-ttu-id="10840-308">若要檢視[評估模型][evaluate-model]模組的輸出，請按一下輸出連接埠，然後選取 [視覺化]。</span><span class="sxs-lookup"><span data-stu-id="10840-308">To view the output from the [Evaluate Model][evaluate-model] module, click the output port, and then select **Visualize**.</span></span>

<span data-ttu-id="10840-309">![實驗的評估結果][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="10840-309">![Evaluation results for the experiment][evaluation-results]
</span></span><br/><span data-ttu-id="10840-310">
***實驗的評估結果***</span><span class="sxs-lookup"><span data-stu-id="10840-310">
***Evaluation results for the experiment***</span></span>

<span data-ttu-id="10840-311">我們的模型會顯示下列統計資料：</span><span class="sxs-lookup"><span data-stu-id="10840-311">The following statistics are shown for our model:</span></span>

- <span data-ttu-id="10840-312">**平均絕對誤差** (MAE)：絕對誤差的平均值 ( *誤差* 是指預測值與實際值之間的差異)。</span><span class="sxs-lookup"><span data-stu-id="10840-312">**Mean Absolute Error** (MAE): The average of absolute errors (an *error* is the difference between the predicted value and the actual value).</span></span>
- <span data-ttu-id="10840-313">**均方根誤差** (RMSE)：對測試資料集所做之預測的平方誤差的評分根平均值。</span><span class="sxs-lookup"><span data-stu-id="10840-313">**Root Mean Squared Error** (RMSE): The square root of the average of squared errors of predictions made on the test dataset.</span></span>
- <span data-ttu-id="10840-314">**相對絕對誤差**：相對於實際值與所有實際值之平均值之間的絕對差異的絕對誤差平均值。</span><span class="sxs-lookup"><span data-stu-id="10840-314">**Relative Absolute Error**: The average of absolute errors relative to the absolute difference between actual values and the average of all actual values.</span></span>
- <span data-ttu-id="10840-315">**相對平方誤差**：相對於實際值與所有實際值之平均值之間的平方差異的平方誤差平均值。</span><span class="sxs-lookup"><span data-stu-id="10840-315">**Relative Squared Error**: The average of squared errors relative to the squared difference between the actual values and the average of all actual values.</span></span>
- <span data-ttu-id="10840-316">**決定係數**：也稱為 **R 平方值**，這是一個統計度量，可指出模型對於資料的適用程度。</span><span class="sxs-lookup"><span data-stu-id="10840-316">**Coefficient of Determination**: Also known as the **R squared value**, this is a statistical metric indicating how well a model fits the data.</span></span>

<span data-ttu-id="10840-317">針對每個誤差統計資料，越小越好。</span><span class="sxs-lookup"><span data-stu-id="10840-317">For each of the error statistics, smaller is better.</span></span> <span data-ttu-id="10840-318">值越小，表示預測越接近實際值。</span><span class="sxs-lookup"><span data-stu-id="10840-318">A smaller value indicates that the predictions more closely match the actual values.</span></span> <span data-ttu-id="10840-319">就 [決定係數] 而言，其值愈接近一 (1.0)，預測就愈精準。</span><span class="sxs-lookup"><span data-stu-id="10840-319">For **Coefficient of Determination**, the closer its value is to one (1.0), the better the predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="10840-320">最終實驗</span><span class="sxs-lookup"><span data-stu-id="10840-320">Final experiment</span></span>

<span data-ttu-id="10840-321">實驗最終應呈現如下：</span><span class="sxs-lookup"><span data-stu-id="10840-321">The final experiment should look something like this:</span></span>

<span data-ttu-id="10840-322">![最終實驗][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="10840-322">![The final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="10840-323">
***最終實驗***</span><span class="sxs-lookup"><span data-stu-id="10840-323">
***The final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="10840-324">後續步驟</span><span class="sxs-lookup"><span data-stu-id="10840-324">Next steps</span></span>

<span data-ttu-id="10840-325">現在您已經完成第一個機器學習服務教學課程並已設定實驗，您可以繼續改善模型，然後再將它部署為預測型 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="10840-325">Now that you've completed the first machine learning tutorial and have your experiment set up, you can continue to improve the model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="10840-326">**逐一檢測以嘗試改善模型** - 例如，您可以變更在預測中使用的功能。</span><span class="sxs-lookup"><span data-stu-id="10840-326">**Iterate to try to improve the model** - For example, you can change the features you use in your prediction.</span></span> <span data-ttu-id="10840-327">或者，您可以修改[線性迴歸][linear-regression]演算法的屬性，或嘗試完全不同的演算法。</span><span class="sxs-lookup"><span data-stu-id="10840-327">Or you can modify the properties of the [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="10840-328">您甚至可以同時在實驗中新增多個機器學習演算法，並使用[評估模型][evaluate-model]模組進行比較 (兩兩相比)。</span><span class="sxs-lookup"><span data-stu-id="10840-328">You can even add multiple machine learning algorithms to your experiment at one time and compare two of them by using the [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="10840-329">如需如何在單一實驗中比較多個模型的範例，請參閱 [Cortana Intelligence 資源庫](https://gallery.cortanaintelligence.com)中的[比較迴歸輸入變數](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5)。</span><span class="sxs-lookup"><span data-stu-id="10840-329">For an example of how to compare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in the [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="10840-330">若要複製實驗的任何反覆運算，請使用頁面底部的 [另存新檔] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="10840-330">To copy any iteration of your experiment, use the **SAVE AS** button at the bottom of the page.</span></span> <span data-ttu-id="10840-331">您可以按一下頁面底部的 [檢視執行歷程記錄]，以檢視實驗的所有反覆運算。</span><span class="sxs-lookup"><span data-stu-id="10840-331">You can see all the iterations of your experiment by clicking **VIEW RUN HISTORY** at the bottom of the page.</span></span> <span data-ttu-id="10840-332">如需詳細資訊，請參閱[在 Azure Machine Learning Studio 中管理實驗逐一查看][runhistory]。</span><span class="sxs-lookup"><span data-stu-id="10840-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="10840-333">**將模型部署為預測性 Web 服務** - 如果您對模型感到滿意，您可以將其部署為 Web 服務，用以透過新資料預測汽車價格。</span><span class="sxs-lookup"><span data-stu-id="10840-333">**Deploy the model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service to be used to predict automobile prices by using new data.</span></span> <span data-ttu-id="10840-334">如需詳細資訊，請參閱[部署 Azure Machine Learning Web 服務][publish]。</span><span class="sxs-lookup"><span data-stu-id="10840-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="10840-335">要深入了解？</span><span class="sxs-lookup"><span data-stu-id="10840-335">Want to learn more?</span></span> <span data-ttu-id="10840-336">如需建立、訓練、評分及部署模型之程序的更廣泛且更詳細的逐步解說，請參閱[使用 Azure Machine Learning 開發預測性解決方案][walkthrough]。</span><span class="sxs-lookup"><span data-stu-id="10840-336">For a more extensive and detailed walkthrough of the process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

[walkthrough]: machine-learning-walkthrough-develop-predictive-solution.md

<!-- Images -->
[sign-in-to-studio]: ./media/machine-learning-create-experiment/sign-in-to-studio.png
[rename-experiment]: ./media/machine-learning-create-experiment/rename-experiment.png
[visualize-auto-data]:./media/machine-learning-create-experiment/visualize-auto-data.png
[select-visualize]: ./media/machine-learning-create-experiment/select-visualize.png
[showing-excluded-column]:./media/machine-learning-create-experiment/showing-excluded-column.png
[set-remove-entire-row]:./media/machine-learning-create-experiment/set-remove-entire-row.png
[early-experiment-run]:./media/machine-learning-create-experiment/early-experiment-run.png
[select-columns-to-include]:./media/machine-learning-create-experiment/select-columns-to-include.png
[second-experiment-run]:./media/machine-learning-create-experiment/second-experiment-run.png
[connect-score-model]:./media/machine-learning-create-experiment/connect-score-model.png
[evaluation-results]:./media/machine-learning-create-experiment/evaluation-results.png
[complete-linear-regression-experiment]:./media/machine-learning-create-experiment/complete-linear-regression-experiment.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs to PNGs to remove animation --> 
[connect-train-model]:./media/machine-learning-create-experiment/connect-train-model.png
[select-price-column]:./media/machine-learning-create-experiment/select-price-column.png

[score-model-output]:./media/machine-learning-create-experiment/score-model-output.png

<!-- Module References -->
[evaluate-model]: https://msdn.microsoft.com/library/azure/927d65ac-3b50-4694-9903-20f6c1672089/
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
[clean-missing-data]: https://msdn.microsoft.com/library/azure/d2c5ca2f-7323-41a3-9b7e-da917c99f0c4/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/
