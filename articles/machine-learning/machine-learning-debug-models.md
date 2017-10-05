---
title: "在 Azure Machine Learning 中為模型偵錯 | Microsoft Docs"
description: "如何在 Azure Machine Learning 中，針對定型模型和計分模型模組所產生的錯誤進行偵錯。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 629dc45e-ac1e-4b7d-b120-08813dc448be
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bradsev;garye
ms.openlocfilehash: d4cc94a6395ea45bccf65d9a9f3118ec98cb258d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="34b53-103">在 Azure Machine Learning 中為模型偵錯</span><span class="sxs-lookup"><span data-stu-id="34b53-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="34b53-104">本文將說明為什麼執行模型時可能會發生以下任一個失敗的潛在原因：</span><span class="sxs-lookup"><span data-stu-id="34b53-104">This article explains the potential reasons why either of the following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="34b53-105">[定型模型][train-model]模組產生錯誤</span><span class="sxs-lookup"><span data-stu-id="34b53-105">the [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="34b53-106">[計分模型][score-model]模組產生不正確的結果</span><span class="sxs-lookup"><span data-stu-id="34b53-106">the [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="34b53-107">定型模型模組產生錯誤</span><span class="sxs-lookup"><span data-stu-id="34b53-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="34b53-109">[定型模型][train-model]模組預期 2 個輸入：</span><span class="sxs-lookup"><span data-stu-id="34b53-109">The [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="34b53-110">來自 Azure Machine Learning 所提供的模型集合的機器學習服務模型類型。</span><span class="sxs-lookup"><span data-stu-id="34b53-110">The type of machine learning model from the collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="34b53-111">含有指定 [標籤] 資料行的定型資料，可指定要預測的變數值 (假設另一個資料行為 [功能])。</span><span class="sxs-lookup"><span data-stu-id="34b53-111">The training data with a specified Label column which specifies the variable to predict (the other columns are assumed to be Features).</span></span>

<span data-ttu-id="34b53-112">此模組會在下列情況中產生錯誤：</span><span class="sxs-lookup"><span data-stu-id="34b53-112">This module can produce an error in the following cases:</span></span>

1. <span data-ttu-id="34b53-113">[標籤] 資料行的指定不正確。</span><span class="sxs-lookup"><span data-stu-id="34b53-113">The Label column is specified incorrectly.</span></span> <span data-ttu-id="34b53-114">如果選取了多個資料行做為 [標籤]，或選取了不正確的資料行索引，即會發生此情況。</span><span class="sxs-lookup"><span data-stu-id="34b53-114">This can happen if either more than one column is selected as the Label or an incorrect column index is selected.</span></span> <span data-ttu-id="34b53-115">例如，如果使用的資料行索引為 30，但輸入資料集只有 25 個資料行，則適用第二個狀況。</span><span class="sxs-lookup"><span data-stu-id="34b53-115">For example, the second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="34b53-116">資料集不包含任何 [功能] 資料行。</span><span class="sxs-lookup"><span data-stu-id="34b53-116">The dataset does not contain any Feature columns.</span></span> <span data-ttu-id="34b53-117">例如，如果輸入資料集只有 1 個標示為 [標籤] 資料行的資料行，則沒有用來建置模型的功能。</span><span class="sxs-lookup"><span data-stu-id="34b53-117">For example, if the input dataset has only one column, which is marked as the Label column, there would be no features with which to build the model.</span></span> <span data-ttu-id="34b53-118">在此情況下，[定型模型][train-model]模組會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="34b53-118">In this case, the [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="34b53-119">輸入資料集 ([功能] 或 [標籤]) 含有無限大值。</span><span class="sxs-lookup"><span data-stu-id="34b53-119">The input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="34b53-120">計分模型模組產生不正確的結果</span><span class="sxs-lookup"><span data-stu-id="34b53-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="34b53-122">在受監督之學習的典型訓練/測試實驗中，[分割資料][split]模組會將原始資料集分成兩個部分：一個用來定型模型，一個則用來對定型模型的表現程度進行計分。</span><span class="sxs-lookup"><span data-stu-id="34b53-122">In a typical training/testing experiment for supervised learning, the [Split Data][split] module divides the original dataset into two parts: one part is used to train the model and one part is used to score how well the trained model performs.</span></span> <span data-ttu-id="34b53-123">接著，使用定型模型為測試資料評分，然後再評估結果以判斷模型的準確性。</span><span class="sxs-lookup"><span data-stu-id="34b53-123">The trained model is then used to score the test data, after which the results are evaluated to determine the accuracy of the model.</span></span>

<span data-ttu-id="34b53-124">[計分模型][score-model]模組需要兩個輸入：</span><span class="sxs-lookup"><span data-stu-id="34b53-124">The [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="34b53-125">來自[定型模型][train-model]模組的定型模型輸出。</span><span class="sxs-lookup"><span data-stu-id="34b53-125">A trained model output from the [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="34b53-126">與用來定型模型之資料集不同的計分資料集。</span><span class="sxs-lookup"><span data-stu-id="34b53-126">A scoring dataset that is different from the dataset used to train the model.</span></span>

<span data-ttu-id="34b53-127">即使實驗成功，[計分模型][score-model]模組可能還是會產生不正確的結果。</span><span class="sxs-lookup"><span data-stu-id="34b53-127">It's possible that even though the experiment succeeds, the [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="34b53-128">有幾個情況可能會導致這個結果：</span><span class="sxs-lookup"><span data-stu-id="34b53-128">Several scenarios may cause this to happen:</span></span>

1. <span data-ttu-id="34b53-129">如果指定的 [標籤] 經過分類，且迴歸模型的資料已定型，則[計分模型][score-model]模組將會產生不正確的輸出。</span><span class="sxs-lookup"><span data-stu-id="34b53-129">If the specified Label is categorical and a regression model is trained on the data, an incorrect output would be produced by the [Score Model][score-model] module.</span></span> <span data-ttu-id="34b53-130">這是因為迴歸需要持需回應變數。</span><span class="sxs-lookup"><span data-stu-id="34b53-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="34b53-131">在此情況下，更適合使用分類模型。</span><span class="sxs-lookup"><span data-stu-id="34b53-131">In this case, it would be more suitable to use a classification model.</span></span> 

2. <span data-ttu-id="34b53-132">同樣地，如果分類模型針對 [標籤] 資料行中包含浮點數的資料集進行訓練，它可能會產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="34b53-132">Similarly, if a classification model is trained on a dataset having floating point numbers in the Label column, it may produce undesirable results.</span></span> <span data-ttu-id="34b53-133">這是因為分類需要離散回應變數，該變數僅允許涉及一組有限且通常比較小的類別的值。</span><span class="sxs-lookup"><span data-stu-id="34b53-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="34b53-134">如果計分資料集不包含用來定型模型的所有特徵，[計分模型][score-model]會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="34b53-134">If the scoring dataset does not contain all the features used to train the model, the [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="34b53-135">如果計分資料集中的資料列在其任何特徵中含有遺漏值或無限值，[計分模型][score-model]將不會產生對應於該資料列的任何輸出。</span><span class="sxs-lookup"><span data-stu-id="34b53-135">If a row in the scoring dataset contains a missing value or an infinite value for any of its features, the [Score Model][score-model] will not produce any output corresponding to that row.</span></span>

5. <span data-ttu-id="34b53-136">對於計分資料集中的所有資料列，[計分模型][score-model]可能會產生相同的輸出。</span><span class="sxs-lookup"><span data-stu-id="34b53-136">The [Score Model][score-model] may produce identical outputs for all rows in the scoring dataset.</span></span> <span data-ttu-id="34b53-137">例如，使用決策樹系嘗試分類時，如果選擇每個分葉節點範例的最小數目大於可用的訓練範例數目時，可能會發生這個情況。</span><span class="sxs-lookup"><span data-stu-id="34b53-137">This could occur, for example, when attempting classification using Decision Forests if the minimum number of samples per leaf node is chosen to be more than the number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

