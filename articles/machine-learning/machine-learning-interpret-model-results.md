---
title: "在機器學習中的 aaaInterpret 模型結果 |Microsoft 文件"
description: "如何 toochoose hello 最佳參數設定演算法使用，並以視覺化方式檢視計分模型輸出。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6230e5ab-a5c0-4c21-a061-47675ba3342c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 52161b1aa5ff3e7a63fc4b1bfb7c5e354eabcc50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a><span data-ttu-id="45712-103">在 Azure Machine Learning 中解譯模型結果</span><span class="sxs-lookup"><span data-stu-id="45712-103">Interpret model results in Azure Machine Learning</span></span>
<span data-ttu-id="45712-104">本主題說明如何 toovisualize 並解譯 Azure Machine Learning Studio 中的預測結果。</span><span class="sxs-lookup"><span data-stu-id="45712-104">This topic explains how toovisualize and interpret prediction results in Azure Machine Learning Studio.</span></span> <span data-ttu-id="45712-105">在培訓模型並進行預測頂端 （「 計分模型 hello"） 之後，您需要 toounderstand，並解譯 hello 預測結果。</span><span class="sxs-lookup"><span data-stu-id="45712-105">After you have trained a model and done predictions on top of it ("scored hello model"), you need toounderstand and interpret hello prediction result.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="45712-106">Azure Machine Learning 中有四個主要的機器學習類型：</span><span class="sxs-lookup"><span data-stu-id="45712-106">There are four major kinds of machine learning models in Azure Machine Learning:</span></span>

* <span data-ttu-id="45712-107">分類</span><span class="sxs-lookup"><span data-stu-id="45712-107">Classification</span></span>
* <span data-ttu-id="45712-108">叢集</span><span class="sxs-lookup"><span data-stu-id="45712-108">Clustering</span></span>
* <span data-ttu-id="45712-109">迴歸</span><span class="sxs-lookup"><span data-stu-id="45712-109">Regression</span></span>
* <span data-ttu-id="45712-110">推薦系統</span><span class="sxs-lookup"><span data-stu-id="45712-110">Recommender systems</span></span>

<span data-ttu-id="45712-111">用來預測在這些模型之上的 hello 模組為：</span><span class="sxs-lookup"><span data-stu-id="45712-111">hello modules used for prediction on top of these models are:</span></span>

* <span data-ttu-id="45712-112">[評分模型][score-model]模組，用於分類和迴歸</span><span class="sxs-lookup"><span data-stu-id="45712-112">[Score Model][score-model] module for classification and regression</span></span>
* <span data-ttu-id="45712-113">[指派 tooClusters] [ assign-to-clusters]適用於叢集模組</span><span class="sxs-lookup"><span data-stu-id="45712-113">[Assign tooClusters][assign-to-clusters] module for clustering</span></span>
* <span data-ttu-id="45712-114">[評分 Matchbox 推薦][score-matchbox-recommender]，用於推薦系統</span><span class="sxs-lookup"><span data-stu-id="45712-114">[Score Matchbox Recommender][score-matchbox-recommender] for recommendation systems</span></span>

<span data-ttu-id="45712-115">本文件說明如何 toointerpret 預測結果的每一個這些模組。</span><span class="sxs-lookup"><span data-stu-id="45712-115">This document explains how toointerpret prediction results for each of these modules.</span></span> <span data-ttu-id="45712-116">如需這些模組的概觀，請參閱[如何 toochoose 參數 toooptimize 您在 Azure Machine Learning 中的演算法](machine-learning-algorithm-parameters-optimize.md)。</span><span class="sxs-lookup"><span data-stu-id="45712-116">For an overview of these modules, see [How toochoose parameters toooptimize your algorithms in Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md).</span></span>

<span data-ttu-id="45712-117">本主題說明預測解譯，但是未說明模型評估。</span><span class="sxs-lookup"><span data-stu-id="45712-117">This topic addresses prediction interpretation but not model evaluation.</span></span> <span data-ttu-id="45712-118">如需有關如何 tooevaluate 自己的模型，請參閱[tooevaluate 建立 Azure Machine Learning 中的效能的模型](machine-learning-evaluate-model-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="45712-118">For more information about how tooevaluate your model, see [How tooevaluate model performance in Azure Machine Learning](machine-learning-evaluate-model-performance.md).</span></span>

<span data-ttu-id="45712-119">如果您是新 tooAzure 機器學習，而且需要協助建立簡易實驗 tooget 啟動，請參閱[Azure Machine Learning Studio 中建立簡易實驗](machine-learning-create-experiment.md)Azure Machine Learning Studio 中。</span><span class="sxs-lookup"><span data-stu-id="45712-119">If you are new tooAzure Machine Learning and need help creating a simple experiment tooget started, see [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md) in Azure Machine Learning Studio.</span></span>

## <a name="classification"></a><span data-ttu-id="45712-120">分類</span><span class="sxs-lookup"><span data-stu-id="45712-120">Classification</span></span>
<span data-ttu-id="45712-121">分類問題方面有兩個子類別：</span><span class="sxs-lookup"><span data-stu-id="45712-121">There are two subcategories of classification problems:</span></span>

* <span data-ttu-id="45712-122">只有兩個分類的問題 (雙類別或二進位分類)</span><span class="sxs-lookup"><span data-stu-id="45712-122">Problems with only two classes (two-class or binary classification)</span></span>
* <span data-ttu-id="45712-123">兩個以上分類的問題 (多類別分類)</span><span class="sxs-lookup"><span data-stu-id="45712-123">Problems with more than two classes (multi-class classification)</span></span>

<span data-ttu-id="45712-124">Azure Machine Learning 具有不同的模組 toodeal 與每一個這些類型的分類，但解譯預測結果的 hello 方法很相似。</span><span class="sxs-lookup"><span data-stu-id="45712-124">Azure Machine Learning has different modules toodeal with each of these types of classification, but hello methods for interpreting their prediction results are similar.</span></span>

### <a name="two-class-classification"></a><span data-ttu-id="45712-125">雙類別分類</span><span class="sxs-lookup"><span data-stu-id="45712-125">Two-class classification</span></span>
<span data-ttu-id="45712-126">**範例實驗**</span><span class="sxs-lookup"><span data-stu-id="45712-126">**Example experiment**</span></span>

<span data-ttu-id="45712-127">二級分類問題的範例是光圈花 hello 分類。</span><span class="sxs-lookup"><span data-stu-id="45712-127">An example of a two-class classification problem is hello classification of iris flowers.</span></span> <span data-ttu-id="45712-128">hello 工作是 tooclassify 光圈花在根據其功能。</span><span class="sxs-lookup"><span data-stu-id="45712-128">hello task is tooclassify iris flowers based on their features.</span></span> <span data-ttu-id="45712-129">hello Azure Machine Learning 中提供的光圈資料集是子集 hello 熱門[光圈資料集](http://en.wikipedia.org/wiki/Iris_flower_data_set)只有兩個花盆物種 （類別 0 和 1） 包含的執行個體。</span><span class="sxs-lookup"><span data-stu-id="45712-129">hello Iris data set provided in Azure Machine Learning is a subset of hello popular [Iris data set](http://en.wikipedia.org/wiki/Iris_flower_data_set) containing instances of only two flower species (classes 0 and 1).</span></span> <span data-ttu-id="45712-130">每個花卉有四個特徵 (萼片長度、萼片寬度、花瓣長度及花瓣寬度)。</span><span class="sxs-lookup"><span data-stu-id="45712-130">There are four features for each flower (sepal length, sepal width, petal length, and petal width).</span></span>

![鳶尾花實驗的螢幕擷取畫面](./media/machine-learning-interpret-model-results/1.png)

<span data-ttu-id="45712-132">圖 1.</span><span class="sxs-lookup"><span data-stu-id="45712-132">Figure 1.</span></span> <span data-ttu-id="45712-133">鳶尾花雙類別分類問題實驗</span><span class="sxs-lookup"><span data-stu-id="45712-133">Iris two-class classification problem experiment</span></span>

<span data-ttu-id="45712-134">實驗已執行的 toosolve 這個問題，如圖 1 所示。</span><span class="sxs-lookup"><span data-stu-id="45712-134">An experiment has been performed toosolve this problem, as shown in Figure 1.</span></span> <span data-ttu-id="45712-135">已訓練及評分雙類別促進式決策樹模型。</span><span class="sxs-lookup"><span data-stu-id="45712-135">A two-class boosted decision tree model has been trained and scored.</span></span> <span data-ttu-id="45712-136">現在您可以視覺化 hello 預測結果從 hello[計分模型][ score-model]模組，依序按一下輸出連接埠 hello hello[計分模型][ score-model]模組，然後按一下**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="45712-136">Now you can visualize hello prediction results from hello [Score Model][score-model] module by clicking hello output port of hello [Score Model][score-model] module and then clicking **Visualize**.</span></span>

![評分模型模組](./media/machine-learning-interpret-model-results/1_1.png)

<span data-ttu-id="45712-138">這會顯示 hello 計分結果，如圖 2 所示。</span><span class="sxs-lookup"><span data-stu-id="45712-138">This brings up hello scoring results as shown in Figure 2.</span></span>

![鳶尾花雙類別分類實驗的結果](./media/machine-learning-interpret-model-results/2.png)

<span data-ttu-id="45712-140">圖 2.</span><span class="sxs-lookup"><span data-stu-id="45712-140">Figure 2.</span></span> <span data-ttu-id="45712-141">視覺化雙類別分類中的評分模型結果</span><span class="sxs-lookup"><span data-stu-id="45712-141">Visualize a score model result in two-class classification</span></span>

<span data-ttu-id="45712-142">**結果解譯**</span><span class="sxs-lookup"><span data-stu-id="45712-142">**Result interpretation**</span></span>

<span data-ttu-id="45712-143">Hello 結果資料表中有六個資料行。</span><span class="sxs-lookup"><span data-stu-id="45712-143">There are six columns in hello results table.</span></span> <span data-ttu-id="45712-144">hello 左四個資料行是 hello 四個功能。</span><span class="sxs-lookup"><span data-stu-id="45712-144">hello left four columns are hello four features.</span></span> <span data-ttu-id="45712-145">hello 右邊的兩個資料行計分標籤和計分機率是 hello 預測結果。</span><span class="sxs-lookup"><span data-stu-id="45712-145">hello right two columns, Scored Labels and Scored Probabilities, are hello prediction results.</span></span> <span data-ttu-id="45712-146">hello 計分機率資料行顯示 hello 機率花所屬 toohello 正數類別 (類別 1)。</span><span class="sxs-lookup"><span data-stu-id="45712-146">hello Scored Probabilities column shows hello probability that a flower belongs toohello positive class (Class 1).</span></span> <span data-ttu-id="45712-147">例如，hello hello 資料行 (0.028571)，則表示 0.028571 hello 第一個正確的機率所屬 tooClass 1 中的第一個數字。</span><span class="sxs-lookup"><span data-stu-id="45712-147">For example, hello first number in hello column (0.028571) means there is 0.028571 probability that hello first flower belongs tooClass 1.</span></span> <span data-ttu-id="45712-148">hello 計分標籤資料行顯示 hello 預測每個季節的類別。</span><span class="sxs-lookup"><span data-stu-id="45712-148">hello Scored Labels column shows hello predicted class for each flower.</span></span> <span data-ttu-id="45712-149">這根據 hello 計分機率資料行。</span><span class="sxs-lookup"><span data-stu-id="45712-149">This is based on hello Scored Probabilities column.</span></span> <span data-ttu-id="45712-150">如果 hello 計分的花牌機率大於 0.5，它被預測為類別 1。</span><span class="sxs-lookup"><span data-stu-id="45712-150">If hello scored probability of a flower is larger than 0.5, it is predicted as Class 1.</span></span> <span data-ttu-id="45712-151">否則會預測為類別 0。</span><span class="sxs-lookup"><span data-stu-id="45712-151">Otherwise, it is predicted as Class 0.</span></span>

<span data-ttu-id="45712-152">**Web 服務發佈**</span><span class="sxs-lookup"><span data-stu-id="45712-152">**Web service publication**</span></span>

<span data-ttu-id="45712-153">已了解並認定為音效 hello 預測結果之後，hello 實驗可以發佈為 web 服務，以便您可以將它部署在不同的應用程式，並呼叫它 tooobtain 類別預測任何新的 iris 花牌上。</span><span class="sxs-lookup"><span data-stu-id="45712-153">After hello prediction results have been understood and judged sound, hello experiment can be published as a web service so that you can deploy it in various applications and call it tooobtain class predictions on any new iris flower.</span></span> <span data-ttu-id="45712-154">toolearn 如何 toochange 訓練試驗為計分試驗，以及發佈為 web 服務，請參閱[發佈 hello Azure Machine Learning web 服務](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="45712-154">toolearn how toochange a training experiment into a scoring experiment and publish it as a web service, see [Publish hello Azure Machine Learning web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span> <span data-ttu-id="45712-155">此程序可提供給您如圖 3 所示的評分實驗。</span><span class="sxs-lookup"><span data-stu-id="45712-155">This procedure provides you with a scoring experiment as shown in Figure 3.</span></span>

![評分實驗的螢幕擷取畫面](./media/machine-learning-interpret-model-results/3.png)

<span data-ttu-id="45712-157">圖 3.</span><span class="sxs-lookup"><span data-stu-id="45712-157">Figure 3.</span></span> <span data-ttu-id="45712-158">計分 hello 光圈二級分類問題實驗</span><span class="sxs-lookup"><span data-stu-id="45712-158">Scoring hello iris two-class classification problem experiment</span></span>

<span data-ttu-id="45712-159">現在您可以針對 hello web 服務需要 tooset hello 輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="45712-159">Now you need tooset hello input and output for hello web service.</span></span> <span data-ttu-id="45712-160">hello 輸入是 hello 右輸入的連接埠[計分模型][score-model]，這是 hello 光圈花功能輸入。</span><span class="sxs-lookup"><span data-stu-id="45712-160">hello input is hello right input port of [Score Model][score-model], which is hello Iris flower features input.</span></span> <span data-ttu-id="45712-161">您好的選擇 hello 輸出取決於您是否想要在 hello 預測類別 （計分標籤）、 hello 計分機率，或兩者。</span><span class="sxs-lookup"><span data-stu-id="45712-161">hello choice of hello output depends on whether you are interested in hello predicted class (scored label), hello scored probability, or both.</span></span> <span data-ttu-id="45712-162">此範例假設您對兩者都感到興趣。</span><span class="sxs-lookup"><span data-stu-id="45712-162">In this example, it is assumed that you are interested in both.</span></span> <span data-ttu-id="45712-163">tooselect hello 預期輸出資料行，使用[資料集內選取資料行][ select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="45712-163">tooselect hello desired output columns, use a [Select Columns in Data set][select-columns] module.</span></span> <span data-ttu-id="45712-164">依序按一下 [選取資料集中的資料行][select-columns] 和 **啟動資料行選取器**，然後選取 [評分標籤] 和 [評分機率]。</span><span class="sxs-lookup"><span data-stu-id="45712-164">Click [Select Columns in Data set][select-columns], click **Launch column selector**, and select **Scored Labels** and **Scored Probabilities**.</span></span> <span data-ttu-id="45712-165">設定 hello 輸出連接埠之後[資料集內選取資料行][ select-columns] ，再次執行，您應該準備好 toopublish hello 計分實驗為 web 服務，即可**發行 WEB服務**。</span><span class="sxs-lookup"><span data-stu-id="45712-165">After setting hello output port of [Select Columns in Data set][select-columns] and running it again, you should be ready toopublish hello scoring experiment as a web service by clicking **PUBLISH WEB SERVICE**.</span></span> <span data-ttu-id="45712-166">如圖 4 所示 hello 最終實驗。</span><span class="sxs-lookup"><span data-stu-id="45712-166">hello final experiment looks like Figure 4.</span></span>

![hello 光圈二級分類實驗](./media/machine-learning-interpret-model-results/4.png)

<span data-ttu-id="45712-168">圖 4.</span><span class="sxs-lookup"><span data-stu-id="45712-168">Figure 4.</span></span> <span data-ttu-id="45712-169">鳶尾花雙類別分類問題的最終評分實驗</span><span class="sxs-lookup"><span data-stu-id="45712-169">Final scoring experiment of an iris two-class classification problem</span></span>

<span data-ttu-id="45712-170">在執行 hello web 服務，並輸入測試執行個體的某些功能值之後，hello 結果會傳回兩個數字。</span><span class="sxs-lookup"><span data-stu-id="45712-170">After you run hello web service and enter some feature values of a test instance, hello result returns two numbers.</span></span> <span data-ttu-id="45712-171">hello 第一個數字為 hello 計分標籤，並 hello 第二種是 hello 計分可能性。</span><span class="sxs-lookup"><span data-stu-id="45712-171">hello first number is hello scored label, and hello second is hello scored probability.</span></span> <span data-ttu-id="45712-172">此花卉預測為類別 1，其機率為 0.9655。</span><span class="sxs-lookup"><span data-stu-id="45712-172">This flower is predicted as Class 1 with 0.9655 probability.</span></span>

![測試解譯評分模型](./media/machine-learning-interpret-model-results/4_1.png)

![測試結果評分](./media/machine-learning-interpret-model-results/5.png)

<span data-ttu-id="45712-175">圖 5.</span><span class="sxs-lookup"><span data-stu-id="45712-175">Figure 5.</span></span> <span data-ttu-id="45712-176">鳶尾花雙類別分類的 Web 服務結果</span><span class="sxs-lookup"><span data-stu-id="45712-176">Web service result of iris two-class classification</span></span>

### <a name="multi-class-classification"></a><span data-ttu-id="45712-177">多類別分類</span><span class="sxs-lookup"><span data-stu-id="45712-177">Multi-class classification</span></span>
<span data-ttu-id="45712-178">**範例實驗**</span><span class="sxs-lookup"><span data-stu-id="45712-178">**Example experiment**</span></span>

<span data-ttu-id="45712-179">在此實驗中，您將執行字母辨識工作，做為多元分類的範例。</span><span class="sxs-lookup"><span data-stu-id="45712-179">In this experiment, you perform a letter-recognition task as an example of multiclass classification.</span></span> <span data-ttu-id="45712-180">hello 分類嘗試 toopredict 特定字母 （類別） 會根據從 hello 手寫的映像擷取某些手寫的屬性值。</span><span class="sxs-lookup"><span data-stu-id="45712-180">hello classifier attempts toopredict a certain letter (class) based on some hand-written attribute values extracted from hello hand-written images.</span></span>

![字母辨識範例](./media/machine-learning-interpret-model-results/5_1.png)

<span data-ttu-id="45712-182">Hello 定型資料，在有 16 手寫的字母映像從擷取的功能。</span><span class="sxs-lookup"><span data-stu-id="45712-182">In hello training data, there are 16 features extracted from hand-written letter images.</span></span> <span data-ttu-id="45712-183">hello 26 字母形成 26 類別。</span><span class="sxs-lookup"><span data-stu-id="45712-183">hello 26 letters form our 26 classes.</span></span> <span data-ttu-id="45712-184">圖 6 顯示將定型的多級分類的實驗字母辨識的模型，而預測 hello 上相同的功能集上測試資料集。</span><span class="sxs-lookup"><span data-stu-id="45712-184">Figure 6 shows an experiment that will train a multiclass classification model for letter recognition and predict on hello same feature set on a test data set.</span></span>

![字母辨識多類別分類實驗](./media/machine-learning-interpret-model-results/6.png)

<span data-ttu-id="45712-186">圖 6.</span><span class="sxs-lookup"><span data-stu-id="45712-186">Figure 6.</span></span> <span data-ttu-id="45712-187">字母辨識多類別分類問題實驗</span><span class="sxs-lookup"><span data-stu-id="45712-187">Letter recognition multiclass classification problem experiment</span></span>

<span data-ttu-id="45712-188">視覺化 hello hello 結果[計分模型][ score-model]模組，依序按一下 hello 輸出連接埠[計分模型][ score-model]模組，然後按一下**視覺化**，如圖 7 所示，您應該看到的內容。</span><span class="sxs-lookup"><span data-stu-id="45712-188">Visualizing hello results from hello [Score Model][score-model] module by clicking hello output port of [Score Model][score-model] module and then clicking **Visualize**, you should see content as shown in Figure 7.</span></span>

![評分模型模組](./media/machine-learning-interpret-model-results/7.png)

<span data-ttu-id="45712-190">圖 7.</span><span class="sxs-lookup"><span data-stu-id="45712-190">Figure 7.</span></span> <span data-ttu-id="45712-191">視覺化多類別分類中的評分模型結果</span><span class="sxs-lookup"><span data-stu-id="45712-191">Visualize score model results in a multi-class classification</span></span>

<span data-ttu-id="45712-192">**結果解譯**</span><span class="sxs-lookup"><span data-stu-id="45712-192">**Result interpretation**</span></span>

<span data-ttu-id="45712-193">hello 左邊 16 個資料行代表 hello 測試集的 hello 功能值。</span><span class="sxs-lookup"><span data-stu-id="45712-193">hello left 16 columns represent hello feature values of hello test set.</span></span> <span data-ttu-id="45712-194">hello 像計分機率類別"XX"hello 二級案例中就如同 hello 計分機率資料行的名稱的資料行。</span><span class="sxs-lookup"><span data-stu-id="45712-194">hello columns with names like Scored Probabilities for Class "XX" are just like hello Scored Probabilities column in hello two-class case.</span></span> <span data-ttu-id="45712-195">它們會顯示 hello 機率 hello 對應的項目屬於特定類別。</span><span class="sxs-lookup"><span data-stu-id="45712-195">They show hello probability that hello corresponding entry falls into a certain class.</span></span> <span data-ttu-id="45712-196">例如，對於 hello 第一個項目沒有 0.003571 機率，則"A"0.000451 機率則是"B，"依此類推。</span><span class="sxs-lookup"><span data-stu-id="45712-196">For example, for hello first entry, there is 0.003571 probability that it is an “A,” 0.000451 probability that it is a “B,” and so forth.</span></span> <span data-ttu-id="45712-197">hello 最後一個資料行 （計分標籤） 是 hello 與計分標籤在 hello 二級案例相同。</span><span class="sxs-lookup"><span data-stu-id="45712-197">hello last column (Scored Labels) is hello same as Scored Labels in hello two-class case.</span></span> <span data-ttu-id="45712-198">它會選取 hello 類別以 hello 最大計分機率為 hello hello 對應項目的預測的類別。</span><span class="sxs-lookup"><span data-stu-id="45712-198">It selects hello class with hello largest scored probability as hello predicted class of hello corresponding entry.</span></span> <span data-ttu-id="45712-199">例如，為 hello 第一個項目 hello 計分標籤是"F"因為它有最大機率 toobe hello"F"(0.916995)。</span><span class="sxs-lookup"><span data-stu-id="45712-199">For example, for hello first entry, hello scored label is “F” since it has hello largest probability toobe an “F” (0.916995).</span></span>

<span data-ttu-id="45712-200">**Web 服務發佈**</span><span class="sxs-lookup"><span data-stu-id="45712-200">**Web service publication**</span></span>

<span data-ttu-id="45712-201">您也可以取得 hello hello 計分標籤的每個項目和 hello 機率計分標籤。</span><span class="sxs-lookup"><span data-stu-id="45712-201">You can also get hello scored label for each entry and hello probability of hello scored label.</span></span> <span data-ttu-id="45712-202">hello 基本邏輯是之間所有 hello 計分機率 toofind hello 最大機率。</span><span class="sxs-lookup"><span data-stu-id="45712-202">hello basic logic is toofind hello largest probability among all hello scored probabilities.</span></span> <span data-ttu-id="45712-203">toodo，您需要 toouse hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="45712-203">toodo this, you need toouse hello [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="45712-204">圖 8 顯示 hello R 程式碼，且圖 9 顯示 hello 實驗的 hello 結果。</span><span class="sxs-lookup"><span data-stu-id="45712-204">hello R code is shown in Figure 8, and hello result of hello experiment is shown in Figure 9.</span></span>

![R 程式碼範例](./media/machine-learning-interpret-model-results/8.png)

<span data-ttu-id="45712-206">圖 8.</span><span class="sxs-lookup"><span data-stu-id="45712-206">Figure 8.</span></span> <span data-ttu-id="45712-207">解壓縮計分標籤和 hello 的 R 程式碼相關聯的機率的 hello 標籤</span><span class="sxs-lookup"><span data-stu-id="45712-207">R code for extracting Scored Labels and hello associated probabilities of hello labels</span></span>

![實驗結果](./media/machine-learning-interpret-model-results/9.png)

<span data-ttu-id="45712-209">圖 9.</span><span class="sxs-lookup"><span data-stu-id="45712-209">Figure 9.</span></span> <span data-ttu-id="45712-210">最終的計分實驗的 hello 字母辨識多級分類問題</span><span class="sxs-lookup"><span data-stu-id="45712-210">Final scoring experiment of hello letter-recognition multiclass classification problem</span></span>

<span data-ttu-id="45712-211">發行和執行 hello web 服務並輸入一些輸入的功能值之後，hello 會傳回結果看起來像是圖 10。</span><span class="sxs-lookup"><span data-stu-id="45712-211">After you publish and run hello web service and enter some input feature values, hello returned result looks like Figure 10.</span></span> <span data-ttu-id="45712-212">此手寫的代號，其擷取 16 的功能，與為 0.9715 機率的預測的 toobe"T"。</span><span class="sxs-lookup"><span data-stu-id="45712-212">This hand-written letter, with its extracted 16 features, is predicted toobe a “T” with 0.9715 probability.</span></span>

![測試解譯評分模組](./media/machine-learning-interpret-model-results/9_1.png)

![測試結果](./media/machine-learning-interpret-model-results/10.png)

<span data-ttu-id="45712-215">圖 10.</span><span class="sxs-lookup"><span data-stu-id="45712-215">Figure 10.</span></span> <span data-ttu-id="45712-216">多類別分類的 Web 服務結果</span><span class="sxs-lookup"><span data-stu-id="45712-216">Web service result of multiclass classification</span></span>

## <a name="regression"></a><span data-ttu-id="45712-217">迴歸</span><span class="sxs-lookup"><span data-stu-id="45712-217">Regression</span></span>
<span data-ttu-id="45712-218">迴歸問題與分類問題不同。</span><span class="sxs-lookup"><span data-stu-id="45712-218">Regression problems are different from classification problems.</span></span> <span data-ttu-id="45712-219">在分類問題，您正嘗試 toopredict 離散類別，例如哪一種類別光圈花屬於。</span><span class="sxs-lookup"><span data-stu-id="45712-219">In a classification problem, you're trying toopredict discrete classes, such as which class an iris flower belongs to.</span></span> <span data-ttu-id="45712-220">但是，您可以看到 hello 下列範例的迴歸問題中，您正嘗試 toopredict 連續變數，例如 hello 汽車價格。</span><span class="sxs-lookup"><span data-stu-id="45712-220">But as you can see in hello following example of a regression problem, you're trying toopredict a continuous variable, such as hello price of a car.</span></span>

<span data-ttu-id="45712-221">**範例實驗**</span><span class="sxs-lookup"><span data-stu-id="45712-221">**Example experiment**</span></span>

<span data-ttu-id="45712-222">使用汽車價格預測做為您的迴歸範例。</span><span class="sxs-lookup"><span data-stu-id="45712-222">Use automobile price prediction as your example for regression.</span></span> <span data-ttu-id="45712-223">您正嘗試根據其功能，包括產生、 燃料類型、 內文類型和磁碟機滾輪一輛車 toopredict hello 價格。</span><span class="sxs-lookup"><span data-stu-id="45712-223">You are trying toopredict hello price of a car based on its features, including make, fuel type, body type, and drive wheel.</span></span> <span data-ttu-id="45712-224">圖 11 顯示 hello 實驗。</span><span class="sxs-lookup"><span data-stu-id="45712-224">hello experiment is shown in Figure 11.</span></span>

![汽車價格迴歸實驗](./media/machine-learning-interpret-model-results/11.png)

<span data-ttu-id="45712-226">圖 11.</span><span class="sxs-lookup"><span data-stu-id="45712-226">Figure 11.</span></span> <span data-ttu-id="45712-227">汽車價格迴歸問題實驗</span><span class="sxs-lookup"><span data-stu-id="45712-227">Automobile price regression problem experiment</span></span>

<span data-ttu-id="45712-228">以視覺化方式檢視 hello[計分模型][ score-model]模組，hello 結果看起來像圖 12。</span><span class="sxs-lookup"><span data-stu-id="45712-228">Visualizing hello [Score Model][score-model] module, hello result looks like Figure 12.</span></span>

![汽車價格預測問題的評分結果](./media/machine-learning-interpret-model-results/12.png)

<span data-ttu-id="45712-230">圖 12.</span><span class="sxs-lookup"><span data-stu-id="45712-230">Figure 12.</span></span> <span data-ttu-id="45712-231">計分結果 hello 汽車價格預測問題</span><span class="sxs-lookup"><span data-stu-id="45712-231">Scoring result for hello automobile price prediction problem</span></span>

<span data-ttu-id="45712-232">**結果解譯**</span><span class="sxs-lookup"><span data-stu-id="45712-232">**Result interpretation**</span></span>

<span data-ttu-id="45712-233">計分的標籤是此計分結果中的 hello 結果資料行。</span><span class="sxs-lookup"><span data-stu-id="45712-233">Scored Labels is hello result column in this scoring result.</span></span> <span data-ttu-id="45712-234">hello 預測每輛汽車價格的 hello 數字。</span><span class="sxs-lookup"><span data-stu-id="45712-234">hello numbers are hello predicted price for each car.</span></span>

<span data-ttu-id="45712-235">**Web 服務發佈**</span><span class="sxs-lookup"><span data-stu-id="45712-235">**Web service publication**</span></span>

<span data-ttu-id="45712-236">您可以發行到 web 服務的 hello 迴歸實驗，並呼叫它在 hello 汽車價格預測 hello 二級分類相同方式使用大小寫。</span><span class="sxs-lookup"><span data-stu-id="45712-236">You can publish hello regression experiment into a web service and call it for automobile price prediction in hello same way as in hello two-class classification use case.</span></span>

![汽車價格迴歸問題的評分實驗](./media/machine-learning-interpret-model-results/13.png)

<span data-ttu-id="45712-238">圖 13.</span><span class="sxs-lookup"><span data-stu-id="45712-238">Figure 13.</span></span> <span data-ttu-id="45712-239">汽車價格迴歸問題的評分實驗</span><span class="sxs-lookup"><span data-stu-id="45712-239">Scoring experiment of an automobile price regression problem</span></span>

<span data-ttu-id="45712-240">執行 hello web 服務，hello 傳回結果看起來像是圖 14。</span><span class="sxs-lookup"><span data-stu-id="45712-240">Running hello web service, hello returned result looks like Figure 14.</span></span> <span data-ttu-id="45712-241">hello 預測這輛汽車價格為 $15,085.52。</span><span class="sxs-lookup"><span data-stu-id="45712-241">hello predicted price for this car is $15,085.52.</span></span>

![測試解譯評分模組](./media/machine-learning-interpret-model-results/13_1.png)

![評分模組結果](./media/machine-learning-interpret-model-results/14.png)

<span data-ttu-id="45712-244">圖 14.</span><span class="sxs-lookup"><span data-stu-id="45712-244">Figure 14.</span></span> <span data-ttu-id="45712-245">汽車價格迴歸問題的 Web 服務結果</span><span class="sxs-lookup"><span data-stu-id="45712-245">Web service result of an automobile price regression problem</span></span>

## <a name="clustering"></a><span data-ttu-id="45712-246">叢集</span><span class="sxs-lookup"><span data-stu-id="45712-246">Clustering</span></span>
<span data-ttu-id="45712-247">**範例實驗**</span><span class="sxs-lookup"><span data-stu-id="45712-247">**Example experiment**</span></span>

<span data-ttu-id="45712-248">我們將使用 hello 光圈資料集一次 toobuild 叢集實驗。</span><span class="sxs-lookup"><span data-stu-id="45712-248">Let’s use hello Iris data set again toobuild a clustering experiment.</span></span> <span data-ttu-id="45712-249">這裡您可以篩選掉 hello hello 資料集中的類別標籤，以便只具有的功能，並可用於叢集。</span><span class="sxs-lookup"><span data-stu-id="45712-249">Here you can filter out hello class labels in hello data set so that it only has features and can be used for clustering.</span></span> <span data-ttu-id="45712-250">在此光圈使用案例，指定在 hello 定型過程中，這表示您將叢集 hello 花兩個類別中的兩個叢集 toobe 的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="45712-250">In this iris use case, specify hello number of clusters toobe two during hello training process, which means you would cluster hello flowers into two classes.</span></span> <span data-ttu-id="45712-251">hello 實驗 圖 15 所示。</span><span class="sxs-lookup"><span data-stu-id="45712-251">hello experiment is shown in Figure 15.</span></span>

![鳶尾花叢集問題實驗](./media/machine-learning-interpret-model-results/15.png)

<span data-ttu-id="45712-253">圖 15.</span><span class="sxs-lookup"><span data-stu-id="45712-253">Figure 15.</span></span> <span data-ttu-id="45712-254">鳶尾花叢集問題實驗</span><span class="sxs-lookup"><span data-stu-id="45712-254">Iris clustering problem experiment</span></span>

<span data-ttu-id="45712-255">叢集與分類的 hello 定型資料集沒有的地真資料標籤本身。</span><span class="sxs-lookup"><span data-stu-id="45712-255">Clustering differs from classification in that hello training data set doesn’t have ground-truth labels by itself.</span></span> <span data-ttu-id="45712-256">叢集群組 hello 訓練資料集的執行個體到不同的叢集。</span><span class="sxs-lookup"><span data-stu-id="45712-256">Clustering groups hello training data set instances into distinct clusters.</span></span> <span data-ttu-id="45712-257">Hello 定型在處理期間，hello 模型標籤 hello 學習 hello 差異及其功能的項目。</span><span class="sxs-lookup"><span data-stu-id="45712-257">During hello training process, hello model labels hello entries by learning hello differences between their features.</span></span> <span data-ttu-id="45712-258">在這之後，您可以使用 hello 定型的模型 toofurther 分類未來的項目。</span><span class="sxs-lookup"><span data-stu-id="45712-258">After that, hello trained model can be used toofurther classify future entries.</span></span> <span data-ttu-id="45712-259">有兩個部分的 hello 結果，我們有興趣內叢集問題。</span><span class="sxs-lookup"><span data-stu-id="45712-259">There are two parts of hello result we are interested in within a clustering problem.</span></span> <span data-ttu-id="45712-260">hello 第一個部分標記 hello 定型資料集，和 hello 第二個會分類新的資料集與 hello 定型的模型。</span><span class="sxs-lookup"><span data-stu-id="45712-260">hello first part is labeling hello training data set, and hello second is classifying a new data set with hello trained model.</span></span>

<span data-ttu-id="45712-261">hello hello 結果的第一個部分可以以視覺化方式檢視，即可保留輸出連接埠的 hello[定型群集模型][ train-clustering-model] ，然後按一下**視覺化**。</span><span class="sxs-lookup"><span data-stu-id="45712-261">hello first part of hello result can be visualized by clicking hello left output port of [Train Clustering Model][train-clustering-model] and then clicking **Visualize**.</span></span> <span data-ttu-id="45712-262">圖 16 顯示 hello 視覺效果。</span><span class="sxs-lookup"><span data-stu-id="45712-262">hello visualization is shown in Figure 16.</span></span>

![叢集結果](./media/machine-learning-interpret-model-results/16.png)

<span data-ttu-id="45712-264">圖 16.</span><span class="sxs-lookup"><span data-stu-id="45712-264">Figure 16.</span></span> <span data-ttu-id="45712-265">以視覺化方式檢視叢集 hello 定型資料集的結果</span><span class="sxs-lookup"><span data-stu-id="45712-265">Visualize clustering result for hello training data set</span></span>

<span data-ttu-id="45712-266">hello hello 第二個部分，叢集 hello 定型群集模型中，新的項目結果所示圖 17。</span><span class="sxs-lookup"><span data-stu-id="45712-266">hello result of hello second part, clustering new entries with hello trained clustering model, is shown in Figure 17.</span></span>

![視覺化叢集結果](./media/machine-learning-interpret-model-results/17.png)

<span data-ttu-id="45712-268">圖 17.</span><span class="sxs-lookup"><span data-stu-id="45712-268">Figure 17.</span></span> <span data-ttu-id="45712-269">視覺化新資料集的叢集結果</span><span class="sxs-lookup"><span data-stu-id="45712-269">Visualize clustering result on a new data set</span></span>

<span data-ttu-id="45712-270">**結果解譯**</span><span class="sxs-lookup"><span data-stu-id="45712-270">**Result interpretation**</span></span>

<span data-ttu-id="45712-271">雖然 hello hello 兩個部分結果源自不同實驗階段，它們看起來 hello 相同，並解譯在 hello 相同的方式。</span><span class="sxs-lookup"><span data-stu-id="45712-271">Although hello results of hello two parts stem from different experiment stages, they look hello same and are interpreted in hello same way.</span></span> <span data-ttu-id="45712-272">hello 前四個資料行的功能。</span><span class="sxs-lookup"><span data-stu-id="45712-272">hello first four columns are features.</span></span> <span data-ttu-id="45712-273">hello 最後一個資料行，指派方式，是 hello 預測結果。</span><span class="sxs-lookup"><span data-stu-id="45712-273">hello last column, Assignments, is hello prediction result.</span></span> <span data-ttu-id="45712-274">hello 預測相同數目的項目指派的 hello toobe hello 相同叢集，也就是在共用相似之處，在某些方面 （這項實驗中使用 hello 預設歐幾里德距離公制）。</span><span class="sxs-lookup"><span data-stu-id="45712-274">hello entries assigned hello same number are predicted toobe in hello same cluster, that is, they share similarities in some way (this experiment uses hello default Euclidean distance metric).</span></span> <span data-ttu-id="45712-275">因為指定的叢集 toobe 2 的 hello 數目，0 或 1，分別標示為指派中的 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="45712-275">Because you specified hello number of clusters toobe 2, hello entries in Assignments are labeled either 0 or 1.</span></span>

<span data-ttu-id="45712-276">**Web 服務發佈**</span><span class="sxs-lookup"><span data-stu-id="45712-276">**Web service publication**</span></span>

<span data-ttu-id="45712-277">您可以發行到 web 服務叢集實驗的 hello 並呼叫它的群集預測 hello 相同方式與 hello 二級分類中使用的大小寫。</span><span class="sxs-lookup"><span data-stu-id="45712-277">You can publish hello clustering experiment into a web service and call it for clustering predictions hello same way as in hello two-class classification use case.</span></span>

![鳶尾花叢集問題的評分實驗](./media/machine-learning-interpret-model-results/18.png)

<span data-ttu-id="45712-279">圖 18.</span><span class="sxs-lookup"><span data-stu-id="45712-279">Figure 18.</span></span> <span data-ttu-id="45712-280">鳶尾花叢集問題的評分實驗</span><span class="sxs-lookup"><span data-stu-id="45712-280">Scoring experiment of an iris clustering problem</span></span>

<span data-ttu-id="45712-281">執行 hello web 服務之後，hello 傳回結果看起來像是圖 19。</span><span class="sxs-lookup"><span data-stu-id="45712-281">After you run hello web service, hello returned result looks like Figure 19.</span></span> <span data-ttu-id="45712-282">此花牌是預測的 toobe 0 叢集中。</span><span class="sxs-lookup"><span data-stu-id="45712-282">This flower is predicted toobe in cluster 0.</span></span>

![測試解譯評分模組](./media/machine-learning-interpret-model-results/18_1.png)

![評分模組結果](./media/machine-learning-interpret-model-results/19.png)

<span data-ttu-id="45712-285">圖 19.</span><span class="sxs-lookup"><span data-stu-id="45712-285">Figure 19.</span></span> <span data-ttu-id="45712-286">鳶尾花雙類別分類的 Web 服務結果</span><span class="sxs-lookup"><span data-stu-id="45712-286">Web service result of iris two-class classification</span></span>

## <a name="recommender-system"></a><span data-ttu-id="45712-287">推薦系統</span><span class="sxs-lookup"><span data-stu-id="45712-287">Recommender system</span></span>
<span data-ttu-id="45712-288">**範例實驗**</span><span class="sxs-lookup"><span data-stu-id="45712-288">**Example experiment**</span></span>

<span data-ttu-id="45712-289">適用於推薦系統，您可以使用 hello 餐廳建議問題，做為範例： 您可以根據分級記錄的客戶建議餐廳。</span><span class="sxs-lookup"><span data-stu-id="45712-289">For recommender systems, you can use hello restaurant recommendation problem as an example: you can recommend restaurants for customers based on their rating history.</span></span> <span data-ttu-id="45712-290">hello 輸入的資料包含三個部分：</span><span class="sxs-lookup"><span data-stu-id="45712-290">hello input data consists of three parts:</span></span>

* <span data-ttu-id="45712-291">來自客戶的餐廳評等</span><span class="sxs-lookup"><span data-stu-id="45712-291">Restaurant ratings from customers</span></span>
* <span data-ttu-id="45712-292">客戶特色資料</span><span class="sxs-lookup"><span data-stu-id="45712-292">Customer feature data</span></span>
* <span data-ttu-id="45712-293">餐廳特色資料</span><span class="sxs-lookup"><span data-stu-id="45712-293">Restaurant feature data</span></span>

<span data-ttu-id="45712-294">有幾件事，我們可以與 hello[定型 Matchbox 推薦][ train-matchbox-recommender] Azure Machine Learning 中的模組：</span><span class="sxs-lookup"><span data-stu-id="45712-294">There are several things we can do with hello [Train Matchbox Recommender][train-matchbox-recommender] module in Azure Machine Learning:</span></span>

* <span data-ttu-id="45712-295">為指定使用者和項目預測評等</span><span class="sxs-lookup"><span data-stu-id="45712-295">Predict ratings for a given user and item</span></span>
* <span data-ttu-id="45712-296">建議您指定使用者的項目 tooa</span><span class="sxs-lookup"><span data-stu-id="45712-296">Recommend items tooa given user</span></span>
* <span data-ttu-id="45712-297">尋找給定使用者的使用者相關的 tooa</span><span class="sxs-lookup"><span data-stu-id="45712-297">Find users related tooa given user</span></span>
* <span data-ttu-id="45712-298">尋找項目相關的 tooa 給定項目</span><span class="sxs-lookup"><span data-stu-id="45712-298">Find items related tooa given item</span></span>

<span data-ttu-id="45712-299">您可以選擇您希望 toodo 從 hello 中的 hello 四個選項中選取**推薦預測種類**功能表。</span><span class="sxs-lookup"><span data-stu-id="45712-299">You can choose what you want toodo by selecting from hello four options in hello **Recommender prediction kind** menu.</span></span> <span data-ttu-id="45712-300">您可以在這裡逐步完成這四個案例。</span><span class="sxs-lookup"><span data-stu-id="45712-300">Here you can walk through all four scenarios.</span></span>

![Matchbox 推薦](./media/machine-learning-interpret-model-results/19_1.png)

<span data-ttu-id="45712-302">典型的推薦系統 Azure Machine Learning 實驗如圖 20 所示。</span><span class="sxs-lookup"><span data-stu-id="45712-302">A typical Azure Machine Learning experiment for a recommender system looks like Figure 20.</span></span> <span data-ttu-id="45712-303">如需有關如何 toouse 這些推薦系統模組，請參閱資訊[定型 matchbox 推薦][ train-matchbox-recommender]和[計分 matchbox 推薦][ score-matchbox-recommender].</span><span class="sxs-lookup"><span data-stu-id="45712-303">For information about how toouse those recommender system modules, see [Train matchbox recommender][train-matchbox-recommender] and [Score matchbox recommender][score-matchbox-recommender].</span></span>

![推薦系統實驗](./media/machine-learning-interpret-model-results/20.png)

<span data-ttu-id="45712-305">圖 20.</span><span class="sxs-lookup"><span data-stu-id="45712-305">Figure 20.</span></span> <span data-ttu-id="45712-306">推薦系統實驗</span><span class="sxs-lookup"><span data-stu-id="45712-306">Recommender system experiment</span></span>

<span data-ttu-id="45712-307">**結果解譯**</span><span class="sxs-lookup"><span data-stu-id="45712-307">**Result interpretation**</span></span>

<span data-ttu-id="45712-308">**為指定使用者和項目預測評等**</span><span class="sxs-lookup"><span data-stu-id="45712-308">**Predict ratings for a given user and item**</span></span>

<span data-ttu-id="45712-309">藉由選取**評等預測**下**推薦預測種類**，您要詢問 hello 推薦系統 toopredict hello 評等來指定的使用者和項目。</span><span class="sxs-lookup"><span data-stu-id="45712-309">By selecting **Rating Prediction** under **Recommender prediction kind**, you are asking hello recommender system toopredict hello rating for a given user and item.</span></span> <span data-ttu-id="45712-310">hello 視覺效果的 hello[計分 Matchbox 推薦][ score-matchbox-recommender]輸出看起來像圖 21。</span><span class="sxs-lookup"><span data-stu-id="45712-310">hello visualization of hello [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 21.</span></span>

![分數 hello 推薦系統-評比預測的結果](./media/machine-learning-interpret-model-results/21.png)

<span data-ttu-id="45712-312">圖 21.</span><span class="sxs-lookup"><span data-stu-id="45712-312">Figure 21.</span></span> <span data-ttu-id="45712-313">以視覺化方式檢視 hello 推薦系統-評等預測中的 hello 分數結果</span><span class="sxs-lookup"><span data-stu-id="45712-313">Visualize hello score result of hello recommender system--rating prediction</span></span>

<span data-ttu-id="45712-314">hello 前兩個資料行是 hello hello 輸入資料所提供的使用者-項目組。</span><span class="sxs-lookup"><span data-stu-id="45712-314">hello first two columns are hello user-item pairs provided by hello input data.</span></span> <span data-ttu-id="45712-315">hello 第三個資料行是 hello 預測的評等的特定項目的使用者。</span><span class="sxs-lookup"><span data-stu-id="45712-315">hello third column is hello predicted rating of a user for a certain item.</span></span> <span data-ttu-id="45712-316">比方說，hello 第一個資料列中 U1048 是的客戶的預測做為 2 toorate 餐廳 135026。</span><span class="sxs-lookup"><span data-stu-id="45712-316">For example, in hello first row, customer U1048 is predicted toorate restaurant 135026 as 2.</span></span>

<span data-ttu-id="45712-317">**建議您指定使用者的項目 tooa**</span><span class="sxs-lookup"><span data-stu-id="45712-317">**Recommend items tooa given user**</span></span>

<span data-ttu-id="45712-318">藉由選取**項目建議**下**推薦預測種類**，您指定使用者的系統 toorecommend 項目 tooa 問 hello 推薦。</span><span class="sxs-lookup"><span data-stu-id="45712-318">By selecting **Item Recommendation** under **Recommender prediction kind**, you're asking hello recommender system toorecommend items tooa given user.</span></span> <span data-ttu-id="45712-319">在此案例中 hello 最後一個參數 toochoose 是*建議的項目選取*。</span><span class="sxs-lookup"><span data-stu-id="45712-319">hello last parameter toochoose in this scenario is *Recommended item selection*.</span></span> <span data-ttu-id="45712-320">hello 選項**從評等項目 （適用於模型評估）**主要是供 hello 定型程序期間的模型評估。</span><span class="sxs-lookup"><span data-stu-id="45712-320">hello option **From Rated Items (for model evaluation)** is primarily for model evaluation during hello training process.</span></span> <span data-ttu-id="45712-321">對於此預測階段，我們選擇 [從所有項目] 。</span><span class="sxs-lookup"><span data-stu-id="45712-321">For this prediction stage, we choose **From All Items**.</span></span> <span data-ttu-id="45712-322">hello 視覺效果的 hello[計分 Matchbox 推薦][ score-matchbox-recommender]輸出看起來像圖 22。</span><span class="sxs-lookup"><span data-stu-id="45712-322">hello visualization of hello [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 22.</span></span>

![推薦系統的評分結果 - 項目推薦](./media/machine-learning-interpret-model-results/22.png)

<span data-ttu-id="45712-324">圖 22.</span><span class="sxs-lookup"><span data-stu-id="45712-324">Figure 22.</span></span> <span data-ttu-id="45712-325">以視覺化方式檢視 hello 推薦系統項目建議分數結果</span><span class="sxs-lookup"><span data-stu-id="45712-325">Visualize score result of hello recommender system--item recommendation</span></span>

<span data-ttu-id="45712-326">所提供的輸入資料 hello hello hello 六個資料行代表 hello 指定使用者識別碼 toorecommend 項目，第的一個。</span><span class="sxs-lookup"><span data-stu-id="45712-326">hello first of hello six columns represents hello given user IDs toorecommend items for, as provided by hello input data.</span></span> <span data-ttu-id="45712-327">hello 其他五個資料行代表 hello 建議 toohello 使用者相關性的遞減順序的項目。</span><span class="sxs-lookup"><span data-stu-id="45712-327">hello other five columns represent hello items recommended toohello user in descending order of relevance.</span></span> <span data-ttu-id="45712-328">例如，hello 第一個資料列，在 hello 最建議的餐廳客戶 U1048 是 134986，後面接著 135018、 134975、 135021 和 132862。</span><span class="sxs-lookup"><span data-stu-id="45712-328">For example, in hello first row, hello most recommended restaurant for customer U1048 is 134986, followed by 135018, 134975, 135021, and 132862.</span></span>

<span data-ttu-id="45712-329">**尋找給定使用者的使用者相關的 tooa**</span><span class="sxs-lookup"><span data-stu-id="45712-329">**Find users related tooa given user**</span></span>

<span data-ttu-id="45712-330">藉由選取**相關使用者**下**推薦預測種類**，您會問 hello 推薦系統 toofind 相關的使用者 tooa 指定使用者。</span><span class="sxs-lookup"><span data-stu-id="45712-330">By selecting **Related Users** under **Recommender prediction kind**, you're asking hello recommender system toofind related users tooa given user.</span></span> <span data-ttu-id="45712-331">相關的使用者是 hello 具有相似的偏好。</span><span class="sxs-lookup"><span data-stu-id="45712-331">Related users are hello users who have similar preferences.</span></span> <span data-ttu-id="45712-332">在此案例中 hello 最後一個參數 toochoose 是*相關使用者選取*。</span><span class="sxs-lookup"><span data-stu-id="45712-332">hello last parameter toochoose in this scenario is *Related user selection*.</span></span> <span data-ttu-id="45712-333">hello 選項**從使用者的評等項目 （適用於模型評估）**主要是供 hello 定型程序期間的模型評估。</span><span class="sxs-lookup"><span data-stu-id="45712-333">hello option **From Users That Rated Items (for model evaluation)** is primarily for model evaluation during hello training process.</span></span> <span data-ttu-id="45712-334">對於此預測階段選擇 [從所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="45712-334">Choose **From All Users** for this prediction stage.</span></span> <span data-ttu-id="45712-335">hello 視覺效果的 hello[計分 Matchbox 推薦][ score-matchbox-recommender]輸出看起來像圖 23。</span><span class="sxs-lookup"><span data-stu-id="45712-335">hello visualization of hello [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 23.</span></span>

![推薦系統的評分結果 - 相關使用者](./media/machine-learning-interpret-model-results/23.png)

<span data-ttu-id="45712-337">圖 23.</span><span class="sxs-lookup"><span data-stu-id="45712-337">Figure 23.</span></span> <span data-ttu-id="45712-338">以視覺化方式檢視 hello 推薦系統相關使用者的分數結果</span><span class="sxs-lookup"><span data-stu-id="45712-338">Visualize score results of hello recommender system--related users</span></span>

<span data-ttu-id="45712-339">第一次 hello 給定使用者所需的 Id toofind hello 六個資料行顯示 hello 的相關使用者所提供的輸入資料。</span><span class="sxs-lookup"><span data-stu-id="45712-339">hello first of hello six columns shows hello given user IDs needed toofind related users, as provided by input data.</span></span> <span data-ttu-id="45712-340">hello 其他五個資料行存放區 hello 相關性的遞減順序中的 hello 使用者預測相關的使用者。</span><span class="sxs-lookup"><span data-stu-id="45712-340">hello other five columns store hello predicted related users of hello user in descending order of relevance.</span></span> <span data-ttu-id="45712-341">例如，在 hello 第一個資料列，hello 客戶 U1048 最相關的客戶是 U1051，後面接著 U1066、 U1044、 U1017 和 U1072。</span><span class="sxs-lookup"><span data-stu-id="45712-341">For example, in hello first row, hello most relevant customer for customer U1048 is U1051, followed by U1066, U1044, U1017, and U1072.</span></span>

<span data-ttu-id="45712-342">**尋找項目相關的 tooa 給定項目**</span><span class="sxs-lookup"><span data-stu-id="45712-342">**Find items related tooa given item**</span></span>

<span data-ttu-id="45712-343">藉由選取**相關項目**下**推薦預測種類**，您要詢問 hello 推薦系統 toofind 相關項目 tooa 給定項目。</span><span class="sxs-lookup"><span data-stu-id="45712-343">By selecting **Related Items** under **Recommender prediction kind**, you are asking hello recommender system toofind related items tooa given item.</span></span> <span data-ttu-id="45712-344">相關項目是 hello 項目最有可能 toobe 喜歡 hello 由相同使用者。</span><span class="sxs-lookup"><span data-stu-id="45712-344">Related items are hello items most likely toobe liked by hello same user.</span></span> <span data-ttu-id="45712-345">在此案例中 hello 最後一個參數 toochoose 是*相關的項目選取*。</span><span class="sxs-lookup"><span data-stu-id="45712-345">hello last parameter toochoose in this scenario is *Related item selection*.</span></span> <span data-ttu-id="45712-346">hello 選項**從評等項目 （適用於模型評估）**主要是供 hello 定型程序期間的模型評估。</span><span class="sxs-lookup"><span data-stu-id="45712-346">hello option **From Rated Items (for model evaluation)** is primarily for model evaluation during hello training process.</span></span> <span data-ttu-id="45712-347">對於此預測階段，我們選擇 [ **從所有項目** ]。</span><span class="sxs-lookup"><span data-stu-id="45712-347">We choose **From All Items** for this prediction stage.</span></span> <span data-ttu-id="45712-348">hello 視覺效果的 hello[計分 Matchbox 推薦][ score-matchbox-recommender]輸出看起來像圖 24。</span><span class="sxs-lookup"><span data-stu-id="45712-348">hello visualization of hello [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 24.</span></span>

![推薦系統的評分結果 - 相關項目](./media/machine-learning-interpret-model-results/24.png)

<span data-ttu-id="45712-350">圖 24.</span><span class="sxs-lookup"><span data-stu-id="45712-350">Figure 24.</span></span> <span data-ttu-id="45712-351">將相關項目-hello 推薦系統的分數結果視覺化</span><span class="sxs-lookup"><span data-stu-id="45712-351">Visualize score results of hello recommender system--related items</span></span>

<span data-ttu-id="45712-352">hello hello 六個資料行代表 hello 指定所需的項目 Id 中的第一個 toofind hello 輸入資料所提供，相關項目。</span><span class="sxs-lookup"><span data-stu-id="45712-352">hello first of hello six columns represents hello given item IDs needed toofind related items, as provided by hello input data.</span></span> <span data-ttu-id="45712-353">hello 其他五個資料行存放區 hello hello 項目以遞減的順序，根據關聯的預測相關的項目。</span><span class="sxs-lookup"><span data-stu-id="45712-353">hello other five columns store hello predicted related items of hello item in descending order in terms of relevance.</span></span> <span data-ttu-id="45712-354">例如，在 hello 第一個資料列項目的 135026 hello 最相關的項目是 135074，後面接著 135035、 132875、 135055 和 134992。</span><span class="sxs-lookup"><span data-stu-id="45712-354">For example, in hello first row, hello most relevant item for item 135026 is 135074, followed by 135035, 132875, 135055, and 134992.</span></span>

<span data-ttu-id="45712-355">**Web 服務發佈**</span><span class="sxs-lookup"><span data-stu-id="45712-355">**Web service publication**</span></span>

<span data-ttu-id="45712-356">hello 程序發行為 web 服務 tooget 預測實驗是每個 hello 四種案例類似。</span><span class="sxs-lookup"><span data-stu-id="45712-356">hello process of publishing these experiments as web services tooget predictions is similar for each of hello four scenarios.</span></span> <span data-ttu-id="45712-357">這裡我們採用 hello 第二個案例 (給定使用者建議項目 tooa) 做為範例。</span><span class="sxs-lookup"><span data-stu-id="45712-357">Here we take hello second scenario (recommend items tooa given user) as an example.</span></span> <span data-ttu-id="45712-358">您可以遵循與其他三個 hello hello 相同的程序。</span><span class="sxs-lookup"><span data-stu-id="45712-358">You can follow hello same procedure with hello other three.</span></span>

<span data-ttu-id="45712-359">儲存 hello 定型推薦系統為定型的模型，以及篩選 hello 輸入的資料 tooa 單一使用者識別碼資料行做為要求，您可以如同圖 25 hello 實驗相連結，並將其發行為 web 服務。</span><span class="sxs-lookup"><span data-stu-id="45712-359">Saving hello trained recommender system as a trained model and filtering hello input data tooa single user ID column as requested, you can hook up hello experiment as in Figure 25 and publish it as a web service.</span></span>

![計分實驗的 hello 餐廳建議問題](./media/machine-learning-interpret-model-results/25.png)

<span data-ttu-id="45712-361">圖 25.</span><span class="sxs-lookup"><span data-stu-id="45712-361">Figure 25.</span></span> <span data-ttu-id="45712-362">計分實驗的 hello 餐廳建議問題</span><span class="sxs-lookup"><span data-stu-id="45712-362">Scoring experiment of hello restaurant recommendation problem</span></span>

<span data-ttu-id="45712-363">執行 hello web 服務，hello 傳回結果看起來像是圖 26。</span><span class="sxs-lookup"><span data-stu-id="45712-363">Running hello web service, hello returned result looks like Figure 26.</span></span> <span data-ttu-id="45712-364">hello 五個建議的餐廳使用者 U1048 是 134986、 135018、 134975、 135021 和 132862。</span><span class="sxs-lookup"><span data-stu-id="45712-364">hello five recommended restaurants for user U1048 are 134986, 135018, 134975, 135021, and 132862.</span></span>

![推薦系統服務的範例](./media/machine-learning-interpret-model-results/25_1.png)

![範例實驗結果](./media/machine-learning-interpret-model-results/26.png)

<span data-ttu-id="45712-367">圖 26.</span><span class="sxs-lookup"><span data-stu-id="45712-367">Figure 26.</span></span> <span data-ttu-id="45712-368">餐廳推薦問題的 Web 服務結果</span><span class="sxs-lookup"><span data-stu-id="45712-368">Web service result of restaurant recommendation problem</span></span>

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
