---
title: "aaaDebug Azure 機器學習的模型 |Microsoft 文件"
description: "如何 toodebug 錯誤所產生的模型定型和計分模型 Azure Machine Learning 中的模組。"
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
ms.openlocfilehash: ee38ca8ce38d4fc7add5ba70c80ab9bb2ceaf1d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="debug-your-model-in-azure-machine-learning"></a><span data-ttu-id="4d951-103">在 Azure Machine Learning 中為模型偵錯</span><span class="sxs-lookup"><span data-stu-id="4d951-103">Debug your Model in Azure Machine Learning</span></span>

<span data-ttu-id="4d951-104">本文說明原因是下列兩個失敗的 hello，可能會發生時執行模型的 hello 潛在原因：</span><span class="sxs-lookup"><span data-stu-id="4d951-104">This article explains hello potential reasons why either of hello following two failures might be encountered when running a model:</span></span>

* <span data-ttu-id="4d951-105">hello[定型模型][ train-model]模組產生的錯誤</span><span class="sxs-lookup"><span data-stu-id="4d951-105">hello [Train Model][train-model] module produces an error</span></span> 
* <span data-ttu-id="4d951-106">hello[計分模型][ score-model]模組會產生不正確的結果</span><span class="sxs-lookup"><span data-stu-id="4d951-106">hello [Score Model][score-model] module produces incorrect results</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="train-model-module-produces-an-error"></a><span data-ttu-id="4d951-107">定型模型模組產生錯誤</span><span class="sxs-lookup"><span data-stu-id="4d951-107">Train Model Module produces an error</span></span>

![image1](./media/machine-learning-debug-models/train_model-1.png)

<span data-ttu-id="4d951-109">hello[定型模型][ train-model]模組必須要有兩個輸入：</span><span class="sxs-lookup"><span data-stu-id="4d951-109">hello [Train Model][train-model] Module expects two inputs:</span></span>

1. <span data-ttu-id="4d951-110">機器學習模型提供的 Azure 機器學習模型 hello 集合中的 hello 型別。</span><span class="sxs-lookup"><span data-stu-id="4d951-110">hello type of machine learning model from hello collection of models provided by Azure Machine Learning.</span></span>
2. <span data-ttu-id="4d951-111">hello 與指定的標籤資料行指定定型資料 hello 變數 toopredict （hello 其他資料行假定 toobe 功能）。</span><span class="sxs-lookup"><span data-stu-id="4d951-111">hello training data with a specified Label column which specifies hello variable toopredict (hello other columns are assumed toobe Features).</span></span>

<span data-ttu-id="4d951-112">此模組可能會產生錯誤在下列情況下的 hello:</span><span class="sxs-lookup"><span data-stu-id="4d951-112">This module can produce an error in hello following cases:</span></span>

1. <span data-ttu-id="4d951-113">hello 標籤資料行指定不正確。</span><span class="sxs-lookup"><span data-stu-id="4d951-113">hello Label column is specified incorrectly.</span></span> <span data-ttu-id="4d951-114">這種情況 hello 標籤以選取多個資料行或不正確的資料行索引。</span><span class="sxs-lookup"><span data-stu-id="4d951-114">This can happen if either more than one column is selected as hello Label or an incorrect column index is selected.</span></span> <span data-ttu-id="4d951-115">例如，如果 30 的資料行索引搭配具有只有 25 的資料行的輸入資料集，會套用 hello 第二個案例。</span><span class="sxs-lookup"><span data-stu-id="4d951-115">For example, hello second case would apply if a column index of 30 is used with an input dataset which has only 25 columns.</span></span>

2. <span data-ttu-id="4d951-116">hello dataset 不含任何特徵資料行。</span><span class="sxs-lookup"><span data-stu-id="4d951-116">hello dataset does not contain any Feature columns.</span></span> <span data-ttu-id="4d951-117">例如，如果 hello 輸入資料集有一個資料行，已標示為 hello 標籤資料行，有哪些 toobuild hello 模型沒有功能。</span><span class="sxs-lookup"><span data-stu-id="4d951-117">For example, if hello input dataset has only one column, which is marked as hello Label column, there would be no features with which toobuild hello model.</span></span> <span data-ttu-id="4d951-118">在此情況下，hello[定型模型][ train-model]模組會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="4d951-118">In this case, hello [Train Model][train-model] module produces an error.</span></span>

3. <span data-ttu-id="4d951-119">hello 輸入資料集 （功能或標籤） 包含無限大值。</span><span class="sxs-lookup"><span data-stu-id="4d951-119">hello input dataset (Features or Label) contains Infinity as a value.</span></span>

## <a name="score-model-module-produces-incorrect-results"></a><span data-ttu-id="4d951-120">計分模型模組產生不正確的結果</span><span class="sxs-lookup"><span data-stu-id="4d951-120">Score Model Module produces incorrect results</span></span>

![image2](./media/machine-learning-debug-models/train_test-2.png)

<span data-ttu-id="4d951-122">在受監督的學習一般定型/測試的實驗，hello[分割資料][ split]模組 hello 原始資料集分成兩個部分： 其中一個部分是使用的 tootrain hello 模型，而且是一個組件tooscore 程度 hello 定型的模型執行。</span><span class="sxs-lookup"><span data-stu-id="4d951-122">In a typical training/testing experiment for supervised learning, hello [Split Data][split] module divides hello original dataset into two parts: one part is used tootrain hello model and one part is used tooscore how well hello trained model performs.</span></span> <span data-ttu-id="4d951-123">然後使用的 tooscore hello 測試資料，在其後 hello 結果會評估的 toodetermine hello 模型精確度的 hello hello 定型的模型。</span><span class="sxs-lookup"><span data-stu-id="4d951-123">hello trained model is then used tooscore hello test data, after which hello results are evaluated toodetermine hello accuracy of hello model.</span></span>

<span data-ttu-id="4d951-124">hello[計分模型][ score-model]模組需要兩個輸入：</span><span class="sxs-lookup"><span data-stu-id="4d951-124">hello [Score Model][score-model] module requires two inputs:</span></span>

1. <span data-ttu-id="4d951-125">Hello 定型的模型輸出[定型模型][ train-model]模組。</span><span class="sxs-lookup"><span data-stu-id="4d951-125">A trained model output from hello [Train Model][train-model] module.</span></span>
2. <span data-ttu-id="4d951-126">不同於 hello 資料集的計分資料集使用 tootrain hello 模型。</span><span class="sxs-lookup"><span data-stu-id="4d951-126">A scoring dataset that is different from hello dataset used tootrain hello model.</span></span>

<span data-ttu-id="4d951-127">它的可能在即使 hello 試驗成功，hello[計分模型][ score-model]模組會產生不正確的結果。</span><span class="sxs-lookup"><span data-stu-id="4d951-127">It's possible that even though hello experiment succeeds, hello [Score Model][score-model] module produces incorrect results.</span></span> <span data-ttu-id="4d951-128">幾個案例可能會造成這個 toohappen:</span><span class="sxs-lookup"><span data-stu-id="4d951-128">Several scenarios may cause this toohappen:</span></span>

1. <span data-ttu-id="4d951-129">如果 hello 指定標籤是類別，而的 hello 資料來定型迴歸模型，會產生不正確的輸出的 hello[計分模型][ score-model]模組。</span><span class="sxs-lookup"><span data-stu-id="4d951-129">If hello specified Label is categorical and a regression model is trained on hello data, an incorrect output would be produced by hello [Score Model][score-model] module.</span></span> <span data-ttu-id="4d951-130">這是因為迴歸需要持需回應變數。</span><span class="sxs-lookup"><span data-stu-id="4d951-130">This is because regression requires a continuous response variable.</span></span> <span data-ttu-id="4d951-131">在此情況下，將更適合 toouse 分類模型。</span><span class="sxs-lookup"><span data-stu-id="4d951-131">In this case, it would be more suitable toouse a classification model.</span></span> 

2. <span data-ttu-id="4d951-132">同樣地，如果分類模型已擁有 hello 標籤資料行中浮點數的資料集進行定型，它可能會產生非預期的結果。</span><span class="sxs-lookup"><span data-stu-id="4d951-132">Similarly, if a classification model is trained on a dataset having floating point numbers in hello Label column, it may produce undesirable results.</span></span> <span data-ttu-id="4d951-133">這是因為分類需要離散回應變數，該變數僅允許涉及一組有限且通常比較小的類別的值。</span><span class="sxs-lookup"><span data-stu-id="4d951-133">This is because classification requires a discrete response variable that only allows values that range over a finite, and usually somewhat small, set of classes.</span></span>

3. <span data-ttu-id="4d951-134">如果 hello 計分資料集不包含所有 hello 所使用的功能 tootrain hello 模型，hello[計分模型][ score-model]會產生錯誤。</span><span class="sxs-lookup"><span data-stu-id="4d951-134">If hello scoring dataset does not contain all hello features used tootrain hello model, hello [Score Model][score-model] produces an error.</span></span>

4. <span data-ttu-id="4d951-135">如果中 hello 計分資料集的資料列包含遺漏值或任何其功能的無限值，hello[計分模型][ score-model]將不會產生任何輸出對應 toothat 資料列。</span><span class="sxs-lookup"><span data-stu-id="4d951-135">If a row in hello scoring dataset contains a missing value or an infinite value for any of its features, hello [Score Model][score-model] will not produce any output corresponding toothat row.</span></span>

5. <span data-ttu-id="4d951-136">hello[計分模型][ score-model]可能會產生相同的 hello 計分資料集的所有資料列的輸出。</span><span class="sxs-lookup"><span data-stu-id="4d951-136">hello [Score Model][score-model] may produce identical outputs for all rows in hello scoring dataset.</span></span> <span data-ttu-id="4d951-137">這可能發生，例如，在嘗試使用決策樹系，如果選擇可用的定型範例的 toobe 多個 hello 數目，則 hello 的每個分葉節點的樣本數目下限的分類。</span><span class="sxs-lookup"><span data-stu-id="4d951-137">This could occur, for example, when attempting classification using Decision Forests if hello minimum number of samples per leaf node is chosen toobe more than hello number of training examples available.</span></span>

<!-- Module References -->
[score-model]: https://msdn.microsoft.com/library/azure/401b4f92-e724-4d5a-be81-d5b0ff9bdb33/
[split]: https://msdn.microsoft.com/library/azure/70530644-c97a-4ab6-85f7-88bf30a8be5f/
[train-model]: https://msdn.microsoft.com/library/azure/5cc7053e-aa30-450d-96c0-dae4be720977/

