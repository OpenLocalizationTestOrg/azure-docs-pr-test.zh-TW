---
title: "資料科學特徵工程設計 | Microsoft Docs"
description: "說明機器學習服務的資料增強程序中特性工程設計的目的，並提供其角色的範例。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 3fde69e8-5e7b-49ad-b3fb-ab8ef6503a4d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: zhangya;bradsev
ms.openlocfilehash: f586e8087a246f3bedf5010e8f6ce7aea1c1ec6a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="feature-engineering-in-data-science"></a><span data-ttu-id="f4867-103">資料科學特徵工程設計</span><span class="sxs-lookup"><span data-stu-id="f4867-103">Feature engineering in data science</span></span>
<span data-ttu-id="f4867-104">本主題說明在機器學習服務的資料增強程序中特徵工程設計的目的，並提供其角色的範例。</span><span class="sxs-lookup"><span data-stu-id="f4867-104">This topic explains the purposes of feature engineering and provides examples of its role in the data enhancement process of machine learning.</span></span> <span data-ttu-id="f4867-105">用來說明此程序的範例是取自 Azure Machine Learning Studio。</span><span class="sxs-lookup"><span data-stu-id="f4867-105">The examples used to illustrate this process are drawn from Azure Machine Learning Studio.</span></span> 

[!INCLUDE [cap-create-features-data-selector](../../includes/cap-create-features-selector.md)]

<span data-ttu-id="f4867-106">這個 **功能表** 所連結的主題會說明如何在各種環境中建立資料的特徵。</span><span class="sxs-lookup"><span data-stu-id="f4867-106">This **menu** links to topics that describe how to create features for data in various environments.</span></span> <span data-ttu-id="f4867-107">此工作是 [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)中的一個步驟。</span><span class="sxs-lookup"><span data-stu-id="f4867-107">This task is a step in the [Team Data Science Process (TDSP)](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="f4867-108">特徵工程設計藉由以協助學習程序的原始資料來建立特徵，以嘗試增加學習演算法的預測能力。</span><span class="sxs-lookup"><span data-stu-id="f4867-108">Feature engineering attempts to increase the predictive power of learning algorithms by creating features from raw data that help facilitate the learning process.</span></span> <span data-ttu-id="f4867-109">特徵的工程設計與選取是何謂 [Team Data Science Process 生命週期？](data-science-process-overview.md)中所概述 TDSP 程序的其中一部分。</span><span class="sxs-lookup"><span data-stu-id="f4867-109">The engineering and selection of features is one part of the TDSP outlined in the [What is the Team Data Science Process lifecycle?](data-science-process-overview.md)</span></span> <span data-ttu-id="f4867-110">特徵工程設計和選取屬於 TDSP 的 **開發特徵** 步驟。</span><span class="sxs-lookup"><span data-stu-id="f4867-110">Feature engineering and selection are parts of the **Develop features** step of the TDSP.</span></span> 

* <span data-ttu-id="f4867-111">**特性工程設計**：此程序嘗試從資料中的現有原始特性建立其他相關特性，以及增加學習演算法的預測功效。</span><span class="sxs-lookup"><span data-stu-id="f4867-111">**feature engineering**: This process attempts to create additional relevant features from the existing raw features in the data, and to increase the predictive power of the learning algorithm.</span></span>
* <span data-ttu-id="f4867-112">**特性選取**：此程序嘗試選取主要的原始資料特性子集，以縮小定型問題的維度。</span><span class="sxs-lookup"><span data-stu-id="f4867-112">**feature selection**: This process selects the key subset of original data features in an attempt to reduce the dimensionality of the training problem.</span></span>

<span data-ttu-id="f4867-113">通常會先套用**特性工程設計**以產生其他特定，然後執行**特性選取**步驟以排除不相關、多餘或高度相關的特性。</span><span class="sxs-lookup"><span data-stu-id="f4867-113">Normally **feature engineering** is applied first to generate additional features, and then the **feature selection** step is performed to eliminate irrelevant, redundant, or highly correlated features.</span></span>

<span data-ttu-id="f4867-114">從收集的原始資料擷取特性，通常可以增強機器學習服務中使用的定型資料。</span><span class="sxs-lookup"><span data-stu-id="f4867-114">The training data used in machine learning can often be enhanced by extraction of features from the raw data collected.</span></span> <span data-ttu-id="f4867-115">學習環境中工程設計特性範例，分類手寫字元的影像的方式是是建立從原始位元分配資料建構的位元密度對應。</span><span class="sxs-lookup"><span data-stu-id="f4867-115">An example of an engineered feature in the context of learning how to classify the images of handwritten characters is creation of a bit density map constructed from the raw bit distribution data.</span></span> <span data-ttu-id="f4867-116">相較於直接使用原始分配，此對應有助於更有效地找出字元的界限。</span><span class="sxs-lookup"><span data-stu-id="f4867-116">This map can help locate the edges of the characters more efficiently than simply using the raw distribution directly.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="creating-features-from-your-data---feature-engineering"></a><span data-ttu-id="f4867-117">從您的資料建立特性 - 特性工程設計</span><span class="sxs-lookup"><span data-stu-id="f4867-117">Creating Features from Your Data - Feature Engineering</span></span>
<span data-ttu-id="f4867-118">定型資料包含由範例所組成的矩陣 (資料列中儲存的記錄或 觀察)，而每個範例都有一組特性 (資料行中儲存的變數或欄位)。</span><span class="sxs-lookup"><span data-stu-id="f4867-118">The training data consists of a matrix composed of examples (records or observations stored in rows), each of which has a set of features (variables or fields stored in columns).</span></span> <span data-ttu-id="f4867-119">在實驗設計中指定的特性預計會將資料中的模式特性化。</span><span class="sxs-lookup"><span data-stu-id="f4867-119">The features specified in the experimental design are expected to characterize the patterns in the data.</span></span> <span data-ttu-id="f4867-120">儘管許多原始資料欄位都可以直接包含在選取用來將模型定型的特性集中，但通常還是需要從原始資料中的特性建構其他 (經過工程設計的) 特性，才能產生增強的定型資料集。</span><span class="sxs-lookup"><span data-stu-id="f4867-120">Although many of the raw data fields can be directly included in the selected feature set used to train a model, it is often the case that additional (engineered) features need to be constructed from the features in the raw data to generate an enhanced training dataset.</span></span>

<span data-ttu-id="f4867-121">應建立何種特性，才能在模型定型時增強資料集？</span><span class="sxs-lookup"><span data-stu-id="f4867-121">What kind of features should be created to enhance the dataset when training a model?</span></span> <span data-ttu-id="f4867-122">經過工程設計的特性可增強定型，還會提供用以區分資料中模式的資訊。</span><span class="sxs-lookup"><span data-stu-id="f4867-122">Engineered features that enhance the training provide information that better differentiates the patterns in the data.</span></span> <span data-ttu-id="f4867-123">我們期望新特性可提供原始或現有特性集中未清楚擷取或顯而易見的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="f4867-123">We expect the new features to provide additional information that is not clearly captured or easily apparent in the original or existing feature set.</span></span> <span data-ttu-id="f4867-124">但此程序是一種藝術。</span><span class="sxs-lookup"><span data-stu-id="f4867-124">But this process is something of an art.</span></span> <span data-ttu-id="f4867-125">健全且有建設性的決策通常需要一些網域.專業知識。</span><span class="sxs-lookup"><span data-stu-id="f4867-125">Sound and productive decisions often require some domain expertise.</span></span>

<span data-ttu-id="f4867-126">從 Azure 機器學習著手時，最簡單的方式是透過 Studio 中提供的範例具體地領會此程序。</span><span class="sxs-lookup"><span data-stu-id="f4867-126">When starting with Azure Machine Learning, it is easiest to grasp this process concretely using samples provided in the Studio.</span></span> <span data-ttu-id="f4867-127">以下呈現兩個範例：</span><span class="sxs-lookup"><span data-stu-id="f4867-127">Two examples are presented here:</span></span>

* <span data-ttu-id="f4867-128">在已知目標值的監督實驗中的 [單車租用數量預測](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) 迴歸範例</span><span class="sxs-lookup"><span data-stu-id="f4867-128">A regression example [Prediction of the number of bike rentals](http://gallery.cortanaintelligence.com/Experiment/Regression-Demand-estimation-4) in a supervised experiment where the target values are known</span></span>
* <span data-ttu-id="f4867-129">使用 [特性雜湊](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)</span><span class="sxs-lookup"><span data-stu-id="f4867-129">A text mining classification example using [Feature Hashing](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/)</span></span>

## <a name="example-1-adding-temporal-features-for-regression-model"></a><span data-ttu-id="f4867-130">範例 1：新增迴歸模型的暫時特性</span><span class="sxs-lookup"><span data-stu-id="f4867-130">Example 1: Adding Temporal Features for Regression Model</span></span>
<span data-ttu-id="f4867-131">讓我們在 Azure Machine Learning Studio 中使用「單車的需求預測」實驗，示範如何設計迴歸工作的特性。</span><span class="sxs-lookup"><span data-stu-id="f4867-131">Let's use the experiment "Demand forecasting of bikes" in Azure Machine Learning Studio to demonstrate how to engineer features for a regression task.</span></span> <span data-ttu-id="f4867-132">這項實驗的目標在於預測單車需求，也就是再特定月份/日期/小時內單車租用的數量。</span><span class="sxs-lookup"><span data-stu-id="f4867-132">The objective of this experiment is to predict the demand for the bikes, that is, the number of bike rentals within a specific month/day/hour.</span></span> <span data-ttu-id="f4867-133">資料集「單車租用 UCI 資料集」作為原始輸入資料使用。</span><span class="sxs-lookup"><span data-stu-id="f4867-133">The dataset "Bike Rental UCI dataset" is used as the raw input data.</span></span> <span data-ttu-id="f4867-134">此資料集是以在美國華盛頓特區維護單車出租網路的 Capital Bikeshare 公司所提供的實際資料為基礎。</span><span class="sxs-lookup"><span data-stu-id="f4867-134">This dataset is based on real data from the Capital Bikeshare company that maintains a bike rental network in Washington DC in the United States.</span></span> <span data-ttu-id="f4867-135">此資料集代表 2011 年和 2012 年中特定一個小時內的單車租用數量，總共包含 17379 個資料列和 17 個資料行。</span><span class="sxs-lookup"><span data-stu-id="f4867-135">The dataset represents the number of bike rentals within a specific hour of a day in the years 2011 and year 2012 and contains 17379 rows and 17 columns.</span></span> <span data-ttu-id="f4867-136">原始特性集包含天氣條件 (溫度/溼度/風速) 和當天的類型 (假日/工作日)。</span><span class="sxs-lookup"><span data-stu-id="f4867-136">The raw feature set contains weather conditions (temperature/humidity/wind speed) and the type of the day (holiday/weekday).</span></span> <span data-ttu-id="f4867-137">要預測的欄位為 "cnt"，代表特定小時內單位租用的計數，其範圍是 1 至 977。</span><span class="sxs-lookup"><span data-stu-id="f4867-137">The field to predict is "cnt", a count which represents the bike rentals within a specific hour and which ranges ranges from 1 to 977.</span></span>

<span data-ttu-id="f4867-138">為了達到在定型資料中建構有效特性的目的，會使用相同的演算法建立四個各有不同定型資料集的迴歸模型，</span><span class="sxs-lookup"><span data-stu-id="f4867-138">With the goal of constructing effective features in the training data, four regression models are built using the same algorithm but with four different training datasets.</span></span> <span data-ttu-id="f4867-139">這四個資料集代表相同的原始輸入資料，但設定的特性數量增加。</span><span class="sxs-lookup"><span data-stu-id="f4867-139">The four datasets represent the same raw input data, but with an increasing number of features set.</span></span> <span data-ttu-id="f4867-140">這些特性可分為四類：</span><span class="sxs-lookup"><span data-stu-id="f4867-140">These features are grouped into four categories:</span></span>

1. <span data-ttu-id="f4867-141">A = 預測日的天氣 + 假日 + 工作日 + 週末特性</span><span class="sxs-lookup"><span data-stu-id="f4867-141">A = weather + holiday + weekday + weekend features for the predicted day</span></span>
2. <span data-ttu-id="f4867-142">B = 過去的 12 小時以來，每小時租出的單車數量</span><span class="sxs-lookup"><span data-stu-id="f4867-142">B = number of bikes that were rented in each of the previous 12 hours</span></span>
3. <span data-ttu-id="f4867-143">C = 過去的 12 天以來，每天在同一個時間租出的單車數量</span><span class="sxs-lookup"><span data-stu-id="f4867-143">C = number of bikes that were rented in each of the previous 12 days at the same hour</span></span>
4. <span data-ttu-id="f4867-144">D = 過去的 12 週以來，在同一天同一個時間租出的單車數量</span><span class="sxs-lookup"><span data-stu-id="f4867-144">D = number of bikes that were rented in each of the previous 12 weeks at the same hour and the same day</span></span>

<span data-ttu-id="f4867-145">除了已存在於原先原始資料中的特性集 A 以外，其他三個特性集是透過特性工程設計程序來建立。</span><span class="sxs-lookup"><span data-stu-id="f4867-145">Besides feature set A, which already exist in the original raw data, the other three sets of features are created through the feature engineering process.</span></span> <span data-ttu-id="f4867-146">特性集 B 會擷取最近的單車需求。</span><span class="sxs-lookup"><span data-stu-id="f4867-146">Feature set B captures very recent demand for the bikes.</span></span> <span data-ttu-id="f4867-147">特性集 C 會擷取某一個小時的單車需求。</span><span class="sxs-lookup"><span data-stu-id="f4867-147">Feature set C captures the demand for bikes at a particular hour.</span></span> <span data-ttu-id="f4867-148">特性集 D 會擷取一週當中某一天某一個小時的單車需求。</span><span class="sxs-lookup"><span data-stu-id="f4867-148">Feature set D captures demand for bikes at particular hour and particular day of the week.</span></span> <span data-ttu-id="f4867-149">四個定型資料集分別包含特性集 A、A+B、A+B+C 和 A+B+C+D。</span><span class="sxs-lookup"><span data-stu-id="f4867-149">The four training datasets each includes feature set A, A+B, A+B+C, and A+B+C+D, respectively.</span></span>

<span data-ttu-id="f4867-150">在 Azure 機器學習實驗中，這四個定型資料集是透過預先處理的輸入資料集中的分支形成。</span><span class="sxs-lookup"><span data-stu-id="f4867-150">In the Azure Machine Learning experiment, these four training datasets are formed via four branches from the pre-processed input dataset.</span></span> <span data-ttu-id="f4867-151">除了最左邊的分支以外，每個分支都包含 [執行 R 指令碼](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/) 模組，其中有一組衍生特性 (特性集 B、C 和 D) 會分別建構並附加至匯入的資料集 。</span><span class="sxs-lookup"><span data-stu-id="f4867-151">Except the left most branch, each of these branches contains an [Execute R Script](https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/) module, in which a set of derived features (feature set B, C, and D) are respectively constructed and appended to the imported dataset.</span></span> <span data-ttu-id="f4867-152">下圖示範左邊第二個分支中用來建立特性集 B 的 R 指令碼。</span><span class="sxs-lookup"><span data-stu-id="f4867-152">The following figure demonstrates the R script used to create feature set B in the second left branch.</span></span>

![建立特性](./media/machine-learning-data-science-create-features/addFeature-Rscripts.png)

<span data-ttu-id="f4867-154">四個模型的效能結果比較彙總在下表中。</span><span class="sxs-lookup"><span data-stu-id="f4867-154">The comparison of the performance results of the four models are summarized in the following table.</span></span> <span data-ttu-id="f4867-155">特性 A+B+C 所呈現的結果最理想。</span><span class="sxs-lookup"><span data-stu-id="f4867-155">The best results are shown by features A+B+C.</span></span> <span data-ttu-id="f4867-156">請注意，當定型資料中包含其他特性集時，錯誤率會降低。</span><span class="sxs-lookup"><span data-stu-id="f4867-156">Note that the error rate decreases when additional feature set are included in the training data.</span></span> <span data-ttu-id="f4867-157">這證實了我們的推測：特性集 B、C 會針對迴歸工作提供其他相關資訊。</span><span class="sxs-lookup"><span data-stu-id="f4867-157">It verifies our presumption that the feature set B, C provide additional relevant information for the regression task.</span></span> <span data-ttu-id="f4867-158">但新增 D 特性似乎不會讓錯誤率降低。</span><span class="sxs-lookup"><span data-stu-id="f4867-158">But adding the D feature does not seem to provide any additional reduction in the error rate.</span></span>

![結果比較](./media/machine-learning-data-science-create-features/result1.png)

## <span data-ttu-id="f4867-160"><a name="example2"></a> 範例 2：在文字採礦中建立特性</span><span class="sxs-lookup"><span data-stu-id="f4867-160"><a name="example2"></a> Example 2: Creating Features in Text Mining</span></span>
<span data-ttu-id="f4867-161">特性工程設計廣泛運用於文字採礦的相關工作，例如文件分類和情感分析。</span><span class="sxs-lookup"><span data-stu-id="f4867-161">Feature engineering is widely applied in tasks related to text mining, such as document classification and sentiment analysis.</span></span> <span data-ttu-id="f4867-162">例如，當我們想要將文件分為數個類別時，通常會假設包含在一個文件類別中的文字/片語比較不可能出現在其他文件類別中。</span><span class="sxs-lookup"><span data-stu-id="f4867-162">For example, when we want to classify documents into several categories, a typical assumption is that the word/phrases included in one doc category are less likely to occur in another doc category.</span></span> <span data-ttu-id="f4867-163">換言之，文字/片語分配的次數能夠描述不同的文件類別。</span><span class="sxs-lookup"><span data-stu-id="f4867-163">In another words, the frequency of the words/phrases distribution is able to characterize different document categories.</span></span> <span data-ttu-id="f4867-164">在文字採礦應用程式中，因為個別的文字內容通常可作為輸入資料，所以建立文字/片語次數相關特性時需要特性工程設計程序。</span><span class="sxs-lookup"><span data-stu-id="f4867-164">In text mining applications, because individual pieces of text-contents usually serve as the input data, the feature engineering process is needed to create the features involving word/phrase frequencies.</span></span>

<span data-ttu-id="f4867-165">為了達成此工作，會套用名為 **特性雜湊** 的技術，有效地將任意文字特性變成索引。</span><span class="sxs-lookup"><span data-stu-id="f4867-165">To achieve this task, a technique called **feature hashing** is applied to efficiently turn arbitrary text features into indices.</span></span> <span data-ttu-id="f4867-166">此方法不會將每個文字特性 (文字/片語) 關聯至特定索引，而是將雜湊函數套用至特性並直接使用其雜湊值作為索引。</span><span class="sxs-lookup"><span data-stu-id="f4867-166">Instead of associating each text feature (words/phrases) to a particular index, this method functions by applying a hash function to the features and using their hash values as indices directly.</span></span>

<span data-ttu-id="f4867-167">Azure 機器學習中有一個 [特性雜湊](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) 模組，方便建立這些文字/片語特性。</span><span class="sxs-lookup"><span data-stu-id="f4867-167">In Azure Machine Learning, there is a [Feature Hashing](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) module that creates these word/phrase features conveniently.</span></span> <span data-ttu-id="f4867-168">下圖顯示使用此模組的範例。</span><span class="sxs-lookup"><span data-stu-id="f4867-168">Following figure shows an example of using this module.</span></span> <span data-ttu-id="f4867-169">輸入資料集包含兩個資料行：1 至 5 的書籍評比，以及實際評論內容。</span><span class="sxs-lookup"><span data-stu-id="f4867-169">The input dataset contains two columns: the book rating ranging from 1 to 5, and the actual review content.</span></span> <span data-ttu-id="f4867-170">此 [特性雜湊](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) 模組的目標在於擷取一些新特性，以顯示特定書籍評論中對應文字/片語的發生次數。</span><span class="sxs-lookup"><span data-stu-id="f4867-170">The goal of this [Feature Hashing](https://msdn.microsoft.com/library/azure/c9a82660-2d9c-411d-8122-4d9e0b3ce92a/) module is to retrieve a bunch of new features that show the occurrence frequency of the corresponding word(s)/phrase(s) within the particular book review.</span></span> <span data-ttu-id="f4867-171">若要使用此模組，我們必須完成下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f4867-171">To use this module, we need to complete the following steps:</span></span>

* <span data-ttu-id="f4867-172">第一步，選取包含輸入文字的資料行 (此例中的 "Col2")。</span><span class="sxs-lookup"><span data-stu-id="f4867-172">First, select the column that contains the input text ("Col2" in this example).</span></span>
* <span data-ttu-id="f4867-173">第二步，將 "Hashing bitsize" 設定為 8，表示將建立 2^8=256 個特性。</span><span class="sxs-lookup"><span data-stu-id="f4867-173">Second, set the "Hashing bitsize" to 8, which means 2^8=256 features will be created.</span></span> <span data-ttu-id="f4867-174">所有文字中的文字/片語會雜湊至 256 個索引。</span><span class="sxs-lookup"><span data-stu-id="f4867-174">The word/phase in all the text will be hashed to 256 indices.</span></span> <span data-ttu-id="f4867-175">"Hashing bitsize" 參數的範圍是 1 至 31。</span><span class="sxs-lookup"><span data-stu-id="f4867-175">The parameter "Hashing bitsize" ranges from 1 to 31.</span></span> <span data-ttu-id="f4867-176">如果將此值設定為較大的數字，文字/片語比較不可能雜湊至相同的索引。</span><span class="sxs-lookup"><span data-stu-id="f4867-176">The word(s)/phrase(s) are less likely to be hashed into the same index if setting it to be a larger number.</span></span>
* <span data-ttu-id="f4867-177">第三步，將 "N-grams" 參數設定為 2。</span><span class="sxs-lookup"><span data-stu-id="f4867-177">Third, set the parameter "N-grams" to 2.</span></span> <span data-ttu-id="f4867-178">這麼做可從輸入文字中取得 unigrams (適用於每一個文字的特性) 和 bigrams (適用於每一對相鄰文字的特性) 的發生次數。</span><span class="sxs-lookup"><span data-stu-id="f4867-178">This gets the occurrence frequency of unigrams (a feature for every single word) and bigrams (a feature for every pair of adjacent words) from the input text.</span></span> <span data-ttu-id="f4867-179">"N-grams" 參數的範圍是 0 至 10，這表示要包含在一個特性中的循序文字數目上限。</span><span class="sxs-lookup"><span data-stu-id="f4867-179">The parameter "N-grams" ranges from 0 to 10, which indicates the maximum number of sequential words to be included in a feature.</span></span>  

![「特性雜湊」模組](./media/machine-learning-data-science-create-features/feature-Hashing1.png)

<span data-ttu-id="f4867-181">下圖顯示這些新特性的外觀。</span><span class="sxs-lookup"><span data-stu-id="f4867-181">The following figure shows what the these new feature look like.</span></span>

![「特性雜湊」範例](./media/machine-learning-data-science-create-features/feature-Hashing2.png)

## <a name="conclusion"></a><span data-ttu-id="f4867-183">結論</span><span class="sxs-lookup"><span data-stu-id="f4867-183">Conclusion</span></span>
<span data-ttu-id="f4867-184">工程設計和選取的特性可提高下列定型程序的效率：嘗試擷取資料中內含的重要資訊。</span><span class="sxs-lookup"><span data-stu-id="f4867-184">Engineered and selected features increase the efficiency of the training process which attempts to extract the key information contained in the data.</span></span> <span data-ttu-id="f4867-185">此外，還可改善這些模型的功效，正確地分類輸入資料以及更精確地預測感興趣的結果。</span><span class="sxs-lookup"><span data-stu-id="f4867-185">They also improve the power of these models to classify the input data accurately and to predict outcomes of interest more robustly.</span></span> <span data-ttu-id="f4867-186">特性工程設計和選取也可結合起來，讓學習更易於以運算方式處理。</span><span class="sxs-lookup"><span data-stu-id="f4867-186">Feature engineering and selection can also combine to make the learning more computationally tractable.</span></span> <span data-ttu-id="f4867-187">其作法是提高而後減少校正或定型模型所需的特性數量。</span><span class="sxs-lookup"><span data-stu-id="f4867-187">It does so by enhancing and then reducing the number of features needed to calibrate or train a model.</span></span> <span data-ttu-id="f4867-188">從數學的角度來看，選取用來定型模型的特性是極小的一組獨立變數，可供解釋資料中的模式，然後成功地預測結果。</span><span class="sxs-lookup"><span data-stu-id="f4867-188">Mathematically speaking, the features selected to train the model are a minimal set of independent variables that explain the patterns in the data and then predict outcomes successfully.</span></span>

<span data-ttu-id="f4867-189">請注意，不一定要執行特性工程設計和特性選取。</span><span class="sxs-lookup"><span data-stu-id="f4867-189">Note that it is not always necessarily to perform feature engineering or feature selection.</span></span> <span data-ttu-id="f4867-190">需要與否取決於我們所擁有或收集的資料、我們挑選的演算法，以及實驗的目標。</span><span class="sxs-lookup"><span data-stu-id="f4867-190">Whether it is needed or not depends on the data we have or collect, the algorithm we pick, and the objective of the experiment.</span></span>
