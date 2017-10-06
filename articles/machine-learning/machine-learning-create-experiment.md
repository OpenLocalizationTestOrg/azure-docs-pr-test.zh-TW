---
title: "aaaA Machine Learning Studio 中的簡易實驗 |Microsoft 文件"
description: "此機器學習服務教學課程會引導您輕鬆進行資料科學實驗。 我們會預測 hello 使用迴歸演算法的汽車價格。"
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
ms.openlocfilehash: fb215851d380acf7d0f4934a426283369f9c4ccb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="machine-learning-tutorial-create-your-first-data-science-experiment-in-azure-machine-learning-studio"></a><span data-ttu-id="f6bed-105">機器學習服務教學課程：在 Azure Machine Learning Studio 中建立您的第一個資料科學實驗</span><span class="sxs-lookup"><span data-stu-id="f6bed-105">Machine learning tutorial: Create your first data science experiment in Azure Machine Learning Studio</span></span>

<span data-ttu-id="f6bed-106">如果您從未使用過 **Azure Machine Learning Studio**，本教學課程很適合您。</span><span class="sxs-lookup"><span data-stu-id="f6bed-106">If you've never used **Azure Machine Learning Studio** before, this tutorial is for you.</span></span>

<span data-ttu-id="f6bed-107">在本教學課程中，我們將逐步引導 hello toouse Studio 第一次 toocreate 機器學習實驗。</span><span class="sxs-lookup"><span data-stu-id="f6bed-107">In this tutorial, we'll walk through how toouse Studio for hello first time toocreate a machine learning experiment.</span></span> <span data-ttu-id="f6bed-108">hello 實驗會測試預測 hello 根據不同的變數，例如產生和技術規格汽車價格的分析模型。</span><span class="sxs-lookup"><span data-stu-id="f6bed-108">hello experiment will test an analytical model that predicts hello price of an automobile based on different variables such as make and technical specifications.</span></span>

> [!NOTE]
> <span data-ttu-id="f6bed-109">本教學課程會示範 hello 基本概念的方式 toodrag 放模組至您的經驗，連接在一起，請執行 hello 實驗，並查看 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="f6bed-109">This tutorial shows you hello basics of how toodrag-and-drop modules onto your experiment, connect them together, run hello experiment, and look at hello results.</span></span> <span data-ttu-id="f6bed-110">我們不打算 toodiscuss hello 的機器學習的一般主題或 tooselect 並用 hello 100 + 內建演算法和資料操作已包含在 Studio 中。</span><span class="sxs-lookup"><span data-stu-id="f6bed-110">We're not going toodiscuss hello general topic of machine learning or how tooselect and use hello 100+ built-in algorithms and data manipulation modules included in Studio.</span></span>
>
><span data-ttu-id="f6bed-111">如果您是新 toomachine 學習，hello 影片系列[為初學者所設計的資料科學](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)可能是很好的起點 toostart。</span><span class="sxs-lookup"><span data-stu-id="f6bed-111">If you're new toomachine learning, hello video series [Data Science for Beginners](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md) might be a good place toostart.</span></span> <span data-ttu-id="f6bed-112">這一系列影片是絕佳的簡介 toomachine 學習使用日常用語和概念。</span><span class="sxs-lookup"><span data-stu-id="f6bed-112">This video series is a great introduction toomachine learning using everyday language and concepts.</span></span>
>
><span data-ttu-id="f6bed-113">如果您是熟悉 machine learning 中，但您想要尋求 Machine Learning Studio 和 hello 機器學習的演算法，它包含更多一般資訊，以下是一些實用的資源：</span><span class="sxs-lookup"><span data-stu-id="f6bed-113">If you're familiar with machine learning, but you're looking for more general information about Machine Learning Studio, and hello machine learning algorithms it contains, here are some good resources:</span></span>
>
- [<span data-ttu-id="f6bed-114">什麼是 Machine Learning Studio？</span><span class="sxs-lookup"><span data-stu-id="f6bed-114">What is Machine Learning Studio?</span></span>](machine-learning-what-is-ml-studio.md) <span data-ttu-id="f6bed-115">- 這是 Studio 的高階概觀。</span><span class="sxs-lookup"><span data-stu-id="f6bed-115">- This is a high-level overview of Studio.</span></span>
- <span data-ttu-id="f6bed-116">[機器學習演算法範例的基本概念](machine-learning-basics-infographic-with-algorithm-examples.md)-此資訊圖很有用，如果您想 toolearn 更多關於 hello 不同類型的機器學習 Studio 隨附的機器學習演算法。</span><span class="sxs-lookup"><span data-stu-id="f6bed-116">[Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md) - This infographic is useful if you want toolearn more about hello different types of machine learning algorithms included with Machine Learning Studio.</span></span>
- <span data-ttu-id="f6bed-117">[機器學習指南](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1)-本指南涵蓋 hello 資訊圖上述項目，但以互動形式類似的資訊。</span><span class="sxs-lookup"><span data-stu-id="f6bed-117">[Machine Learning Guide](https://gallery.cortanaintelligence.com/Tutorial/Machine-Learning-Guide-1) - This guide covers similar information as hello infographic above, but in an interactive format.</span></span>
- <span data-ttu-id="f6bed-118">[機器學習演算法小祕技](machine-learning-algorithm-cheat-sheet.md)和[如何 toochoose 演算法為 Microsoft Azure 機器學習](machine-learning-algorithm-choice.md)-此可下載海報和隨附的文章討論深度 hello Studio 演算法。</span><span class="sxs-lookup"><span data-stu-id="f6bed-118">[Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md) and [How toochoose algorithms for Microsoft Azure Machine Learning](machine-learning-algorithm-choice.md) - This downloadable poster and accompanying article discuss hello Studio algorithms in depth.</span></span>
- <span data-ttu-id="f6bed-119">[Machine Learning Studio： 演算法和模組說明](https://msdn.microsoft.com/library/azure/dn905974.aspx)-這是所有 Studio 模組，包括機器學習演算法，hello 完整的參考</span><span class="sxs-lookup"><span data-stu-id="f6bed-119">[Machine Learning Studio: Algorithm and Module Help](https://msdn.microsoft.com/library/azure/dn905974.aspx) - This is hello complete reference for all Studio modules, including machine learning algorithms,</span></span>

<!-- -->

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="how-does-machine-learning-studio-help"></a><span data-ttu-id="f6bed-120">Machine Learning Studio 如何協助您？</span><span class="sxs-lookup"><span data-stu-id="f6bed-120">How does Machine Learning Studio help?</span></span>

<span data-ttu-id="f6bed-121">Machine Learning Studio 可輕鬆 tooset 向上實驗中使用拖放模組預先排定使用預測模型的技巧。</span><span class="sxs-lookup"><span data-stu-id="f6bed-121">Machine Learning Studio makes it easy tooset up an experiment using drag-and-drop modules preprogrammed with predictive modeling techniques.</span></span>

<span data-ttu-id="f6bed-122">使用互動式的視覺化工作區，可以拖放***資料集***和***分析***模組到互動式畫布。</span><span class="sxs-lookup"><span data-stu-id="f6bed-122">Using an interactive, visual workspace, you drag-and-drop ***datasets*** and analysis ***modules*** onto an interactive canvas.</span></span> <span data-ttu-id="f6bed-123">連接在一起的 tooform***實驗***Machine Learning Studio 中執行。</span><span class="sxs-lookup"><span data-stu-id="f6bed-123">You connect them together tooform an ***experiment*** that you run in Machine Learning Studio.</span></span>
<span data-ttu-id="f6bed-124">您***建立模型***， ***hello 模型定型***，和***分數與測試 hello 模型***。</span><span class="sxs-lookup"><span data-stu-id="f6bed-124">You ***create a model***, ***train hello model***, and ***score and test hello model***.</span></span>

<span data-ttu-id="f6bed-125">您可以在逐一查看您的模型設計，編輯 hello 實驗，並執行直到它可讓您 hello 想要的結果。</span><span class="sxs-lookup"><span data-stu-id="f6bed-125">You can iterate on your model design, editing hello experiment and running it until it gives you hello results you're looking for.</span></span> <span data-ttu-id="f6bed-126">當您的模型就緒後，您可以將其發行為 ***Web 服務***，讓其他人可以傳送新資料到該服務，並取得預測結果。</span><span class="sxs-lookup"><span data-stu-id="f6bed-126">When your model is ready, you can publish it as a ***web service*** so that others can send it new data and get predictions in return.</span></span>

## <a name="open-machine-learning-studio"></a><span data-ttu-id="f6bed-127">開啟 Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="f6bed-127">Open Machine Learning Studio</span></span>

<span data-ttu-id="f6bed-128">Studio 中，以啟動 tooget 移過[https://studio.azureml.net](https://studio.azureml.net)。</span><span class="sxs-lookup"><span data-stu-id="f6bed-128">tooget started with Studio, go too[https://studio.azureml.net](https://studio.azureml.net).</span></span> <span data-ttu-id="f6bed-129">如果您之前已登入過 Machine Learning Studio，請按一下 [登入]。</span><span class="sxs-lookup"><span data-stu-id="f6bed-129">If you’ve signed into Machine Learning Studio before, click **Sign In**.</span></span> <span data-ttu-id="f6bed-130">否則，請按一下 [由此註冊] 並選擇免費或付費選項。</span><span class="sxs-lookup"><span data-stu-id="f6bed-130">Otherwise, click **Sign up here** and choose between free and paid options.</span></span>

<span data-ttu-id="f6bed-131">![登入 tooMachine Learning Studio][sign-in-to-studio]
</span><span class="sxs-lookup"><span data-stu-id="f6bed-131">![Sign in tooMachine Learning Studio][sign-in-to-studio]
</span></span><br/><span data-ttu-id="f6bed-132">
***登入 tooMachine Learning Studio***</span><span class="sxs-lookup"><span data-stu-id="f6bed-132">
***Sign in tooMachine Learning Studio***</span></span>

## <a name="five-steps-toocreate-an-experiment"></a><span data-ttu-id="f6bed-133">五個步驟 toocreate 實驗</span><span class="sxs-lookup"><span data-stu-id="f6bed-133">Five steps toocreate an experiment</span></span>

<span data-ttu-id="f6bed-134">在此機器學習教學課程中，您將遵循五個基本步驟 toobuild Machine Learning Studio toocreate，定型，在實驗和計分模型：</span><span class="sxs-lookup"><span data-stu-id="f6bed-134">In this machine learning tutorial, you'll follow five basic steps toobuild an experiment in Machine Learning Studio toocreate, train, and score your model:</span></span>

- <span data-ttu-id="f6bed-135">**建立模型**</span><span class="sxs-lookup"><span data-stu-id="f6bed-135">**Create a model**</span></span>
    - <span data-ttu-id="f6bed-136">[步驟 1：取得資料]</span><span class="sxs-lookup"><span data-stu-id="f6bed-136">[Step 1: Get data]</span></span>
    - <span data-ttu-id="f6bed-137">[步驟 2： 準備 hello 資料]</span><span class="sxs-lookup"><span data-stu-id="f6bed-137">[Step 2: Prepare hello data]</span></span>
    - <span data-ttu-id="f6bed-138">[步驟 3：定義功能]</span><span class="sxs-lookup"><span data-stu-id="f6bed-138">[Step 3: Define features]</span></span>
- <span data-ttu-id="f6bed-139">**定型 hello 模型**</span><span class="sxs-lookup"><span data-stu-id="f6bed-139">**Train hello model**</span></span>
    - <span data-ttu-id="f6bed-140">[步驟 4：選擇及套用學習演算法]</span><span class="sxs-lookup"><span data-stu-id="f6bed-140">[Step 4: Choose and apply a learning algorithm]</span></span>
- <span data-ttu-id="f6bed-141">**分數與測試 hello 模型**</span><span class="sxs-lookup"><span data-stu-id="f6bed-141">**Score and test hello model**</span></span>
    - <span data-ttu-id="f6bed-142">[步驟 5：預測新的汽車價格]</span><span class="sxs-lookup"><span data-stu-id="f6bed-142">[Step 5: Predict new automobile prices]</span></span>

[步驟 1：取得資料]: #step-1-get-data
[步驟 2： 準備 hello 資料]: #step-2-prepare-the-data
[步驟 3：定義功能]: #step-3-define-features
[步驟 4：選擇及套用學習演算法]: #step-4-choose-and-apply-a-learning-algorithm
[步驟 5：預測新的汽車價格]: #step-5-predict-new-automobile-prices

> [!TIP] 
> <span data-ttu-id="f6bed-148">您可以找到 hello 的下列實驗中 hello [Cortana 智慧組件庫](https://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="f6bed-148">You can find a working copy of hello following experiment in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span> <span data-ttu-id="f6bed-149">跳過**[第一次的資料科學實驗-汽車價格預測](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)**按一下**在 Studio 中開啟**toodownload hello 到機器學習的實驗的複本Studio 工作區。</span><span class="sxs-lookup"><span data-stu-id="f6bed-149">Go too**[Your first data science experiment - Automobile price prediction](https://gallery.cortanaintelligence.com/Experiment/Your-first-data-science-experiment-Automobile-price-prediction-1)** and click **Open in Studio** toodownload a copy of hello experiment into your Machine Learning Studio workspace.</span></span>


## <a name="step-1-get-data"></a><span data-ttu-id="f6bed-150">步驟 1：取得資料</span><span class="sxs-lookup"><span data-stu-id="f6bed-150">Step 1: Get data</span></span>

<span data-ttu-id="f6bed-151">您需要 tooperform 機器學習 hello 第一件事是資料。</span><span class="sxs-lookup"><span data-stu-id="f6bed-151">hello first thing you need tooperform machine learning is data.</span></span>
<span data-ttu-id="f6bed-152">Machine Learning Studio 隨附多個範例資料集供您使用，或者，您可以從許多來源匯入資料。</span><span class="sxs-lookup"><span data-stu-id="f6bed-152">There are several sample datasets included with Machine Learning Studio that you can use, or you can import data from many sources.</span></span> <span data-ttu-id="f6bed-153">此範例中，我們將使用 hello 範例資料集，**汽車價格資料 (Raw)**，被包含在您的工作區。</span><span class="sxs-lookup"><span data-stu-id="f6bed-153">For this example, we'll use hello sample dataset, **Automobile price data (Raw)**, that's included in your workspace.</span></span>
<span data-ttu-id="f6bed-154">此資料集將包含許多個別汽車的項目，包括製造、模型、技術規格和價格等資訊。</span><span class="sxs-lookup"><span data-stu-id="f6bed-154">This dataset includes entries for various individual automobiles, including information such as make, model, technical specifications, and price.</span></span>

<span data-ttu-id="f6bed-155">以下是如何 tooget hello 到您的經驗的資料集。</span><span class="sxs-lookup"><span data-stu-id="f6bed-155">Here's how tooget hello dataset into your experiment.</span></span>

1. <span data-ttu-id="f6bed-156">按一下 建立新的實驗**+ 新增**在 hello hello Machine Learning Studio 視窗底部，選取**實驗**，然後選取**空白實驗**。</span><span class="sxs-lookup"><span data-stu-id="f6bed-156">Create a new experiment by clicking **+NEW** at hello bottom of hello Machine Learning Studio window, select **EXPERIMENT**, and then select **Blank Experiment**.</span></span>

2. <span data-ttu-id="f6bed-157">hello 實驗會給予您可以查看 hello hello 畫布上方的預設名稱。</span><span class="sxs-lookup"><span data-stu-id="f6bed-157">hello experiment is given a default name that you can see at hello top of hello canvas.</span></span> <span data-ttu-id="f6bed-158">選取這段文字，並將它重新命名 toosomething 有意義，例如**汽車價格預測**。</span><span class="sxs-lookup"><span data-stu-id="f6bed-158">Select this text and rename it toosomething meaningful, for example, **Automobile price prediction**.</span></span> <span data-ttu-id="f6bed-159">hello 名稱不需要 toobe 唯一。</span><span class="sxs-lookup"><span data-stu-id="f6bed-159">hello name doesn't need toobe unique.</span></span>

    ![重新命名 hello 實驗][rename-experiment]

2. <span data-ttu-id="f6bed-161">toohello hello 實驗畫布左邊是資料集和模組的調色盤。</span><span class="sxs-lookup"><span data-stu-id="f6bed-161">toohello left of hello experiment canvas is a palette of datasets and modules.</span></span> <span data-ttu-id="f6bed-162">型別**汽車**在 hello 搜尋 方塊上方標示為此調色盤 toofind hello 資料集的 hello**汽車價格資料 (Raw)**。</span><span class="sxs-lookup"><span data-stu-id="f6bed-162">Type **automobile** in hello Search box at hello top of this palette toofind hello dataset labeled **Automobile price data (Raw)**.</span></span> <span data-ttu-id="f6bed-163">將此資料集 toohello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="f6bed-163">Drag this dataset toohello experiment canvas.</span></span>

    <span data-ttu-id="f6bed-164">![尋找 hello 汽車的資料集，並將它拖曳至 hello 實驗畫布][type-automobile]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-164">![Find hello automobile dataset and drag it onto hello experiment canvas][type-automobile]
    </span></span><br/>
 <span data-ttu-id="f6bed-165">***尋找 hello 汽車的資料集，並將它拖曳至 hello 實驗畫布***</span><span class="sxs-lookup"><span data-stu-id="f6bed-165">***Find hello automobile dataset and drag it onto hello experiment canvas***</span></span>

<span data-ttu-id="f6bed-166">toosee 什麼這項資料看來，按一下底端 hello hello 汽車的資料集，hello 輸出連接埠，然後選取**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="f6bed-166">toosee what this data looks like, click hello output port at hello bottom of hello automobile dataset, and then select **Visualize**.</span></span>

<span data-ttu-id="f6bed-167">![按一下 hello 輸出連接埠，然後選取 「 視覺化"][select-visualize]
</span><span class="sxs-lookup"><span data-stu-id="f6bed-167">![Click hello output port and select "Visualize"][select-visualize]
</span></span><br/><span data-ttu-id="f6bed-168">
***按一下 hello 輸出連接埠，然後選取 「 視覺化"***</span><span class="sxs-lookup"><span data-stu-id="f6bed-168">
***Click hello output port and select "Visualize"***</span></span>

> [!TIP]
> <span data-ttu-id="f6bed-169">資料集和模組具有輸入和輸出連接埠由小圓形-在 hello 上方的輸入連接埠輸出 hello 底端的連接埠。</span><span class="sxs-lookup"><span data-stu-id="f6bed-169">Datasets and modules have input and output ports represented by small circles - input ports at hello top, output ports at hello bottom.</span></span>
<span data-ttu-id="f6bed-170">toocreate 透過實驗資料的流程，您連接的另一個模組 tooan 輸入埠的輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="f6bed-170">toocreate a flow of data through your experiment, you'll connect an output port of one module tooan input port of another.</span></span>
<span data-ttu-id="f6bed-171">在任何時候，您可以按一下資料集或模組 toosee hello 輸出連接埠 hello 資料看起來像此時 hello 資料流程中。</span><span class="sxs-lookup"><span data-stu-id="f6bed-171">At any time, you can click hello output port of a dataset or module toosee what hello data looks like at that point in hello data flow.</span></span>

<span data-ttu-id="f6bed-172">在此範例資料集中，汽車的每個執行個體顯示為一個資料列，並與每個汽車相關聯的 hello 變數顯示為資料行。</span><span class="sxs-lookup"><span data-stu-id="f6bed-172">In this sample dataset, each instance of an automobile appears as a row, and hello variables associated with each automobile appear as columns.</span></span> <span data-ttu-id="f6bed-173">指定特定的汽車 hello 變數，我們 tootry toopredict hello 價格最右側資料行 (資料行 26，標題為"price") 中。</span><span class="sxs-lookup"><span data-stu-id="f6bed-173">Given hello variables for a specific automobile, we're going tootry toopredict hello price in far-right column (column 26, titled "price").</span></span>

<span data-ttu-id="f6bed-174">![在 hello 資料視覺效果視窗中檢視 hello 汽車資料][visualize-auto-data]
</span><span class="sxs-lookup"><span data-stu-id="f6bed-174">![View hello automobile data in hello data visualization window][visualize-auto-data]
</span></span><br/><span data-ttu-id="f6bed-175">
***在 hello 資料視覺效果視窗中檢視 hello 汽車資料***</span><span class="sxs-lookup"><span data-stu-id="f6bed-175">
***View hello automobile data in hello data visualization window***</span></span>

<span data-ttu-id="f6bed-176">按一下 hello 關閉 hello 視覺效果視窗"**x**"hello 右上角。</span><span class="sxs-lookup"><span data-stu-id="f6bed-176">Close hello visualization window by clicking hello "**x**" in hello upper-right corner.</span></span>

## <a name="step-2-prepare-hello-data"></a><span data-ttu-id="f6bed-177">步驟 2： 準備 hello 資料</span><span class="sxs-lookup"><span data-stu-id="f6bed-177">Step 2: Prepare hello data</span></span>

<span data-ttu-id="f6bed-178">資料集通常必須先經過某些前置處理，才能進行分析。</span><span class="sxs-lookup"><span data-stu-id="f6bed-178">A dataset usually requires some preprocessing before it can be analyzed.</span></span> <span data-ttu-id="f6bed-179">例如，您可能已注意到 hello 遺漏 hello 的各種不同的資料列的資料行中存在的值。</span><span class="sxs-lookup"><span data-stu-id="f6bed-179">For example, you might have noticed hello missing values present in hello columns of various rows.</span></span> <span data-ttu-id="f6bed-180">Toobe 清除 hello 模型可以分析 hello 資料正確，因此需要這些遺漏的值。</span><span class="sxs-lookup"><span data-stu-id="f6bed-180">These missing values need toobe cleaned so hello model can analyze hello data correctly.</span></span> <span data-ttu-id="f6bed-181">在我們的案例中，我們將移除含有遺漏值的所有資料列。</span><span class="sxs-lookup"><span data-stu-id="f6bed-181">In our case, we'll remove any rows that have missing values.</span></span> <span data-ttu-id="f6bed-182">此外，hello**正常化損失**資料行有大比例的遺漏值，因此我們將會排除該資料行 hello 模型完全。</span><span class="sxs-lookup"><span data-stu-id="f6bed-182">Also, hello **normalized-losses** column has a large proportion of missing values, so we'll exclude that column from hello model altogether.</span></span>

> [!TIP]
> <span data-ttu-id="f6bed-183">清理 hello 遺漏值，從輸入資料是使用大多數 hello 模組的必要條件。</span><span class="sxs-lookup"><span data-stu-id="f6bed-183">Cleaning hello missing values from input data is a prerequisite for using most of hello modules.</span></span>

<span data-ttu-id="f6bed-184">我們先新增移除 hello 模組**正常化損失**資料行完全，然後我們將會移除有遺漏資料的任何資料列的另一個模組。</span><span class="sxs-lookup"><span data-stu-id="f6bed-184">First we add a module that removes hello **normalized-losses** column completely, and then we add another module that removes any row that has missing data.</span></span>

1. <span data-ttu-id="f6bed-185">型別**選取資料行**在 hello 搜尋 方塊上方的 hello 模組調色盤 toofind hello hello[資料集中選取的資料行][ select-columns]模組，然後將它拖曳 toohello 實驗畫布.</span><span class="sxs-lookup"><span data-stu-id="f6bed-185">Type **select columns** in hello Search box at hello top of hello module palette toofind hello [Select Columns in Dataset][select-columns] module, then drag it toohello experiment canvas.</span></span> <span data-ttu-id="f6bed-186">此模組可讓我們 tooselect 我們想 tooinclude 中或排除的哪些資料行 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="f6bed-186">This module allows us tooselect which columns of data we want tooinclude or exclude in hello model.</span></span>

2. <span data-ttu-id="f6bed-187">連接 hello hello 輸出連接埠**汽車價格資料 (Raw)**資料集 toohello 輸入連接埠 hello[資料集中選取的資料行][ select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="f6bed-187">Connect hello output port of hello **Automobile price data (Raw)** dataset toohello input port of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="f6bed-188">![加入 hello 」 選取資料行中資料集 」 模組 toohello 實驗畫布，其連接][type-select-columns]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-188">![Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it][type-select-columns]
    </span></span><br/>
 <span data-ttu-id="f6bed-189">***加入 hello 」 選取資料行中資料集 」 模組 toohello 實驗畫布，其連接***</span><span class="sxs-lookup"><span data-stu-id="f6bed-189">***Add hello "Select Columns in Dataset" module toohello experiment canvas and connect it***</span></span>

3. <span data-ttu-id="f6bed-190">按一下 hello[資料集中選取的資料行][ select-columns]模組，然後按一下**啟動資料行選取器**在 hello**屬性**窗格。</span><span class="sxs-lookup"><span data-stu-id="f6bed-190">Click hello [Select Columns in Dataset][select-columns] module and click **Launch column selector** in hello **Properties** pane.</span></span>

    - <span data-ttu-id="f6bed-191">Hello 左側，按一下 **規則**</span><span class="sxs-lookup"><span data-stu-id="f6bed-191">On hello left, click **With rules**</span></span>
    - <span data-ttu-id="f6bed-192">在 [開始於] 下，按一下 [所有資料行]。</span><span class="sxs-lookup"><span data-stu-id="f6bed-192">Under **Begin With**, click **All columns**.</span></span> <span data-ttu-id="f6bed-193">這樣便會指引[資料集中選取的資料行][ select-columns] toopass 透過所有的 hello 資料行 （除了我們 tooexclude 有關這些資料行）。</span><span class="sxs-lookup"><span data-stu-id="f6bed-193">This directs [Select Columns in Dataset][select-columns] toopass through all hello columns (except those columns we're about tooexclude).</span></span>
    - <span data-ttu-id="f6bed-194">從 [hello] 下拉式清單，選取 [**排除**和**資料行名稱**，然後按一下hello] 文字方塊內。</span><span class="sxs-lookup"><span data-stu-id="f6bed-194">From hello drop-downs, select **Exclude** and **column names**, and then click inside hello text box.</span></span> <span data-ttu-id="f6bed-195">資料行清單隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="f6bed-195">A list of columns is displayed.</span></span> <span data-ttu-id="f6bed-196">選取**正常化損失**，而且它是加入的 toohello 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="f6bed-196">Select **normalized-losses**, and it's added toohello text box.</span></span>
    - <span data-ttu-id="f6bed-197">按一下 hello （確定） 的核取記號按鈕 tooclose hello 資料行選取器 （在 hello 右下方)。</span><span class="sxs-lookup"><span data-stu-id="f6bed-197">Click hello check mark (OK) button tooclose hello column selector (on hello lower-right).</span></span>

    <span data-ttu-id="f6bed-198">![啟動 hello 資料行選取器，並排除 hello"正常化損失 」 資料行][launch-column-selector]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-198">![Launch hello column selector and exclude hello "normalized-losses" column][launch-column-selector]
    </span></span><br/>
 <span data-ttu-id="f6bed-199">***啟動 hello 資料行選取器，並排除 hello"正常化損失 」 資料行***</span><span class="sxs-lookup"><span data-stu-id="f6bed-199">***Launch hello column selector and exclude hello "normalized-losses" column***</span></span>

    <span data-ttu-id="f6bed-200">現在 hello 屬性 窗格**資料集中選取的資料行**指出它將會傳遞通過所有資料行除了 hello 集中**正常化損失**。</span><span class="sxs-lookup"><span data-stu-id="f6bed-200">Now hello properties pane for **Select Columns in Dataset** indicates that it will pass through all columns from hello dataset except **normalized-losses**.</span></span>

    <span data-ttu-id="f6bed-201">![hello 屬性 窗格會顯示已排除該 hello"正常化損失 」 資料行][showing-excluded-column]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-201">![hello properties pane shows that hello "normalized-losses" column is excluded][showing-excluded-column]
    </span></span><br/>
 <span data-ttu-id="f6bed-202">***hello 屬性 窗格會顯示已排除該 hello"正常化損失 」 資料行***</span><span class="sxs-lookup"><span data-stu-id="f6bed-202">***hello properties pane shows that hello "normalized-losses" column is excluded***</span></span>

    > [!TIP]
    <span data-ttu-id="f6bed-203">您可以新增註解 tooa 模組按兩下 hello 模組和輸入的文字。</span><span class="sxs-lookup"><span data-stu-id="f6bed-203">You can add a comment tooa module by double-clicking hello module and entering text.</span></span> <span data-ttu-id="f6bed-204">這可協助您快速地查看哪些 hello 模組負責在您實驗中。</span><span class="sxs-lookup"><span data-stu-id="f6bed-204">This can help you see at a glance what hello module is doing in your experiment.</span></span> <span data-ttu-id="f6bed-205">在此情況下按兩下 hello[資料集中選取的資料行][ select-columns]模組和類型 hello 註解 」"排除正常化損失。</span><span class="sxs-lookup"><span data-stu-id="f6bed-205">In this case double-click hello [Select Columns in Dataset][select-columns] module and type hello comment "Exclude normalized losses."</span></span>
    >
    >


    <span data-ttu-id="f6bed-206">![按兩下模組 tooadd 註解][add-comment]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-206">![Double-click a module tooadd a comment][add-comment]
    </span></span><br/>
 <span data-ttu-id="f6bed-207">***按兩下模組 tooadd 註解***</span><span class="sxs-lookup"><span data-stu-id="f6bed-207">***Double-click a module tooadd a comment***</span></span>

3. <span data-ttu-id="f6bed-208">拖曳 hello[清除遺漏資料][ clean-missing-data]模組 toohello 實驗畫布，並將它連接 toohello[資料集中選取的資料行][ select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="f6bed-208">Drag hello [Clean Missing Data][clean-missing-data] module toohello experiment canvas and connect it toohello [Select Columns in Dataset][select-columns] module.</span></span> <span data-ttu-id="f6bed-209">在 hello**屬性**窗格中，選取**移除整個資料列**下**清潔模式**。</span><span class="sxs-lookup"><span data-stu-id="f6bed-209">In hello **Properties** pane, select **Remove entire row** under **Cleaning mode**.</span></span> <span data-ttu-id="f6bed-210">這樣便會指引[清除遺漏資料][ clean-missing-data] tooclean hello 資料，藉由移除有任何遺漏值的資料列。</span><span class="sxs-lookup"><span data-stu-id="f6bed-210">This directs [Clean Missing Data][clean-missing-data] tooclean hello data by removing rows that have any missing values.</span></span> <span data-ttu-id="f6bed-211">按兩下 hello 模組，然後輸入 hello 註解 [移除遺漏的值資料列]。</span><span class="sxs-lookup"><span data-stu-id="f6bed-211">Double-click hello module and type hello comment "Remove missing value rows."</span></span>

    <span data-ttu-id="f6bed-212">![設定 hello 清理模式太 」 移除整個資料列"hello"清除遺漏資料 」 模組][set-remove-entire-row]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-212">![Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module][set-remove-entire-row]
    </span></span><br/>
 <span data-ttu-id="f6bed-213">***設定 hello 清理模式太 」 移除整個資料列"hello"清除遺漏資料 」 模組***</span><span class="sxs-lookup"><span data-stu-id="f6bed-213">***Set hello cleaning mode too"Remove entire row" for hello "Clean Missing Data" module***</span></span>

4. <span data-ttu-id="f6bed-214">按一下以執行 hello 實驗**執行**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="f6bed-214">Run hello experiment by clicking **RUN** at hello bottom of hello page.</span></span>

    <span data-ttu-id="f6bed-215">當 hello 實驗完成執行時，所有 hello 模組都有綠色核取記號 tooindicate 它們順利完成。</span><span class="sxs-lookup"><span data-stu-id="f6bed-215">When hello experiment has finished running, all hello modules have a green check mark tooindicate that they finished successfully.</span></span> <span data-ttu-id="f6bed-216">請注意也 hello**完成的執行**hello 右上角中的狀態。</span><span class="sxs-lookup"><span data-stu-id="f6bed-216">Notice also hello **Finished running** status in hello upper-right corner.</span></span>

<span data-ttu-id="f6bed-217">![在執行 hello 實驗看起來應該像這樣][early-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="f6bed-217">![After running it, hello experiment should look something like this][early-experiment-run]
</span></span><br/><span data-ttu-id="f6bed-218">
***在執行 hello 實驗看起來應該像這樣***</span><span class="sxs-lookup"><span data-stu-id="f6bed-218">
***After running it, hello experiment should look something like this***</span></span>

> [!TIP]
> <span data-ttu-id="f6bed-219">為什麼沒有我們 hello 實驗立即執行？</span><span class="sxs-lookup"><span data-stu-id="f6bed-219">Why did we run hello experiment now?</span></span> <span data-ttu-id="f6bed-220">所執行的 hello 實驗 hello 我們資料的資料行定義傳遞 hello 資料集，透過 hello[資料集中選取的資料行][ select-columns]模組，以及透過 hello[清除遺漏資料][ clean-missing-data]模組。</span><span class="sxs-lookup"><span data-stu-id="f6bed-220">By running hello experiment, hello column definitions for our data pass from hello dataset, through hello [Select Columns in Dataset][select-columns] module, and through hello [Clean Missing Data][clean-missing-data] module.</span></span> <span data-ttu-id="f6bed-221">這表示我們太連接任何模組[清除遺漏資料][ clean-missing-data]也會有此相同資訊。</span><span class="sxs-lookup"><span data-stu-id="f6bed-221">This means that any modules we connect too[Clean Missing Data][clean-missing-data] will also have this same information.</span></span>

<span data-ttu-id="f6bed-222">我們已完成設定 toothis 點 hello 實驗中所有是全新的 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="f6bed-222">All we have done in hello experiment up toothis point is clean hello data.</span></span> <span data-ttu-id="f6bed-223">如果您想 tooview hello 清除資料集時，按一下左 hello 輸出連接埠的 hello[清除遺漏資料][ clean-missing-data]模組，然後選取**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="f6bed-223">If you want tooview hello cleaned dataset, click hello left output port of hello [Clean Missing Data][clean-missing-data] module and select **Visualize**.</span></span> <span data-ttu-id="f6bed-224">請注意該 hello**正常化損失**資料行已不再包含在內，，有沒有遺漏值。</span><span class="sxs-lookup"><span data-stu-id="f6bed-224">Notice that hello **normalized-losses** column is no longer included, and there are no missing values.</span></span>

<span data-ttu-id="f6bed-225">現在 hello 資料是乾淨的我們已準備好 toospecify 功能我們要 toouse hello 預測模型中的。</span><span class="sxs-lookup"><span data-stu-id="f6bed-225">Now that hello data is clean, we're ready toospecify what features we're going toouse in hello predictive model.</span></span>

## <a name="step-3-define-features"></a><span data-ttu-id="f6bed-226">步驟 3：定義功能</span><span class="sxs-lookup"><span data-stu-id="f6bed-226">Step 3: Define features</span></span>

<span data-ttu-id="f6bed-227">在機器學習中， *功能* 是您感興趣的某項目的個別可測量的屬性。</span><span class="sxs-lookup"><span data-stu-id="f6bed-227">In machine learning, *features* are individual measurable properties of something you’re interested in.</span></span> <span data-ttu-id="f6bed-228">在我們的資料集中，每個資料列都代表一部汽車，而每個資料行是該汽車的功能。</span><span class="sxs-lookup"><span data-stu-id="f6bed-228">In our dataset, each row represents one automobile, and each column is a feature of that automobile.</span></span>

<span data-ttu-id="f6bed-229">您想 toosolve 尋找一組良好的功能來建立預測模型需要的試驗與 hello 問題的相關知識。</span><span class="sxs-lookup"><span data-stu-id="f6bed-229">Finding a good set of features for creating a predictive model requires experimentation and knowledge about hello problem you want toosolve.</span></span> <span data-ttu-id="f6bed-230">某些功能可更好預測比其他 hello 目標。</span><span class="sxs-lookup"><span data-stu-id="f6bed-230">Some features are better for predicting hello target than others.</span></span> <span data-ttu-id="f6bed-231">此外，某些功能與其他功能具有強相關性，而且可以移除。</span><span class="sxs-lookup"><span data-stu-id="f6bed-231">Also, some features have a strong correlation with other features and can be removed.</span></span> <span data-ttu-id="f6bed-232">例如，城市 mpg 和高速公路 mpg 密切相關因此我們可以保留其中一個，而不會大幅影響 hello 預測移除其他 hello。</span><span class="sxs-lookup"><span data-stu-id="f6bed-232">For example, city-mpg and highway-mpg are closely related so we can keep one and remove hello other without significantly affecting hello prediction.</span></span>

<span data-ttu-id="f6bed-233">我們來建置在我們的資料集使用 hello 功能子集的模型。</span><span class="sxs-lookup"><span data-stu-id="f6bed-233">Let's build a model that uses a subset of hello features in our dataset.</span></span> <span data-ttu-id="f6bed-234">您可以於稍後回顧並選取不同的功能、 hello 實驗再次執行，並檢查是否可以取得更好的結果。</span><span class="sxs-lookup"><span data-stu-id="f6bed-234">You can come back later and select different features, run hello experiment again, and see if you get better results.</span></span> <span data-ttu-id="f6bed-235">但 toostart，讓我們來試試 hello 下列功能：</span><span class="sxs-lookup"><span data-stu-id="f6bed-235">But toostart, let's try hello following features:</span></span>

    make, body-style, wheel-base, engine-size, horsepower, peak-rpm, highway-mpg, price


1. <span data-ttu-id="f6bed-236">拖曳其他[資料集中選取的資料行][ select-columns]模組 toohello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="f6bed-236">Drag another [Select Columns in Dataset][select-columns] module toohello experiment canvas.</span></span> <span data-ttu-id="f6bed-237">連接保留 hello 輸出連接埠的 hello[清除遺漏資料][ clean-missing-data]模組 toohello 輸入的 hello[資料集中選取的資料行][ select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="f6bed-237">Connect hello left output port of hello [Clean Missing Data][clean-missing-data] module toohello input of hello [Select Columns in Dataset][select-columns] module.</span></span>

    <span data-ttu-id="f6bed-238">![連接 hello 」 選取資料行中資料集 」 模組 toohello 」 清除遺漏資料 」 模組][connect-clean-to-select]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-238">![Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module][connect-clean-to-select]
    </span></span><br/>
 <span data-ttu-id="f6bed-239">***連接 hello 」 選取資料行中資料集 」 模組 toohello 」 清除遺漏資料 」 模組***</span><span class="sxs-lookup"><span data-stu-id="f6bed-239">***Connect hello "Select Columns in Dataset" module toohello "Clean Missing Data" module***</span></span>

2. <span data-ttu-id="f6bed-240">按兩下 hello 模組，然後輸入 [預測的選取功能。]</span><span class="sxs-lookup"><span data-stu-id="f6bed-240">Double-click hello module and type "Select features for prediction."</span></span>

2. <span data-ttu-id="f6bed-241">按一下**啟動資料行選取器**在 hello**屬性**窗格。</span><span class="sxs-lookup"><span data-stu-id="f6bed-241">Click **Launch column selector** in hello **Properties** pane.</span></span>

3. <span data-ttu-id="f6bed-242">按一下 [套用規則] 。</span><span class="sxs-lookup"><span data-stu-id="f6bed-242">Click **With rules**.</span></span>

4. <span data-ttu-id="f6bed-243">在 [開始於] 下，按一下 [無資料行]。</span><span class="sxs-lookup"><span data-stu-id="f6bed-243">Under **Begin With**, click **No columns**.</span></span> <span data-ttu-id="f6bed-244">在 hello 篩選資料列，選取**Include**和**資料行名稱**hello 文字方塊中選取的資料行名稱清單。</span><span class="sxs-lookup"><span data-stu-id="f6bed-244">In hello filter row, select **Include** and **column names** and select our list of column names in hello text box.</span></span> <span data-ttu-id="f6bed-245">除了 hello 我們在此指定的這會指示 hello 模組 toonot （功能） 的任何資料行傳遞。</span><span class="sxs-lookup"><span data-stu-id="f6bed-245">This directs hello module toonot pass through any columns (features) except hello ones that we specify.</span></span>

5. <span data-ttu-id="f6bed-246">按一下 [hello] 核取記號 （確定） 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6bed-246">Click hello check mark (OK) button.</span></span>

    <span data-ttu-id="f6bed-247">![選取 hello （功能） 的資料行 tooinclude hello 預測中][select-columns-to-include]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-247">![Select hello columns (features) tooinclude in hello prediction][select-columns-to-include]
    </span></span><br/>
 <span data-ttu-id="f6bed-248">***選取 hello （功能） 的資料行 tooinclude hello 預測中***</span><span class="sxs-lookup"><span data-stu-id="f6bed-248">***Select hello columns (features) tooinclude in hello prediction***</span></span>

<span data-ttu-id="f6bed-249">這會產生已篩選的資料集，其中包含我們想要學習的演算法 hello 下一個步驟中，我們將使用 toopass toohello hello 功能。</span><span class="sxs-lookup"><span data-stu-id="f6bed-249">This produces a filtered dataset containing only hello features we want toopass toohello learning algorithm we'll use in hello next step.</span></span> <span data-ttu-id="f6bed-250">稍後您可以返回，並選取不同的功能重新嘗試。</span><span class="sxs-lookup"><span data-stu-id="f6bed-250">Later, you can return and try again with a different selection of features.</span></span>

## <a name="step-4-choose-and-apply-a-learning-algorithm"></a><span data-ttu-id="f6bed-251">步驟 4：選擇及套用學習演算法</span><span class="sxs-lookup"><span data-stu-id="f6bed-251">Step 4: Choose and apply a learning algorithm</span></span>

<span data-ttu-id="f6bed-252">既然 hello 資料已就緒，建構預測的模型包含的定型和測試。</span><span class="sxs-lookup"><span data-stu-id="f6bed-252">Now that hello data is ready, constructing a predictive model consists of training and testing.</span></span> <span data-ttu-id="f6bed-253">我們將使用我們資料 tootrain hello 的模型，並接著我們將測試 hello 模型 toosee 就能 toopredict 價格的程度。</span><span class="sxs-lookup"><span data-stu-id="f6bed-253">We'll use our data tootrain hello model, and then we'll test hello model toosee how closely it's able toopredict prices.</span></span>
<!-- For now, don't worry about *why* we need tootrain and then test a model.-->

<span data-ttu-id="f6bed-254">*分類*和*迴歸*是兩種受監督的機器學習服務演算法。</span><span class="sxs-lookup"><span data-stu-id="f6bed-254">*Classification* and *regression* are two types of supervised machine learning algorithms.</span></span> <span data-ttu-id="f6bed-255">「分類」可從一組已定義的類別預測答案，例如色彩 (紅色、藍色或綠色)。</span><span class="sxs-lookup"><span data-stu-id="f6bed-255">Classification predicts an answer from a defined set of categories, such as a color (red, blue, or green).</span></span> <span data-ttu-id="f6bed-256">迴歸是使用的 toopredict 數字。</span><span class="sxs-lookup"><span data-stu-id="f6bed-256">Regression is used toopredict a number.</span></span>

<span data-ttu-id="f6bed-257">因為我們想要 toopredict 價格是數字，我們會使用迴歸演算法。</span><span class="sxs-lookup"><span data-stu-id="f6bed-257">Because we want toopredict price, which is a number, we'll use a regression algorithm.</span></span> <span data-ttu-id="f6bed-258">在此範例中，我們將使用簡單*線性迴歸*模型。</span><span class="sxs-lookup"><span data-stu-id="f6bed-258">For this example, we'll use a simple *linear regression* model.</span></span>

> [!TIP]
> <span data-ttu-id="f6bed-259">如果您想要深入了解不同類型的機器學習演算法 toolearn toouse 它們，您可能會在 hello 資料科學初學者數列檢視 hello 第一個視訊[hello 五個問題的資料科學答案](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md)。</span><span class="sxs-lookup"><span data-stu-id="f6bed-259">If you want toolearn more about different types of machine learning algorithms and when toouse them, you might view hello first video in hello Data Science for Beginners series, [hello five questions data science answers](machine-learning-data-science-for-beginners-the-5-questions-data-science-answers.md).</span></span> <span data-ttu-id="f6bed-260">您也可以查看 hello 資訊圖[機器學習演算法範例的基本概念](machine-learning-basics-infographic-with-algorithm-examples.md)，或簽出 hello[機器學習演算法小祕技](machine-learning-algorithm-cheat-sheet.md)。</span><span class="sxs-lookup"><span data-stu-id="f6bed-260">You might also look at hello infographic [Machine learning basics with algorithm examples](machine-learning-basics-infographic-with-algorithm-examples.md), or check out hello [Machine learning algorithm cheat sheet](machine-learning-algorithm-cheat-sheet.md).</span></span>

<span data-ttu-id="f6bed-261">我們來定型 hello 模型提供一組包含 hello 價格的資料。</span><span class="sxs-lookup"><span data-stu-id="f6bed-261">We train hello model by giving it a set of data that includes hello price.</span></span> <span data-ttu-id="f6bed-262">hello 模型掃描 hello 資料和外觀汽車的功能和其價格之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="f6bed-262">hello model scans hello data and look for correlations between an automobile's features and its price.</span></span> <span data-ttu-id="f6bed-263">然後，我們將測試 hello 模型-我們將提供我們很熟悉的汽車的一組功能，請參閱如何關閉 hello 模型就 toopredicting hello 已知的價格。</span><span class="sxs-lookup"><span data-stu-id="f6bed-263">Then we'll test hello model - we'll give it a set of features for automobiles we're familiar with and see how close hello model comes toopredicting hello known price.</span></span>

<span data-ttu-id="f6bed-264">Hello 模型的定型和測試時將 hello 資料分割成個別的定型集和測試資料集，我們會使用我們的資料。</span><span class="sxs-lookup"><span data-stu-id="f6bed-264">We'll use our data for both training hello model and testing it by splitting hello data into separate training and testing datasets.</span></span>

1. <span data-ttu-id="f6bed-265">選取並拖曳 hello[分割資料][ split]模組 toohello 實驗畫布並將它連接 toohello 上次[資料集中選取的資料行][ select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="f6bed-265">Select and drag hello [Split Data][split] module toohello experiment canvas and connect it toohello last [Select Columns in Dataset][select-columns] module.</span></span>

2. <span data-ttu-id="f6bed-266">按一下 hello[分割資料][ split]模組 tooselect 它。</span><span class="sxs-lookup"><span data-stu-id="f6bed-266">Click hello [Split Data][split] module tooselect it.</span></span> <span data-ttu-id="f6bed-267">尋找 hello **hello 中的資料列的分數，第一次輸出資料集**(在 hello**屬性**hello 畫布的右窗格 toohello) 並將它設定 too0.75。</span><span class="sxs-lookup"><span data-stu-id="f6bed-267">Find hello **Fraction of rows in hello first output dataset** (in hello **Properties** pane toohello right of hello canvas) and set it too0.75.</span></span> <span data-ttu-id="f6bed-268">如此一來，我們將使用 75%的 hello 資料 tootrain hello 模型中，按住不放回 25%的測試 （更新版本中，您可以嘗試使用不同的百分比）。</span><span class="sxs-lookup"><span data-stu-id="f6bed-268">This way, we'll use 75 percent of hello data tootrain hello model, and hold back 25 percent for testing (later, you can experiment with using different percentages).</span></span>

    <span data-ttu-id="f6bed-269">![分割分數的 hello 「 分割資料 」 模組 too0.75 組 hello][set-split-data-percentage]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-269">![Set hello split fraction of hello "Split Data" module too0.75][set-split-data-percentage]
    </span></span><br/>
 <span data-ttu-id="f6bed-270">***分割分數的 hello 「 分割資料 」 模組 too0.75 組 hello***</span><span class="sxs-lookup"><span data-stu-id="f6bed-270">***Set hello split fraction of hello "Split Data" module too0.75***</span></span>

    > [!TIP]
    > <span data-ttu-id="f6bed-271">藉由變更 hello**隨機種子**參數，您可以產生不同的隨機取樣，用於定型和測試。</span><span class="sxs-lookup"><span data-stu-id="f6bed-271">By changing hello **Random seed** parameter, you can produce different random samples for training and testing.</span></span> <span data-ttu-id="f6bed-272">此參數控制 hello 植入 hello 虛擬亂數產生器。</span><span class="sxs-lookup"><span data-stu-id="f6bed-272">This parameter controls hello seeding of hello pseudo-random number generator.</span></span>

2. <span data-ttu-id="f6bed-273">執行 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="f6bed-273">Run hello experiment.</span></span> <span data-ttu-id="f6bed-274">Hello 實驗執行時，hello[資料集中選取的資料行][ select-columns]和[分割資料][ split]模組傳遞的資料行定義 toohello接下來我們將持續加入的模組。</span><span class="sxs-lookup"><span data-stu-id="f6bed-274">When hello experiment is run, hello [Select Columns in Dataset][select-columns] and [Split Data][split] modules pass column definitions toohello modules we'll be adding next.</span></span>  

3. <span data-ttu-id="f6bed-275">學習演算法，tooselect hello 展開 hello**機器學習**hello 模組調色盤 toohello 靠左 類別目錄的 hello 畫布，，然後展開**初始化模型**。</span><span class="sxs-lookup"><span data-stu-id="f6bed-275">tooselect hello learning algorithm, expand hello **Machine Learning** category in hello module palette toohello left of hello canvas, and then expand **Initialize Model**.</span></span> <span data-ttu-id="f6bed-276">這會顯示數種類別可以使用的 tooinitialize 機器學習演算法的模組。</span><span class="sxs-lookup"><span data-stu-id="f6bed-276">This displays several categories of modules that can be used tooinitialize machine learning algorithms.</span></span> <span data-ttu-id="f6bed-277">此實驗中，選取 hello[線性迴歸][ linear-regression]模組下 hello**迴歸**類別，並將它拖曳 toohello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="f6bed-277">For this experiment, select hello [Linear Regression][linear-regression] module under hello **Regression** category, and drag it toohello experiment canvas.</span></span>
<span data-ttu-id="f6bed-278">（您也可以尋找 hello 模組 hello 調色盤搜尋方塊中輸入 「 線性迴歸 」。）</span><span class="sxs-lookup"><span data-stu-id="f6bed-278">(You can also find hello module by typing "linear regression" in hello palette Search box.)</span></span>

4. <span data-ttu-id="f6bed-279">尋找並拖曳 hello[定型模型][ train-model]模組 toohello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="f6bed-279">Find and drag hello [Train Model][train-model] module toohello experiment canvas.</span></span> <span data-ttu-id="f6bed-280">Hello hello 輸出連接[線性迴歸][ linear-regression]模組 toohello 左輸入的 hello[定型模型][ train-model]模組，並連接 hello定型資料 （由左連接埠） 的輸出 hello[分割資料][ split]模組 toohello 右邊輸入 hello[定型模型][ train-model]模組。</span><span class="sxs-lookup"><span data-stu-id="f6bed-280">Connect hello output of hello [Linear Regression][linear-regression] module toohello left input of hello [Train Model][train-model] module, and connect hello training data output (left port) of hello [Split Data][split] module toohello right input of hello [Train Model][train-model] module.</span></span>

    <span data-ttu-id="f6bed-281">![連接 hello 「 定型模型 」 模組 tooboth hello 「 線性迴歸 」 和 「 分割資料 」 模組][connect-train-model]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-281">![Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules][connect-train-model]
    </span></span><br/>
 <span data-ttu-id="f6bed-282">***連接 hello 「 定型模型 」 模組 tooboth hello 「 線性迴歸 」 和 「 分割資料 」 模組***</span><span class="sxs-lookup"><span data-stu-id="f6bed-282">***Connect hello "Train Model" module tooboth hello "Linear Regression" and "Split Data" modules***</span></span>

5. <span data-ttu-id="f6bed-283">按一下 hello[定型模型][ train-model]模組中，按一下 [**啟動資料行選取器**在 hello**屬性**窗格中，然後再選取 hello **價格**資料行。</span><span class="sxs-lookup"><span data-stu-id="f6bed-283">Click hello [Train Model][train-model] module, click **Launch column selector** in hello **Properties** pane, and then select hello **price** column.</span></span> <span data-ttu-id="f6bed-284">這是我們的模型會持續 toopredict hello 值。</span><span class="sxs-lookup"><span data-stu-id="f6bed-284">This is hello value that our model is going toopredict.</span></span>

    <span data-ttu-id="f6bed-285">您選取 hello**價格**移動從 hello hello 資料行選取器中的資料行**可用的資料行**清單 toohello**選取的資料行**清單。</span><span class="sxs-lookup"><span data-stu-id="f6bed-285">You select hello **price** column in hello column selector by moving it from hello **Available columns** list toohello **Selected columns** list.</span></span>

    <span data-ttu-id="f6bed-286">![選取 hello 「 定型模型 」 模組的 hello 價格資料行][select-price-column]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-286">![Select hello price column for hello "Train Model" module][select-price-column]
    </span></span><br/>
 <span data-ttu-id="f6bed-287">***選取 hello 「 定型模型 」 模組的 hello 價格資料行***</span><span class="sxs-lookup"><span data-stu-id="f6bed-287">***Select hello price column for hello "Train Model" module***</span></span>

6. <span data-ttu-id="f6bed-288">執行 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="f6bed-288">Run hello experiment.</span></span>

<span data-ttu-id="f6bed-289">我們現在有可能是使用的 tooscore 新汽車資料 toomake 價格預測定型的迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="f6bed-289">We now have a trained regression model that can be used tooscore new automobile data toomake price predictions.</span></span>

<span data-ttu-id="f6bed-290">![開始執行之後，hello 實驗現在看起來應該類似下面的][second-experiment-run]
</span><span class="sxs-lookup"><span data-stu-id="f6bed-290">![After running, hello experiment should now look something like this][second-experiment-run]
</span></span><br/><span data-ttu-id="f6bed-291">
***開始執行之後，hello 實驗現在看起來應該類似下面的***</span><span class="sxs-lookup"><span data-stu-id="f6bed-291">
***After running, hello experiment should now look something like this***</span></span>

## <a name="step-5-predict-new-automobile-prices"></a><span data-ttu-id="f6bed-292">步驟 5：預測新的汽車價格</span><span class="sxs-lookup"><span data-stu-id="f6bed-292">Step 5: Predict new automobile prices</span></span>

<span data-ttu-id="f6bed-293">既然我們已經定型 hello 模型使用 75%的資料，我們可以使用 tooscore hello 其他的百分之 25 hello 資料 toosee 程度我們模型函式。</span><span class="sxs-lookup"><span data-stu-id="f6bed-293">Now that we've trained hello model using 75 percent of our data, we can use it tooscore hello other 25 percent of hello data toosee how well our model functions.</span></span>

1. <span data-ttu-id="f6bed-294">尋找並拖曳 hello[計分模型][ score-model]模組 toohello 實驗畫布。</span><span class="sxs-lookup"><span data-stu-id="f6bed-294">Find and drag hello [Score Model][score-model] module toohello experiment canvas.</span></span> <span data-ttu-id="f6bed-295">Hello hello 輸出連接[定型模型][ train-model]左輸入的連接埠的模組 toohello[計分模型][score-model]。</span><span class="sxs-lookup"><span data-stu-id="f6bed-295">Connect hello output of hello [Train Model][train-model] module toohello left input port of [Score Model][score-model].</span></span> <span data-ttu-id="f6bed-296">連接 hello 測試資料 （右連接埠） 的輸出 hello[分割資料][ split]模組 toohello 右輸入的連接埠[計分模型][score-model]。</span><span class="sxs-lookup"><span data-stu-id="f6bed-296">Connect hello test data output (right port) of hello [Split Data][split] module toohello right input port of [Score Model][score-model].</span></span>

    <span data-ttu-id="f6bed-297">![連接 hello 「 計分模型 」 模組 tooboth hello 「 定型模型 」 和 「 分割資料 」 模組][connect-score-model]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-297">![Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules][connect-score-model]
    </span></span><br/>
 <span data-ttu-id="f6bed-298">***連接 hello 「 計分模型 」 模組 tooboth hello 「 定型模型 」 和 「 分割資料 」 模組***</span><span class="sxs-lookup"><span data-stu-id="f6bed-298">***Connect hello "Score Model" module tooboth hello "Train Model" and "Split Data" modules***</span></span>

2. <span data-ttu-id="f6bed-299">執行 hello 實驗，並檢視 hello hello 輸出[計分模型][ score-model]模組 (按一下 hello 輸出連接埠[計分模型][ score-model]選取**視覺化**)。</span><span class="sxs-lookup"><span data-stu-id="f6bed-299">Run hello experiment and view hello output from hello [Score Model][score-model] module (click hello output port of [Score Model][score-model] and select **Visualize**).</span></span> <span data-ttu-id="f6bed-300">hello 輸出顯示 hello 價格的預測的值，和 hello hello 測試資料的已知的值。</span><span class="sxs-lookup"><span data-stu-id="f6bed-300">hello output shows hello predicted values for price and hello known values from hello test data.</span></span>  

    <span data-ttu-id="f6bed-301">![Hello 「 計分模型 」 模組的輸出][score-model-output]
    </span><span class="sxs-lookup"><span data-stu-id="f6bed-301">![Output of hello "Score Model" module][score-model-output]
    </span></span><br/>
 <span data-ttu-id="f6bed-302">***Hello 「 計分模型 」 模組的輸出***</span><span class="sxs-lookup"><span data-stu-id="f6bed-302">***Output of hello "Score Model" module***</span></span>

3. <span data-ttu-id="f6bed-303">最後，我們測試 hello hello 結果的品質。</span><span class="sxs-lookup"><span data-stu-id="f6bed-303">Finally, we test hello quality of hello results.</span></span> <span data-ttu-id="f6bed-304">選取並拖曳 hello[評估模型][ evaluate-model]模組 toohello 實驗畫布與 hello hello 輸出連接[計分模型][ score-model]剩餘的輸入模組 toohello[評估模型][evaluate-model]。</span><span class="sxs-lookup"><span data-stu-id="f6bed-304">Select and drag hello [Evaluate Model][evaluate-model] module toohello experiment canvas, and connect hello output of hello [Score Model][score-model] module toohello left input of [Evaluate Model][evaluate-model].</span></span>

    > [!TIP]
    > <span data-ttu-id="f6bed-305">有兩個輸入連接埠上 hello[評估模型][ evaluate-model]模組因為它可以是使用的 toocompare 兩個模型並存。</span><span class="sxs-lookup"><span data-stu-id="f6bed-305">There are two input ports on hello [Evaluate Model][evaluate-model] module because it can be used toocompare two models side by side.</span></span> <span data-ttu-id="f6bed-306">稍後，您可以加入另一個演算法 toohello 實驗，並使用[評估模型][ evaluate-model] toosee 哪一項提供更好的結果。</span><span class="sxs-lookup"><span data-stu-id="f6bed-306">Later, you can add another algorithm toohello experiment and use [Evaluate Model][evaluate-model] toosee which one gives better results.</span></span>

4. <span data-ttu-id="f6bed-307">執行 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="f6bed-307">Run hello experiment.</span></span>

<span data-ttu-id="f6bed-308">hello tooview hello 輸出[評估模型][ evaluate-model]模組中，按一下 hello 輸出連接埠]，然後選取**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="f6bed-308">tooview hello output from hello [Evaluate Model][evaluate-model] module, click hello output port, and then select **Visualize**.</span></span>

<span data-ttu-id="f6bed-309">![Hello 實驗的評估結果][evaluation-results]
</span><span class="sxs-lookup"><span data-stu-id="f6bed-309">![Evaluation results for hello experiment][evaluation-results]
</span></span><br/><span data-ttu-id="f6bed-310">
***Hello 實驗的評估結果***</span><span class="sxs-lookup"><span data-stu-id="f6bed-310">
***Evaluation results for hello experiment***</span></span>

<span data-ttu-id="f6bed-311">hello 下列統計資料會顯示為我們的模型：</span><span class="sxs-lookup"><span data-stu-id="f6bed-311">hello following statistics are shown for our model:</span></span>

- <span data-ttu-id="f6bed-312">**平均絕對誤差**(MAE): hello 的絕對錯誤平均值 (*錯誤*hello 差異 hello 預測值和 hello 實際值)。</span><span class="sxs-lookup"><span data-stu-id="f6bed-312">**Mean Absolute Error** (MAE): hello average of absolute errors (an *error* is hello difference between hello predicted value and hello actual value).</span></span>
- <span data-ttu-id="f6bed-313">**根平均平方誤差**(RMSE): hello 的平方根 hello 平均平方錯誤 hello 測試資料集上所做的預測。</span><span class="sxs-lookup"><span data-stu-id="f6bed-313">**Root Mean Squared Error** (RMSE): hello square root of hello average of squared errors of predictions made on hello test dataset.</span></span>
- <span data-ttu-id="f6bed-314">**相對的絕對誤差**: hello 的絕對錯誤相對 toohello 絕對實際值與平均之間差異 hello 所有的實際值的平均值。</span><span class="sxs-lookup"><span data-stu-id="f6bed-314">**Relative Absolute Error**: hello average of absolute errors relative toohello absolute difference between actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="f6bed-315">**相對平方誤差**: hello 平均平方的錯誤相對 toohello 平方 hello 實際值與所有的實際值的平均值，hello 之間的差異。</span><span class="sxs-lookup"><span data-stu-id="f6bed-315">**Relative Squared Error**: hello average of squared errors relative toohello squared difference between hello actual values and hello average of all actual values.</span></span>
- <span data-ttu-id="f6bed-316">**判斷的係數**： 也稱為 hello **R 平方值**，這是統計度量，表示模型適合 hello 資料的程度。</span><span class="sxs-lookup"><span data-stu-id="f6bed-316">**Coefficient of Determination**: Also known as hello **R squared value**, this is a statistical metric indicating how well a model fits hello data.</span></span>

<span data-ttu-id="f6bed-317">Hello 錯誤的每個統計資料，較小，則更好。</span><span class="sxs-lookup"><span data-stu-id="f6bed-317">For each of hello error statistics, smaller is better.</span></span> <span data-ttu-id="f6bed-318">較小的值會指出 hello 預測會更緊密符合 hello 實際值。</span><span class="sxs-lookup"><span data-stu-id="f6bed-318">A smaller value indicates that hello predictions more closely match hello actual values.</span></span> <span data-ttu-id="f6bed-319">如**判斷的係數**，hello 接近其值是 tooone (1.0)，hello 較佳的 hello 預測。</span><span class="sxs-lookup"><span data-stu-id="f6bed-319">For **Coefficient of Determination**, hello closer its value is tooone (1.0), hello better hello predictions.</span></span>

## <a name="final-experiment"></a><span data-ttu-id="f6bed-320">最終實驗</span><span class="sxs-lookup"><span data-stu-id="f6bed-320">Final experiment</span></span>

<span data-ttu-id="f6bed-321">hello 最終實驗看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="f6bed-321">hello final experiment should look something like this:</span></span>

<span data-ttu-id="f6bed-322">![hello 最終實驗][complete-linear-regression-experiment]
</span><span class="sxs-lookup"><span data-stu-id="f6bed-322">![hello final experiment][complete-linear-regression-experiment]
</span></span><br/><span data-ttu-id="f6bed-323">
***hello 最終實驗***</span><span class="sxs-lookup"><span data-stu-id="f6bed-323">
***hello final experiment***</span></span>

## <a name="next-steps"></a><span data-ttu-id="f6bed-324">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f6bed-324">Next steps</span></span>

<span data-ttu-id="f6bed-325">既然您已經完成 hello 第一個機器學習教學課程，並以您的經驗設定，您可以繼續 tooimprove hello 模型，並再將其部署為在預測 web 服務。</span><span class="sxs-lookup"><span data-stu-id="f6bed-325">Now that you've completed hello first machine learning tutorial and have your experiment set up, you can continue tooimprove hello model and then deploy it as a predictive web service.</span></span>

- <span data-ttu-id="f6bed-326">**逐一查看 tootry tooimprove hello 模型**-例如，您可以變更您預測中使用的 hello 功能。</span><span class="sxs-lookup"><span data-stu-id="f6bed-326">**Iterate tootry tooimprove hello model** - For example, you can change hello features you use in your prediction.</span></span> <span data-ttu-id="f6bed-327">您可以修改的 hello hello 屬性或者[線性迴歸][ linear-regression]演算法或完全嘗試不同的演算法。</span><span class="sxs-lookup"><span data-stu-id="f6bed-327">Or you can modify hello properties of hello [Linear Regression][linear-regression] algorithm or try a different algorithm altogether.</span></span> <span data-ttu-id="f6bed-328">您甚至可以加入多個機器學習演算法 tooyour 實驗一次並比較其中兩個使用 hello[評估模型][ evaluate-model]模組。</span><span class="sxs-lookup"><span data-stu-id="f6bed-328">You can even add multiple machine learning algorithms tooyour experiment at one time and compare two of them by using hello [Evaluate Model][evaluate-model] module.</span></span>
<span data-ttu-id="f6bed-329">如需如何 toocompare 多個模型中單一實驗中，請參閱[比較迴歸輸入變數](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5)在 hello [Cortana 智慧組件庫](https://gallery.cortanaintelligence.com)。</span><span class="sxs-lookup"><span data-stu-id="f6bed-329">For an example of how toocompare multiple models in a single experiment, see [Compare Regressors](https://gallery.cortanaintelligence.com/Experiment/Compare-Regressors-5) in hello [Cortana Intelligence Gallery](https://gallery.cortanaintelligence.com).</span></span>

    > [!TIP]
    > <span data-ttu-id="f6bed-330">toocopy 您實驗中，使用 hello 任何反覆項目**SAVE AS**在 hello hello 頁面底部的按鈕。</span><span class="sxs-lookup"><span data-stu-id="f6bed-330">toocopy any iteration of your experiment, use hello **SAVE AS** button at hello bottom of hello page.</span></span> <span data-ttu-id="f6bed-331">您可以按一下來查看所有的 hello 反覆項目的實驗的**檢視執行記錄**hello hello 頁底端。</span><span class="sxs-lookup"><span data-stu-id="f6bed-331">You can see all hello iterations of your experiment by clicking **VIEW RUN HISTORY** at hello bottom of hello page.</span></span> <span data-ttu-id="f6bed-332">如需詳細資訊，請參閱[在 Azure Machine Learning Studio 中管理實驗逐一查看][runhistory]。</span><span class="sxs-lookup"><span data-stu-id="f6bed-332">For more details, see [Manage experiment iterations in Azure Machine Learning Studio][runhistory].</span></span>

[runhistory]: machine-learning-manage-experiment-iterations.md

- <span data-ttu-id="f6bed-333">**部署為預測的 web 服務的 hello 模型**-當您滿意您的模型，您可以將它部署為 web 服務 toobe 所使用新的資料使用 toopredict 汽車價格。</span><span class="sxs-lookup"><span data-stu-id="f6bed-333">**Deploy hello model as a predictive web service** - When you're satisfied with your model, you can deploy it as a web service toobe used toopredict automobile prices by using new data.</span></span> <span data-ttu-id="f6bed-334">如需詳細資訊，請參閱[部署 Azure Machine Learning Web 服務][publish]。</span><span class="sxs-lookup"><span data-stu-id="f6bed-334">For more details, see [Deploy an Azure Machine Learning web service][publish].</span></span>

[publish]: machine-learning-publish-a-machine-learning-web-service.md

<span data-ttu-id="f6bed-335">想要更多的 toolearn 嗎？</span><span class="sxs-lookup"><span data-stu-id="f6bed-335">Want toolearn more?</span></span> <span data-ttu-id="f6bed-336">建立、 培訓、 計分，和部署模型 hello 程序的更廣泛且詳細逐步解說，請參閱[使用 Azure Machine Learning 開發預測解決方案][walkthrough]。</span><span class="sxs-lookup"><span data-stu-id="f6bed-336">For a more extensive and detailed walkthrough of hello process of creating, training, scoring, and deploying a model, see [Develop a predictive solution by using Azure Machine Learning][walkthrough].</span></span>

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

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
[type-automobile]:./media/machine-learning-create-experiment/type-automobile.png
[type-select-columns]:./media/machine-learning-create-experiment/type-select-columns.png
[launch-column-selector]:./media/machine-learning-create-experiment/launch-column-selector.png
[add-comment]:./media/machine-learning-create-experiment/add-comment.png
[connect-clean-to-select]:./media/machine-learning-create-experiment/connect-clean-to-select.png

[set-split-data-percentage]:./media/machine-learning-create-experiment/set-split-data-percentage.png

<!-- temporarily switching GIFs tooPNGs tooremove animation --> 
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
