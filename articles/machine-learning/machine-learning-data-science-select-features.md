---
title: "Team Data Science Process 中的特徵選取 | Microsoft Docs"
description: "說明機器學習服務的資料增強程序中功能選取的目的，並提供其角色的範例。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 878541f5-1df8-4368-889a-ced6852aba47
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: ab97ee8278be567ff46d9b0f762d3c5c6cafa412
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="feature-selection-in-the-team-data-science-process-tdsp"></a><span data-ttu-id="109f7-103">Team Data Science Process (TDSP) 中的特徵選取</span><span class="sxs-lookup"><span data-stu-id="109f7-103">Feature selection in the Team Data Science Process (TDSP)</span></span>
<span data-ttu-id="109f7-104">本文說明機器學習服務的資料增強程序中特徵選取的目的，並提供其角色的範例。</span><span class="sxs-lookup"><span data-stu-id="109f7-104">This article explains the purposes of feature selection and provides examples of its role in the data enhancement process of machine learning.</span></span> <span data-ttu-id="109f7-105">這些範例是根據 Azure Machine Learning Studio 繪製。</span><span class="sxs-lookup"><span data-stu-id="109f7-105">These examples are drawn from Azure Machine Learning Studio.</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

<span data-ttu-id="109f7-106">特徵的工程設計與選取是[何謂Team Data Science Process 生命週期？](data-science-process-overview.md)中所概述 Team Data Science Process (TDSP) 程序的其中一部分。</span><span class="sxs-lookup"><span data-stu-id="109f7-106">The engineering and selection of features is one part of the Team Data Science Process (TDSP) outlined in [What is the Team Data Science Process?](data-science-process-overview.md).</span></span> <span data-ttu-id="109f7-107">特徵工程設計和選取屬於 TDSP 的 **開發特徵** 步驟。</span><span class="sxs-lookup"><span data-stu-id="109f7-107">Feature engineering and selection are parts of the **Develop features** step of the TDSP.</span></span>

* <span data-ttu-id="109f7-108">**特性工程設計**：此程序嘗試從資料中的現有原始特性建立其他相關特性，以及增加學習演算法的預測功效。</span><span class="sxs-lookup"><span data-stu-id="109f7-108">**feature engineering**: This process attempts to create additional relevant features from the existing raw features in the data, and to increase predictive power to the learning algorithm.</span></span>
* <span data-ttu-id="109f7-109">**特性選取**：此程序嘗試選取主要的原始資料特性子集，以縮小定型問題的維度。</span><span class="sxs-lookup"><span data-stu-id="109f7-109">**feature selection**: This process selects the key subset of original data features in an attempt to reduce the dimensionality of the training problem.</span></span>

<span data-ttu-id="109f7-110">通常會先套用**特性工程設計**以產生其他特定，然後執行**特性選取**步驟以排除不相關、多餘或高度相關的特性。</span><span class="sxs-lookup"><span data-stu-id="109f7-110">Normally **feature engineering** is applied first to generate additional features, and then the **feature selection** step is performed to eliminate irrelevant, redundant, or highly correlated features.</span></span>

## <a name="filtering-features-from-your-data---feature-selection"></a><span data-ttu-id="109f7-111">從您的資料篩選特性 - 特性選取</span><span class="sxs-lookup"><span data-stu-id="109f7-111">Filtering Features from Your Data - Feature Selection</span></span>
<span data-ttu-id="109f7-112">特性選取程序通常適用於定型資料集的建構，以便進行預測性建模工作，例如分類或迴歸工作。</span><span class="sxs-lookup"><span data-stu-id="109f7-112">Feature selection is a process that is commonly applied for the construction of training datasets for predictive modeling tasks such as classification or regression tasks.</span></span> <span data-ttu-id="109f7-113">其目的在於從原始資料集中選取一小組特性，使用極小一組的特性來代表資料中的最大變異量，藉此縮小其維度。</span><span class="sxs-lookup"><span data-stu-id="109f7-113">The goal is to select a subset of the features from the original dataset that reduce its dimensions by using a minimal set of features to represent the maximum amount of variance in the data.</span></span> <span data-ttu-id="109f7-114">因此，此特性子集是要用於定型模型的唯一特性。</span><span class="sxs-lookup"><span data-stu-id="109f7-114">This subset of features are, then, the only features to be included to train the model.</span></span> <span data-ttu-id="109f7-115">特性選取有兩個主要目的。</span><span class="sxs-lookup"><span data-stu-id="109f7-115">Feature selection serves two main purposes.</span></span>

* <span data-ttu-id="109f7-116">第一，特性選取通常會排除不相關、多餘或高度相關的特性，進而提高分類正確性。</span><span class="sxs-lookup"><span data-stu-id="109f7-116">First, feature selection often increases classification accuracy by eliminating irrelevant, redundant, or highly correlated features.</span></span>
* <span data-ttu-id="109f7-117">第二，減少特性數目，讓模型定型程序更有效率。</span><span class="sxs-lookup"><span data-stu-id="109f7-117">Second, it decreases the number of features which makes model training process more efficient.</span></span> <span data-ttu-id="109f7-118">對於定型代價昂貴的學習者 (例如支援向量機器) 而言，這格外重要。</span><span class="sxs-lookup"><span data-stu-id="109f7-118">This is particularly important for learners that are expensive to train such as support vector machines.</span></span>

<span data-ttu-id="109f7-119">雖然特性選取設法要減少資料集中用於定型模型的特性數目 ，但通常不是指「維度縮減」。</span><span class="sxs-lookup"><span data-stu-id="109f7-119">Although feature selection does seek to reduce the number of features in the dataset used to train the model, it is not usually referred to by the term "dimensionality reduction".</span></span> <span data-ttu-id="109f7-120">特性選取方法會擷取資料中的原始特性子集，但不會加以變更。</span><span class="sxs-lookup"><span data-stu-id="109f7-120">Feature selection methods extract a subset of original features in the data without changing them.</span></span>  <span data-ttu-id="109f7-121">維度縮減方法會運用經過工程設計的特性，轉換原始特性並加以修改。</span><span class="sxs-lookup"><span data-stu-id="109f7-121">Dimensionality reduction methods employ engineered features that can transform the original features and thus modify them.</span></span> <span data-ttu-id="109f7-122">維度縮減方法的範例包含主成分分析、典型相關分析和奇異值分解。</span><span class="sxs-lookup"><span data-stu-id="109f7-122">Examples of dimensionality reduction methods include Principal Component Analysis, canonical correlation analysis, and Singular Value Decomposition.</span></span>

<span data-ttu-id="109f7-123">監督環境中有一個廣泛應用的特性選取方法類別，稱之為「以篩選為基礎的特性選取」。</span><span class="sxs-lookup"><span data-stu-id="109f7-123">Among others, one widely applied category of feature selection methods in a supervised context is called "filter based feature selection".</span></span> <span data-ttu-id="109f7-124">這些方法會評估每個特性與目標屬性之間的相關性，套用統計量值以將評分指派給每個特性。</span><span class="sxs-lookup"><span data-stu-id="109f7-124">By evaluating the correlation between each feature and the target attribute, these methods apply a statistical measure to assign a score to each feature.</span></span> <span data-ttu-id="109f7-125">接著會依分數將特性排名，而分數可用來設定保留或排除特定特性的臨界值。</span><span class="sxs-lookup"><span data-stu-id="109f7-125">The features are then ranked by the score, which may be used to help set the threshold for keeping or eliminating a specific feature.</span></span> <span data-ttu-id="109f7-126">這些方法中使用的統計量值範例包含皮耳森相關、相互資訊和卡方檢定。</span><span class="sxs-lookup"><span data-stu-id="109f7-126">Examples of the statistical measures used in these methods include Person correlation, mutual information, and the Chi squared test.</span></span>

<span data-ttu-id="109f7-127">Azure Machine Learning Studio 中有針對特性選取而提供的模組。</span><span class="sxs-lookup"><span data-stu-id="109f7-127">In Azure Machine Learning Studio, there are modules provided for feature selection.</span></span> <span data-ttu-id="109f7-128">如下圖所示，這些模組包含[以篩選為基礎的特性選取][filter-based-feature-selection]和[費雪線性判別分析][fisher-linear-discriminant-analysis]。</span><span class="sxs-lookup"><span data-stu-id="109f7-128">As shown in the following figure, these modules include [Filter-Based Feature Selection][filter-based-feature-selection] and [Fisher Linear Discriminant Analysis][fisher-linear-discriminant-analysis].</span></span>

![特性選取範例](./media/machine-learning-data-science-select-features/feature-Selection.png)

<span data-ttu-id="109f7-130">例如，請考慮使用[以篩選為基礎的特徵選取][filter-based-feature-selection]模組。</span><span class="sxs-lookup"><span data-stu-id="109f7-130">Consider, for example, the use of the [Filter-Based Feature Selection][filter-based-feature-selection] module.</span></span> <span data-ttu-id="109f7-131">為了方便起見，我們繼續使用上述的文字採礦範例。</span><span class="sxs-lookup"><span data-stu-id="109f7-131">For the purpose of convenience, we continue to use the text mining example outlined above.</span></span> <span data-ttu-id="109f7-132">假設在透過[特徵雜湊][feature-hashing]模組建立一組 256 個特徵之後，我們想要建立一個迴歸模型，其回應變數為 "Col1" 並代表 1 至 5 的書籍評論評比。</span><span class="sxs-lookup"><span data-stu-id="109f7-132">Assume that we want to build a regression model after a set of 256 features are created through the [Feature Hashing][feature-hashing] module, and that the response variable is the "Col1" and represents a book review ratings ranging from 1 to 5.</span></span> <span data-ttu-id="109f7-133">將 [特性評分方法] 設定為 [皮耳森相關]，則 [目標欄] 會是 "Col1"，而 [所需的特性數] 會是 50。</span><span class="sxs-lookup"><span data-stu-id="109f7-133">By setting "Feature scoring method" to be "Pearson Correlation", the "Target column" to be "Col1", and the "Number of desired features" to 50.</span></span> <span data-ttu-id="109f7-134">然後，[以篩選為基礎的特徵選取][filter-based-feature-selection]模組會產生一個包含 50 個特徵且目標屬性為 "Col1" 的資料集。</span><span class="sxs-lookup"><span data-stu-id="109f7-134">Then the module [Filter-Based Feature Selection][filter-based-feature-selection] will produce a dataset containing 50 features together with the target attribute "Col1".</span></span> <span data-ttu-id="109f7-135">下圖顯示此實驗的流程以及我們剛才描述的輸入參數。</span><span class="sxs-lookup"><span data-stu-id="109f7-135">The following figure shows the flow of this experiment and the input parameters we just described.</span></span>

![特性選取範例](./media/machine-learning-data-science-select-features/feature-Selection1.png)

<span data-ttu-id="109f7-137">下圖顯示結果產生的資料集。</span><span class="sxs-lookup"><span data-stu-id="109f7-137">The following figure shows the resulting datasets.</span></span> <span data-ttu-id="109f7-138">每個特性都是根據本身與目標屬性 "Col1" 之間的皮耳森相關進行評分。</span><span class="sxs-lookup"><span data-stu-id="109f7-138">Each feature is scored based on the Pearson Correlation between itself and the target attribute "Col1".</span></span> <span data-ttu-id="109f7-139">系統會保留最高分的特性。</span><span class="sxs-lookup"><span data-stu-id="109f7-139">The features with top scores are kept.</span></span>

![特性選取範例](./media/machine-learning-data-science-select-features/feature-Selection2.png)

<span data-ttu-id="109f7-141">下圖顯示所選特性的對應評分。</span><span class="sxs-lookup"><span data-stu-id="109f7-141">The corresponding scores of the selected features are shown in the following figure.</span></span>

![特性選取範例](./media/machine-learning-data-science-select-features/feature-Selection3.png)

<span data-ttu-id="109f7-143">套用[以篩選為基礎的特徵選取][filter-based-feature-selection]模組，以選取 256 個特徵中的 50 個特徵，因為根據「皮耳森相關」評分方法，其具有目標變數 "Col1" 的最相關特徵。</span><span class="sxs-lookup"><span data-stu-id="109f7-143">By applying this [Filter-Based Feature Selection][filter-based-feature-selection] module, 50 out of 256 features are selected because they have the most correlated features with the target variable "Col1", based on the scoring method "Pearson Correlation".</span></span>

## <a name="conclusion"></a><span data-ttu-id="109f7-144">結論</span><span class="sxs-lookup"><span data-stu-id="109f7-144">Conclusion</span></span>
<span data-ttu-id="109f7-145">功能工程設計和選取是兩種常見的工程設計和選取的功能，可提高下列定型程序的效率：嘗試擷取資料中內含的重要資訊。</span><span class="sxs-lookup"><span data-stu-id="109f7-145">Feature engineering and feature selection are two commonly Engineered and selected features increase the efficiency of the training process which attempts to extract the key information contained in the data.</span></span> <span data-ttu-id="109f7-146">此外，還可改善這些模型的功效，正確地分類輸入資料以及更精確地預測感興趣的結果。</span><span class="sxs-lookup"><span data-stu-id="109f7-146">They also improve the power of these models to classify the input data accurately and to predict outcomes of interest more robustly.</span></span> <span data-ttu-id="109f7-147">特性工程設計和選取也可結合起來，讓學習更易於以運算方式處理。</span><span class="sxs-lookup"><span data-stu-id="109f7-147">Feature engineering and selection can also combine to make the learning more computationally tractable.</span></span> <span data-ttu-id="109f7-148">其作法是提高而後減少校正或定型模型所需的特性數量。</span><span class="sxs-lookup"><span data-stu-id="109f7-148">It does so by enhancing and then reducing the number of features needed to calibrate or train a model.</span></span> <span data-ttu-id="109f7-149">從數學的角度來看，選取用來定型模型的特性是極小的一組獨立變數，可供解釋資料中的模式，然後成功地預測結果。</span><span class="sxs-lookup"><span data-stu-id="109f7-149">Mathematically speaking, the features selected to train the model are a minimal set of independent variables that explain the patterns in the data and then predict outcomes successfully.</span></span>

<span data-ttu-id="109f7-150">請注意，不一定要執行特性工程設計和特性選取。</span><span class="sxs-lookup"><span data-stu-id="109f7-150">Note that it is not always necessarily to perform feature engineering or feature selection.</span></span> <span data-ttu-id="109f7-151">需要與否取決於我們所擁有或收集的資料、我們挑選的演算法，以及實驗的目標。</span><span class="sxs-lookup"><span data-stu-id="109f7-151">Whether it is needed or not depends on the data we have or collect, the algorithm we pick, and the objective of the experiment.</span></span>

<!-- Module References -->
[feature-hashing]: https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/
[filter-based-feature-selection]: https://msdn.microsoft.com/library/azure/918b356b-045c-412b-aa12-94a1d2dad90f/
[fisher-linear-discriminant-analysis]: https://msdn.microsoft.com/library/azure/dcaab0b2-59ca-4bec-bb66-79fd23540080/

