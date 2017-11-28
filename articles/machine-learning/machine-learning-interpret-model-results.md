---
title: "在 Machine Learning 中解譯模型結果 | Microsoft Docs"
description: "如何針對使用和視覺化評分模型輸出的演算法選擇最佳的參數設定。"
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
ms.openlocfilehash: 939dd7b359b4f5c248ade47b794102f4930994b1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="interpret-model-results-in-azure-machine-learning"></a><span data-ttu-id="00b0e-103">在 Azure Machine Learning 中解譯模型結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-103">Interpret model results in Azure Machine Learning</span></span>
<span data-ttu-id="00b0e-104">本主題說明如何視覺化和解譯 Azure Machine Learning Studio 中的預測結果。</span><span class="sxs-lookup"><span data-stu-id="00b0e-104">This topic explains how to visualize and interpret prediction results in Azure Machine Learning Studio.</span></span> <span data-ttu-id="00b0e-105">在您訓練好模型並完成其預測 (「模型評分」) 之後，您必須了解和解譯預測結果。</span><span class="sxs-lookup"><span data-stu-id="00b0e-105">After you have trained a model and done predictions on top of it ("scored the model"), you need to understand and interpret the prediction result.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="00b0e-106">Azure Machine Learning 中有四個主要的機器學習類型：</span><span class="sxs-lookup"><span data-stu-id="00b0e-106">There are four major kinds of machine learning models in Azure Machine Learning:</span></span>

* <span data-ttu-id="00b0e-107">分類</span><span class="sxs-lookup"><span data-stu-id="00b0e-107">Classification</span></span>
* <span data-ttu-id="00b0e-108">叢集</span><span class="sxs-lookup"><span data-stu-id="00b0e-108">Clustering</span></span>
* <span data-ttu-id="00b0e-109">迴歸</span><span class="sxs-lookup"><span data-stu-id="00b0e-109">Regression</span></span>
* <span data-ttu-id="00b0e-110">推薦系統</span><span class="sxs-lookup"><span data-stu-id="00b0e-110">Recommender systems</span></span>

<span data-ttu-id="00b0e-111">用來預測這些模型的模組如下︰</span><span class="sxs-lookup"><span data-stu-id="00b0e-111">The modules used for prediction on top of these models are:</span></span>

* <span data-ttu-id="00b0e-112">[評分模型][score-model]模組，用於分類和迴歸</span><span class="sxs-lookup"><span data-stu-id="00b0e-112">[Score Model][score-model] module for classification and regression</span></span>
* <span data-ttu-id="00b0e-113">[指派至叢集][assign-to-clusters]模組，用於加入叢集</span><span class="sxs-lookup"><span data-stu-id="00b0e-113">[Assign to Clusters][assign-to-clusters] module for clustering</span></span>
* <span data-ttu-id="00b0e-114">[評分 Matchbox 推薦][score-matchbox-recommender]，用於推薦系統</span><span class="sxs-lookup"><span data-stu-id="00b0e-114">[Score Matchbox Recommender][score-matchbox-recommender] for recommendation systems</span></span>

<span data-ttu-id="00b0e-115">本文件說明如何針對每個模組解譯預測結果。</span><span class="sxs-lookup"><span data-stu-id="00b0e-115">This document explains how to interpret prediction results for each of these modules.</span></span> <span data-ttu-id="00b0e-116">如需這些模組的概觀，請參閱[如何選擇參數來最佳化 Azure Machine Learning 中的演算法](machine-learning-algorithm-parameters-optimize.md)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-116">For an overview of these modules, see [How to choose parameters to optimize your algorithms in Azure Machine Learning](machine-learning-algorithm-parameters-optimize.md).</span></span>

<span data-ttu-id="00b0e-117">本主題說明預測解譯，但是未說明模型評估。</span><span class="sxs-lookup"><span data-stu-id="00b0e-117">This topic addresses prediction interpretation but not model evaluation.</span></span> <span data-ttu-id="00b0e-118">如需如何評估模型的詳細資訊，請參閱[如何在 Azure Machine Learning 中評估模型效能](machine-learning-evaluate-model-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-118">For more information about how to evaluate your model, see [How to evaluate model performance in Azure Machine Learning](machine-learning-evaluate-model-performance.md).</span></span>

<span data-ttu-id="00b0e-119">如果您是 Azure Machine Learning 的新手，並且需要建立簡單實驗以開始使用的說明，請參閱[在 Azure Machine Learning Studio 中建立簡單實驗](machine-learning-create-experiment.md)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-119">If you are new to Azure Machine Learning and need help creating a simple experiment to get started, see [Create a simple experiment in Azure Machine Learning Studio](machine-learning-create-experiment.md) in Azure Machine Learning Studio.</span></span>

## <a name="classification"></a><span data-ttu-id="00b0e-120">分類</span><span class="sxs-lookup"><span data-stu-id="00b0e-120">Classification</span></span>
<span data-ttu-id="00b0e-121">分類問題方面有兩個子類別：</span><span class="sxs-lookup"><span data-stu-id="00b0e-121">There are two subcategories of classification problems:</span></span>

* <span data-ttu-id="00b0e-122">只有兩個分類的問題 (雙類別或二進位分類)</span><span class="sxs-lookup"><span data-stu-id="00b0e-122">Problems with only two classes (two-class or binary classification)</span></span>
* <span data-ttu-id="00b0e-123">兩個以上分類的問題 (多類別分類)</span><span class="sxs-lookup"><span data-stu-id="00b0e-123">Problems with more than two classes (multi-class classification)</span></span>

<span data-ttu-id="00b0e-124">Azure Machine Learning 有不同的模組可以處理各種類型的分類，但解譯其預設結果的方法相似。</span><span class="sxs-lookup"><span data-stu-id="00b0e-124">Azure Machine Learning has different modules to deal with each of these types of classification, but the methods for interpreting their prediction results are similar.</span></span>

### <a name="two-class-classification"></a><span data-ttu-id="00b0e-125">雙類別分類</span><span class="sxs-lookup"><span data-stu-id="00b0e-125">Two-class classification</span></span>
<span data-ttu-id="00b0e-126">**範例實驗**</span><span class="sxs-lookup"><span data-stu-id="00b0e-126">**Example experiment**</span></span>

<span data-ttu-id="00b0e-127">雙類別分類問題的範例是鳶尾花的分類。</span><span class="sxs-lookup"><span data-stu-id="00b0e-127">An example of a two-class classification problem is the classification of iris flowers.</span></span> <span data-ttu-id="00b0e-128">作法是根據特徵來分類鳶尾花。</span><span class="sxs-lookup"><span data-stu-id="00b0e-128">The task is to classify iris flowers based on their features.</span></span> <span data-ttu-id="00b0e-129">Azure Machine Learning 中提供的鳶尾花資料集是熱門[鳶尾花資料集](http://en.wikipedia.org/wiki/Iris_flower_data_set)的子集，僅包含兩個花卉物種 (類別 0 和 1) 的執行個體。</span><span class="sxs-lookup"><span data-stu-id="00b0e-129">The Iris data set provided in Azure Machine Learning is a subset of the popular [Iris data set](http://en.wikipedia.org/wiki/Iris_flower_data_set) containing instances of only two flower species (classes 0 and 1).</span></span> <span data-ttu-id="00b0e-130">每個花卉有四個特徵 (萼片長度、萼片寬度、花瓣長度及花瓣寬度)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-130">There are four features for each flower (sepal length, sepal width, petal length, and petal width).</span></span>

![鳶尾花實驗的螢幕擷取畫面](./media/machine-learning-interpret-model-results/1.png)

<span data-ttu-id="00b0e-132">圖 1.</span><span class="sxs-lookup"><span data-stu-id="00b0e-132">Figure 1.</span></span> <span data-ttu-id="00b0e-133">鳶尾花雙類別分類問題實驗</span><span class="sxs-lookup"><span data-stu-id="00b0e-133">Iris two-class classification problem experiment</span></span>

<span data-ttu-id="00b0e-134">已執行實驗以解決此問題，如「圖 1」所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-134">An experiment has been performed to solve this problem, as shown in Figure 1.</span></span> <span data-ttu-id="00b0e-135">已訓練及評分雙類別促進式決策樹模型。</span><span class="sxs-lookup"><span data-stu-id="00b0e-135">A two-class boosted decision tree model has been trained and scored.</span></span> <span data-ttu-id="00b0e-136">您現在可以從[評分模型][score-model]模組將預測結果視覺化，方法是按一下[評分模型][score-model]模組的輸出連接埠，然後按一下 [視覺化]。</span><span class="sxs-lookup"><span data-stu-id="00b0e-136">Now you can visualize the prediction results from the [Score Model][score-model] module by clicking the output port of the [Score Model][score-model] module and then clicking **Visualize**.</span></span>

![評分模型模組](./media/machine-learning-interpret-model-results/1_1.png)

<span data-ttu-id="00b0e-138">這樣會帶出評分結果，如圖 2 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-138">This brings up the scoring results as shown in Figure 2.</span></span>

![鳶尾花雙類別分類實驗的結果](./media/machine-learning-interpret-model-results/2.png)

<span data-ttu-id="00b0e-140">圖 2.</span><span class="sxs-lookup"><span data-stu-id="00b0e-140">Figure 2.</span></span> <span data-ttu-id="00b0e-141">視覺化雙類別分類中的評分模型結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-141">Visualize a score model result in two-class classification</span></span>

<span data-ttu-id="00b0e-142">**結果解譯**</span><span class="sxs-lookup"><span data-stu-id="00b0e-142">**Result interpretation**</span></span>

<span data-ttu-id="00b0e-143">結果資料表中有六個資料行。</span><span class="sxs-lookup"><span data-stu-id="00b0e-143">There are six columns in the results table.</span></span> <span data-ttu-id="00b0e-144">左側四個資料行是四個特徵。</span><span class="sxs-lookup"><span data-stu-id="00b0e-144">The left four columns are the four features.</span></span> <span data-ttu-id="00b0e-145">右側兩個資料行 (「評分標籤」和「評分機率」) 是預測結果。</span><span class="sxs-lookup"><span data-stu-id="00b0e-145">The right two columns, Scored Labels and Scored Probabilities, are the prediction results.</span></span> <span data-ttu-id="00b0e-146">「評分機率」資料行顯示花卉屬於正類別 (類別 1) 的機率。</span><span class="sxs-lookup"><span data-stu-id="00b0e-146">The Scored Probabilities column shows the probability that a flower belongs to the positive class (Class 1).</span></span> <span data-ttu-id="00b0e-147">例如，資料行中的第一個數字 (0.028571) 表示第一個花卉屬於類別 1 的機率有 0.028571。</span><span class="sxs-lookup"><span data-stu-id="00b0e-147">For example, the first number in the column (0.028571) means there is 0.028571 probability that the first flower belongs to Class 1.</span></span> <span data-ttu-id="00b0e-148">「評分標籤」資料行顯示每個花卉的預測類別。</span><span class="sxs-lookup"><span data-stu-id="00b0e-148">The Scored Labels column shows the predicted class for each flower.</span></span> <span data-ttu-id="00b0e-149">這是根據「評分機率」資料行。</span><span class="sxs-lookup"><span data-stu-id="00b0e-149">This is based on the Scored Probabilities column.</span></span> <span data-ttu-id="00b0e-150">如果花卉的評分機率大於 0.5，則會預測為類別 1。</span><span class="sxs-lookup"><span data-stu-id="00b0e-150">If the scored probability of a flower is larger than 0.5, it is predicted as Class 1.</span></span> <span data-ttu-id="00b0e-151">否則會預測為類別 0。</span><span class="sxs-lookup"><span data-stu-id="00b0e-151">Otherwise, it is predicted as Class 0.</span></span>

<span data-ttu-id="00b0e-152">**Web 服務發佈**</span><span class="sxs-lookup"><span data-stu-id="00b0e-152">**Web service publication**</span></span>

<span data-ttu-id="00b0e-153">了解預測結果並且完全評判之後，可以將實驗發佈為 Web 服務，以便您在各種應用程式中進行部署及呼叫，以取得任何新的鳶尾花的類別預測。</span><span class="sxs-lookup"><span data-stu-id="00b0e-153">After the prediction results have been understood and judged sound, the experiment can be published as a web service so that you can deploy it in various applications and call it to obtain class predictions on any new iris flower.</span></span> <span data-ttu-id="00b0e-154">若要了解如何將訓練實驗變更為評分實驗並且發佈為 Web 服務，請參閱[發佈 Azure Machine Learning Web 服務](machine-learning-walkthrough-5-publish-web-service.md)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-154">To learn how to change a training experiment into a scoring experiment and publish it as a web service, see [Publish the Azure Machine Learning web service](machine-learning-walkthrough-5-publish-web-service.md).</span></span> <span data-ttu-id="00b0e-155">此程序可提供給您如圖 3 所示的評分實驗。</span><span class="sxs-lookup"><span data-stu-id="00b0e-155">This procedure provides you with a scoring experiment as shown in Figure 3.</span></span>

![評分實驗的螢幕擷取畫面](./media/machine-learning-interpret-model-results/3.png)

<span data-ttu-id="00b0e-157">圖 3.</span><span class="sxs-lookup"><span data-stu-id="00b0e-157">Figure 3.</span></span> <span data-ttu-id="00b0e-158">鳶尾花雙類別分類問題實驗評分</span><span class="sxs-lookup"><span data-stu-id="00b0e-158">Scoring the iris two-class classification problem experiment</span></span>

<span data-ttu-id="00b0e-159">您現在必須設定 Web 服務的輸入和輸出。</span><span class="sxs-lookup"><span data-stu-id="00b0e-159">Now you need to set the input and output for the web service.</span></span> <span data-ttu-id="00b0e-160">輸入是[評分模型][score-model]的右側輸入連接埠，這是鳶尾花的特徵輸入。</span><span class="sxs-lookup"><span data-stu-id="00b0e-160">The input is the right input port of [Score Model][score-model], which is the Iris flower features input.</span></span> <span data-ttu-id="00b0e-161">輸出的選擇取決於您是對於預測類別 (評分標籤)、評分機率或兩者感到興趣。</span><span class="sxs-lookup"><span data-stu-id="00b0e-161">The choice of the output depends on whether you are interested in the predicted class (scored label), the scored probability, or both.</span></span> <span data-ttu-id="00b0e-162">此範例假設您對兩者都感到興趣。</span><span class="sxs-lookup"><span data-stu-id="00b0e-162">In this example, it is assumed that you are interested in both.</span></span> <span data-ttu-id="00b0e-163">若要選取想要的輸出資料行，請使用[選取資料集中的資料行][select-columns]模組。</span><span class="sxs-lookup"><span data-stu-id="00b0e-163">To select the desired output columns, use a [Select Columns in Data set][select-columns] module.</span></span> <span data-ttu-id="00b0e-164">依序按一下 [選取資料集中的資料行][select-columns] 和 **啟動資料行選取器**，然後選取 [評分標籤] 和 [評分機率]。</span><span class="sxs-lookup"><span data-stu-id="00b0e-164">Click [Select Columns in Data set][select-columns], click **Launch column selector**, and select **Scored Labels** and **Scored Probabilities**.</span></span> <span data-ttu-id="00b0e-165">設定 [選取資料集中的資料行][select-columns] 的輸出連接埠並再次執行之後，您應該就可以按一下 [發佈 WEB 服務]，將評分實驗發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="00b0e-165">After setting the output port of [Select Columns in Data set][select-columns] and running it again, you should be ready to publish the scoring experiment as a web service by clicking **PUBLISH WEB SERVICE**.</span></span> <span data-ttu-id="00b0e-166">最終實驗如「圖 4」所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-166">The final experiment looks like Figure 4.</span></span>

![鳶尾花雙類別分類實驗](./media/machine-learning-interpret-model-results/4.png)

<span data-ttu-id="00b0e-168">圖 4.</span><span class="sxs-lookup"><span data-stu-id="00b0e-168">Figure 4.</span></span> <span data-ttu-id="00b0e-169">鳶尾花雙類別分類問題的最終評分實驗</span><span class="sxs-lookup"><span data-stu-id="00b0e-169">Final scoring experiment of an iris two-class classification problem</span></span>

<span data-ttu-id="00b0e-170">執行 Web 服務並且輸入測試執行個體的一些特徵值之後，結果會傳回兩個數字。</span><span class="sxs-lookup"><span data-stu-id="00b0e-170">After you run the web service and enter some feature values of a test instance, the result returns two numbers.</span></span> <span data-ttu-id="00b0e-171">第一個數字是評分標籤，而第二個數字是評分機率。</span><span class="sxs-lookup"><span data-stu-id="00b0e-171">The first number is the scored label, and the second is the scored probability.</span></span> <span data-ttu-id="00b0e-172">此花卉預測為類別 1，其機率為 0.9655。</span><span class="sxs-lookup"><span data-stu-id="00b0e-172">This flower is predicted as Class 1 with 0.9655 probability.</span></span>

![測試解譯評分模型](./media/machine-learning-interpret-model-results/4_1.png)

![測試結果評分](./media/machine-learning-interpret-model-results/5.png)

<span data-ttu-id="00b0e-175">圖 5.</span><span class="sxs-lookup"><span data-stu-id="00b0e-175">Figure 5.</span></span> <span data-ttu-id="00b0e-176">鳶尾花雙類別分類的 Web 服務結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-176">Web service result of iris two-class classification</span></span>

### <a name="multi-class-classification"></a><span data-ttu-id="00b0e-177">多類別分類</span><span class="sxs-lookup"><span data-stu-id="00b0e-177">Multi-class classification</span></span>
<span data-ttu-id="00b0e-178">**範例實驗**</span><span class="sxs-lookup"><span data-stu-id="00b0e-178">**Example experiment**</span></span>

<span data-ttu-id="00b0e-179">在此實驗中，您將執行字母辨識工作，做為多元分類的範例。</span><span class="sxs-lookup"><span data-stu-id="00b0e-179">In this experiment, you perform a letter-recognition task as an example of multiclass classification.</span></span> <span data-ttu-id="00b0e-180">分類器會嘗試根據一些從手寫影像中擷取的手寫屬性值，預測特定字母 (類別)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-180">The classifier attempts to predict a certain letter (class) based on some hand-written attribute values extracted from the hand-written images.</span></span>

![字母辨識範例](./media/machine-learning-interpret-model-results/5_1.png)

<span data-ttu-id="00b0e-182">在定型資料中，有 16 個擷取自手寫字母影像的特徵。</span><span class="sxs-lookup"><span data-stu-id="00b0e-182">In the training data, there are 16 features extracted from hand-written letter images.</span></span> <span data-ttu-id="00b0e-183">26 個字母形成 26 個類別。</span><span class="sxs-lookup"><span data-stu-id="00b0e-183">The 26 letters form our 26 classes.</span></span> <span data-ttu-id="00b0e-184">圖 6 顯示的實驗將以訓練多元分類模型進行字母辨識，並在測試資料集上針對相同的特徵集進行預測。</span><span class="sxs-lookup"><span data-stu-id="00b0e-184">Figure 6 shows an experiment that will train a multiclass classification model for letter recognition and predict on the same feature set on a test data set.</span></span>

![字母辨識多類別分類實驗](./media/machine-learning-interpret-model-results/6.png)

<span data-ttu-id="00b0e-186">圖 6.</span><span class="sxs-lookup"><span data-stu-id="00b0e-186">Figure 6.</span></span> <span data-ttu-id="00b0e-187">字母辨識多類別分類問題實驗</span><span class="sxs-lookup"><span data-stu-id="00b0e-187">Letter recognition multiclass classification problem experiment</span></span>

<span data-ttu-id="00b0e-188">從[評分模型][score-model]模組將結果視覺化，方法是按一下[評分模型][score-model]模組的輸出連接埠，然後按一下 [視覺化]，您應會看見如圖 7 所示的內容。</span><span class="sxs-lookup"><span data-stu-id="00b0e-188">Visualizing the results from the [Score Model][score-model] module by clicking the output port of [Score Model][score-model] module and then clicking **Visualize**, you should see content as shown in Figure 7.</span></span>

![評分模型模組](./media/machine-learning-interpret-model-results/7.png)

<span data-ttu-id="00b0e-190">圖 7.</span><span class="sxs-lookup"><span data-stu-id="00b0e-190">Figure 7.</span></span> <span data-ttu-id="00b0e-191">視覺化多類別分類中的評分模型結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-191">Visualize score model results in a multi-class classification</span></span>

<span data-ttu-id="00b0e-192">**結果解譯**</span><span class="sxs-lookup"><span data-stu-id="00b0e-192">**Result interpretation**</span></span>

<span data-ttu-id="00b0e-193">左側 16 個資料行代表測試集的特徵值。</span><span class="sxs-lookup"><span data-stu-id="00b0e-193">The left 16 columns represent the feature values of the test set.</span></span> <span data-ttu-id="00b0e-194">類別 "XX" 之名稱為「評分機率」之類的資料行，就像是雙類別案例的「評分機率」資料行。</span><span class="sxs-lookup"><span data-stu-id="00b0e-194">The columns with names like Scored Probabilities for Class "XX" are just like the Scored Probabilities column in the two-class case.</span></span> <span data-ttu-id="00b0e-195">它們會顯示對應項目落在特定類別的機率。</span><span class="sxs-lookup"><span data-stu-id="00b0e-195">They show the probability that the corresponding entry falls into a certain class.</span></span> <span data-ttu-id="00b0e-196">例如，對於第一個項目，有 0.003571 的機率是 “A”，有 0.000451 的機率是 “B”，依此類推。</span><span class="sxs-lookup"><span data-stu-id="00b0e-196">For example, for the first entry, there is 0.003571 probability that it is an “A,” 0.000451 probability that it is a “B,” and so forth.</span></span> <span data-ttu-id="00b0e-197">最後的資料行 (評分標籤) 與雙類別案例的「評分標籤」相同。</span><span class="sxs-lookup"><span data-stu-id="00b0e-197">The last column (Scored Labels) is the same as Scored Labels in the two-class case.</span></span> <span data-ttu-id="00b0e-198">它會選取具有最大評分機率的類別做為對應項目的預測類別。</span><span class="sxs-lookup"><span data-stu-id="00b0e-198">It selects the class with the largest scored probability as the predicted class of the corresponding entry.</span></span> <span data-ttu-id="00b0e-199">例如，對於第一個項目，評分標籤為 “F”，因為它的最大機率是 “F” (0.916995)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-199">For example, for the first entry, the scored label is “F” since it has the largest probability to be an “F” (0.916995).</span></span>

<span data-ttu-id="00b0e-200">**Web 服務發佈**</span><span class="sxs-lookup"><span data-stu-id="00b0e-200">**Web service publication**</span></span>

<span data-ttu-id="00b0e-201">您也可以取得每個項目的評分標籤以及評分標籤的機率。</span><span class="sxs-lookup"><span data-stu-id="00b0e-201">You can also get the scored label for each entry and the probability of the scored label.</span></span> <span data-ttu-id="00b0e-202">基本邏輯是尋找所有評分機率當中最大的機率。</span><span class="sxs-lookup"><span data-stu-id="00b0e-202">The basic logic is to find the largest probability among all the scored probabilities.</span></span> <span data-ttu-id="00b0e-203">若要這麼做，您需要使用[執行 R 指令碼][execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="00b0e-203">To do this, you need to use the [Execute R Script][execute-r-script] module.</span></span> <span data-ttu-id="00b0e-204">R 程式碼如圖 8 所示，實驗的結果如圖 9 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-204">The R code is shown in Figure 8, and the result of the experiment is shown in Figure 9.</span></span>

![R 程式碼範例](./media/machine-learning-interpret-model-results/8.png)

<span data-ttu-id="00b0e-206">圖 8.</span><span class="sxs-lookup"><span data-stu-id="00b0e-206">Figure 8.</span></span> <span data-ttu-id="00b0e-207">R 程式碼，用以擷取評分標籤和標籤的相關聯機率</span><span class="sxs-lookup"><span data-stu-id="00b0e-207">R code for extracting Scored Labels and the associated probabilities of the labels</span></span>

![實驗結果](./media/machine-learning-interpret-model-results/9.png)

<span data-ttu-id="00b0e-209">圖 9.</span><span class="sxs-lookup"><span data-stu-id="00b0e-209">Figure 9.</span></span> <span data-ttu-id="00b0e-210">字母辨識多類別分類問題的最終評分實驗</span><span class="sxs-lookup"><span data-stu-id="00b0e-210">Final scoring experiment of the letter-recognition multiclass classification problem</span></span>

<span data-ttu-id="00b0e-211">發佈及執行 Web 服務並輸入一些輸入特徵值之後，傳回的結果如圖 10 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-211">After you publish and run the web service and enter some input feature values, the returned result looks like Figure 10.</span></span> <span data-ttu-id="00b0e-212">此手寫字母具有其擷取的 16 個特徵，預測為 “T” 的機率是 0.9715。</span><span class="sxs-lookup"><span data-stu-id="00b0e-212">This hand-written letter, with its extracted 16 features, is predicted to be a “T” with 0.9715 probability.</span></span>

![測試解譯評分模組](./media/machine-learning-interpret-model-results/9_1.png)

![測試結果](./media/machine-learning-interpret-model-results/10.png)

<span data-ttu-id="00b0e-215">圖 10.</span><span class="sxs-lookup"><span data-stu-id="00b0e-215">Figure 10.</span></span> <span data-ttu-id="00b0e-216">多類別分類的 Web 服務結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-216">Web service result of multiclass classification</span></span>

## <a name="regression"></a><span data-ttu-id="00b0e-217">迴歸</span><span class="sxs-lookup"><span data-stu-id="00b0e-217">Regression</span></span>
<span data-ttu-id="00b0e-218">迴歸問題與分類問題不同。</span><span class="sxs-lookup"><span data-stu-id="00b0e-218">Regression problems are different from classification problems.</span></span> <span data-ttu-id="00b0e-219">在分類問題中，您會嘗試預測離散案例，例如鳶尾花屬於哪個類別。</span><span class="sxs-lookup"><span data-stu-id="00b0e-219">In a classification problem, you're trying to predict discrete classes, such as which class an iris flower belongs to.</span></span> <span data-ttu-id="00b0e-220">但如以下迴歸問題範例所示，您會嘗試預測連續變數，例如汽車的價格。</span><span class="sxs-lookup"><span data-stu-id="00b0e-220">But as you can see in the following example of a regression problem, you're trying to predict a continuous variable, such as the price of a car.</span></span>

<span data-ttu-id="00b0e-221">**範例實驗**</span><span class="sxs-lookup"><span data-stu-id="00b0e-221">**Example experiment**</span></span>

<span data-ttu-id="00b0e-222">使用汽車價格預測做為您的迴歸範例。</span><span class="sxs-lookup"><span data-stu-id="00b0e-222">Use automobile price prediction as your example for regression.</span></span> <span data-ttu-id="00b0e-223">您會嘗試根據汽車的特徵預測其價格，例如製造、燃料類型、車體類型和驅動輪。</span><span class="sxs-lookup"><span data-stu-id="00b0e-223">You are trying to predict the price of a car based on its features, including make, fuel type, body type, and drive wheel.</span></span> <span data-ttu-id="00b0e-224">實驗如「圖 11」所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-224">The experiment is shown in Figure 11.</span></span>

![汽車價格迴歸實驗](./media/machine-learning-interpret-model-results/11.png)

<span data-ttu-id="00b0e-226">圖 11.</span><span class="sxs-lookup"><span data-stu-id="00b0e-226">Figure 11.</span></span> <span data-ttu-id="00b0e-227">汽車價格迴歸問題實驗</span><span class="sxs-lookup"><span data-stu-id="00b0e-227">Automobile price regression problem experiment</span></span>

<span data-ttu-id="00b0e-228">視覺化[評分模型][score-model]模組，結果如圖 12 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-228">Visualizing the [Score Model][score-model] module, the result looks like Figure 12.</span></span>

![汽車價格預測問題的評分結果](./media/machine-learning-interpret-model-results/12.png)

<span data-ttu-id="00b0e-230">圖 12.</span><span class="sxs-lookup"><span data-stu-id="00b0e-230">Figure 12.</span></span> <span data-ttu-id="00b0e-231">汽車價格預測問題的評分結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-231">Scoring result for the automobile price prediction problem</span></span>

<span data-ttu-id="00b0e-232">**結果解譯**</span><span class="sxs-lookup"><span data-stu-id="00b0e-232">**Result interpretation**</span></span>

<span data-ttu-id="00b0e-233">「評分標籤」是此評分結果中的結果資料行。</span><span class="sxs-lookup"><span data-stu-id="00b0e-233">Scored Labels is the result column in this scoring result.</span></span> <span data-ttu-id="00b0e-234">數字是每部汽車的預測價格。</span><span class="sxs-lookup"><span data-stu-id="00b0e-234">The numbers are the predicted price for each car.</span></span>

<span data-ttu-id="00b0e-235">**Web 服務發佈**</span><span class="sxs-lookup"><span data-stu-id="00b0e-235">**Web service publication**</span></span>

<span data-ttu-id="00b0e-236">您可以將迴歸實驗發佈至 Web 服務，並且針對汽車價格預測呼叫，方式與雙類別分類使用案例中的方式相同。</span><span class="sxs-lookup"><span data-stu-id="00b0e-236">You can publish the regression experiment into a web service and call it for automobile price prediction in the same way as in the two-class classification use case.</span></span>

![汽車價格迴歸問題的評分實驗](./media/machine-learning-interpret-model-results/13.png)

<span data-ttu-id="00b0e-238">圖 13.</span><span class="sxs-lookup"><span data-stu-id="00b0e-238">Figure 13.</span></span> <span data-ttu-id="00b0e-239">汽車價格迴歸問題的評分實驗</span><span class="sxs-lookup"><span data-stu-id="00b0e-239">Scoring experiment of an automobile price regression problem</span></span>

<span data-ttu-id="00b0e-240">執行 Web 服務，傳回的結果如「圖 14」所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-240">Running the web service, the returned result looks like Figure 14.</span></span> <span data-ttu-id="00b0e-241">此汽車的預測價格為 $15,085.52。</span><span class="sxs-lookup"><span data-stu-id="00b0e-241">The predicted price for this car is $15,085.52.</span></span>

![測試解譯評分模組](./media/machine-learning-interpret-model-results/13_1.png)

![評分模組結果](./media/machine-learning-interpret-model-results/14.png)

<span data-ttu-id="00b0e-244">圖 14.</span><span class="sxs-lookup"><span data-stu-id="00b0e-244">Figure 14.</span></span> <span data-ttu-id="00b0e-245">汽車價格迴歸問題的 Web 服務結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-245">Web service result of an automobile price regression problem</span></span>

## <a name="clustering"></a><span data-ttu-id="00b0e-246">叢集</span><span class="sxs-lookup"><span data-stu-id="00b0e-246">Clustering</span></span>
<span data-ttu-id="00b0e-247">**範例實驗**</span><span class="sxs-lookup"><span data-stu-id="00b0e-247">**Example experiment**</span></span>

<span data-ttu-id="00b0e-248">讓我們再次使用鳶尾花資料集來建立叢集實驗。</span><span class="sxs-lookup"><span data-stu-id="00b0e-248">Let’s use the Iris data set again to build a clustering experiment.</span></span> <span data-ttu-id="00b0e-249">您可以在這裡篩選資料集中的類別標籤，使其僅具有特徵並可用於叢集。</span><span class="sxs-lookup"><span data-stu-id="00b0e-249">Here you can filter out the class labels in the data set so that it only has features and can be used for clustering.</span></span> <span data-ttu-id="00b0e-250">在此鳶尾花使用案例中，將訓練處理期間的叢集數指定為 2，表示您想要將花卉叢集為兩個類別。</span><span class="sxs-lookup"><span data-stu-id="00b0e-250">In this iris use case, specify the number of clusters to be two during the training process, which means you would cluster the flowers into two classes.</span></span> <span data-ttu-id="00b0e-251">實驗如「圖 15」所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-251">The experiment is shown in Figure 15.</span></span>

![鳶尾花叢集問題實驗](./media/machine-learning-interpret-model-results/15.png)

<span data-ttu-id="00b0e-253">圖 15.</span><span class="sxs-lookup"><span data-stu-id="00b0e-253">Figure 15.</span></span> <span data-ttu-id="00b0e-254">鳶尾花叢集問題實驗</span><span class="sxs-lookup"><span data-stu-id="00b0e-254">Iris clustering problem experiment</span></span>

<span data-ttu-id="00b0e-255">叢集與分類的不同之處在於訓練資料集本身沒有實況標籤。</span><span class="sxs-lookup"><span data-stu-id="00b0e-255">Clustering differs from classification in that the training data set doesn’t have ground-truth labels by itself.</span></span> <span data-ttu-id="00b0e-256">將訓練資料集執行個體群組至不同的叢集。</span><span class="sxs-lookup"><span data-stu-id="00b0e-256">Clustering groups the training data set instances into distinct clusters.</span></span> <span data-ttu-id="00b0e-257">在訓練處理期間，模型會為項目加上標籤，方法是學習其特徵之間的差異。</span><span class="sxs-lookup"><span data-stu-id="00b0e-257">During the training process, the model labels the entries by learning the differences between their features.</span></span> <span data-ttu-id="00b0e-258">之後，定型模型可進一步用來分類未來的項目。</span><span class="sxs-lookup"><span data-stu-id="00b0e-258">After that, the trained model can be used to further classify future entries.</span></span> <span data-ttu-id="00b0e-259">在叢集問題當中，我們感興趣的結果有兩個部分。</span><span class="sxs-lookup"><span data-stu-id="00b0e-259">There are two parts of the result we are interested in within a clustering problem.</span></span> <span data-ttu-id="00b0e-260">第一個部分是為訓練資料集加上標籤，而第二個部分是使用定型模型來分類新的資料集。</span><span class="sxs-lookup"><span data-stu-id="00b0e-260">The first part is labeling the training data set, and the second is classifying a new data set with the trained model.</span></span>

<span data-ttu-id="00b0e-261">您可以按一下[訓練叢集模型][train-clustering-model]的左側輸出連接埠，然後按一下 [視覺化]，將結果的第一個部分視覺化。</span><span class="sxs-lookup"><span data-stu-id="00b0e-261">The first part of the result can be visualized by clicking the left output port of [Train Clustering Model][train-clustering-model] and then clicking **Visualize**.</span></span> <span data-ttu-id="00b0e-262">視覺化如圖 16 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-262">The visualization is shown in Figure 16.</span></span>

![叢集結果](./media/machine-learning-interpret-model-results/16.png)

<span data-ttu-id="00b0e-264">圖 16.</span><span class="sxs-lookup"><span data-stu-id="00b0e-264">Figure 16.</span></span> <span data-ttu-id="00b0e-265">視覺化訓練資料集的叢集結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-265">Visualize clustering result for the training data set</span></span>

<span data-ttu-id="00b0e-266">結果的第二個部分，使用已訓練的叢集模型叢集新的項目，如「圖 17」所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-266">The result of the second part, clustering new entries with the trained clustering model, is shown in Figure 17.</span></span>

![視覺化叢集結果](./media/machine-learning-interpret-model-results/17.png)

<span data-ttu-id="00b0e-268">圖 17.</span><span class="sxs-lookup"><span data-stu-id="00b0e-268">Figure 17.</span></span> <span data-ttu-id="00b0e-269">視覺化新資料集的叢集結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-269">Visualize clustering result on a new data set</span></span>

<span data-ttu-id="00b0e-270">**結果解譯**</span><span class="sxs-lookup"><span data-stu-id="00b0e-270">**Result interpretation**</span></span>

<span data-ttu-id="00b0e-271">雖然兩個部分的結果出自於不同的實驗階段，但是其外觀相同，並且是以相同的方式進行解譯。</span><span class="sxs-lookup"><span data-stu-id="00b0e-271">Although the results of the two parts stem from different experiment stages, they look the same and are interpreted in the same way.</span></span> <span data-ttu-id="00b0e-272">前面四個資料行是特徵。</span><span class="sxs-lookup"><span data-stu-id="00b0e-272">The first four columns are features.</span></span> <span data-ttu-id="00b0e-273">最後一個資料行 (指派) 是預測結果。</span><span class="sxs-lookup"><span data-stu-id="00b0e-273">The last column, Assignments, is the prediction result.</span></span> <span data-ttu-id="00b0e-274">已指派相同數字的項目預測為在相同叢集中，也就是說，它們某種程度上有相似之處 (此實驗使用預設的歐幾里德距離度量)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-274">The entries assigned the same number are predicted to be in the same cluster, that is, they share similarities in some way (this experiment uses the default Euclidean distance metric).</span></span> <span data-ttu-id="00b0e-275">因為您將叢集數目指定為 2，則 [指派] 中的項目會標示為 0 或 1。</span><span class="sxs-lookup"><span data-stu-id="00b0e-275">Because you specified the number of clusters to be 2, the entries in Assignments are labeled either 0 or 1.</span></span>

<span data-ttu-id="00b0e-276">**Web 服務發佈**</span><span class="sxs-lookup"><span data-stu-id="00b0e-276">**Web service publication**</span></span>

<span data-ttu-id="00b0e-277">您可以將叢集實驗發佈至 Web 服務，並且針對叢集預測呼叫，方式與雙類別分類使用案例中的方式相同。</span><span class="sxs-lookup"><span data-stu-id="00b0e-277">You can publish the clustering experiment into a web service and call it for clustering predictions the same way as in the two-class classification use case.</span></span>

![鳶尾花叢集問題的評分實驗](./media/machine-learning-interpret-model-results/18.png)

<span data-ttu-id="00b0e-279">圖 18.</span><span class="sxs-lookup"><span data-stu-id="00b0e-279">Figure 18.</span></span> <span data-ttu-id="00b0e-280">鳶尾花叢集問題的評分實驗</span><span class="sxs-lookup"><span data-stu-id="00b0e-280">Scoring experiment of an iris clustering problem</span></span>

<span data-ttu-id="00b0e-281">執行 Web 服務之後，傳回的結果如圖 19 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-281">After you run the web service, the returned result looks like Figure 19.</span></span> <span data-ttu-id="00b0e-282">此花卉預測為在叢集 0 中。</span><span class="sxs-lookup"><span data-stu-id="00b0e-282">This flower is predicted to be in cluster 0.</span></span>

![測試解譯評分模組](./media/machine-learning-interpret-model-results/18_1.png)

![評分模組結果](./media/machine-learning-interpret-model-results/19.png)

<span data-ttu-id="00b0e-285">圖 19.</span><span class="sxs-lookup"><span data-stu-id="00b0e-285">Figure 19.</span></span> <span data-ttu-id="00b0e-286">鳶尾花雙類別分類的 Web 服務結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-286">Web service result of iris two-class classification</span></span>

## <a name="recommender-system"></a><span data-ttu-id="00b0e-287">推薦系統</span><span class="sxs-lookup"><span data-stu-id="00b0e-287">Recommender system</span></span>
<span data-ttu-id="00b0e-288">**範例實驗**</span><span class="sxs-lookup"><span data-stu-id="00b0e-288">**Example experiment**</span></span>

<span data-ttu-id="00b0e-289">對於推薦系統，您可以使用餐廳推薦問題做為範例：您可以根據餐廳的評等歷史為客戶推薦餐廳。</span><span class="sxs-lookup"><span data-stu-id="00b0e-289">For recommender systems, you can use the restaurant recommendation problem as an example: you can recommend restaurants for customers based on their rating history.</span></span> <span data-ttu-id="00b0e-290">輸入資料是由三個部分組成：</span><span class="sxs-lookup"><span data-stu-id="00b0e-290">The input data consists of three parts:</span></span>

* <span data-ttu-id="00b0e-291">來自客戶的餐廳評等</span><span class="sxs-lookup"><span data-stu-id="00b0e-291">Restaurant ratings from customers</span></span>
* <span data-ttu-id="00b0e-292">客戶特色資料</span><span class="sxs-lookup"><span data-stu-id="00b0e-292">Customer feature data</span></span>
* <span data-ttu-id="00b0e-293">餐廳特色資料</span><span class="sxs-lookup"><span data-stu-id="00b0e-293">Restaurant feature data</span></span>

<span data-ttu-id="00b0e-294">我們可以使用 Azure Machine Learning 的[訓練 Matchbox 推薦][train-matchbox-recommender]模組做許多事情：</span><span class="sxs-lookup"><span data-stu-id="00b0e-294">There are several things we can do with the [Train Matchbox Recommender][train-matchbox-recommender] module in Azure Machine Learning:</span></span>

* <span data-ttu-id="00b0e-295">為指定使用者和項目預測評等</span><span class="sxs-lookup"><span data-stu-id="00b0e-295">Predict ratings for a given user and item</span></span>
* <span data-ttu-id="00b0e-296">對指定使用者推薦項目</span><span class="sxs-lookup"><span data-stu-id="00b0e-296">Recommend items to a given user</span></span>
* <span data-ttu-id="00b0e-297">尋找指定使用者相關的使用者</span><span class="sxs-lookup"><span data-stu-id="00b0e-297">Find users related to a given user</span></span>
* <span data-ttu-id="00b0e-298">尋找指定項目相關的項目</span><span class="sxs-lookup"><span data-stu-id="00b0e-298">Find items related to a given item</span></span>

<span data-ttu-id="00b0e-299">您可以選擇想要執行的動作，方法是從 [推薦預測種類] 功能表中的四個選項進行選取。</span><span class="sxs-lookup"><span data-stu-id="00b0e-299">You can choose what you want to do by selecting from the four options in the **Recommender prediction kind** menu.</span></span> <span data-ttu-id="00b0e-300">您可以在這裡逐步完成這四個案例。</span><span class="sxs-lookup"><span data-stu-id="00b0e-300">Here you can walk through all four scenarios.</span></span>

![Matchbox 推薦](./media/machine-learning-interpret-model-results/19_1.png)

<span data-ttu-id="00b0e-302">典型的推薦系統 Azure Machine Learning 實驗如圖 20 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-302">A typical Azure Machine Learning experiment for a recommender system looks like Figure 20.</span></span> <span data-ttu-id="00b0e-303">如需如何使用這些推薦系統模組的詳細資訊，請參閱[訓練 Matchbox 推薦][train-matchbox-recommender]和[評分 Matchbox 推薦][score-matchbox-recommender]。</span><span class="sxs-lookup"><span data-stu-id="00b0e-303">For information about how to use those recommender system modules, see [Train matchbox recommender][train-matchbox-recommender] and [Score matchbox recommender][score-matchbox-recommender].</span></span>

![推薦系統實驗](./media/machine-learning-interpret-model-results/20.png)

<span data-ttu-id="00b0e-305">圖 20.</span><span class="sxs-lookup"><span data-stu-id="00b0e-305">Figure 20.</span></span> <span data-ttu-id="00b0e-306">推薦系統實驗</span><span class="sxs-lookup"><span data-stu-id="00b0e-306">Recommender system experiment</span></span>

<span data-ttu-id="00b0e-307">**結果解譯**</span><span class="sxs-lookup"><span data-stu-id="00b0e-307">**Result interpretation**</span></span>

<span data-ttu-id="00b0e-308">**為指定使用者和項目預測評等**</span><span class="sxs-lookup"><span data-stu-id="00b0e-308">**Predict ratings for a given user and item**</span></span>

<span data-ttu-id="00b0e-309">藉由選取 [推薦預測種類] 之下的 [評等預測]，您會要求推薦系統預測指定使用者和項目的評等。</span><span class="sxs-lookup"><span data-stu-id="00b0e-309">By selecting **Rating Prediction** under **Recommender prediction kind**, you are asking the recommender system to predict the rating for a given user and item.</span></span> <span data-ttu-id="00b0e-310">[評分 Matchbox 推薦][score-matchbox-recommender]輸出的視覺化如圖 21 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-310">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 21.</span></span>

![推薦系統的評分結果 - 評等預測](./media/machine-learning-interpret-model-results/21.png)

<span data-ttu-id="00b0e-312">圖 21.</span><span class="sxs-lookup"><span data-stu-id="00b0e-312">Figure 21.</span></span> <span data-ttu-id="00b0e-313">視覺化推薦系統的評分結果 - 評等預測</span><span class="sxs-lookup"><span data-stu-id="00b0e-313">Visualize the score result of the recommender system--rating prediction</span></span>

<span data-ttu-id="00b0e-314">前兩個資料行是輸入資料提供的使用者-項目組。</span><span class="sxs-lookup"><span data-stu-id="00b0e-314">The first two columns are the user-item pairs provided by the input data.</span></span> <span data-ttu-id="00b0e-315">第三個資料行是對於特定項目之使用者的預測評等。</span><span class="sxs-lookup"><span data-stu-id="00b0e-315">The third column is the predicted rating of a user for a certain item.</span></span> <span data-ttu-id="00b0e-316">例如，在第一個資料列中，預測客戶 U1048 將餐廳 135026 評等為 2。</span><span class="sxs-lookup"><span data-stu-id="00b0e-316">For example, in the first row, customer U1048 is predicted to rate restaurant 135026 as 2.</span></span>

<span data-ttu-id="00b0e-317">**對指定使用者推薦項目**</span><span class="sxs-lookup"><span data-stu-id="00b0e-317">**Recommend items to a given user**</span></span>

<span data-ttu-id="00b0e-318">藉由選取 [推薦預測種類] 之下的 [項目推薦]，您會要求推薦系統對指定使用者推薦項目。</span><span class="sxs-lookup"><span data-stu-id="00b0e-318">By selecting **Item Recommendation** under **Recommender prediction kind**, you're asking the recommender system to recommend items to a given user.</span></span> <span data-ttu-id="00b0e-319">此案例中需要選擇的最後一個參數是「推薦項目選取」。</span><span class="sxs-lookup"><span data-stu-id="00b0e-319">The last parameter to choose in this scenario is *Recommended item selection*.</span></span> <span data-ttu-id="00b0e-320">選項 [ **從評等項目 (針對模型評估)** ] 主要適用於訓練處理期間的模型評估。</span><span class="sxs-lookup"><span data-stu-id="00b0e-320">The option **From Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span></span> <span data-ttu-id="00b0e-321">對於此預測階段，我們選擇 [從所有項目] 。</span><span class="sxs-lookup"><span data-stu-id="00b0e-321">For this prediction stage, we choose **From All Items**.</span></span> <span data-ttu-id="00b0e-322">[評分 Matchbox 推薦][score-matchbox-recommender]輸出的視覺化如圖 22 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-322">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 22.</span></span>

![推薦系統的評分結果 - 項目推薦](./media/machine-learning-interpret-model-results/22.png)

<span data-ttu-id="00b0e-324">圖 22.</span><span class="sxs-lookup"><span data-stu-id="00b0e-324">Figure 22.</span></span> <span data-ttu-id="00b0e-325">視覺化推薦系統的評分結果 - 項目推薦</span><span class="sxs-lookup"><span data-stu-id="00b0e-325">Visualize score result of the recommender system--item recommendation</span></span>

<span data-ttu-id="00b0e-326">六個資料行中的第一個資料行代表用於推薦項目的指定使用者識別碼，由輸入資料提供。</span><span class="sxs-lookup"><span data-stu-id="00b0e-326">The first of the six columns represents the given user IDs to recommend items for, as provided by the input data.</span></span> <span data-ttu-id="00b0e-327">其他五個資料行代表對使用者推薦的項目 (以相關性的遞減順序排序)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-327">The other five columns represent the items recommended to the user in descending order of relevance.</span></span> <span data-ttu-id="00b0e-328">例如，在第一個資料列中，對客戶 U1048 最推薦的餐廳是 134986，接下來是 135018、134975、135021 及 132862。</span><span class="sxs-lookup"><span data-stu-id="00b0e-328">For example, in the first row, the most recommended restaurant for customer U1048 is 134986, followed by 135018, 134975, 135021, and 132862.</span></span>

<span data-ttu-id="00b0e-329">**尋找指定使用者相關的使用者**</span><span class="sxs-lookup"><span data-stu-id="00b0e-329">**Find users related to a given user**</span></span>

<span data-ttu-id="00b0e-330">藉由選取 [推薦預測種類] 之下的 [相關使用者]，您會要求推薦系統尋找指定使用者的相關使用者。</span><span class="sxs-lookup"><span data-stu-id="00b0e-330">By selecting **Related Users** under **Recommender prediction kind**, you're asking the recommender system to find related users to a given user.</span></span> <span data-ttu-id="00b0e-331">相關使用者是具有類似偏好的使用者。</span><span class="sxs-lookup"><span data-stu-id="00b0e-331">Related users are the users who have similar preferences.</span></span> <span data-ttu-id="00b0e-332">此案例中需要選擇的最後一個參數是「相關使用者選取」。</span><span class="sxs-lookup"><span data-stu-id="00b0e-332">The last parameter to choose in this scenario is *Related user selection*.</span></span> <span data-ttu-id="00b0e-333">[從評等項目的使用者 (針對模型評估)] 選項主要適用於訓練處理期間的模型評估。</span><span class="sxs-lookup"><span data-stu-id="00b0e-333">The option **From Users That Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span></span> <span data-ttu-id="00b0e-334">對於此預測階段選擇 [從所有使用者]。</span><span class="sxs-lookup"><span data-stu-id="00b0e-334">Choose **From All Users** for this prediction stage.</span></span> <span data-ttu-id="00b0e-335">[評分 Matchbox 推薦][score-matchbox-recommender]輸出的視覺化如圖 23 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-335">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 23.</span></span>

![推薦系統的評分結果 - 相關使用者](./media/machine-learning-interpret-model-results/23.png)

<span data-ttu-id="00b0e-337">圖 23.</span><span class="sxs-lookup"><span data-stu-id="00b0e-337">Figure 23.</span></span> <span data-ttu-id="00b0e-338">視覺化推薦系統的評分結果 - 相關使用者</span><span class="sxs-lookup"><span data-stu-id="00b0e-338">Visualize score results of the recommender system--related users</span></span>

<span data-ttu-id="00b0e-339">六個資料行中的第一個資料行顯示尋找相關使用者所需的指定使用者識別碼，由輸入資料提供。</span><span class="sxs-lookup"><span data-stu-id="00b0e-339">The first of the six columns shows the given user IDs needed to find related users, as provided by input data.</span></span> <span data-ttu-id="00b0e-340">其他五個資料行會儲存使用者的預測相關使用者 (以相關性的遞減順序排序)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-340">The other five columns store the predicted related users of the user in descending order of relevance.</span></span> <span data-ttu-id="00b0e-341">例如，在第一個資料列中，對於客戶 U1048 最相關的客戶是 U1051，接下來是 U1066、U1044、U1017 及 U1072。</span><span class="sxs-lookup"><span data-stu-id="00b0e-341">For example, in the first row, the most relevant customer for customer U1048 is U1051, followed by U1066, U1044, U1017, and U1072.</span></span>

<span data-ttu-id="00b0e-342">**尋找指定項目相關的項目**</span><span class="sxs-lookup"><span data-stu-id="00b0e-342">**Find items related to a given item**</span></span>

<span data-ttu-id="00b0e-343">藉由選取 [推薦預測種類] 之下的 [相關項目]，您會要求推薦系統尋找指定項目的相關項目。</span><span class="sxs-lookup"><span data-stu-id="00b0e-343">By selecting **Related Items** under **Recommender prediction kind**, you are asking the recommender system to find related items to a given item.</span></span> <span data-ttu-id="00b0e-344">相關項目是相同使用者最有可能喜歡的項目。</span><span class="sxs-lookup"><span data-stu-id="00b0e-344">Related items are the items most likely to be liked by the same user.</span></span> <span data-ttu-id="00b0e-345">此案例中需要選擇的最後一個參數是「相關項目選取」。</span><span class="sxs-lookup"><span data-stu-id="00b0e-345">The last parameter to choose in this scenario is *Related item selection*.</span></span> <span data-ttu-id="00b0e-346">選項 [ **從評等項目 (針對模型評估)** ] 主要適用於訓練處理期間的模型評估。</span><span class="sxs-lookup"><span data-stu-id="00b0e-346">The option **From Rated Items (for model evaluation)** is primarily for model evaluation during the training process.</span></span> <span data-ttu-id="00b0e-347">對於此預測階段，我們選擇 [ **從所有項目** ]。</span><span class="sxs-lookup"><span data-stu-id="00b0e-347">We choose **From All Items** for this prediction stage.</span></span> <span data-ttu-id="00b0e-348">[評分 Matchbox 推薦][score-matchbox-recommender]輸出的視覺化如圖 24 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-348">The visualization of the [Score Matchbox Recommender][score-matchbox-recommender] output looks like Figure 24.</span></span>

![推薦系統的評分結果 - 相關項目](./media/machine-learning-interpret-model-results/24.png)

<span data-ttu-id="00b0e-350">圖 24.</span><span class="sxs-lookup"><span data-stu-id="00b0e-350">Figure 24.</span></span> <span data-ttu-id="00b0e-351">視覺化推薦系統的評分結果 - 相關項目</span><span class="sxs-lookup"><span data-stu-id="00b0e-351">Visualize score results of the recommender system--related items</span></span>

<span data-ttu-id="00b0e-352">六個資料行中的第一個資料行代表尋找相關項目所需的指定項目識別碼，由輸入資料提供。</span><span class="sxs-lookup"><span data-stu-id="00b0e-352">The first of the six columns represents the given item IDs needed to find related items, as provided by the input data.</span></span> <span data-ttu-id="00b0e-353">其他五個資料行會儲存項目的預測相關項目 (以相關性的遞減順序排序)。</span><span class="sxs-lookup"><span data-stu-id="00b0e-353">The other five columns store the predicted related items of the item in descending order in terms of relevance.</span></span> <span data-ttu-id="00b0e-354">例如，在第一個資料列中，對項目 135026 最相關的項目是 135074，接下來是 135035、132875、135055 及 134992。</span><span class="sxs-lookup"><span data-stu-id="00b0e-354">For example, in the first row, the most relevant item for item 135026 is 135074, followed by 135035, 132875, 135055, and 134992.</span></span>

<span data-ttu-id="00b0e-355">**Web 服務發佈**</span><span class="sxs-lookup"><span data-stu-id="00b0e-355">**Web service publication**</span></span>

<span data-ttu-id="00b0e-356">將這些實驗發佈為 Web 服務以取得預測的處理類似於四個案例。</span><span class="sxs-lookup"><span data-stu-id="00b0e-356">The process of publishing these experiments as web services to get predictions is similar for each of the four scenarios.</span></span> <span data-ttu-id="00b0e-357">我們在這裡採用第二個案例 (對指定的使用者推薦項目) 做為範例。</span><span class="sxs-lookup"><span data-stu-id="00b0e-357">Here we take the second scenario (recommend items to a given user) as an example.</span></span> <span data-ttu-id="00b0e-358">您可以遵循其他三個案例的相同程序。</span><span class="sxs-lookup"><span data-stu-id="00b0e-358">You can follow the same procedure with the other three.</span></span>

<span data-ttu-id="00b0e-359">將已訓練的推薦系統儲存為定型模型，並將輸入資料篩選為要求的單一使用者識別碼資料行，您可以連結如圖 25 所示的實驗，並且將其發佈為 Web 服務。</span><span class="sxs-lookup"><span data-stu-id="00b0e-359">Saving the trained recommender system as a trained model and filtering the input data to a single user ID column as requested, you can hook up the experiment as in Figure 25 and publish it as a web service.</span></span>

![餐廳推薦問題的評分實驗](./media/machine-learning-interpret-model-results/25.png)

<span data-ttu-id="00b0e-361">圖 25.</span><span class="sxs-lookup"><span data-stu-id="00b0e-361">Figure 25.</span></span> <span data-ttu-id="00b0e-362">餐廳推薦問題的評分實驗</span><span class="sxs-lookup"><span data-stu-id="00b0e-362">Scoring experiment of the restaurant recommendation problem</span></span>

<span data-ttu-id="00b0e-363">執行 Web 服務，傳回的結果如圖 26 所示。</span><span class="sxs-lookup"><span data-stu-id="00b0e-363">Running the web service, the returned result looks like Figure 26.</span></span> <span data-ttu-id="00b0e-364">對於使用者 U1048 的五個推薦餐廳是 134986、135018、134975、135021 及 132862。</span><span class="sxs-lookup"><span data-stu-id="00b0e-364">The five recommended restaurants for user U1048 are 134986, 135018, 134975, 135021, and 132862.</span></span>

![推薦系統服務的範例](./media/machine-learning-interpret-model-results/25_1.png)

![範例實驗結果](./media/machine-learning-interpret-model-results/26.png)

<span data-ttu-id="00b0e-367">圖 26.</span><span class="sxs-lookup"><span data-stu-id="00b0e-367">Figure 26.</span></span> <span data-ttu-id="00b0e-368">餐廳推薦問題的 Web 服務結果</span><span class="sxs-lookup"><span data-stu-id="00b0e-368">Web service result of restaurant recommendation problem</span></span>

<!-- Module References -->
[assign-to-clusters]: https://msdn.microsoft.com/library/azure/eed3ee76-e8aa-46e6-907c-9ca767f5c114/
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[select-columns]: https://msdn.microsoft.com/library/azure/1ec722fa-b623-4e26-a44e-a50c6d726223/
[score-matchbox-recommender]: https://msdn.microsoft.com/library/azure/55544522-9a10-44bd-884f-9a91a9cec2cd/
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[train-clustering-model]: https://msdn.microsoft.com/library/azure/bb43c744-f7fa-41d0-ae67-74ae75da3ffd/
[train-matchbox-recommender]: https://msdn.microsoft.com/library/azure/fa4aa69d-2f1c-4ba4-ad5f-90ea3a515b4c/
