---
title: "清除並準備 Azure Machine Learning 的資料 | Microsoft Docs"
description: "前置處理和清除資料，為用於機器學習服務做準備。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: bdf659ec-4881-4324-8b9c-747cbfa0c3cd
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: cfaccad0a7d81950d80486dcb0d9e6520deab9b3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="tasks-to-prepare-data-for-enhanced-machine-learning"></a><span data-ttu-id="26b42-103">準備增強機器學習服務的資料的工作</span><span class="sxs-lookup"><span data-stu-id="26b42-103">Tasks to prepare data for enhanced machine learning</span></span>
<span data-ttu-id="26b42-104">前置處理和清除資料是很重要的工作，必須先執行這些工作，才能有效地將資料集用於機器學習服務。</span><span class="sxs-lookup"><span data-stu-id="26b42-104">Pre-processing and cleaning data are important tasks that typically must be conducted before dataset can be used effectively for machine learning.</span></span> <span data-ttu-id="26b42-105">未經處理的資料通常會有雜訊且不可靠，還可能會有遺漏值。</span><span class="sxs-lookup"><span data-stu-id="26b42-105">Raw data is often noisy and unreliable, and may be missing values.</span></span> <span data-ttu-id="26b42-106">使用這類資料進行模型化可能會產生誤導的結果。</span><span class="sxs-lookup"><span data-stu-id="26b42-106">Using such data for modeling can produce misleading results.</span></span> <span data-ttu-id="26b42-107">這些工作屬於 Team Data Science Process (TDSP)，通常會遵循用來探索及計劃所需預先處理的資料集初始探索。</span><span class="sxs-lookup"><span data-stu-id="26b42-107">These tasks are part of the Team Data Science Process (TDSP) and typically follow an initial exploration of a dataset used to discover and plan the pre-processing required.</span></span> <span data-ttu-id="26b42-108">如需更多關於 TDSP 程序的詳細指示，請參閱 [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)中概述的步驟。</span><span class="sxs-lookup"><span data-stu-id="26b42-108">For more detailed instructions on the TDSP process, see the steps outlined in the [Team Data Science Process](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/).</span></span>

<span data-ttu-id="26b42-109">前置處理和清除工作，例如資料探索工作，可以在各種不同環境中實行，例如 SQL 或 Hive 或 Azure Machine Learning Studio，並使用各種工具與語言，例如 R 或 Python，取決於您的資料的儲存位置和格式。</span><span class="sxs-lookup"><span data-stu-id="26b42-109">Pre-processing and cleaning tasks, like the data exploration task, can be carried out in a wide variety of environments, such as SQL or Hive or Azure Machine Learning Studio, and with various tools and languages, such as R or Python, depending where your data is stored and how it is formatted.</span></span> <span data-ttu-id="26b42-110">由於 TDSP 本質上是反覆的，所以這些工作可以在程序工作流程中的各個步驟進行。</span><span class="sxs-lookup"><span data-stu-id="26b42-110">Since TDSP is iterative in nature, these tasks can take place at various steps in the  workflow of the process.</span></span>

<span data-ttu-id="26b42-111">本文將介紹各種不同的資料處理概念和工作，讓您可以在將資料擷取到 Azure Machine Learning 前後執行這些工作。</span><span class="sxs-lookup"><span data-stu-id="26b42-111">This article introduces various data processing concepts and tasks that can be undertaken either before or after ingesting data into Azure Machine Learning.</span></span>

<span data-ttu-id="26b42-112">如需在 Azure Machine Learning Studio 內執行資料探索和前置處理的範例，請參閱 [在 Azure Machine Learning Studio 中前置處理資料](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) 影片。</span><span class="sxs-lookup"><span data-stu-id="26b42-112">For an example of data exploration and pre-processing done inside Azure Machine Learning studio, see the [Pre-processing data in Azure Machine Learning Studio](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/) video.</span></span>

## <a name="why-pre-process-and-clean-data"></a><span data-ttu-id="26b42-113">為何要前置處理和清除資料？</span><span class="sxs-lookup"><span data-stu-id="26b42-113">Why pre-process and clean data?</span></span>
<span data-ttu-id="26b42-114">真實世界的資料是從各種不同的來源和程序蒐集而來，其中可能包含危及資料集品質的違規或損毀資料。</span><span class="sxs-lookup"><span data-stu-id="26b42-114">Real world data is gathered from various sources and processes and it may contain irregularities or corrupt data compromising the quality of the dataset.</span></span> <span data-ttu-id="26b42-115">一般會發生的資料品質問題如下：</span><span class="sxs-lookup"><span data-stu-id="26b42-115">The typical data quality issues that arise are:</span></span>

* <span data-ttu-id="26b42-116">**不完整**：資料缺少屬性或包含遺漏值。</span><span class="sxs-lookup"><span data-stu-id="26b42-116">**Incomplete**: Data lacks attributes or containing missing values.</span></span>
* <span data-ttu-id="26b42-117">**雜訊**：資料包含錯誤的記錄或極端值。</span><span class="sxs-lookup"><span data-stu-id="26b42-117">**Noisy**: Data contains erroneous records or outliers.</span></span>
* <span data-ttu-id="26b42-118">**不一致**：資料包含衝突的記錄或不一致之處。</span><span class="sxs-lookup"><span data-stu-id="26b42-118">**Inconsistent**: Data contains conflicting records or discrepancies.</span></span>

<span data-ttu-id="26b42-119">資料品質是品質預測模型的必要條件。</span><span class="sxs-lookup"><span data-stu-id="26b42-119">Quality data is a prerequisite for quality predictive models.</span></span> <span data-ttu-id="26b42-120">若要避免「垃圾進、垃圾出」並改善資料品質，進而提升模型效能，請務必管理資料健康狀態畫面，以便及早發現資料問題，並決定對應資料的處理和清除步驟。</span><span class="sxs-lookup"><span data-stu-id="26b42-120">To avoid "garbage in, garbage out" and improve data quality and therefore model performance, it is imperative to conduct a data health screen to spot data issues early and decide on the corresponding data processing and cleaning steps.</span></span>

## <a name="what-are-some-typical-data-health-screens-that-are-employed"></a><span data-ttu-id="26b42-121">哪些是要採用的典型資料健康狀態畫面？</span><span class="sxs-lookup"><span data-stu-id="26b42-121">What are some typical data health screens that are employed?</span></span>
<span data-ttu-id="26b42-122">我們可以藉由檢查下列項目，來檢查一般的資料品質：</span><span class="sxs-lookup"><span data-stu-id="26b42-122">We can check the general quality of data by checking:</span></span>

* <span data-ttu-id="26b42-123">**記錄**數目。</span><span class="sxs-lookup"><span data-stu-id="26b42-123">The number of **records**.</span></span>
* <span data-ttu-id="26b42-124">**屬性** (或**功能**) 數目。</span><span class="sxs-lookup"><span data-stu-id="26b42-124">The number of **attributes** (or **features**).</span></span>
* <span data-ttu-id="26b42-125">屬性 **資料類型** (名義、序數或連續)。</span><span class="sxs-lookup"><span data-stu-id="26b42-125">The attribute **data types** (nominal, ordinal, or continuous).</span></span>
* <span data-ttu-id="26b42-126">**遺漏值**的數目。</span><span class="sxs-lookup"><span data-stu-id="26b42-126">The number of **missing values**.</span></span>
* <span data-ttu-id="26b42-127">**格式正確** 。</span><span class="sxs-lookup"><span data-stu-id="26b42-127">**Well-formedness** of the data.</span></span>
  * <span data-ttu-id="26b42-128">如果資料是 TSV 或 CSV 格式，檢查資料行分隔符號和行分隔符號是否一律會正確分隔資料行與行。</span><span class="sxs-lookup"><span data-stu-id="26b42-128">If the data is in TSV or CSV, check that the column separators and line separators always correctly separate columns and lines.</span></span>
  * <span data-ttu-id="26b42-129">如果資料是 HTML 或 XML 格式，請根據各自的標準來檢查資料格式是否正確。</span><span class="sxs-lookup"><span data-stu-id="26b42-129">If the data is in HTML or XML format, check whether the data is well formed based on their respective standards.</span></span>
  * <span data-ttu-id="26b42-130">可能也需要進行剖析，以從半結構化或非結構化的資料擷取結構化資訊。</span><span class="sxs-lookup"><span data-stu-id="26b42-130">Parsing may also be necessary in order to extract structured information from semi-structured or unstructured data.</span></span>
* <span data-ttu-id="26b42-131">**不一致的資料記錄**。</span><span class="sxs-lookup"><span data-stu-id="26b42-131">**Inconsistent data records**.</span></span> <span data-ttu-id="26b42-132">檢查是否允許值範圍。</span><span class="sxs-lookup"><span data-stu-id="26b42-132">Check the range of values are allowed.</span></span> <span data-ttu-id="26b42-133">例如，如果資料包含學生 GPA，可檢查 GPA 是否位於指定範圍內 (假設是 0~4)。</span><span class="sxs-lookup"><span data-stu-id="26b42-133">e.g. If the data contains student GPA, check if the GPA is in the designated range, say 0~4.</span></span>

<span data-ttu-id="26b42-134">當您找到資料問題時， **處理步驟** 是必需的，這通常包含清除遺漏值、資料正規化、離散化、可移除和 (或) 取代可能影響資料對齊之內嵌字元的文字處理、共通欄位的混合資料類型，以及其他項目。</span><span class="sxs-lookup"><span data-stu-id="26b42-134">When you find issues with data, **processing steps** are necessary which often involves cleaning missing values, data normalization, discretization, text processing to remove and/or replace embedded characters which may affect data alignment, mixed data types in common fields, and others.</span></span>

<span data-ttu-id="26b42-135">**Azure Machine Learning 會取用正確格式的表格式資料**。</span><span class="sxs-lookup"><span data-stu-id="26b42-135">**Azure Machine Learning consumes well-formed tabular data**.</span></span>  <span data-ttu-id="26b42-136">如果資料已是表格形式，則可在 Machine Learning Studio 中使用 Azure Machine Learning 直接執行資料前置處理。</span><span class="sxs-lookup"><span data-stu-id="26b42-136">If the data is already in tabular form, data pre-processing can be performed directly with Azure Machine Learning in the Machine Learning Studio.</span></span>  <span data-ttu-id="26b42-137">如果資料的格式不是表格式，假設是 XML，就可能需要進行剖析，才能將資料的格式轉換成表格式。</span><span class="sxs-lookup"><span data-stu-id="26b42-137">If data is not in tabular form, say it is in XML, parsing may be required in order to convert the data to tabular form.</span></span>  

## <a name="what-are-some-of-the-major-tasks-in-data-pre-processing"></a><span data-ttu-id="26b42-138">資料前置處理中有哪些主要工作？</span><span class="sxs-lookup"><span data-stu-id="26b42-138">What are some of the major tasks in data pre-processing?</span></span>
* <span data-ttu-id="26b42-139">**資料清除**：填入值或遺漏值，偵測並移除雜訊資料和極端值。</span><span class="sxs-lookup"><span data-stu-id="26b42-139">**Data cleaning**:  Fill in or missing values, detect and remove noisy data and outliers.</span></span>
* <span data-ttu-id="26b42-140">**資料轉換**：將資料標準化，以減少維度和雜訊。</span><span class="sxs-lookup"><span data-stu-id="26b42-140">**Data transformation**:  Normalize data to reduce dimensions and noise.</span></span>
* <span data-ttu-id="26b42-141">**資料縮減**：取樣資料記錄或屬性，以進行較簡單的資料處理。</span><span class="sxs-lookup"><span data-stu-id="26b42-141">**Data reduction**:  Sample data records or attributes for easier data handling.</span></span>
* <span data-ttu-id="26b42-142">**資料離散化**：將連續屬性轉換為類別屬性，以方便搭配特定的機器學習服務方法來使用。</span><span class="sxs-lookup"><span data-stu-id="26b42-142">**Data discretization**:  Convert continuous attributes to categorical attributes for ease of use with certain machine learning methods.</span></span>
* <span data-ttu-id="26b42-143">**文字清除**：移除可能造成資料對齊錯誤的內嵌字元，例如，定位鍵分隔的資料檔中的內嵌定位鍵、可能中斷記錄的內嵌新行等。</span><span class="sxs-lookup"><span data-stu-id="26b42-143">**Text cleaning**: remove embedded characters which may cause data misalignment, for e.g., embedded tabs in a tab-separated data file, embedded new lines which may break records, etc.</span></span>

<span data-ttu-id="26b42-144">下列各節將詳細說明一些資料處理步驟。</span><span class="sxs-lookup"><span data-stu-id="26b42-144">The sections below detail some of these data processing steps.</span></span>

## <a name="how-to-deal-with-missing-values"></a><span data-ttu-id="26b42-145">如何處理遺漏值？</span><span class="sxs-lookup"><span data-stu-id="26b42-145">How to deal with missing values?</span></span>
<span data-ttu-id="26b42-146">若要處理遺漏值，最好先識別遺漏值的原因，以便對問題進行更好的控制。</span><span class="sxs-lookup"><span data-stu-id="26b42-146">To deal with missing values, it is best to first identify the reason for the missing values to better handle the problem.</span></span> <span data-ttu-id="26b42-147">典型的遺漏值處理方法如下：</span><span class="sxs-lookup"><span data-stu-id="26b42-147">Typical missing value handling methods are:</span></span>

* <span data-ttu-id="26b42-148">**刪除**：移除具有遺漏值的記錄。</span><span class="sxs-lookup"><span data-stu-id="26b42-148">**Deletion**: Remove records with missing values</span></span>
* <span data-ttu-id="26b42-149">**虛擬替代**：使用虛擬值來取代遺漏值，例如，對類別值使用 *unknown* ，或對數值使用 0。</span><span class="sxs-lookup"><span data-stu-id="26b42-149">**Dummy substitution**: Replace missing values with a dummy value: e.g, *unknown* for categorical or 0 for numerical values.</span></span>
* <span data-ttu-id="26b42-150">**平均值替代**：如果遺漏值是數值，可使用平均值來取代遺漏值。</span><span class="sxs-lookup"><span data-stu-id="26b42-150">**Mean substitution**: If the missing data is numerical, replace the missing values with the mean.</span></span>
* <span data-ttu-id="26b42-151">**頻率替代**：如果遺漏值是類別，可使用最常用的項目來取代遺漏值。</span><span class="sxs-lookup"><span data-stu-id="26b42-151">**Frequent substitution**: If the missing data is categorical, replace the missing values with the most frequent item</span></span>
* <span data-ttu-id="26b42-152">**迴歸替代**：利用迴歸方法，使用迴歸值來取代遺漏值。</span><span class="sxs-lookup"><span data-stu-id="26b42-152">**Regression substitution**: Use a regression method to replace missing values with regressed values.</span></span>  

## <a name="how-to-normalize-data"></a><span data-ttu-id="26b42-153">如何將資料標準化？</span><span class="sxs-lookup"><span data-stu-id="26b42-153">How to normalize data?</span></span>
<span data-ttu-id="26b42-154">資料標準化會將數值範圍重新調整為指定的範圍。</span><span class="sxs-lookup"><span data-stu-id="26b42-154">Data normalization re-scales numerical values to a specified range.</span></span> <span data-ttu-id="26b42-155">常用的資料正規化方法包括：</span><span class="sxs-lookup"><span data-stu-id="26b42-155">Popular data normalization methods include:</span></span>

* <span data-ttu-id="26b42-156">**最小值與最大值標準化**：以線性方式將資料轉換為範圍，例如介於 0 和 1 之間時，其中最小值會調整為 0，最大值則調整為 1。</span><span class="sxs-lookup"><span data-stu-id="26b42-156">**Min-Max Normalization**: Linearly transform the data to a range, say between 0 and 1, where the min value is scaled to 0 and max value to 1.</span></span>
* <span data-ttu-id="26b42-157">**Z 分數標準化**：根據平均值和標準差來調整資料範圍：將資料和平均值之間的差距除以標準差。</span><span class="sxs-lookup"><span data-stu-id="26b42-157">**Z-score Normalization**: Scale data based on mean and standard deviation: divide the difference between the data and the mean by the standard deviation.</span></span>
* <span data-ttu-id="26b42-158">**小數點調整**：藉由移動屬性值的小數點來調整資料範圍。</span><span class="sxs-lookup"><span data-stu-id="26b42-158">**Decimal scaling**: Scale the data by moving the decimal point of the attribute value.</span></span>  

## <a name="how-to-discretize-data"></a><span data-ttu-id="26b42-159">如何將資料離散化？</span><span class="sxs-lookup"><span data-stu-id="26b42-159">How to discretize data?</span></span>
<span data-ttu-id="26b42-160">您可以藉由將連續值轉換成名義屬性或間隔來將資料離散化。</span><span class="sxs-lookup"><span data-stu-id="26b42-160">Data can be discretized by converting continuous values to nominal attributes or intervals.</span></span> <span data-ttu-id="26b42-161">以下提供一些執行此動作的方法：</span><span class="sxs-lookup"><span data-stu-id="26b42-161">Some ways of doing this are:</span></span>

* <span data-ttu-id="26b42-162">**等寬分類收納**：將屬性的所有可能值範圍分成 N 個同樣大小的群組，並使用分類收納號碼來指派落於某一個分類收納中的值。</span><span class="sxs-lookup"><span data-stu-id="26b42-162">**Equal-Width Binning**: Divide the range of all possible values of an attribute into N groups of the same size, and assign the values that fall in a bin with the bin number.</span></span>
* <span data-ttu-id="26b42-163">**等高分類收納**：將屬性的所有可能值範圍分成 N 個包含相同執行個體數目的群組，然後使用分類收納號碼來指派落於某一個分類收納中的值。</span><span class="sxs-lookup"><span data-stu-id="26b42-163">**Equal-Height Binning**: Divide the range of all possible values of an attribute into N groups, each containing the same number of instances, then assign the values that fall in a bin with the bin number.</span></span>  

## <a name="how-to-reduce-data"></a><span data-ttu-id="26b42-164">如何縮減資料？</span><span class="sxs-lookup"><span data-stu-id="26b42-164">How to reduce data?</span></span>
<span data-ttu-id="26b42-165">有各種方法可用來縮減資料大小，以便更容易處理資料。</span><span class="sxs-lookup"><span data-stu-id="26b42-165">There are various methods to reduce data size for easier data handling.</span></span> <span data-ttu-id="26b42-166">根據資料大小和網域而定，您可以套用下列方法：</span><span class="sxs-lookup"><span data-stu-id="26b42-166">Depending on data size and the domain, the following methods can be applied:</span></span>

* <span data-ttu-id="26b42-167">**記錄取樣**：取樣資料記錄，並且只從資料中選擇代表性子集。</span><span class="sxs-lookup"><span data-stu-id="26b42-167">**Record Sampling**: Sample the data records and only choose the representative subset from the data.</span></span>
* <span data-ttu-id="26b42-168">**屬性取樣**：只從資料選取一組最重要的屬性子集。</span><span class="sxs-lookup"><span data-stu-id="26b42-168">**Attribute Sampling**: Select only a subset of the most important attributes from the data.</span></span>  
* <span data-ttu-id="26b42-169">**彙總**：將資料分組，並儲存每個群組的數目。</span><span class="sxs-lookup"><span data-stu-id="26b42-169">**Aggregation**: Divide the data into groups and store the numbers for each group.</span></span> <span data-ttu-id="26b42-170">例如，可以將某一家連鎖餐廳在過去 20 年的每日營收數字彙總為每月營收，以縮減資料大小。</span><span class="sxs-lookup"><span data-stu-id="26b42-170">For example, the daily revenue numbers of a restaurant chain over the past 20 years can be aggregated to monthly revenue to reduce the size of the data.</span></span>  

## <a name="how-to-clean-text-data"></a><span data-ttu-id="26b42-171">如何清除文字資料？</span><span class="sxs-lookup"><span data-stu-id="26b42-171">How to clean text data?</span></span>
<span data-ttu-id="26b42-172">**表格式資料中的文字欄位** 可能包含影響資料行對齊和 (或) 記錄界限的字元。</span><span class="sxs-lookup"><span data-stu-id="26b42-172">**Text fields in tabular data** may include characters which affect columns alignment and/or record boundaries.</span></span> <span data-ttu-id="26b42-173">例如，定位鍵分隔檔案的內嵌定位鍵可能導致資料行對齊錯誤，而內嵌的新行字元會中斷記錄行。</span><span class="sxs-lookup"><span data-stu-id="26b42-173">For e.g., embedded tabs in a tab-separated file cause column misalignment, and embedded new line characters break record lines.</span></span> <span data-ttu-id="26b42-174">寫入/讀取文字時，不適當的文字編碼處理會造成資訊遺失，而意外引進無法讀取的字元 (例如 null)，這可能也會影響文字剖析。</span><span class="sxs-lookup"><span data-stu-id="26b42-174">Improper text encoding handling while writing/reading text leads to information loss, inadvertent introduction of unreadable characters, e.g., nulls, and may also affect text parsing.</span></span> <span data-ttu-id="26b42-175">您可以需要仔細地進行剖析和編輯，以清除文字欄位來取得正確的對齊方式，及 (或) 從非結構化或半結構化的文字資料中擷取結構化資料。</span><span class="sxs-lookup"><span data-stu-id="26b42-175">Careful parsing and editing may be required in order to clean text fields for proper alignment and/or to extract structured data from unstructured or semi-structured text data.</span></span>

<span data-ttu-id="26b42-176">**資料探索** 可讓您檢視早期資料。</span><span class="sxs-lookup"><span data-stu-id="26b42-176">**Data exploration** offers an early view into the data.</span></span> <span data-ttu-id="26b42-177">在此步驟中可以發現一些資料問題，然後套用對應的方法以解決這些問題。</span><span class="sxs-lookup"><span data-stu-id="26b42-177">A number of data issues can be uncovered during this step and  corresponding methods can be applied to address those issues.</span></span>  <span data-ttu-id="26b42-178">請務必提出問題，例如，問題的來源是什麼，以及問題可能是如何引發的。</span><span class="sxs-lookup"><span data-stu-id="26b42-178">It is important to ask questions such as what is the source of the issue and how the issue may have been introduced.</span></span> <span data-ttu-id="26b42-179">這也有助於您決定必須採取以解決這些問題的資料處理步驟。</span><span class="sxs-lookup"><span data-stu-id="26b42-179">This also helps you decide on the data processing steps that need to be taken to resolve them.</span></span> <span data-ttu-id="26b42-180">深入探討某一個想要從資料衍生的類型，也可用來排列資料處理工作的優先順序。</span><span class="sxs-lookup"><span data-stu-id="26b42-180">The kind of insights one intends to derive from the data can also be used to prioritize the data processing effort.</span></span>

## <a name="references"></a><span data-ttu-id="26b42-181">參考</span><span class="sxs-lookup"><span data-stu-id="26b42-181">References</span></span>
> <span data-ttu-id="26b42-182">*Data Mining: Concepts and Techniques*(資料採礦：觀念與技術)，第三版，Morgan Kaufmann，2011，Jiawei Han、Micheline Kamber 及 Jian Pei</span><span class="sxs-lookup"><span data-stu-id="26b42-182">*Data Mining: Concepts and Techniques*, Third Edition, Morgan Kaufmann, 2011, Jiawei Han, Micheline Kamber, and Jian Pei</span></span>
> 
> 

