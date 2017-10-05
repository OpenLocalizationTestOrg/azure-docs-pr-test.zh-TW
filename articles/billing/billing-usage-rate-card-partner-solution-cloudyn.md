---
title: "Microsoft Azure 使用量和 RateCard API 可讓 Cloudyn 提供 ITFM 給客戶 | Microsoft Docs"
description: "提供 Microsoft Azure 計費合作夥伴 Cloudyn 將 Azure 計費 API 整合至其產品的經驗所得來的獨特觀點。  這特別適用於有興趣使用/嘗試將 Cloudyn 用於 Azure 服務的客戶。"
services: 
documentationcenter: 
author: BryanLa
manager: tonguyen
editor: 
tags: billing
ms.assetid: f1397397-7e92-4c20-9862-ab6b93afefb7
ms.service: billing
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: billing
ms.date: 02/03/2017
ms.author: mobandyo;bryanla
ms.openlocfilehash: fac0ee2e9cbc87c8b3d04675551bba61f7a532b6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-to-provide-itfm-for-customers"></a><span data-ttu-id="6509a-104">Microsoft Azure 使用情況和 RateCard API 可讓 Cloudyn 提供 ITFM 給客戶</span><span class="sxs-lookup"><span data-stu-id="6509a-104">Microsoft Azure Usage and RateCard APIs Enable Cloudyn to Provide ITFM for Customers</span></span>
<span data-ttu-id="6509a-105">Cloudyn (Microsoft 開發夥伴和雲端管理功能的領導提供者) 是為一項新 Microsoft Azure 資源使用情況與 RateCard API 的私人預覽所選取。</span><span class="sxs-lookup"><span data-stu-id="6509a-105">Cloudyn, a Microsoft development partner and a leading provider of cloud management capabilities, was chosen for a private preview of the new Microsoft Azure Resource Usage and RateCard APIs.</span></span>  <span data-ttu-id="6509a-106">使用情況 API 可為訂用帳戶提供預估的 Azure 耗用量資料。</span><span class="sxs-lookup"><span data-stu-id="6509a-106">The Usage API provides access to estimated Azure consumption data for a subscription.</span></span> <span data-ttu-id="6509a-107">RateCard API 提供非企業合約 (EA) 客戶所有 Azure 服務的完整定價資訊。</span><span class="sxs-lookup"><span data-stu-id="6509a-107">The RateCard API provides complete pricing information of all Azure services, for non-Enterprise Agreement (EA) customers.</span></span> <span data-ttu-id="6509a-108">當這些 API 整合在一起時，會提供完整的資訊基礎給 IT 財務管理 (ITFM) 工具的輸入，例如 Cloudyn 所提供的工具。</span><span class="sxs-lookup"><span data-stu-id="6509a-108">Integrated together, these APIs provide a complete information basis for input into IT Financial Management (ITFM) tools such as those provided by Cloudyn.</span></span>

## <a name="introduction"></a><span data-ttu-id="6509a-109">簡介</span><span class="sxs-lookup"><span data-stu-id="6509a-109">Introduction</span></span>
<span data-ttu-id="6509a-110">使用情況 API 的資料和 RateCard API 的資料之間所謂的「乘法」(使用情況 [單位] 價格 [$unit] = 詳細使用情況和成本) 會建立最細微、精確且可靠的計費資訊，可供目前的 Azure 使用。</span><span class="sxs-lookup"><span data-stu-id="6509a-110">The so-called “multiplication” of data from the Usage API with data from the RateCard API (usage [units] price[$unit] = Detailed Usage and Cost) creates the most granular, accurate and reliable billing information available for Azure today.</span></span>

![ITFM 概觀][1]

<span data-ttu-id="6509a-112">使用這些 API 可提供與客戶的使用情況和成本相關的重要資訊，讓 Cloudyn 可利用簡單的程式設計方式分析客戶帳戶，並為其客戶執行各種 ITFM 工作。</span><span class="sxs-lookup"><span data-stu-id="6509a-112">Consuming these APIs provides key information on customers’ usage and costs, allowing Cloudyn to analyze customer accounts in a simple, programmatic manner, and to perform various ITFM tasks for its customers.</span></span>

## <a name="integrating-cloudyn-with-the-ratecard-and-usage-apis"></a><span data-ttu-id="6509a-113">整合 Cloudyn 和 RateCard 使用情況 API</span><span class="sxs-lookup"><span data-stu-id="6509a-113">Integrating Cloudyn with the RateCard and Usage APIs</span></span>
<span data-ttu-id="6509a-114">RateCard API 需要數個輸入參數 -- 例如區域資訊、貨幣及區域設定 --，但最重要的一種是 OfferDurableID，它會指定客戶正在使用的 Azure 優惠類型 (隨收隨付、舊版 6 及 12 個月的承諾方案、MSDN 優惠、MPN 優惠、促銷優惠和其他類型)。</span><span class="sxs-lookup"><span data-stu-id="6509a-114">The RateCard API requires several input parameters -- like region info, currency and locale -- but the most important one is OfferDurableID, which specifies the type of Azure offering the customer is using (Pay-as-you-Go, legacy 6 and 12-month commitment plans, MSDN offers, MPN offers, promotional offers and others).</span></span> <span data-ttu-id="6509a-115">OfferDurableID 位於指定訂用帳戶之「優惠識別碼」下的 [Azure 使用情況和計費入口網站](https://account.windowsazure.com/Subscriptions)。</span><span class="sxs-lookup"><span data-stu-id="6509a-115">The OfferDurableID can be found in the [Azure Usage and Billing portal](https://account.windowsazure.com/Subscriptions), under the "Offer ID" for the given subscription.</span></span>

<span data-ttu-id="6509a-116">在註冊 [Cloudyn for Azure](https://www.cloudyn.com/microsoft-azure/) 服務時，客戶可以加入其 OfferDurableID 程式碼，可讓 Cloudyn 透過 RateCard API 提取其相關定價資訊。</span><span class="sxs-lookup"><span data-stu-id="6509a-116">Upon registration for [Cloudyn for Azure](https://www.cloudyn.com/microsoft-azure/) services, customers can add their OfferDurableID code, which allows Cloudyn to pull their relevant pricing information through the RateCard API.</span></span>  <span data-ttu-id="6509a-117">如需各種類型的優惠資訊，請參閱 [Microsoft Azure 優惠詳細資料](https://azure.microsoft.com/support/legal/offer-details/) 頁面。</span><span class="sxs-lookup"><span data-stu-id="6509a-117">Information on the different types of offers can be found one the [Microsoft Azure Offer Details](https://azure.microsoft.com/support/legal/offer-details/) page.</span></span>

![Cloudyn ITFM 引擎概觀][2]

<span data-ttu-id="6509a-119">除了 Azure 效能 API 之外，Cloudyn 還使用了使用情況和 RateCard API，建立其他層的視覺化、分析、警示、報告、成本管理和可行的建議，提供可靠的企業雲端 ITFM 工具給 Azure 客戶。</span><span class="sxs-lookup"><span data-stu-id="6509a-119">Cloudyn uses both the Usage and RateCard APIs, in addition to the Azure Performance API, to create additional layers of visualization, analytics, alerting, reporting, cost management and actionable recommendations, providing Azure customers a reliable enterprise cloud ITFM tool.</span></span>

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a><span data-ttu-id="6509a-120">Cloudyn ITFM 使用由使用情況和 RateCard API 整合啟用的案例</span><span class="sxs-lookup"><span data-stu-id="6509a-120">Cloudyn ITFM use cases enabled by Usage and RateCard API integration</span></span>
<span data-ttu-id="6509a-121">一般 Cloudyn ITFM 所使用的案例都由使用情況和 RateCard API 啟用，包括：</span><span class="sxs-lookup"><span data-stu-id="6509a-121">Common Cloudyn ITFM use cases enabled by usage and RateCard APIs include:</span></span>

* <span data-ttu-id="6509a-122">**成本分析** - 可讓雲端成本細分成任何原生識別維度 (提供者、服務、帳戶、區域等)。</span><span class="sxs-lookup"><span data-stu-id="6509a-122">**Cost Analysis** - Allows cloud costs to be broken down to any native identifying dimension (provider, service, account, region etc.).</span></span> <span data-ttu-id="6509a-123">藉由提供每個帳戶最細微的使用情況和成本資料分解，然後由 Cloudyn 將其分組和篩選，並以圖型或表格的形式呈現給使用者，Azure 使用情況和 RateCard API 可讓這個工作變簡單。</span><span class="sxs-lookup"><span data-stu-id="6509a-123">The Azure Usage and RateCard APIs make this an easy task, by providing the most granular breakdown of usage and cost data per account, which is then grouped and filtered by Cloudyn and presented to the user, in a graphic or tabular form.</span></span>

![成本分析圓形圖][3]

* <span data-ttu-id="6509a-125">**成本配置 360** - 可讓財務與 IT 管理者發現其雲端部署的實際成本分解、驅動程式和趨勢。</span><span class="sxs-lookup"><span data-stu-id="6509a-125">**Cost Allocation 360** - Enables finance and IT managers to uncover the actual cost breakdown, drivers and trends of their cloud deployment.</span></span> <span data-ttu-id="6509a-126">它還可以進一步讓管理者輕鬆地建立部署費用與商務單位、部門、區域之間的關聯、針對雲端成本提供前所未有的見解，並且促進企業計費和回報。</span><span class="sxs-lookup"><span data-stu-id="6509a-126">It further allows managers to easily associate deployment expenses with business units, departments, regions, and more, providing unprecedented insights into cloud costs, and facilitating enterprise chargebacks and showbacks.</span></span> <span data-ttu-id="6509a-127">Azure 使用情況和 RateCard API 可做為 Cloudyn 成本配置引擎的輸入，藉由定義方法和商務邏輯以配置未標記或無法標記的資源，進而輔助 API。</span><span class="sxs-lookup"><span data-stu-id="6509a-127">The Azure Usage and RateCard APIs serve as input to Cloudyn’s cost allocation engine, which complements the APIs by defining methods and business logic for allocating untagged or untaggable resources.</span></span>

![成本配置 360 圖表][4]

* <span data-ttu-id="6509a-129">**具有成本效益的大小** - 提供正確的大小建議給使用量過低的虛擬機器，進而減少客戶對於過大或過度佈建機器的費用。</span><span class="sxs-lookup"><span data-stu-id="6509a-129">**Cost-Effective Sizing** - Provides right-sizing recommendations for underutilized virtual machines, thus reducing the customer’s expenses on oversized or over-provisioned machines.</span></span> <span data-ttu-id="6509a-130">它是藉由檢查虛擬機器 CPU 和 RAM 計量 (透過效能 API)、執行階段的時數 (透過使用情況 API) 和成本 (透過 RateCard API) 來達成效果。</span><span class="sxs-lookup"><span data-stu-id="6509a-130">It does so by examining virtual machine CPU and RAM metrics (via Performance API), hours of run-time (via Usage API) and cost (via RateCard API).</span></span> <span data-ttu-id="6509a-131">然後 Cloudyn 會根據使用量過低的 CPU 或 RAM 資源 (效能) 提供正確大小的建議，並且將 VM 之間的價格差異 (RateCard) 乘以使用量過低機器的實際使用時間 (使用情況)，以計算出預估的節約效益。</span><span class="sxs-lookup"><span data-stu-id="6509a-131">Cloudyn then provides right-sizing recommendations based on underutilized CPU or RAM resources (Performance), and calculates estimated savings by multiplying the price delta (RateCard) between the VMs by the actual time-utilization (Usage) of the underutilized machine.</span></span>

![符合成本效益的大小][5]

* <span data-ttu-id="6509a-133">**雲端移植建議** - 提供雲端移植的財務建議。</span><span class="sxs-lookup"><span data-stu-id="6509a-133">**Cloud Porting Recommendations** - Provides financial advice on cloud porting.</span></span> <span data-ttu-id="6509a-134">它會檢查使用者目前部署在主要雲端廠商的雲端資源成本，並且和其在 Azure 上對等的部署成本進行比較。</span><span class="sxs-lookup"><span data-stu-id="6509a-134">It examines a user's current costs of cloud resources which are deployed on major cloud vendors, and compares it to the cost of an equivalent deployment on Azure.</span></span> <span data-ttu-id="6509a-135">然後它會提供細微的、每個資源的、財務型的移植建議給 Azure。</span><span class="sxs-lookup"><span data-stu-id="6509a-135">It then provides granular, per-resource, financially-based porting recommendations to Azure.</span></span> <span data-ttu-id="6509a-136">評估 Azure 上所需之對等部署 (根據效能計量和使用者喜好設定) 之後，Cloudyn 會使用 RateCard API 評估 Azure 上對等部署的成本。</span><span class="sxs-lookup"><span data-stu-id="6509a-136">After assessing the equivalent deployment required on Azure (based on performance metrics and user preferences), Cloudyn uses the RateCard API to evaluate the cost of the equivalent deployment on Azure.</span></span>
* <span data-ttu-id="6509a-137">**效能報告** - 由 Azure 的效能 API 啟用，這些報告提供 CPU 和 RAM 使用量的陣列功能給最佳化建議。</span><span class="sxs-lookup"><span data-stu-id="6509a-137">**Performance Reports** - Enabled by Azure’s performance API, these reports provide an array of features from CPU and RAM utilization to optimization recommendations.</span></span> <span data-ttu-id="6509a-138">以下是執行個體使用量報告的範例，根據平均 CPU 使用量來呈現執行個體分解。</span><span class="sxs-lookup"><span data-stu-id="6509a-138">Below is an instance utilization report example, presenting instance breakdown by average CPU utilization.</span></span>

![效能報告][6]

* <span data-ttu-id="6509a-140">**類別管理員** - 為缺乏組織的雲端資源帶來秩序的強大 Cloudyn 功能。</span><span class="sxs-lookup"><span data-stu-id="6509a-140">**Category manager** - A powerful feature in Cloudyn that brings order to unorganized cloud resources.</span></span> <span data-ttu-id="6509a-141">它可讓使用者自由建立自己的唯一類別 (標記) 以進行符合商業實務的有效測量和報告。</span><span class="sxs-lookup"><span data-stu-id="6509a-141">It provides users the freedom to create their own unique categories (tags) for effective measuring and reporting that is in line with business practices.</span></span> <span data-ttu-id="6509a-142">此外，使用者可以輕鬆地管理和分類不一致的標記 (也就是錯字和其他不一致)，並且自動偵測未標記的資源以達成精確的成本屬性。</span><span class="sxs-lookup"><span data-stu-id="6509a-142">Further, users can easily regulate and categorize inconsistent tagging (i.e. typos and other discrepancies) and automatically detect untagged resources for accurate cost attribution.</span></span>

![類別管理員][7]

## <a name="video"></a><span data-ttu-id="6509a-144">影片</span><span class="sxs-lookup"><span data-stu-id="6509a-144">Video</span></span>
<span data-ttu-id="6509a-145">以下短片顯示 Azure 客戶如何使用 Azure 和 Azure 計費 API 的 Cloudyn，從 Azure 耗用量資料取得見解。</span><span class="sxs-lookup"><span data-stu-id="6509a-145">Here's a short video which shows how an Azure customer can use Cloudyn for Azure and the Azure Billing APIs, to gain insights from their Azure consumption data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="6509a-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6509a-146">Next Steps</span></span>
* <span data-ttu-id="6509a-147">開始免費 [Cloudyn for Azure](https://www.cloudyn.com/microsoft-azure/) 試用版，查看如何利用 Microsoft Azure 雲端部署的自訂報告和分析取得成本透明度。</span><span class="sxs-lookup"><span data-stu-id="6509a-147">Start a free [Cloudyn for Azure](https://www.cloudyn.com/microsoft-azure/) trial to see how you can obtain cost transparency with customized reporting and analytics for your Microsoft Azure cloud deployment.</span></span>
* <span data-ttu-id="6509a-148">請參閱 [深入了解 Microsoft Azure 資源耗用量](billing-usage-rate-card-overview.md) 以取得 Azure 資源使用情況和 RateCard API 的概觀。</span><span class="sxs-lookup"><span data-stu-id="6509a-148">See [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md) for an overview of the Azure Resource Usage and RateCard APIs.</span></span>
* <span data-ttu-id="6509a-149">查看 [Azure 計費 REST API 參考](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) 以取得屬於 Azure 資源管理員所提供之 API 集合的兩個 API 之詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6509a-149">Check out the [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more information on both APIs, which are part of the set of APIs provided by the Azure Resource Manager.</span></span>
* <span data-ttu-id="6509a-150">如果您想要探究範例程式碼，請查看 [Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?term=billing)上的＜Microsoft Azure 計費 API 程式碼範例＞。</span><span class="sxs-lookup"><span data-stu-id="6509a-150">If you would like to dive right into the sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span></span>

## <a name="learn-more"></a><span data-ttu-id="6509a-151">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="6509a-151">Learn More</span></span>
* <span data-ttu-id="6509a-152">若要深入了解 Microsoft Azure 企業合約 (EA) 優惠，請瀏覽 [授權企業用 Azure](https://azure.microsoft.com/pricing/enterprise-agreement/)</span><span class="sxs-lookup"><span data-stu-id="6509a-152">To learn more about Microsoft Azure Enterprise Agreement (EA) offers, please visit [Licensing Azure for the Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/)</span></span>
* <span data-ttu-id="6509a-153">請參閱 [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md) 一文，以深入了解 Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="6509a-153">See the [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) article to learn more about the Azure Resource Manager.</span></span>
* <span data-ttu-id="6509a-154">如需協助了解雲端花費之必要工具套件的其他資訊，請參閱 Gartner 文章 [IT 財務管理 (ITFM) 工具的市場指南](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb)。</span><span class="sxs-lookup"><span data-stu-id="6509a-154">For additional information on the suite of tools necessary to help in gaining an understanding of cloud spend, please refer to  Gartner article [Market Guide for IT Financial Management (ITFM) Tools](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).</span></span>

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
