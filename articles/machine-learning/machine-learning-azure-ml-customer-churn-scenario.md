---
title: "使用機器學習分析客戶流失 | Microsoft Docs"
description: "開發整合式模型以分析及評分客戶流失的案例研究"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: 1333ffe2-59b8-4f40-9be7-3bf1173fc38d
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 84916fc86fd731b3544a0d389325d9a1d14e1a39
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a><span data-ttu-id="9a40d-103">使用 Azure Machine Learning 分析客戶流失</span><span class="sxs-lookup"><span data-stu-id="9a40d-103">Analyzing Customer Churn by using Azure Machine Learning</span></span>
## <a name="overview"></a><span data-ttu-id="9a40d-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9a40d-104">Overview</span></span>
<span data-ttu-id="9a40d-105">本文提供使用 Azure Machine Learning 建置客戶流失分析專案的參考實作。</span><span class="sxs-lookup"><span data-stu-id="9a40d-105">This article presents a reference implementation of a customer churn analysis project that is built by using Azure Machine Learning.</span></span> <span data-ttu-id="9a40d-106">在本文中將討論關聯的一般模型，可全面性地解決產業客戶流失的問題。</span><span class="sxs-lookup"><span data-stu-id="9a40d-106">In this article, we discuss associated generic models for holistically solving the problem of industrial customer churn.</span></span> <span data-ttu-id="9a40d-107">對於以機器學習建立的模型，我們也衡量其正確性，同時評估進一步開發的方向。</span><span class="sxs-lookup"><span data-stu-id="9a40d-107">We also measure the accuracy of models that are built by using Machine Learning, and we assess directions for further development.</span></span>  

### <a name="acknowledgements"></a><span data-ttu-id="9a40d-108">通知</span><span class="sxs-lookup"><span data-stu-id="9a40d-108">Acknowledgements</span></span>
<span data-ttu-id="9a40d-109">這項實驗是由 Microsoft 的首席資料科學家 Serge Berger 和 Microsoft Azure Machine Learning 的前產品經理 Roger Barga 共同開發和測試。</span><span class="sxs-lookup"><span data-stu-id="9a40d-109">This experiment was developed and tested by Serge Berger, Principal Data Scientist at Microsoft, and Roger Barga, formerly Product Manager for Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="9a40d-110">Azure 文件小組高度認可其專業知識，並感謝他們分享這份白皮書。</span><span class="sxs-lookup"><span data-stu-id="9a40d-110">The Azure documentation team gratefully acknowledges their expertise and thanks them for sharing this white paper.</span></span>

> [!NOTE]
> <span data-ttu-id="9a40d-111">這項實驗中使用的資料無法公開使用。</span><span class="sxs-lookup"><span data-stu-id="9a40d-111">The data used for this experiment is not publicly available.</span></span> <span data-ttu-id="9a40d-112">如需如何建置客戶流失分析的機器學習模型範例，請參閱︰[Cortana Intelligence 資源庫](http://gallery.cortanaintelligence.com/)中的[售業客戶流失模型範本](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1)</span><span class="sxs-lookup"><span data-stu-id="9a40d-112">For an example of how to build a machine learning model for churn analysis, see: [Retail churn model template](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)</span></span>
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="the-problem-of-customer-churn"></a><span data-ttu-id="9a40d-113">客戶流失的問題</span><span class="sxs-lookup"><span data-stu-id="9a40d-113">The problem of customer churn</span></span>
<span data-ttu-id="9a40d-114">消費者市場和所有企業產業中的公司都必須處理客戶流失的問題。</span><span class="sxs-lookup"><span data-stu-id="9a40d-114">Businesses in the consumer market and in all enterprise sectors have to deal with churn.</span></span> <span data-ttu-id="9a40d-115">有時，客戶流失太多會影響政策決定。</span><span class="sxs-lookup"><span data-stu-id="9a40d-115">Sometimes churn is excessive and influences policy decisions.</span></span> <span data-ttu-id="9a40d-116">傳統的解決方案是預測流失傾向較高的客戶，透過特別禮遇、行銷活動或給予特殊待遇，滿足他們的需求。</span><span class="sxs-lookup"><span data-stu-id="9a40d-116">The traditional solution is to predict high-propensity churners and address their needs via a concierge service, marketing campaigns, or by applying special dispensations.</span></span> <span data-ttu-id="9a40d-117">這些作法隨著產業而不同，甚至在同一產業的不同消費群之間也會不同 (例如電信業)。</span><span class="sxs-lookup"><span data-stu-id="9a40d-117">These approaches can vary from industry to industry and even from a particular consumer cluster to another within one industry (for example, telecommunications).</span></span>

<span data-ttu-id="9a40d-118">共同點就是公司必須將這些額外的客戶維繫工作量降到最低。</span><span class="sxs-lookup"><span data-stu-id="9a40d-118">The common factor is that businesses need to minimize these special customer retention efforts.</span></span> <span data-ttu-id="9a40d-119">因此，一般的作法是以流失機率來評比每位客戶，然後解決排名前 N 位的客戶。</span><span class="sxs-lookup"><span data-stu-id="9a40d-119">Thus, a natural methodology would be to score every customer with the probability of churn and address the top N ones.</span></span> <span data-ttu-id="9a40d-120">排名前面的客戶可能是對公司最有利潤的客戶；例如在更複雜的情況下，選擇要給予特殊待遇的候選者時會採用利潤函數。</span><span class="sxs-lookup"><span data-stu-id="9a40d-120">The top customers might be the most profitable ones; for example, in more sophisticated scenarios, a profit function is employed during the selection of candidates for special dispensation.</span></span> <span data-ttu-id="9a40d-121">這些考量只不過是處理客戶流失的整體策略的一部分。</span><span class="sxs-lookup"><span data-stu-id="9a40d-121">However, these considerations are only a part of the holistic strategy for dealing with churn.</span></span> <span data-ttu-id="9a40d-122">公司也需要考慮風險 (和相關的風險容忍度)、介入的程度和成本，以及合理的客戶區隔。</span><span class="sxs-lookup"><span data-stu-id="9a40d-122">Businesses also have to take into account risk (and associated risk tolerance), the level and cost of the intervention, and plausible customer segmentation.</span></span>  

## <a name="industry-outlook-and-approaches"></a><span data-ttu-id="9a40d-123">產業展望和作法</span><span class="sxs-lookup"><span data-stu-id="9a40d-123">Industry outlook and approaches</span></span>
<span data-ttu-id="9a40d-124">駕輕就熟地處理客戶流失是成熟產業的一項特徵。</span><span class="sxs-lookup"><span data-stu-id="9a40d-124">Sophisticated handling of churn is a sign of a mature industry.</span></span> <span data-ttu-id="9a40d-125">電信產業是典型的例子，用戶更換供應商的頻率很高。</span><span class="sxs-lookup"><span data-stu-id="9a40d-125">The classic example is the telecommunications industry where subscribers are known to frequently switch from one provider to another.</span></span> <span data-ttu-id="9a40d-126">這種志願性流失是最主要問題所在。</span><span class="sxs-lookup"><span data-stu-id="9a40d-126">This voluntary churn is a prime concern.</span></span> <span data-ttu-id="9a40d-127">再者，供應商對於「流失成因」 已累積大量經驗，亦即促成客戶更換供應商的因素。</span><span class="sxs-lookup"><span data-stu-id="9a40d-127">Moreover, providers have accumulated significant knowledge about *churn drivers*, which are the factors that drive customers to switch.</span></span>

<span data-ttu-id="9a40d-128">例如，在行動電話業務中，手機或裝置選擇是導致客戶流失的一個明顯因素。</span><span class="sxs-lookup"><span data-stu-id="9a40d-128">For instance, handset or device choice is a well-known driver of churn in the mobile phone business.</span></span> <span data-ttu-id="9a40d-129">因此，常用的手段是補助新用戶的手機價格，但對既有客戶收取全額的升級費用。</span><span class="sxs-lookup"><span data-stu-id="9a40d-129">As a result, a popular policy is to subsidize the price of a handset for new subscribers and charging a full price to existing customers for an upgrade.</span></span> <span data-ttu-id="9a40d-130">根據歷史經驗，這種手段反而造成使客戶跳槽到另一家供應商來尋找新的折扣，使得供應商不得不修正策略。</span><span class="sxs-lookup"><span data-stu-id="9a40d-130">Historically, this policy has led to customers hopping from one provider to another to get a new discount, which in turn, has prompted providers to refine their strategies.</span></span>

<span data-ttu-id="9a40d-131">手機產品日新月異，是造成以最新手機款式為主的客戶流失模型迅速失效的一項因素。</span><span class="sxs-lookup"><span data-stu-id="9a40d-131">High volatility in handset offerings is a factor that very quickly invalidates models of churn that are based on current handset models.</span></span> <span data-ttu-id="9a40d-132">此外，行動電話不只是通訊裝置，也是流行的代表 (例外 iPhone)，而這些社會性指標並不在一般的電信資料集之內。</span><span class="sxs-lookup"><span data-stu-id="9a40d-132">Additionally, mobile phones are not only telecommunication devices; they are also fashion statements (consider the iPhone), and these social predictors are outside the scope of regular telecommunications data sets.</span></span>

<span data-ttu-id="9a40d-133">建構模型的最後結果就是，單純地排除客戶流失的已知原因，就不可能設計出一套完美的策略。</span><span class="sxs-lookup"><span data-stu-id="9a40d-133">The net result for modeling is that you cannot devise a sound policy simply by eliminating known reasons for churn.</span></span> <span data-ttu-id="9a40d-134">事實上，持續性的模型建構策略是 **必要的**，包括量化類別變項的傳統模型 (例如決策樹)。</span><span class="sxs-lookup"><span data-stu-id="9a40d-134">In fact, a continuous modeling strategy, including classic models that quantify categorical variables (such as decision trees), is **mandatory**.</span></span>

<span data-ttu-id="9a40d-135">組織對客戶利用巨量資料集來進行巨量資料分析 (尤其是根據巨量資料的客戶流失偵測)，當做解決問題的有效手段。</span><span class="sxs-lookup"><span data-stu-id="9a40d-135">Using big data sets on their customers, organizations are performing big data analytics (in particular, churn detection based on big data) as an effective approach to the problem.</span></span> <span data-ttu-id="9a40d-136">您可以在＜建議＞中的 ETL 一節深入了解對付客戶流失問題的巨量資料作法。</span><span class="sxs-lookup"><span data-stu-id="9a40d-136">You can find more about the big data approach to the problem of churn in the Recommendations on ETL section.</span></span>  

## <a name="methodology-to-model-customer-churn"></a><span data-ttu-id="9a40d-137">客戶流失模型建構方法</span><span class="sxs-lookup"><span data-stu-id="9a40d-137">Methodology to model customer churn</span></span>
<span data-ttu-id="9a40d-138">圖 1-3 顯示解決客戶流失時常用的問題解決流程。</span><span class="sxs-lookup"><span data-stu-id="9a40d-138">A common problem-solving process to solve customer churn is depicted in Figures 1-3:</span></span>  

1. <span data-ttu-id="9a40d-139">風險模型可讓您考量動作如何影響機率和風險。</span><span class="sxs-lookup"><span data-stu-id="9a40d-139">A risk model allows you to consider how actions affect probability and risk.</span></span>
2. <span data-ttu-id="9a40d-140">介入模型讓您考量介入程度如何影響客戶流失機率和顧客終身價值 (CLV) 的數量。</span><span class="sxs-lookup"><span data-stu-id="9a40d-140">An intervention model allows you to consider how the level of intervention could affect the probability of churn and the amount of customer lifetime value (CLV).</span></span>
3. <span data-ttu-id="9a40d-141">此分析本身會形成定性分析，再逐步發展成以客戶族群為目標的積極行銷活動，以提供最佳服務。</span><span class="sxs-lookup"><span data-stu-id="9a40d-141">This analysis lends itself to a qualitative analysis that is escalated to a proactive marketing campaign that targets customer segments to deliver the optimal offer.</span></span>  

![][1]

<span data-ttu-id="9a40d-142">這個預視方法是應付流失最好的方法，但是會伴隨複雜性：我們必須開發多模型原型，並且追蹤模型之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="9a40d-142">This forward looking approach is the best way to treat churn, but it comes with complexity: we have to develop a multi-model archetype and trace dependencies between the models.</span></span> <span data-ttu-id="9a40d-143">模型之間的互動可封裝起來，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="9a40d-143">The interaction among models can be encapsulated as shown in the following diagram:</span></span>  

![][2]

<span data-ttu-id="9a40d-144">*圖 4：多模型整合原型*</span><span class="sxs-lookup"><span data-stu-id="9a40d-144">*Figure 4: Unified multi-model archetype*</span></span>  

<span data-ttu-id="9a40d-145">如果要對客戶維繫提出一套全面性解決辦法，則不同模型之間的互動是關鍵。</span><span class="sxs-lookup"><span data-stu-id="9a40d-145">Interaction between the models is key if we are to deliver a holistic approach to customer retention.</span></span> <span data-ttu-id="9a40d-146">每個模型必然隨著時間而退化；因此，架構是一種隱性的環路 (類似於以 CRISP-DM 資料採礦標準所設定的原型，[***3***])。</span><span class="sxs-lookup"><span data-stu-id="9a40d-146">Each model necessarily degrades over time; therefore, the architecture is an implicit loop (similar to the archetype set by the CRISP-DM data mining standard, [***3***]).</span></span>  

<span data-ttu-id="9a40d-147">風險-決策-行場區隔/分解的整個循環仍然是一般化結構，適用於解決許多商業問題。</span><span class="sxs-lookup"><span data-stu-id="9a40d-147">The overall cycle of risk-decision-marketing segmentation/decomposition is still a generalized structure, which is applicable to many business problems.</span></span> <span data-ttu-id="9a40d-148">客戶流失分析只是這群問題的一種很明顯的典型例子，因為它指出複雜商業問題的所有特徵，而這種問題無法以簡單的預測方案來解決。</span><span class="sxs-lookup"><span data-stu-id="9a40d-148">Churn analysis is simply a strong representative of this group of problems because it exhibits all the traits of a complex business problem that does not allow a simplified predictive solution.</span></span> <span data-ttu-id="9a40d-149">方法中並未特別指出現代處理客戶流失辦法中的社會層面，社會層面封裝在模型原型中，就像在任何模型中一樣。</span><span class="sxs-lookup"><span data-stu-id="9a40d-149">The social aspects of the modern approach to churn are not particularly highlighted in the approach, but the social aspects are encapsulated in the modeling archetype, as they would be in any model.</span></span>  

<span data-ttu-id="9a40d-150">此處增添的一項重要部分是巨量資料分析。</span><span class="sxs-lookup"><span data-stu-id="9a40d-150">An interesting addition here is big data analytics.</span></span> <span data-ttu-id="9a40d-151">現今，電信業和零售業都竭盡所能地收集客戶的資料，可明顯預期銜接多重模型的需求將成為共同的趨勢，浮現的趨勢例如物聯網和普及化裝置，讓公司能夠將智慧型解決方案運用在許多層面上。</span><span class="sxs-lookup"><span data-stu-id="9a40d-151">Today's telecommunication and retail businesses collect exhaustive data about their customers, and we can easily foresee that the need for multi-model connectivity will become a common trend, given emerging trends such as the Internet of Things and ubiquitous devices, which allow business to employ smart solutions at multiple layers.</span></span>  

 

## <a name="implementing-the-modeling-archetype-in-machine-learning-studio"></a><span data-ttu-id="9a40d-152">在 Machine Learning Studio 中實作模型原型</span><span class="sxs-lookup"><span data-stu-id="9a40d-152">Implementing the modeling archetype in Machine Learning Studio</span></span>
<span data-ttu-id="9a40d-153">根據剛才說明的問題，實作一套整合的模型化和評分方法的最佳方式為何？</span><span class="sxs-lookup"><span data-stu-id="9a40d-153">Given the problem just described, what is the best way to implement an integrated modeling and scoring approach?</span></span> <span data-ttu-id="9a40d-154">在本節中，我們將示範如何利用 Azure Machine Learning Studio 來達成這項目的。</span><span class="sxs-lookup"><span data-stu-id="9a40d-154">In this section, we will demonstrate how we accomplished this by using Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="9a40d-155">針對客戶流失來設計整體原型時，多重模型方法不可或缺。</span><span class="sxs-lookup"><span data-stu-id="9a40d-155">The multi-model approach is a must when designing a global archetype for churn.</span></span> <span data-ttu-id="9a40d-156">即使是作法中的評分 (預測) 部分也應該為多重模型。</span><span class="sxs-lookup"><span data-stu-id="9a40d-156">Even the scoring (predictive) part of the approach should be multi-model.</span></span>  

<span data-ttu-id="9a40d-157">下圖顯示我們已建立的原型，在 Machine Learning Studio 中採用四種評分演算法來預測客戶流失。</span><span class="sxs-lookup"><span data-stu-id="9a40d-157">The following diagram shows the prototype we created, which employs four scoring algorithms in Machine Learning Studio to predict churn.</span></span> <span data-ttu-id="9a40d-158">使用多重模型方法的理由不只是為了建立集成分類器來提高準確性，也是為了避免過度訓練，同時改善制式的特徵選擇。</span><span class="sxs-lookup"><span data-stu-id="9a40d-158">The reason for using a multi-model approach is not only to create an ensemble classifier to increase accuracy, but also to protect against over-fitting and to improve prescriptive feature selection.</span></span>  

![][3]

<span data-ttu-id="9a40d-159">*圖 5：客戶流失模型建構方法的原型*</span><span class="sxs-lookup"><span data-stu-id="9a40d-159">*Figure 5: Prototype of a churn modeling approach*</span></span>  

<span data-ttu-id="9a40d-160">以下幾節提供我們使用 Machine Learning Studio 實作的原型評分模型的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="9a40d-160">The following sections provide more details about the prototype scoring model that we implemented by using Machine Learning Studio.</span></span>  

### <a name="data-selection-and-preparation"></a><span data-ttu-id="9a40d-161">選擇和準備資料</span><span class="sxs-lookup"><span data-stu-id="9a40d-161">Data selection and preparation</span></span>
<span data-ttu-id="9a40d-162">用來建立模型和給客戶評分的資料取自於一個 CRM 垂直解決方案，為了保護客戶隱私，資料皆經過模糊處理。</span><span class="sxs-lookup"><span data-stu-id="9a40d-162">The data used to build the models and score customers was obtained from a CRM vertical solution, with the data obfuscated to protect customer privacy.</span></span> <span data-ttu-id="9a40d-163">資料包含美國 8,000 個訂用帳戶的相關資訊，並結合了三個來源：佈建資料 (訂用帳戶中繼資料)、活動資料 (系統的使用方式)，以及客戶支援資料。</span><span class="sxs-lookup"><span data-stu-id="9a40d-163">The data contains information about 8,000 subscriptions in the U.S., and it combines three sources: provisioning data (subscription metadata), activity data (usage of the system), and customer support data.</span></span> <span data-ttu-id="9a40d-164">資料不包含客戶的任何業務相關資訊；例如，不含忠誠度中繼資料或信用分數。</span><span class="sxs-lookup"><span data-stu-id="9a40d-164">The data does not include any business related information about the customers; for example, it does not include loyalty metadata or credit scores.</span></span>  

<span data-ttu-id="9a40d-165">為了簡單起見，ETL 和資料淨化處理不在討論範圍內，因為我們假設資料準備已在別處完成。</span><span class="sxs-lookup"><span data-stu-id="9a40d-165">For simplicity, ETL and data cleansing processes are out of scope because we assume that data preparation has already been done elsewhere.</span></span>   

<span data-ttu-id="9a40d-166">模型的特徵選擇取決於預測變數組的初步顯著計分，包含在利用隨機森林模組的程序中。</span><span class="sxs-lookup"><span data-stu-id="9a40d-166">Feature selection for modeling is based on preliminary significance scoring of the set of predictors, included in the process that uses the random forest module.</span></span> <span data-ttu-id="9a40d-167">在 Machine Learning Studio 中實作時，我們計算代表性特徵的平均值、中位數和範圍。</span><span class="sxs-lookup"><span data-stu-id="9a40d-167">For the implementation in Machine Learning Studio, we calculated the mean, median, and ranges for representative features.</span></span> <span data-ttu-id="9a40d-168">舉例來說，我們加上定性資料的總合，例如使用者活動的最小值和最大值。</span><span class="sxs-lookup"><span data-stu-id="9a40d-168">For example, we added aggregates for the qualitative data, such as minimum and maximum values for user activity.</span></span>    

<span data-ttu-id="9a40d-169">我們也取得最近 6 個月的暫時資訊。</span><span class="sxs-lookup"><span data-stu-id="9a40d-169">We also captured temporal information for the most recent six months.</span></span> <span data-ttu-id="9a40d-170">我們分析一年的資料後，發現即使存在統計顯著趨勢，對客戶流失的效應也會在六個月後遞減。</span><span class="sxs-lookup"><span data-stu-id="9a40d-170">We analyzed data for one year and we established that even if there were statistically significant trends, the effect on churn is greatly diminished after six months.</span></span>  

<span data-ttu-id="9a40d-171">最重要的一點是整個過程 (包括 ETL、特徵選擇和模型化) 都在 Machine Learning Studio 中實作，並採用 Microsoft Azure 中的資料來源。</span><span class="sxs-lookup"><span data-stu-id="9a40d-171">The most important point is that the entire process, including ETL, feature selection, and modeling was implemented in Machine Learning Studio, using data sources in Microsoft Azure.</span></span>   

<span data-ttu-id="9a40d-172">下圖顯示使用的資料。</span><span class="sxs-lookup"><span data-stu-id="9a40d-172">The following diagrams illustrate the data that was used.</span></span>  

![][4]

<span data-ttu-id="9a40d-173">*圖 6：資料來源摘錄 (經過模糊處理)*</span><span class="sxs-lookup"><span data-stu-id="9a40d-173">*Figure 6: Excerpt of data source (obfuscated)*</span></span>  

![][5]

<span data-ttu-id="9a40d-174">*圖 7：從資料來源擷取的特徵*</span><span class="sxs-lookup"><span data-stu-id="9a40d-174">*Figure 7: Features extracted from data source*</span></span>
 

> <span data-ttu-id="9a40d-175">請注意，這項資料為私人所有，因此不能分享模型和資料。</span><span class="sxs-lookup"><span data-stu-id="9a40d-175">Note that this data is private and therefore the model and data cannot be shared.</span></span>
> <span data-ttu-id="9a40d-176">如需使用公開可用資料的類似模型，請參閱此 [Cortana Intelligence 資源庫](http://gallery.cortanaintelligence.com/)中的實驗範例：[電信公司客戶流失](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383)。</span><span class="sxs-lookup"><span data-stu-id="9a40d-176">However, for a similar model using publicly available data, see this sample experiment in the [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/): [Telco Customer Churn](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).</span></span>
> 
> <span data-ttu-id="9a40d-177">若要深入了解如何使用 Cortana Intelligence Suite 實作客戶流失分析模型，我們也推薦資深程式經理 Wee Hyong Tok 的 [這段影片](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) 。</span><span class="sxs-lookup"><span data-stu-id="9a40d-177">To learn more about how you can implement a churn analysis model using Cortana Intelligence Suite, we also recommend [this video](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) by Senior Program Manager Wee Hyong Tok.</span></span> 
> 
> 

### <a name="algorithms-used-in-the-prototype"></a><span data-ttu-id="9a40d-178">原型中使用的演算法</span><span class="sxs-lookup"><span data-stu-id="9a40d-178">Algorithms used in the prototype</span></span>
<span data-ttu-id="9a40d-179">我們採用下列四種機器學習演算法來建立原型 (沒有自訂)：</span><span class="sxs-lookup"><span data-stu-id="9a40d-179">We used the following four machine learning algorithms to build the prototype (no customization):</span></span>  

1. <span data-ttu-id="9a40d-180">邏輯式迴歸 (LR)</span><span class="sxs-lookup"><span data-stu-id="9a40d-180">Logistic regression (LR)</span></span>
2. <span data-ttu-id="9a40d-181">推進式決策樹 (BT)</span><span class="sxs-lookup"><span data-stu-id="9a40d-181">Boosted decision tree (BT)</span></span>
3. <span data-ttu-id="9a40d-182">平均感知器 (AP)</span><span class="sxs-lookup"><span data-stu-id="9a40d-182">Averaged perceptron (AP)</span></span>
4. <span data-ttu-id="9a40d-183">支援向量機器 (SVM)</span><span class="sxs-lookup"><span data-stu-id="9a40d-183">Support vector machine (SVM)</span></span>  

<span data-ttu-id="9a40d-184">下圖顯示實驗設計介面的一部分，指出模型的建立順序：</span><span class="sxs-lookup"><span data-stu-id="9a40d-184">The following diagram illustrates a portion of the experiment design surface, which indicates the sequence in which the models were created:</span></span>  

![][6]  

<span data-ttu-id="9a40d-185">*圖 8：在 Machine Learning Studio 中建立模型*</span><span class="sxs-lookup"><span data-stu-id="9a40d-185">*Figure 8: Creating models in Machine Learning Studio*</span></span>  

### <a name="scoring-methods"></a><span data-ttu-id="9a40d-186">評分方法</span><span class="sxs-lookup"><span data-stu-id="9a40d-186">Scoring methods</span></span>
<span data-ttu-id="9a40d-187">我們使用已標示的訓練資料集來對這四種模型評分。</span><span class="sxs-lookup"><span data-stu-id="9a40d-187">We scored the four models by using a labeled training dataset.</span></span>  

<span data-ttu-id="9a40d-188">我們也提交評分資料集給使用 SAS Enterprise Miner 12 桌上型版本建立的比較模型。</span><span class="sxs-lookup"><span data-stu-id="9a40d-188">We also submitted the scoring dataset to a comparable model built by using the desktop edition of SAS Enterprise Miner 12.</span></span> <span data-ttu-id="9a40d-189">我們測量 SAS 模型和所有四個 Machine Learning Studio 模型的正確性。</span><span class="sxs-lookup"><span data-stu-id="9a40d-189">We measured the accuracy of the SAS model and all four Machine Learning Studio models.</span></span>  

## <a name="results"></a><span data-ttu-id="9a40d-190">結果</span><span class="sxs-lookup"><span data-stu-id="9a40d-190">Results</span></span>
<span data-ttu-id="9a40d-191">在本節中，我們根據評分資料集，提出關於模型正確性的調查結果。</span><span class="sxs-lookup"><span data-stu-id="9a40d-191">In this section, we present our findings about the accuracy of the models, based on the scoring dataset.</span></span>  

### <a name="accuracy-and-precision-of-scoring"></a><span data-ttu-id="9a40d-192">評分的正確性和準確度</span><span class="sxs-lookup"><span data-stu-id="9a40d-192">Accuracy and precision of scoring</span></span>
<span data-ttu-id="9a40d-193">一般而言，在 Azure Machine Learning 中實作的正確性低於 SAS 大約 10-15% (曲線下面積或 AUC)。</span><span class="sxs-lookup"><span data-stu-id="9a40d-193">Generally, the implementation in Azure Machine Learning is behind SAS in accuracy by about 10-15% (Area Under Curve or AUC).</span></span>  

<span data-ttu-id="9a40d-194">不過，客戶流失中最重要的度量是分類誤判率；亦即，在分類器所預測排名前 N 位的流失客戶中，哪些實際上並 **沒有** 流失，但仍享受到特殊待遇？</span><span class="sxs-lookup"><span data-stu-id="9a40d-194">However, the most important metric in churn is the misclassification rate: that is, of the top N churners as predicted by the classifier, which of them actually did **not** churn, and yet received special treatment?</span></span> <span data-ttu-id="9a40d-195">下圖比較所有模型的此項分類誤判率：</span><span class="sxs-lookup"><span data-stu-id="9a40d-195">The following diagram compares this misclassification rate for all the models:</span></span>  

![][7]

<span data-ttu-id="9a40d-196">*圖 9：Passau 原型曲線下面積*</span><span class="sxs-lookup"><span data-stu-id="9a40d-196">*Figure 9: Passau prototype area under curve*</span></span>

### <a name="using-auc-to-compare-results"></a><span data-ttu-id="9a40d-197">使用 AUC 來比較結果</span><span class="sxs-lookup"><span data-stu-id="9a40d-197">Using AUC to compare results</span></span>
<span data-ttu-id="9a40d-198">曲線下面積 (AUC) 是一種度量，代表正負母體的計分分布之間「可分性」  的總體量測。</span><span class="sxs-lookup"><span data-stu-id="9a40d-198">Area Under Curve (AUC) is a metric that represents a global measure of *separability* between the distributions of scores for positive and negative populations.</span></span> <span data-ttu-id="9a40d-199">它類似傳統的「受測者操作特徵」(ROC) 圖形，但一項重要的差別是 AUC 度量不需要您選擇臨界值。</span><span class="sxs-lookup"><span data-stu-id="9a40d-199">It is similar to the traditional Receiver Operator Characteristic (ROC) graph, but one important difference is that the AUC metric does not require you to choose a threshold value.</span></span> <span data-ttu-id="9a40d-200">它會總結「所有」  可能選擇的結果。</span><span class="sxs-lookup"><span data-stu-id="9a40d-200">Instead, it summarizes the results over **all** possible choices.</span></span> <span data-ttu-id="9a40d-201">反之，傳統 ROC 圖會在垂直軸顯示正比率，在水平軸顯示誤判率，而分類臨界值會變化。</span><span class="sxs-lookup"><span data-stu-id="9a40d-201">In contrast, the traditional ROC graph shows the positive rate on the vertical axis and the false positive rate on the horizontal axis, and the classification threshold varies.</span></span>   

<span data-ttu-id="9a40d-202">AUC 通常用來判斷不同演算法 (或不同系統) 是否有用處，因為它可根據 AUC 值來比較模型。</span><span class="sxs-lookup"><span data-stu-id="9a40d-202">AUC is generally used as a measure of worth for different algorithms (or different systems) because it allows models to be compared by means of their AUC values.</span></span> <span data-ttu-id="9a40d-203">這在如氣象和生物科學等領域是常用的方法。</span><span class="sxs-lookup"><span data-stu-id="9a40d-203">This is a popular approach in industries such as meteorology and biosciences.</span></span> <span data-ttu-id="9a40d-204">因此，AUC 是一種評估分類器表現的普遍工具。</span><span class="sxs-lookup"><span data-stu-id="9a40d-204">Thus, AUC represents a popular tool for assessing classifier performance.</span></span>  

### <a name="comparing-misclassification-rates"></a><span data-ttu-id="9a40d-205">比較分類誤判率</span><span class="sxs-lookup"><span data-stu-id="9a40d-205">Comparing misclassification rates</span></span>
<span data-ttu-id="9a40d-206">我們使用大約 8,000 個訂用帳戶的 CRM 資料，在相關資料集上比較分類誤判率。</span><span class="sxs-lookup"><span data-stu-id="9a40d-206">We compared the misclassification rates on the dataset in question by using the CRM data of approximately 8,000 subscriptions.</span></span>  

* <span data-ttu-id="9a40d-207">SAS 分類誤判率為 10-15%。</span><span class="sxs-lookup"><span data-stu-id="9a40d-207">The SAS misclassification rate was 10-15%.</span></span>
* <span data-ttu-id="9a40d-208">Machine Learning Studio 對排名前 200-300 位流失客戶的分類誤判率為 15-20%。</span><span class="sxs-lookup"><span data-stu-id="9a40d-208">The Machine Learning Studio misclassification rate was 15-20% for the top 200-300 churners.</span></span>  

<span data-ttu-id="9a40d-209">在電信業中，只提供特別禮遇或其他特殊待遇給最可能流失的客戶是很重要的。</span><span class="sxs-lookup"><span data-stu-id="9a40d-209">In the telecommunications industry, it is important to address only those customers who have the highest risk to churn by offering them a concierge service or other special treatment.</span></span> <span data-ttu-id="9a40d-210">在這方面，Machine Learning Studio 實作所獲得的成果與 SAS 模型旗鼓相當。</span><span class="sxs-lookup"><span data-stu-id="9a40d-210">In that respect, the Machine Learning Studio implementation achieves results on par with the SAS model.</span></span>  

<span data-ttu-id="9a40d-211">基於同樣的理由，正確性比準確度更重要，因為我們最在意的是正確地將可能流失的客戶分類。</span><span class="sxs-lookup"><span data-stu-id="9a40d-211">By the same token, accuracy is more important than precision because we are mostly interested in correctly classifying potential churners.</span></span>  

<span data-ttu-id="9a40d-212">下圖取自於維基百科，以生動、簡單明瞭的圖形來描述其中的關聯性：</span><span class="sxs-lookup"><span data-stu-id="9a40d-212">The following diagram from Wikipedia depicts the relationship in a lively, easy-to-understand graphic:</span></span>  

![][8]

<span data-ttu-id="9a40d-213">*圖 10：正確性和準確度之間的取捨*</span><span class="sxs-lookup"><span data-stu-id="9a40d-213">*Figure 10: Tradeoff between accuracy and precision*</span></span>

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a><span data-ttu-id="9a40d-214">推進式決策樹模型的正確性與準確度結果</span><span class="sxs-lookup"><span data-stu-id="9a40d-214">Accuracy and precision results for boosted decision tree model</span></span>
<span data-ttu-id="9a40d-215">下列圖表針對推進式決策樹模型，列出利用 Machine Learning Studio 原型來評分所得出的原始結果，剛好就是四種模型中最正確的模型：</span><span class="sxs-lookup"><span data-stu-id="9a40d-215">The following chart displays the raw results from scoring using the Machine Learning prototype for the boosted decision tree model, which happens to be the most accurate among the four models:</span></span>  

![][9]

<span data-ttu-id="9a40d-216">*圖 11：推進式決策樹模型的特性*</span><span class="sxs-lookup"><span data-stu-id="9a40d-216">*Figure 11: Boosted decision tree model characteristics*</span></span>

## <a name="performance-comparison"></a><span data-ttu-id="9a40d-217">表現比較</span><span class="sxs-lookup"><span data-stu-id="9a40d-217">Performance comparison</span></span>
<span data-ttu-id="9a40d-218">我們使用 Machine Learning Studio 模型和一個以 SAS Enterprise Miner 12.1 桌上型版本建立的比較模型，比較資料評分的速度。</span><span class="sxs-lookup"><span data-stu-id="9a40d-218">We compared the speed at which data was scored using the Machine Learning Studio models and a comparable model created by using the desktop edition of SAS Enterprise Miner 12.1.</span></span>  

<span data-ttu-id="9a40d-219">下表總結演算法的表現：</span><span class="sxs-lookup"><span data-stu-id="9a40d-219">The following table summarizes the performance of the algorithms:</span></span>  

<span data-ttu-id="9a40d-220">*表 1.演算法的整體表現 (正確性)*</span><span class="sxs-lookup"><span data-stu-id="9a40d-220">*Table 1. General performance (accuracy) of the algorithms*</span></span>

| <span data-ttu-id="9a40d-221">LR</span><span class="sxs-lookup"><span data-stu-id="9a40d-221">LR</span></span> | <span data-ttu-id="9a40d-222">BT</span><span class="sxs-lookup"><span data-stu-id="9a40d-222">BT</span></span> | <span data-ttu-id="9a40d-223">AP</span><span class="sxs-lookup"><span data-stu-id="9a40d-223">AP</span></span> | <span data-ttu-id="9a40d-224">SVM</span><span class="sxs-lookup"><span data-stu-id="9a40d-224">SVM</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9a40d-225">平均模型</span><span class="sxs-lookup"><span data-stu-id="9a40d-225">Average Model</span></span> |<span data-ttu-id="9a40d-226">最佳模型</span><span class="sxs-lookup"><span data-stu-id="9a40d-226">The Best Model</span></span> |<span data-ttu-id="9a40d-227">表現不佳</span><span class="sxs-lookup"><span data-stu-id="9a40d-227">Underperforming</span></span> |<span data-ttu-id="9a40d-228">平均模型</span><span class="sxs-lookup"><span data-stu-id="9a40d-228">Average Model</span></span> |

<span data-ttu-id="9a40d-229">在執行速度方面，裝載於 Machine Learning Studio 中的模型比 SAS 快 15-25%，但正確性大致相等。</span><span class="sxs-lookup"><span data-stu-id="9a40d-229">The models hosted in Machine Learning Studio outperformed SAS by 15-25% for speed of execution, but accuracy was largely on par.</span></span>  

## <a name="discussion-and-recommendations"></a><span data-ttu-id="9a40d-230">討論與建議</span><span class="sxs-lookup"><span data-stu-id="9a40d-230">Discussion and recommendations</span></span>
<span data-ttu-id="9a40d-231">在電信業中，已出現許多作法來分析客戶流失，包括：</span><span class="sxs-lookup"><span data-stu-id="9a40d-231">In the telecommunications industry, several practices have emerged to analyze churn, including:</span></span>  

* <span data-ttu-id="9a40d-232">導出四個基本類別的度量：</span><span class="sxs-lookup"><span data-stu-id="9a40d-232">Derive metrics for four fundamental categories:</span></span>
  * <span data-ttu-id="9a40d-233">**實體 (例如訂用帳戶)**。</span><span class="sxs-lookup"><span data-stu-id="9a40d-233">**Entity (for example, a subscription)**.</span></span> <span data-ttu-id="9a40d-234">提供訂用帳戶及/或客戶 (客源流失主題的對象) 的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="9a40d-234">Provision basic information about the subscription and/or customer that is the subject of churn.</span></span>
  * <span data-ttu-id="9a40d-235">**活動**。</span><span class="sxs-lookup"><span data-stu-id="9a40d-235">**Activity**.</span></span> <span data-ttu-id="9a40d-236">取得與實體相關的所有可能使用資訊，例如登入數目。</span><span class="sxs-lookup"><span data-stu-id="9a40d-236">Obtain all possible usage information that is related to the entity, for example, the number of logins.</span></span>
  * <span data-ttu-id="9a40d-237">**客戶支援**。</span><span class="sxs-lookup"><span data-stu-id="9a40d-237">**Customer support**.</span></span> <span data-ttu-id="9a40d-238">從客戶支援記錄中取得資訊，指出訂用帳戶是否有問題或曾經與客戶支援的互動。</span><span class="sxs-lookup"><span data-stu-id="9a40d-238">Harvest information from customer support logs to indicate whether the subscription had issues or interactions with customer support.</span></span>
  * <span data-ttu-id="9a40d-239">**競爭性和商務資料**。</span><span class="sxs-lookup"><span data-stu-id="9a40d-239">**Competitive and business data**.</span></span> <span data-ttu-id="9a40d-240">取得與客戶有關的任何可能資訊 (例如可能無法取得或難以追蹤)。</span><span class="sxs-lookup"><span data-stu-id="9a40d-240">Obtain any information possible about the customer (for example, can be unavailable or hard to track).</span></span>
* <span data-ttu-id="9a40d-241">使用重要性來引導特徵選擇。</span><span class="sxs-lookup"><span data-stu-id="9a40d-241">Use importance to drive feature selection.</span></span> <span data-ttu-id="9a40d-242">這意味著推進式決策樹模型一定是可行的方法。</span><span class="sxs-lookup"><span data-stu-id="9a40d-242">This implies that the boosted decision tree model is always a promising approach.</span></span>  

<span data-ttu-id="9a40d-243">使用這四個類別製造出一種假象，讓人誤以為簡單的「確定性」  分析方法 (根據在每個類別的合理因素上形成的跡象) 就足以發現有流失風險的客戶。</span><span class="sxs-lookup"><span data-stu-id="9a40d-243">The use of these four categories creates the illusion that a simple *deterministic* approach, based on indexes formed on reasonable factors per category, should suffice to identify customers at risk for churn.</span></span> <span data-ttu-id="9a40d-244">可惜，雖然這種想法看似可行，但卻是一種誤解。</span><span class="sxs-lookup"><span data-stu-id="9a40d-244">Unfortunately, although this notion seems plausible, it is a false understanding.</span></span> <span data-ttu-id="9a40d-245">原因在於客戶流失是一種短暫效應，而造成客戶流失的因素通常是暫時狀態。</span><span class="sxs-lookup"><span data-stu-id="9a40d-245">The reason is that churn is a temporal effect and the factors contributing to churn are usually in transient states.</span></span> <span data-ttu-id="9a40d-246">今天導致客戶想要離開的原因，到了明天可能就不一樣，且六個月之後一定不同。</span><span class="sxs-lookup"><span data-stu-id="9a40d-246">What leads a customer to consider leaving today might be different tomorrow, and it certainly will be different six months from now.</span></span> <span data-ttu-id="9a40d-247">因此，有必要使用「機率」  模型。</span><span class="sxs-lookup"><span data-stu-id="9a40d-247">Therefore, a *probabilistic* model is a necessity.</span></span>  

<span data-ttu-id="9a40d-248">公司經常忽略這項重要的觀察，通常寧可選擇商業智慧導向的方法而不做分析，主要是因為前者較吸引人，直接了當就自動完成。</span><span class="sxs-lookup"><span data-stu-id="9a40d-248">This important observation is often overlooked in business, which generally prefers a business intelligence-oriented approach to analytics, mostly because it is an easier sell and admits straightforward automation.</span></span>  

<span data-ttu-id="9a40d-249">然而，採用 Machine Learning Studio 進行自助式分析的價值在於，這四種資訊 (依部門分類) 將成為在客戶流失方面進行機器學習時的寶貴資料來源。</span><span class="sxs-lookup"><span data-stu-id="9a40d-249">However, the promise of self-service analytics by using Machine Learning Studio is that the four categories of information, graded by division or department, become a valuable source for machine learning about churn.</span></span>  

<span data-ttu-id="9a40d-250">Azure Machine Learning 中另一項吸引人的功能是可以將自訂模組加入既有預先定義之模組的儲存機制中。</span><span class="sxs-lookup"><span data-stu-id="9a40d-250">Another exciting capability coming in Azure Machine Learning is the ability to add a custom module to the repository of predefined modules that are already available.</span></span> <span data-ttu-id="9a40d-251">這項功能基本上讓人有機會針對垂直市場選取程式庫和建立範本。</span><span class="sxs-lookup"><span data-stu-id="9a40d-251">This capability, essentially, creates an opportunity to select libraries and create templates for vertical markets.</span></span> <span data-ttu-id="9a40d-252">這是 Azure Machine Learning 在市場中脫穎而出的一項重要利器。</span><span class="sxs-lookup"><span data-stu-id="9a40d-252">It is an important differentiator of Azure Machine Learning in the market place.</span></span>  

<span data-ttu-id="9a40d-253">我們希望未來繼續探討這個主題，特別是關於巨量資料分析。</span><span class="sxs-lookup"><span data-stu-id="9a40d-253">We hope to continue this topic in the future, especially related to big data analytics.</span></span>
  

## <a name="conclusion"></a><span data-ttu-id="9a40d-254">結論</span><span class="sxs-lookup"><span data-stu-id="9a40d-254">Conclusion</span></span>
<span data-ttu-id="9a40d-255">本文說明一套實用的方法，採取通用的架構來處理客戶流失這個普遍的問題。</span><span class="sxs-lookup"><span data-stu-id="9a40d-255">This paper describes a sensible approach to tackling the common problem of customer churn by using a generic framework.</span></span> <span data-ttu-id="9a40d-256">我們採用原型來給模型評分，並使用 Azure Machine Learning 來實作。</span><span class="sxs-lookup"><span data-stu-id="9a40d-256">We considered a prototype for scoring models and implemented it by using Azure Machine Learning.</span></span> <span data-ttu-id="9a40d-257">最後，我們依據 SAS 中可比較的演算法，評估原型解決方案的正確性和表現。</span><span class="sxs-lookup"><span data-stu-id="9a40d-257">Finally, we assessed the accuracy and performance of the prototype solution with regard to comparable algorithms in SAS.</span></span>  

<span data-ttu-id="9a40d-258">**其他資訊：**</span><span class="sxs-lookup"><span data-stu-id="9a40d-258">**For more information:**</span></span>  

<span data-ttu-id="9a40d-259">本文對您有幫助嗎？</span><span class="sxs-lookup"><span data-stu-id="9a40d-259">Did this paper help you?</span></span> <span data-ttu-id="9a40d-260">請提供意見給我們。</span><span class="sxs-lookup"><span data-stu-id="9a40d-260">Please give us your feedback.</span></span> <span data-ttu-id="9a40d-261">請以 1 (非常差) 到 5 (非常好) 來評分，告訴我們您對本文有何評價，以及為何這樣評分？</span><span class="sxs-lookup"><span data-stu-id="9a40d-261">Tell us on a scale of 1 (poor) to 5 (excellent), how would you rate this paper and why have you given it this rating?</span></span> <span data-ttu-id="9a40d-262">例如：</span><span class="sxs-lookup"><span data-stu-id="9a40d-262">For example:</span></span>  

* <span data-ttu-id="9a40d-263">您給予較高評價是因為範例良好、螢幕擷取畫面精美、文章論述清楚，還是別有原因？</span><span class="sxs-lookup"><span data-stu-id="9a40d-263">Are you rating it high due to having good examples, excellent screen shots, clear writing, or another reason?</span></span>
* <span data-ttu-id="9a40d-264">您給予較低評價是因為範例不當、螢幕擷取畫面模糊，還是文章論述含糊不清？</span><span class="sxs-lookup"><span data-stu-id="9a40d-264">Are you rating it low due to poor examples, fuzzy screen shots, or unclear writing?</span></span>  

<span data-ttu-id="9a40d-265">這些意見將有助於改善我們所發表的白皮書品質。</span><span class="sxs-lookup"><span data-stu-id="9a40d-265">This feedback will help us improve the quality of white papers we release.</span></span>   

<span data-ttu-id="9a40d-266">[傳送意見](mailto:sqlfback@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="9a40d-266">[Send feedback](mailto:sqlfback@microsoft.com).</span></span>
 

## <a name="references"></a><span data-ttu-id="9a40d-267">參考</span><span class="sxs-lookup"><span data-stu-id="9a40d-267">References</span></span>
<span data-ttu-id="9a40d-268">[1] Predictive Analytics: Beyond the Predictions (預測性分析：超出預測)，W. McKnight，資訊管理，2011 年 7 月/8 月，第 18-20 頁。</span><span class="sxs-lookup"><span data-stu-id="9a40d-268">[1] Predictive Analytics: Beyond the Predictions, W. McKnight, Information Management, July/August 2011, p.18-20.</span></span>  

<span data-ttu-id="9a40d-269">[2] 維基百科文章：[正確性與準確度](http://en.wikipedia.org/wiki/Accuracy_and_precision)</span><span class="sxs-lookup"><span data-stu-id="9a40d-269">[2] Wikipedia article: [Accuracy and precision](http://en.wikipedia.org/wiki/Accuracy_and_precision)</span></span>

<span data-ttu-id="9a40d-270">[3] [CRISP-DM 1.0：資料採礦逐步指南](http://www.the-modeling-agency.com/crisp-dm.pdf)</span><span class="sxs-lookup"><span data-stu-id="9a40d-270">[3] [CRISP-DM 1.0: Step-by-Step Data Mining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf)</span></span>   

<span data-ttu-id="9a40d-271">[4] [巨量資料行銷：更有效地吸引您的客戶和促進價值](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)</span><span class="sxs-lookup"><span data-stu-id="9a40d-271">[4] [Big Data Marketing: Engage Your Customers More Effectively and Drive Value](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)</span></span>

<span data-ttu-id="9a40d-272">[5] [Cortana Intelligence 資源庫](http://gallery.cortanaintelligence.com/)中的[電信公司客戶流失模型範本](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5)</span><span class="sxs-lookup"><span data-stu-id="9a40d-272">[5] [Telco churn model template](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)</span></span> 
 

## <a name="appendix"></a><span data-ttu-id="9a40d-273">附錄</span><span class="sxs-lookup"><span data-stu-id="9a40d-273">Appendix</span></span>
![][10]

<span data-ttu-id="9a40d-274">*圖 12：客戶流失原型的簡報擷取畫面*</span><span class="sxs-lookup"><span data-stu-id="9a40d-274">*Figure 12: Snapshot of a presentation on churn prototype*</span></span>

<span data-ttu-id="9a40d-275">[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png</span><span class="sxs-lookup"><span data-stu-id="9a40d-275">[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png</span></span>
<span data-ttu-id="9a40d-276">[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png</span><span class="sxs-lookup"><span data-stu-id="9a40d-276">[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png</span></span>
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
