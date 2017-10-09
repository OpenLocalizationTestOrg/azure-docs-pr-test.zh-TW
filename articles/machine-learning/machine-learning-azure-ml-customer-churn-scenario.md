---
title: "客戶變換使用機器學習 aaaAnalyzing |Microsoft 文件"
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
ms.openlocfilehash: 070e6a2ebe4f2fe439a42ffe1a3fa9d6d3788d62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="analyzing-customer-churn-by-using-azure-machine-learning"></a><span data-ttu-id="9cac4-103">使用 Azure Machine Learning 分析客戶流失</span><span class="sxs-lookup"><span data-stu-id="9cac4-103">Analyzing Customer Churn by using Azure Machine Learning</span></span>
## <a name="overview"></a><span data-ttu-id="9cac4-104">概觀</span><span class="sxs-lookup"><span data-stu-id="9cac4-104">Overview</span></span>
<span data-ttu-id="9cac4-105">本文提供使用 Azure Machine Learning 建置客戶流失分析專案的參考實作。</span><span class="sxs-lookup"><span data-stu-id="9cac4-105">This article presents a reference implementation of a customer churn analysis project that is built by using Azure Machine Learning.</span></span> <span data-ttu-id="9cac4-106">在本文中，我們會討論而加以進行歷程解決的工業客戶變換的 hello 問題的相關聯的一般模型。</span><span class="sxs-lookup"><span data-stu-id="9cac4-106">In this article, we discuss associated generic models for holistically solving hello problem of industrial customer churn.</span></span> <span data-ttu-id="9cac4-107">我們也會測量 hello 建立使用機器學習模型的精確度，我們評估進一步開發之用的說明。</span><span class="sxs-lookup"><span data-stu-id="9cac4-107">We also measure hello accuracy of models that are built by using Machine Learning, and we assess directions for further development.</span></span>  

### <a name="acknowledgements"></a><span data-ttu-id="9cac4-108">通知</span><span class="sxs-lookup"><span data-stu-id="9cac4-108">Acknowledgements</span></span>
<span data-ttu-id="9cac4-109">這項實驗是由 Microsoft 的首席資料科學家 Serge Berger 和 Microsoft Azure Machine Learning 的前產品經理 Roger Barga 共同開發和測試。</span><span class="sxs-lookup"><span data-stu-id="9cac4-109">This experiment was developed and tested by Serge Berger, Principal Data Scientist at Microsoft, and Roger Barga, formerly Product Manager for Microsoft Azure Machine Learning.</span></span> <span data-ttu-id="9cac4-110">hello Azure 文件小組非常感謝認可其專業知識，並感謝共用這份技術白皮書。</span><span class="sxs-lookup"><span data-stu-id="9cac4-110">hello Azure documentation team gratefully acknowledges their expertise and thanks them for sharing this white paper.</span></span>

> [!NOTE]
> <span data-ttu-id="9cac4-111">使用此實驗的 hello 資料不公開可用。</span><span class="sxs-lookup"><span data-stu-id="9cac4-111">hello data used for this experiment is not publicly available.</span></span> <span data-ttu-id="9cac4-112">如 toobuild 機器學習的變換分析模型的方式範例，請參閱：[零售變換模型範本](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1)中[Cortana 智慧組件庫](http://gallery.cortanaintelligence.com/)</span><span class="sxs-lookup"><span data-stu-id="9cac4-112">For an example of how toobuild a machine learning model for churn analysis, see: [Retail churn model template](https://gallery.cortanaintelligence.com/Collection/Retail-Customer-Churn-Prediction-Template-1) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)</span></span>
> 
> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="hello-problem-of-customer-churn"></a><span data-ttu-id="9cac4-113">客戶變換的 hello 問題</span><span class="sxs-lookup"><span data-stu-id="9cac4-113">hello problem of customer churn</span></span>
<span data-ttu-id="9cac4-114">企業和所有的企業磁區 hello 消費者市場中有 toodeal 與變換。</span><span class="sxs-lookup"><span data-stu-id="9cac4-114">Businesses in hello consumer market and in all enterprise sectors have toodeal with churn.</span></span> <span data-ttu-id="9cac4-115">有時，客戶流失太多會影響政策決定。</span><span class="sxs-lookup"><span data-stu-id="9cac4-115">Sometimes churn is excessive and influences policy decisions.</span></span> <span data-ttu-id="9cac4-116">hello 傳統方案 toopredict 高傾向 churners 並解決透過指引服務，行銷活動，或藉由套用特殊 dispensations 其需求。</span><span class="sxs-lookup"><span data-stu-id="9cac4-116">hello traditional solution is toopredict high-propensity churners and address their needs via a concierge service, marketing campaigns, or by applying special dispensations.</span></span> <span data-ttu-id="9cac4-117">從業界 tooindustry 和甚至特定取用者叢集 tooanother 一個產業 （例如，電信） 內，這些方法可能會不同。</span><span class="sxs-lookup"><span data-stu-id="9cac4-117">These approaches can vary from industry tooindustry and even from a particular consumer cluster tooanother within one industry (for example, telecommunications).</span></span>

<span data-ttu-id="9cac4-118">hello 共同因素是企業需要 toominimize 這些特殊的客戶保留投入時間。</span><span class="sxs-lookup"><span data-stu-id="9cac4-118">hello common factor is that businesses need toominimize these special customer retention efforts.</span></span> <span data-ttu-id="9cac4-119">因此，自然方法會 tooscore hello 機率變換每位客戶，解決 hello 前 n 個項目。</span><span class="sxs-lookup"><span data-stu-id="9cac4-119">Thus, a natural methodology would be tooscore every customer with hello probability of churn and address hello top N ones.</span></span> <span data-ttu-id="9cac4-120">hello 最佳客戶可能 hello 最有利潤的;例如，在更複雜的情況下，收益函式會採用在 hello 選取特殊 dispensation 候選項目期間。</span><span class="sxs-lookup"><span data-stu-id="9cac4-120">hello top customers might be hello most profitable ones; for example, in more sophisticated scenarios, a profit function is employed during hello selection of candidates for special dispensation.</span></span> <span data-ttu-id="9cac4-121">不過，這些考量是只包含 hello 變換處理的整體策略的一部分。</span><span class="sxs-lookup"><span data-stu-id="9cac4-121">However, these considerations are only a part of hello holistic strategy for dealing with churn.</span></span> <span data-ttu-id="9cac4-122">企業也有到帳戶風險 （和相關聯的風險承受度） tootake hello 層級和 hello 介入和擬真客戶區隔的成本。</span><span class="sxs-lookup"><span data-stu-id="9cac4-122">Businesses also have tootake into account risk (and associated risk tolerance), hello level and cost of hello intervention, and plausible customer segmentation.</span></span>  

## <a name="industry-outlook-and-approaches"></a><span data-ttu-id="9cac4-123">產業展望和作法</span><span class="sxs-lookup"><span data-stu-id="9cac4-123">Industry outlook and approaches</span></span>
<span data-ttu-id="9cac4-124">駕輕就熟地處理客戶流失是成熟產業的一項特徵。</span><span class="sxs-lookup"><span data-stu-id="9cac4-124">Sophisticated handling of churn is a sign of a mature industry.</span></span> <span data-ttu-id="9cac4-125">hello 典型的範例 hello 電信業界位置是 「 訂閱者 」 從一個提供者 tooanother 已知的 toofrequently 交換器。</span><span class="sxs-lookup"><span data-stu-id="9cac4-125">hello classic example is hello telecommunications industry where subscribers are known toofrequently switch from one provider tooanother.</span></span> <span data-ttu-id="9cac4-126">這種志願性流失是最主要問題所在。</span><span class="sxs-lookup"><span data-stu-id="9cac4-126">This voluntary churn is a prime concern.</span></span> <span data-ttu-id="9cac4-127">此外，提供者已經累積相當了解有關*變換驅動程式*，而該磁碟機客戶 tooswitch 是 hello 因素。</span><span class="sxs-lookup"><span data-stu-id="9cac4-127">Moreover, providers have accumulated significant knowledge about *churn drivers*, which are hello factors that drive customers tooswitch.</span></span>

<span data-ttu-id="9cac4-128">比方說，手持式裝置選擇會是已知的 hello 行動電話公司中變換驅動程式。</span><span class="sxs-lookup"><span data-stu-id="9cac4-128">For instance, handset or device choice is a well-known driver of churn in hello mobile phone business.</span></span> <span data-ttu-id="9cac4-129">如此一來，熱門原則是新的 「 訂閱者 」 和充電完整價格 tooexisting 升級客戶話筒 toosubsidize hello 價格。</span><span class="sxs-lookup"><span data-stu-id="9cac4-129">As a result, a popular policy is toosubsidize hello price of a handset for new subscribers and charging a full price tooexisting customers for an upgrade.</span></span> <span data-ttu-id="9cac4-130">在過去，此原則導致 toocustomers 跳動從一個提供者 tooanother tooget 新折扣，亦有提示您提供者 toorefine 其策略。</span><span class="sxs-lookup"><span data-stu-id="9cac4-130">Historically, this policy has led toocustomers hopping from one provider tooanother tooget a new discount, which in turn, has prompted providers toorefine their strategies.</span></span>

<span data-ttu-id="9cac4-131">手機產品日新月異，是造成以最新手機款式為主的客戶流失模型迅速失效的一項因素。</span><span class="sxs-lookup"><span data-stu-id="9cac4-131">High volatility in handset offerings is a factor that very quickly invalidates models of churn that are based on current handset models.</span></span> <span data-ttu-id="9cac4-132">此外，行動電話不是只有電信裝置。它們也方式陳述式 （請考慮 hello iPhone），而且這些社交預測量是一般的電信資料集的 hello 範圍外。</span><span class="sxs-lookup"><span data-stu-id="9cac4-132">Additionally, mobile phones are not only telecommunication devices; they are also fashion statements (consider hello iPhone), and these social predictors are outside hello scope of regular telecommunications data sets.</span></span>

<span data-ttu-id="9cac4-133">hello 用於模型化的最後結果就是您無法只藉由消除變換的已知的原因設計音效的原則。</span><span class="sxs-lookup"><span data-stu-id="9cac4-133">hello net result for modeling is that you cannot devise a sound policy simply by eliminating known reasons for churn.</span></span> <span data-ttu-id="9cac4-134">事實上，持續性的模型建構策略是 **必要的**，包括量化類別變項的傳統模型 (例如決策樹)。</span><span class="sxs-lookup"><span data-stu-id="9cac4-134">In fact, a continuous modeling strategy, including classic models that quantify categorical variables (such as decision trees), is **mandatory**.</span></span>

<span data-ttu-id="9cac4-135">客戶使用大型資料集，組織執行巨量資料分析 （尤其是，根據巨量資料變換偵測） 為有效的方法 toohello 問題。</span><span class="sxs-lookup"><span data-stu-id="9cac4-135">Using big data sets on their customers, organizations are performing big data analytics (in particular, churn detection based on big data) as an effective approach toohello problem.</span></span> <span data-ttu-id="9cac4-136">您可以找到更多關於變換 hello 建議 ETL > 一節中的 hello 巨量資料方法 toohello 問題。</span><span class="sxs-lookup"><span data-stu-id="9cac4-136">You can find more about hello big data approach toohello problem of churn in hello Recommendations on ETL section.</span></span>  

## <a name="methodology-toomodel-customer-churn"></a><span data-ttu-id="9cac4-137">方法 toomodel 客戶變換</span><span class="sxs-lookup"><span data-stu-id="9cac4-137">Methodology toomodel customer churn</span></span>
<span data-ttu-id="9cac4-138">常見解決問題的程序 toosolve 客戶變換描繪數字 1-3:</span><span class="sxs-lookup"><span data-stu-id="9cac4-138">A common problem-solving process toosolve customer churn is depicted in Figures 1-3:</span></span>  

1. <span data-ttu-id="9cac4-139">風險模型可讓您 tooconsider 動作如何影響機率和風險。</span><span class="sxs-lookup"><span data-stu-id="9cac4-139">A risk model allows you tooconsider how actions affect probability and risk.</span></span>
2. <span data-ttu-id="9cac4-140">操作模型可讓您 tooconsider hello 介入的程度可能會影響 hello 機率變換 hello 數量及客戶存留時間值 (CLV) 的方式。</span><span class="sxs-lookup"><span data-stu-id="9cac4-140">An intervention model allows you tooconsider how hello level of intervention could affect hello probability of churn and hello amount of customer lifetime value (CLV).</span></span>
3. <span data-ttu-id="9cac4-141">這項分析本身是擴大的 tooa 主動式行銷活動的目標客戶區段 toodeliver hello 最佳優惠的 tooa 質化分析。</span><span class="sxs-lookup"><span data-stu-id="9cac4-141">This analysis lends itself tooa qualitative analysis that is escalated tooa proactive marketing campaign that targets customer segments toodeliver hello optimal offer.</span></span>  

![][1]

<span data-ttu-id="9cac4-142">這種預視的方法是最佳方式 tootreat 變換 hello，但它隨附複雜度： 我們有 toodevelop hello 模型之間多模型原型和追蹤相依性。</span><span class="sxs-lookup"><span data-stu-id="9cac4-142">This forward looking approach is hello best way tootreat churn, but it comes with complexity: we have toodevelop a multi-model archetype and trace dependencies between hello models.</span></span> <span data-ttu-id="9cac4-143">可以封裝 hello 模型間的互動，hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="9cac4-143">hello interaction among models can be encapsulated as shown in hello following diagram:</span></span>  

![][2]

<span data-ttu-id="9cac4-144">*圖 4：多模型整合原型*</span><span class="sxs-lookup"><span data-stu-id="9cac4-144">*Figure 4: Unified multi-model archetype*</span></span>  

<span data-ttu-id="9cac4-145">Hello 模型之間的互動是索引鍵，如果我們 toodeliver 全面性方法 toocustomer 保留。</span><span class="sxs-lookup"><span data-stu-id="9cac4-145">Interaction between hello models is key if we are toodeliver a holistic approach toocustomer retention.</span></span> <span data-ttu-id="9cac4-146">每一個模型一定隨著時間逐漸降低。因此，hello 架構是隱含的迴圈 (類似 toohello 原型 hello CRISP-DM 資料採礦的標準，來設定 [***3***])。</span><span class="sxs-lookup"><span data-stu-id="9cac4-146">Each model necessarily degrades over time; therefore, hello architecture is an implicit loop (similar toohello archetype set by hello CRISP-DM data mining standard, [***3***]).</span></span>  

<span data-ttu-id="9cac4-147">hello 風險決策行銷分割/分解的整個週期仍然是通用的結構，也就是適用的 toomany 商務問題。</span><span class="sxs-lookup"><span data-stu-id="9cac4-147">hello overall cycle of risk-decision-marketing segmentation/decomposition is still a generalized structure, which is applicable toomany business problems.</span></span> <span data-ttu-id="9cac4-148">變換分析是只是這個群組的問題是強式代表值，因為它所表現的簡化預測方案不允許有複雜的商務問題的所有 hello 特性。</span><span class="sxs-lookup"><span data-stu-id="9cac4-148">Churn analysis is simply a strong representative of this group of problems because it exhibits all hello traits of a complex business problem that does not allow a simplified predictive solution.</span></span> <span data-ttu-id="9cac4-149">hello 社交 hello 現代方法 toochurn 層面不特別以反白顯示 hello 方法，但 hello 社交層面封裝在 hello 模型原型，因為它們可以在任何模型。</span><span class="sxs-lookup"><span data-stu-id="9cac4-149">hello social aspects of hello modern approach toochurn are not particularly highlighted in hello approach, but hello social aspects are encapsulated in hello modeling archetype, as they would be in any model.</span></span>  

<span data-ttu-id="9cac4-150">此處增添的一項重要部分是巨量資料分析。</span><span class="sxs-lookup"><span data-stu-id="9cac4-150">An interesting addition here is big data analytics.</span></span> <span data-ttu-id="9cac4-151">現今的電信和零售企業收集徹底瞭解他們的客戶的資料和我們可以輕鬆地預測該 hello 需要針對多模型連線將會變成一般趨勢，指定新趨勢，例如 hello 物聯網和無所不在的裝置，可讓多個層級 tooemploy 商務智慧方案。</span><span class="sxs-lookup"><span data-stu-id="9cac4-151">Today's telecommunication and retail businesses collect exhaustive data about their customers, and we can easily foresee that hello need for multi-model connectivity will become a common trend, given emerging trends such as hello Internet of Things and ubiquitous devices, which allow business tooemploy smart solutions at multiple layers.</span></span>  

 

## <a name="implementing-hello-modeling-archetype-in-machine-learning-studio"></a><span data-ttu-id="9cac4-152">實作模型原型，Machine Learning Studio 中的 hello</span><span class="sxs-lookup"><span data-stu-id="9cac4-152">Implementing hello modeling archetype in Machine Learning Studio</span></span>
<span data-ttu-id="9cac4-153">指定 hello 剛剛所述的問題，什麼是最佳方式 tooimplement hello 整合式的模型及計分方法？</span><span class="sxs-lookup"><span data-stu-id="9cac4-153">Given hello problem just described, what is hello best way tooimplement an integrated modeling and scoring approach?</span></span> <span data-ttu-id="9cac4-154">在本節中，我們將示範如何利用 Azure Machine Learning Studio 來達成這項目的。</span><span class="sxs-lookup"><span data-stu-id="9cac4-154">In this section, we will demonstrate how we accomplished this by using Azure Machine Learning Studio.</span></span>  

<span data-ttu-id="9cac4-155">hello 多模型方法時，必須設計全域變換的原型。</span><span class="sxs-lookup"><span data-stu-id="9cac4-155">hello multi-model approach is a must when designing a global archetype for churn.</span></span> <span data-ttu-id="9cac4-156">即使 hello 計分 hello 方法 （預測） 的一部分應該多模型。</span><span class="sxs-lookup"><span data-stu-id="9cac4-156">Even hello scoring (predictive) part of hello approach should be multi-model.</span></span>  

<span data-ttu-id="9cac4-157">hello 下列圖表顯示 hello 原型建立，其採用 Machine Learning Studio toopredict 變換量的四個計分演算法。</span><span class="sxs-lookup"><span data-stu-id="9cac4-157">hello following diagram shows hello prototype we created, which employs four scoring algorithms in Machine Learning Studio toopredict churn.</span></span> <span data-ttu-id="9cac4-158">hello 原因使用多模型的方式是不僅 toocreate 集團分類 tooincrease 精確度，而且還 tooprotect 防止過度配度與 tooimprove 精準的特徵選取。</span><span class="sxs-lookup"><span data-stu-id="9cac4-158">hello reason for using a multi-model approach is not only toocreate an ensemble classifier tooincrease accuracy, but also tooprotect against over-fitting and tooimprove prescriptive feature selection.</span></span>  

![][3]

<span data-ttu-id="9cac4-159">*圖 5：客戶流失模型建構方法的原型*</span><span class="sxs-lookup"><span data-stu-id="9cac4-159">*Figure 5: Prototype of a churn modeling approach*</span></span>  

<span data-ttu-id="9cac4-160">hello 下列各節提供更多詳細 hello 原型計分我們實作是利用 Machine Learning Studio 中的模型。</span><span class="sxs-lookup"><span data-stu-id="9cac4-160">hello following sections provide more details about hello prototype scoring model that we implemented by using Machine Learning Studio.</span></span>  

### <a name="data-selection-and-preparation"></a><span data-ttu-id="9cac4-161">選擇和準備資料</span><span class="sxs-lookup"><span data-stu-id="9cac4-161">Data selection and preparation</span></span>
<span data-ttu-id="9cac4-162">使用 toobuild hello 模型 hello 資料和分數客戶已經 CRM 垂直方案中，從取得的 hello 資料模糊化 tooprotect 客戶隱私權。</span><span class="sxs-lookup"><span data-stu-id="9cac4-162">hello data used toobuild hello models and score customers was obtained from a CRM vertical solution, with hello data obfuscated tooprotect customer privacy.</span></span> <span data-ttu-id="9cac4-163">hello 資料包含在 hello 美國、 8000 訂用帳戶資訊，而且它會結合三個來源： 佈建資料 （訂用帳戶中繼資料），活動資料 （hello 系統的使用方式），以及客戶支援的資料。</span><span class="sxs-lookup"><span data-stu-id="9cac4-163">hello data contains information about 8,000 subscriptions in hello U.S., and it combines three sources: provisioning data (subscription metadata), activity data (usage of hello system), and customer support data.</span></span> <span data-ttu-id="9cac4-164">hello 資料不包含任何商務相關 hello 客戶; 的相關資訊例如，它不包含忠誠度中繼資料或參與名單的分數。</span><span class="sxs-lookup"><span data-stu-id="9cac4-164">hello data does not include any business related information about hello customers; for example, it does not include loyalty metadata or credit scores.</span></span>  

<span data-ttu-id="9cac4-165">為了簡單起見，ETL 和資料淨化處理不在討論範圍內，因為我們假設資料準備已在別處完成。</span><span class="sxs-lookup"><span data-stu-id="9cac4-165">For simplicity, ETL and data cleansing processes are out of scope because we assume that data preparation has already been done elsewhere.</span></span>   

<span data-ttu-id="9cac4-166">模型的特徵選取根據 hello 組預測值，包含使用 hello 隨機樹系模組的 hello 程序中的計分初步的重要性。</span><span class="sxs-lookup"><span data-stu-id="9cac4-166">Feature selection for modeling is based on preliminary significance scoring of hello set of predictors, included in hello process that uses hello random forest module.</span></span> <span data-ttu-id="9cac4-167">Machine Learning Studio 中的 hello 實作，我們可以計算 hello 平均、 中間值和具代表性的功能範圍。</span><span class="sxs-lookup"><span data-stu-id="9cac4-167">For hello implementation in Machine Learning Studio, we calculated hello mean, median, and ranges for representative features.</span></span> <span data-ttu-id="9cac4-168">例如，我們加入 hello 質化資料，例如使用者活動的最小和最大值的彙總。</span><span class="sxs-lookup"><span data-stu-id="9cac4-168">For example, we added aggregates for hello qualitative data, such as minimum and maximum values for user activity.</span></span>    

<span data-ttu-id="9cac4-169">我們也會擷取暫時資訊 hello 最近六個月。</span><span class="sxs-lookup"><span data-stu-id="9cac4-169">We also captured temporal information for hello most recent six months.</span></span> <span data-ttu-id="9cac4-170">一年的分析資料，我們建立，即使沒有統計上明顯的趨勢，變換 hello 影響會大為降低六個月後。</span><span class="sxs-lookup"><span data-stu-id="9cac4-170">We analyzed data for one year and we established that even if there were statistically significant trends, hello effect on churn is greatly diminished after six months.</span></span>  

<span data-ttu-id="9cac4-171">hello 最重要的一點是 hello 整個程序，包括 ETL，特徵選取，而且模型已實作在機器學習 Studio 中，使用 Microsoft Azure 中的資料來源。</span><span class="sxs-lookup"><span data-stu-id="9cac4-171">hello most important point is that hello entire process, including ETL, feature selection, and modeling was implemented in Machine Learning Studio, using data sources in Microsoft Azure.</span></span>   

<span data-ttu-id="9cac4-172">hello 下列圖表說明 hello 所使用的資料。</span><span class="sxs-lookup"><span data-stu-id="9cac4-172">hello following diagrams illustrate hello data that was used.</span></span>  

![][4]

<span data-ttu-id="9cac4-173">*圖 6：資料來源摘錄 (經過模糊處理)*</span><span class="sxs-lookup"><span data-stu-id="9cac4-173">*Figure 6: Excerpt of data source (obfuscated)*</span></span>  

![][5]

<span data-ttu-id="9cac4-174">*圖 7：從資料來源擷取的特徵*</span><span class="sxs-lookup"><span data-stu-id="9cac4-174">*Figure 7: Features extracted from data source*</span></span>
 

> <span data-ttu-id="9cac4-175">請注意，這項資料是私用，因此無法共用 hello 模型和資料。</span><span class="sxs-lookup"><span data-stu-id="9cac4-175">Note that this data is private and therefore hello model and data cannot be shared.</span></span>
> <span data-ttu-id="9cac4-176">不過，類似的模型，使用可公開可用的資料，請參閱下列範例實驗中 hello [Cortana 智慧組件庫](http://gallery.cortanaintelligence.com/):[電信公司客戶變換](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383)。</span><span class="sxs-lookup"><span data-stu-id="9cac4-176">However, for a similar model using publicly available data, see this sample experiment in hello [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/): [Telco Customer Churn](http://gallery.cortanaintelligence.com/Experiment/31c19425ee874f628c847f7e2d93e383).</span></span>
> 
> <span data-ttu-id="9cac4-177">深入了解如何實作使用 Cortana 智慧套件的變換分析模型 toolearn，我們也建議[這段影片](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html)由資深方案經理 Wee Wee-hyong Tok。</span><span class="sxs-lookup"><span data-stu-id="9cac4-177">toolearn more about how you can implement a churn analysis model using Cortana Intelligence Suite, we also recommend [this video](https://info.microsoft.com/Webinar-Harness-Predictive-Customer-Churn-Model.html) by Senior Program Manager Wee Hyong Tok.</span></span> 
> 
> 

### <a name="algorithms-used-in-hello-prototype"></a><span data-ttu-id="9cac4-178">Hello 原型中使用的演算法</span><span class="sxs-lookup"><span data-stu-id="9cac4-178">Algorithms used in hello prototype</span></span>
<span data-ttu-id="9cac4-179">我們使用下列四個機器學習演算法的 hello toobuild hello 原型 （沒有任何自訂）：</span><span class="sxs-lookup"><span data-stu-id="9cac4-179">We used hello following four machine learning algorithms toobuild hello prototype (no customization):</span></span>  

1. <span data-ttu-id="9cac4-180">邏輯式迴歸 (LR)</span><span class="sxs-lookup"><span data-stu-id="9cac4-180">Logistic regression (LR)</span></span>
2. <span data-ttu-id="9cac4-181">推進式決策樹 (BT)</span><span class="sxs-lookup"><span data-stu-id="9cac4-181">Boosted decision tree (BT)</span></span>
3. <span data-ttu-id="9cac4-182">平均感知器 (AP)</span><span class="sxs-lookup"><span data-stu-id="9cac4-182">Averaged perceptron (AP)</span></span>
4. <span data-ttu-id="9cac4-183">支援向量機器 (SVM)</span><span class="sxs-lookup"><span data-stu-id="9cac4-183">Support vector machine (SVM)</span></span>  

<span data-ttu-id="9cac4-184">hello 下列圖表說明 hello 實驗設計介面，表示哪些 hello 模型所建立的 hello 順序的一部分：</span><span class="sxs-lookup"><span data-stu-id="9cac4-184">hello following diagram illustrates a portion of hello experiment design surface, which indicates hello sequence in which hello models were created:</span></span>  

![][6]  

<span data-ttu-id="9cac4-185">*圖 8：在 Machine Learning Studio 中建立模型*</span><span class="sxs-lookup"><span data-stu-id="9cac4-185">*Figure 8: Creating models in Machine Learning Studio*</span></span>  

### <a name="scoring-methods"></a><span data-ttu-id="9cac4-186">評分方法</span><span class="sxs-lookup"><span data-stu-id="9cac4-186">Scoring methods</span></span>
<span data-ttu-id="9cac4-187">我們使用標籤的定型資料集評分 hello 四個模型。</span><span class="sxs-lookup"><span data-stu-id="9cac4-187">We scored hello four models by using a labeled training dataset.</span></span>  

<span data-ttu-id="9cac4-188">我們也送出 hello 計分的 SAS Enterprise 器 12 hello 桌面版本來建立資料集 tooa 比較模型。</span><span class="sxs-lookup"><span data-stu-id="9cac4-188">We also submitted hello scoring dataset tooa comparable model built by using hello desktop edition of SAS Enterprise Miner 12.</span></span> <span data-ttu-id="9cac4-189">我們會測量 hello hello SAS 模型和所有的四種 Machine Learning Studio 模型的精確度。</span><span class="sxs-lookup"><span data-stu-id="9cac4-189">We measured hello accuracy of hello SAS model and all four Machine Learning Studio models.</span></span>  

## <a name="results"></a><span data-ttu-id="9cac4-190">結果</span><span class="sxs-lookup"><span data-stu-id="9cac4-190">Results</span></span>
<span data-ttu-id="9cac4-191">在本節中，我們提供我們的發現有關 hello hello 計分資料集為基礎的 hello 模型精確度。</span><span class="sxs-lookup"><span data-stu-id="9cac4-191">In this section, we present our findings about hello accuracy of hello models, based on hello scoring dataset.</span></span>  

### <a name="accuracy-and-precision-of-scoring"></a><span data-ttu-id="9cac4-192">評分的正確性和準確度</span><span class="sxs-lookup"><span data-stu-id="9cac4-192">Accuracy and precision of scoring</span></span>
<span data-ttu-id="9cac4-193">一般而言，Azure Machine Learning 中的 hello 實作位於 SAS 中大約 10-15%（在曲線區域或 AUC） 的精確度。</span><span class="sxs-lookup"><span data-stu-id="9cac4-193">Generally, hello implementation in Azure Machine Learning is behind SAS in accuracy by about 10-15% (Area Under Curve or AUC).</span></span>  

<span data-ttu-id="9cac4-194">不過，hello 變換中最重要的度量是 hello 錯誤分類速率： 也就是的 hello 前 n 個 churners 做為預測 hello 分類，其中實際執行**不**變換，，和在尚未收到特殊的處理方式？ hello下列圖表比較所有 hello 模型此錯誤分類率：</span><span class="sxs-lookup"><span data-stu-id="9cac4-194">However, hello most important metric in churn is hello misclassification rate: that is, of hello top N churners as predicted by hello classifier, which of them actually did **not** churn, and yet received special treatment? hello following diagram compares this misclassification rate for all hello models:</span></span>  

![][7]

<span data-ttu-id="9cac4-195">*圖 9：Passau 原型曲線下面積*</span><span class="sxs-lookup"><span data-stu-id="9cac4-195">*Figure 9: Passau prototype area under curve*</span></span>

### <a name="using-auc-toocompare-results"></a><span data-ttu-id="9cac4-196">使用 AUC toocompare 結果</span><span class="sxs-lookup"><span data-stu-id="9cac4-196">Using AUC toocompare results</span></span>
<span data-ttu-id="9cac4-197">在曲線區域 (AUC) 是代表全域的量值的標準*separability*之間的正數和負數的母體擴展的分數的 hello 散發。</span><span class="sxs-lookup"><span data-stu-id="9cac4-197">Area Under Curve (AUC) is a metric that represents a global measure of *separability* between hello distributions of scores for positive and negative populations.</span></span> <span data-ttu-id="9cac4-198">它類似 toohello 傳統接收者運算子特性 (ROC) 圖形中，但是有一個重要差異是該 hello AUC 度量不需要您 toochoose 臨界值。</span><span class="sxs-lookup"><span data-stu-id="9cac4-198">It is similar toohello traditional Receiver Operator Characteristic (ROC) graph, but one important difference is that hello AUC metric does not require you toochoose a threshold value.</span></span> <span data-ttu-id="9cac4-199">相反地，它摘述 hello 結果透過**所有**可能的選項。</span><span class="sxs-lookup"><span data-stu-id="9cac4-199">Instead, it summarizes hello results over **all** possible choices.</span></span> <span data-ttu-id="9cac4-200">相反地，hello 傳統 ROC 圖表顯示 hello 正數速率的 hello 垂直軸和 hello false 正數的速率 hello 水平軸上和 hello 分類臨界值而有所不同。</span><span class="sxs-lookup"><span data-stu-id="9cac4-200">In contrast, hello traditional ROC graph shows hello positive rate on hello vertical axis and hello false positive rate on hello horizontal axis, and hello classification threshold varies.</span></span>   

<span data-ttu-id="9cac4-201">AUC 通常作為值得的量值不同的演算法 （或不同的系統） 因為它可讓模型 toobe 透過其 AUC 值進行比較。</span><span class="sxs-lookup"><span data-stu-id="9cac4-201">AUC is generally used as a measure of worth for different algorithms (or different systems) because it allows models toobe compared by means of their AUC values.</span></span> <span data-ttu-id="9cac4-202">這在如氣象和生物科學等領域是常用的方法。</span><span class="sxs-lookup"><span data-stu-id="9cac4-202">This is a popular approach in industries such as meteorology and biosciences.</span></span> <span data-ttu-id="9cac4-203">因此，AUC 是一種評估分類器表現的普遍工具。</span><span class="sxs-lookup"><span data-stu-id="9cac4-203">Thus, AUC represents a popular tool for assessing classifier performance.</span></span>  

### <a name="comparing-misclassification-rates"></a><span data-ttu-id="9cac4-204">比較分類誤判率</span><span class="sxs-lookup"><span data-stu-id="9cac4-204">Comparing misclassification rates</span></span>
<span data-ttu-id="9cac4-205">我們使用的大約每 8,000 個訂閱 hello CRM 資料比較 hello hello 資料集有問題的錯誤分類比率。</span><span class="sxs-lookup"><span data-stu-id="9cac4-205">We compared hello misclassification rates on hello dataset in question by using hello CRM data of approximately 8,000 subscriptions.</span></span>  

* <span data-ttu-id="9cac4-206">hello SAS 錯誤分類速率為 10-15%。</span><span class="sxs-lookup"><span data-stu-id="9cac4-206">hello SAS misclassification rate was 10-15%.</span></span>
* <span data-ttu-id="9cac4-207">hello Machine Learning Studio 錯誤分類成本是 hello top 200-300 churners 15 20%。</span><span class="sxs-lookup"><span data-stu-id="9cac4-207">hello Machine Learning Studio misclassification rate was 15-20% for hello top 200-300 churners.</span></span>  

<span data-ttu-id="9cac4-208">在 hello 電信產業、 很重要的 tooaddress 僅具有這些客戶 hello 最高風險 toochurn 藉由提供它們指引服務或其他特殊的處理。</span><span class="sxs-lookup"><span data-stu-id="9cac4-208">In hello telecommunications industry, it is important tooaddress only those customers who have hello highest risk toochurn by offering them a concierge service or other special treatment.</span></span> <span data-ttu-id="9cac4-209">在這方面，hello Machine Learning Studio 實作達成與 hello SAS 模型同等的結果。</span><span class="sxs-lookup"><span data-stu-id="9cac4-209">In that respect, hello Machine Learning Studio implementation achieves results on par with hello SAS model.</span></span>  

<span data-ttu-id="9cac4-210">Hello 的相同語彙基元，精確度為有效位數比更重要因為我們最感興趣正確分類潛在 churners。</span><span class="sxs-lookup"><span data-stu-id="9cac4-210">By hello same token, accuracy is more important than precision because we are mostly interested in correctly classifying potential churners.</span></span>  

<span data-ttu-id="9cac4-211">hello 維基百科中的下列圖表描述熱烈、 容易瞭解圖形中的 hello 關聯性：</span><span class="sxs-lookup"><span data-stu-id="9cac4-211">hello following diagram from Wikipedia depicts hello relationship in a lively, easy-to-understand graphic:</span></span>  

![][8]

<span data-ttu-id="9cac4-212">*圖 10：正確性和準確度之間的取捨*</span><span class="sxs-lookup"><span data-stu-id="9cac4-212">*Figure 10: Tradeoff between accuracy and precision*</span></span>

### <a name="accuracy-and-precision-results-for-boosted-decision-tree-model"></a><span data-ttu-id="9cac4-213">推進式決策樹模型的正確性與準確度結果</span><span class="sxs-lookup"><span data-stu-id="9cac4-213">Accuracy and precision results for boosted decision tree model</span></span>
<span data-ttu-id="9cac4-214">下列圖表顯示 hello 未經處理的 hello 得到的計分 hello 促進式決策樹模型，這種 toobe hello 最精確 hello 四種模型之間使用 hello Machine Learning 原型：</span><span class="sxs-lookup"><span data-stu-id="9cac4-214">hello following chart displays hello raw results from scoring using hello Machine Learning prototype for hello boosted decision tree model, which happens toobe hello most accurate among hello four models:</span></span>  

![][9]

<span data-ttu-id="9cac4-215">*圖 11：推進式決策樹模型的特性*</span><span class="sxs-lookup"><span data-stu-id="9cac4-215">*Figure 11: Boosted decision tree model characteristics*</span></span>

## <a name="performance-comparison"></a><span data-ttu-id="9cac4-216">表現比較</span><span class="sxs-lookup"><span data-stu-id="9cac4-216">Performance comparison</span></span>
<span data-ttu-id="9cac4-217">我們比較 hello 速度資料已計分使用 hello Machine Learning Studio 模型和建立 hello 桌面版本的 SAS 企業器 12.1 來比較模型。</span><span class="sxs-lookup"><span data-stu-id="9cac4-217">We compared hello speed at which data was scored using hello Machine Learning Studio models and a comparable model created by using hello desktop edition of SAS Enterprise Miner 12.1.</span></span>  

<span data-ttu-id="9cac4-218">hello 下表摘要說明 hello 演算法 hello 的效能：</span><span class="sxs-lookup"><span data-stu-id="9cac4-218">hello following table summarizes hello performance of hello algorithms:</span></span>  

<span data-ttu-id="9cac4-219">*表 1.一般效能 （精確度） 的 hello 演算法*</span><span class="sxs-lookup"><span data-stu-id="9cac4-219">*Table 1. General performance (accuracy) of hello algorithms*</span></span>

| <span data-ttu-id="9cac4-220">LR</span><span class="sxs-lookup"><span data-stu-id="9cac4-220">LR</span></span> | <span data-ttu-id="9cac4-221">BT</span><span class="sxs-lookup"><span data-stu-id="9cac4-221">BT</span></span> | <span data-ttu-id="9cac4-222">AP</span><span class="sxs-lookup"><span data-stu-id="9cac4-222">AP</span></span> | <span data-ttu-id="9cac4-223">SVM</span><span class="sxs-lookup"><span data-stu-id="9cac4-223">SVM</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9cac4-224">平均模型</span><span class="sxs-lookup"><span data-stu-id="9cac4-224">Average Model</span></span> |<span data-ttu-id="9cac4-225">hello 最佳模型</span><span class="sxs-lookup"><span data-stu-id="9cac4-225">hello Best Model</span></span> |<span data-ttu-id="9cac4-226">表現不佳</span><span class="sxs-lookup"><span data-stu-id="9cac4-226">Underperforming</span></span> |<span data-ttu-id="9cac4-227">平均模型</span><span class="sxs-lookup"><span data-stu-id="9cac4-227">Average Model</span></span> |

<span data-ttu-id="9cac4-228">裝載的效能勝過 SAS 15-25%的執行，但精確度的速度是主要在長條上方，Machine Learning Studio 中的 hello 模型。</span><span class="sxs-lookup"><span data-stu-id="9cac4-228">hello models hosted in Machine Learning Studio outperformed SAS by 15-25% for speed of execution, but accuracy was largely on par.</span></span>  

## <a name="discussion-and-recommendations"></a><span data-ttu-id="9cac4-229">討論與建議</span><span class="sxs-lookup"><span data-stu-id="9cac4-229">Discussion and recommendations</span></span>
<span data-ttu-id="9cac4-230">在 hello 電信產業、 幾個作法應有 tooanalyze 變換，包括：</span><span class="sxs-lookup"><span data-stu-id="9cac4-230">In hello telecommunications industry, several practices have emerged tooanalyze churn, including:</span></span>  

* <span data-ttu-id="9cac4-231">導出四個基本類別的度量：</span><span class="sxs-lookup"><span data-stu-id="9cac4-231">Derive metrics for four fundamental categories:</span></span>
  * <span data-ttu-id="9cac4-232">**實體 (例如訂用帳戶)**。</span><span class="sxs-lookup"><span data-stu-id="9cac4-232">**Entity (for example, a subscription)**.</span></span> <span data-ttu-id="9cac4-233">佈建 hello 訂用帳戶及/或變換 hello 主體的客戶的基本資訊。</span><span class="sxs-lookup"><span data-stu-id="9cac4-233">Provision basic information about hello subscription and/or customer that is hello subject of churn.</span></span>
  * <span data-ttu-id="9cac4-234">**活動**。</span><span class="sxs-lookup"><span data-stu-id="9cac4-234">**Activity**.</span></span> <span data-ttu-id="9cac4-235">取得是相關的 toohello 實體，例如 hello 登入數目的所有可能的使用方式資訊。</span><span class="sxs-lookup"><span data-stu-id="9cac4-235">Obtain all possible usage information that is related toohello entity, for example, hello number of logins.</span></span>
  * <span data-ttu-id="9cac4-236">**客戶支援**。</span><span class="sxs-lookup"><span data-stu-id="9cac4-236">**Customer support**.</span></span> <span data-ttu-id="9cac4-237">蒐集資訊從客戶支援記錄 tooindicate，是否 hello 訂閱有問題或互動與客戶支援。</span><span class="sxs-lookup"><span data-stu-id="9cac4-237">Harvest information from customer support logs tooindicate whether hello subscription had issues or interactions with customer support.</span></span>
  * <span data-ttu-id="9cac4-238">**競爭性和商務資料**。</span><span class="sxs-lookup"><span data-stu-id="9cac4-238">**Competitive and business data**.</span></span> <span data-ttu-id="9cac4-239">取得 hello 客戶有關的任何可能的資訊 （例如，可以是無法使用或硬 tootrack）。</span><span class="sxs-lookup"><span data-stu-id="9cac4-239">Obtain any information possible about hello customer (for example, can be unavailable or hard tootrack).</span></span>
* <span data-ttu-id="9cac4-240">使用重要性 toodrive 特徵選取。</span><span class="sxs-lookup"><span data-stu-id="9cac4-240">Use importance toodrive feature selection.</span></span> <span data-ttu-id="9cac4-241">這表示該 hello 促進式決策樹模型中永遠是我們的方法。</span><span class="sxs-lookup"><span data-stu-id="9cac4-241">This implies that hello boosted decision tree model is always a promising approach.</span></span>  

<span data-ttu-id="9cac4-242">hello 這四種類型的使用會建立 hello 假象簡單*決定性*索引於合理的因素，每個類別，格式為基礎的方法，應該可以滿足 tooidentify 客戶變換的風險。</span><span class="sxs-lookup"><span data-stu-id="9cac4-242">hello use of these four categories creates hello illusion that a simple *deterministic* approach, based on indexes formed on reasonable factors per category, should suffice tooidentify customers at risk for churn.</span></span> <span data-ttu-id="9cac4-243">可惜，雖然這種想法看似可行，但卻是一種誤解。</span><span class="sxs-lookup"><span data-stu-id="9cac4-243">Unfortunately, although this notion seems plausible, it is a false understanding.</span></span> <span data-ttu-id="9cac4-244">hello 原因是變換是暫時的效果，而且 hello 因素造成 toochurn 通常是暫時性的狀態。</span><span class="sxs-lookup"><span data-stu-id="9cac4-244">hello reason is that churn is a temporal effect and hello factors contributing toochurn are usually in transient states.</span></span> <span data-ttu-id="9cac4-245">導致客戶 tooconsider 離開目前可能是不同明天，而它一定會是不同六個月從現在。</span><span class="sxs-lookup"><span data-stu-id="9cac4-245">What leads a customer tooconsider leaving today might be different tomorrow, and it certainly will be different six months from now.</span></span> <span data-ttu-id="9cac4-246">因此，有必要使用「機率」  模型。</span><span class="sxs-lookup"><span data-stu-id="9cac4-246">Therefore, a *probabilistic* model is a necessity.</span></span>  

<span data-ttu-id="9cac4-247">商務，通常慣用 business intelligence 導向方法 tooanalytics 經常忽略這個重要的觀察，大部分，因為它更容易銷售接受簡單的自動化。</span><span class="sxs-lookup"><span data-stu-id="9cac4-247">This important observation is often overlooked in business, which generally prefers a business intelligence-oriented approach tooanalytics, mostly because it is an easier sell and admits straightforward automation.</span></span>  

<span data-ttu-id="9cac4-248">不過，hello 承諾的自助式分析使用 Machine Learning Studio 是資訊的 hello 四種分類，來評分依部門，變成變換的機器學習的重要來源。</span><span class="sxs-lookup"><span data-stu-id="9cac4-248">However, hello promise of self-service analytics by using Machine Learning Studio is that hello four categories of information, graded by division or department, become a valuable source for machine learning about churn.</span></span>  

<span data-ttu-id="9cac4-249">另一個有趣的功能即將在 Azure Machine Learning 中是 hello 能力 tooadd 已有的預先定義之模組的自訂模組 toohello 儲存機制。</span><span class="sxs-lookup"><span data-stu-id="9cac4-249">Another exciting capability coming in Azure Machine Learning is hello ability tooadd a custom module toohello repository of predefined modules that are already available.</span></span> <span data-ttu-id="9cac4-250">這項功能，基本上，建立商機 tooselect 文件庫，並建立市場都有的範本。</span><span class="sxs-lookup"><span data-stu-id="9cac4-250">This capability, essentially, creates an opportunity tooselect libraries and create templates for vertical markets.</span></span> <span data-ttu-id="9cac4-251">它是 Azure Machine Learning hello 服務商場中的重要差異。</span><span class="sxs-lookup"><span data-stu-id="9cac4-251">It is an important differentiator of Azure Machine Learning in hello market place.</span></span>  

<span data-ttu-id="9cac4-252">我們希望 toocontinue hello 未來，特別相關 toobig 資料分析中的這個主題。</span><span class="sxs-lookup"><span data-stu-id="9cac4-252">We hope toocontinue this topic in hello future, especially related toobig data analytics.</span></span>
  

## <a name="conclusion"></a><span data-ttu-id="9cac4-253">結論</span><span class="sxs-lookup"><span data-stu-id="9cac4-253">Conclusion</span></span>
<span data-ttu-id="9cac4-254">這份文件使用一般架構，可用來描述客戶變換的實用方法 tootackling hello 一般問題。</span><span class="sxs-lookup"><span data-stu-id="9cac4-254">This paper describes a sensible approach tootackling hello common problem of customer churn by using a generic framework.</span></span> <span data-ttu-id="9cac4-255">我們採用原型來給模型評分，並使用 Azure Machine Learning 來實作。</span><span class="sxs-lookup"><span data-stu-id="9cac4-255">We considered a prototype for scoring models and implemented it by using Azure Machine Learning.</span></span> <span data-ttu-id="9cac4-256">最後，我們會評估 hello 精確度和 hello 原型方案中使用 SAS 而考慮 toocomparable 演算法的效能。</span><span class="sxs-lookup"><span data-stu-id="9cac4-256">Finally, we assessed hello accuracy and performance of hello prototype solution with regard toocomparable algorithms in SAS.</span></span>  

<span data-ttu-id="9cac4-257">**其他資訊：**</span><span class="sxs-lookup"><span data-stu-id="9cac4-257">**For more information:**</span></span>  

<span data-ttu-id="9cac4-258">本文對您有幫助嗎？</span><span class="sxs-lookup"><span data-stu-id="9cac4-258">Did this paper help you?</span></span> <span data-ttu-id="9cac4-259">請提供意見給我們。</span><span class="sxs-lookup"><span data-stu-id="9cac4-259">Please give us your feedback.</span></span> <span data-ttu-id="9cac4-260">小數位數為 1 （很差） too5 （很好） 上告訴我們您會如何對這份文件，為什麼您打此分級？</span><span class="sxs-lookup"><span data-stu-id="9cac4-260">Tell us on a scale of 1 (poor) too5 (excellent), how would you rate this paper and why have you given it this rating?</span></span> <span data-ttu-id="9cac4-261">例如：</span><span class="sxs-lookup"><span data-stu-id="9cac4-261">For example:</span></span>  

* <span data-ttu-id="9cac4-262">評分很高的到期 toohaving 很好的例子，絕佳的螢幕擷取畫面，清楚明確或因為其他原因？</span><span class="sxs-lookup"><span data-stu-id="9cac4-262">Are you rating it high due toohaving good examples, excellent screen shots, clear writing, or another reason?</span></span>
* <span data-ttu-id="9cac4-263">評分很低的到期 toopoor 範例、 模糊的螢幕擷取畫面或不清楚撰寫？</span><span class="sxs-lookup"><span data-stu-id="9cac4-263">Are you rating it low due toopoor examples, fuzzy screen shots, or unclear writing?</span></span>  

<span data-ttu-id="9cac4-264">這份回函將協助我們改善 hello 發行我們的技術白皮書品質。</span><span class="sxs-lookup"><span data-stu-id="9cac4-264">This feedback will help us improve hello quality of white papers we release.</span></span>   

<span data-ttu-id="9cac4-265">[傳送意見](mailto:sqlfback@microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="9cac4-265">[Send feedback](mailto:sqlfback@microsoft.com).</span></span>
 

## <a name="references"></a><span data-ttu-id="9cac4-266">參考</span><span class="sxs-lookup"><span data-stu-id="9cac4-266">References</span></span>
<span data-ttu-id="9cac4-267">[1] predictive Analytics: hello 預測，W McKnight，Information Management 年 7 月/年 8 月 2011，p.18 20 之外。</span><span class="sxs-lookup"><span data-stu-id="9cac4-267">[1] Predictive Analytics: Beyond hello Predictions, W. McKnight, Information Management, July/August 2011, p.18-20.</span></span>  

<span data-ttu-id="9cac4-268">[2] 維基百科文章：[正確性與準確度](http://en.wikipedia.org/wiki/Accuracy_and_precision)</span><span class="sxs-lookup"><span data-stu-id="9cac4-268">[2] Wikipedia article: [Accuracy and precision](http://en.wikipedia.org/wiki/Accuracy_and_precision)</span></span>

<span data-ttu-id="9cac4-269">[3] [CRISP-DM 1.0：資料採礦逐步指南](http://www.the-modeling-agency.com/crisp-dm.pdf)</span><span class="sxs-lookup"><span data-stu-id="9cac4-269">[3] [CRISP-DM 1.0: Step-by-Step Data Mining Guide](http://www.the-modeling-agency.com/crisp-dm.pdf)</span></span>   

<span data-ttu-id="9cac4-270">[4] [巨量資料行銷：更有效地吸引您的客戶和促進價值](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)</span><span class="sxs-lookup"><span data-stu-id="9cac4-270">[4] [Big Data Marketing: Engage Your Customers More Effectively and Drive Value](http://www.amazon.com/Big-Data-Marketing-Customers-Effectively/dp/1118733894/ref=sr_1_12?ie=UTF8&qid=1387541531&sr=8-12&keywords=customer+churn)</span></span>

<span data-ttu-id="9cac4-271">[5] [Cortana Intelligence 資源庫](http://gallery.cortanaintelligence.com/)中的[電信公司客戶流失模型範本](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5)</span><span class="sxs-lookup"><span data-stu-id="9cac4-271">[5] [Telco churn model template](http://gallery.cortanaintelligence.com/Experiment/Telco-Customer-Churn-5) in [Cortana Intelligence Gallery](http://gallery.cortanaintelligence.com/)</span></span> 
 

## <a name="appendix"></a><span data-ttu-id="9cac4-272">附錄</span><span class="sxs-lookup"><span data-stu-id="9cac4-272">Appendix</span></span>
![][10]

<span data-ttu-id="9cac4-273">*圖 12：客戶流失原型的簡報擷取畫面*</span><span class="sxs-lookup"><span data-stu-id="9cac4-273">*Figure 12: Snapshot of a presentation on churn prototype*</span></span>

[1]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-1.png
[2]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-2.png
[3]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-3.png
[4]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-4.png
[5]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-5.png
[6]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-6.png
[7]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-7.png
[8]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-8.png
[9]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-9.png
[10]: ./media/machine-learning-azure-ml-customer-churn-scenario/churn-10.png
