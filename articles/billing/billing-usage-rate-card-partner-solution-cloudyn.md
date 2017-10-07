---
title: "aaaMicrosoft Azure 使用量和 RateCard Api 啟用 Cloudyn tooProvide 客戶 ITFM |Microsoft 文件"
description: "從 Microsoft Azure 計費夥伴 Cloudyn，他們將 hello Azure 計費 Api 整合至其產品的經驗提供唯一的檢視方塊。  這特別適用於有興趣使用/嘗試將 Cloudyn 用於 Azure 服務的客戶。"
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
ms.openlocfilehash: e221ac8b8feebb725a1cc669c8143ab829621a8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoft-azure-usage-and-ratecard-apis-enable-cloudyn-tooprovide-itfm-for-customers"></a><span data-ttu-id="211be-104">Microsoft Azure 的使用量和 RateCard Api 啟用 Cloudyn tooProvide ITFM 客戶</span><span class="sxs-lookup"><span data-stu-id="211be-104">Microsoft Azure Usage and RateCard APIs Enable Cloudyn tooProvide ITFM for Customers</span></span>
<span data-ttu-id="211be-105">Cloudyn、 Microsoft 開發夥伴和前置的提供者的雲端管理功能，因為已選擇 private preview 中的 hello 新 Microsoft Azure 資源使用量和 RateCard 應用程式開發介面。</span><span class="sxs-lookup"><span data-stu-id="211be-105">Cloudyn, a Microsoft development partner and a leading provider of cloud management capabilities, was chosen for a private preview of hello new Microsoft Azure Resource Usage and RateCard APIs.</span></span>  <span data-ttu-id="211be-106">hello 使用量 API 提供的訂用帳戶存取 tooestimated Azure 耗用量資料。</span><span class="sxs-lookup"><span data-stu-id="211be-106">hello Usage API provides access tooestimated Azure consumption data for a subscription.</span></span> <span data-ttu-id="211be-107">hello RateCard API 提供所有 Azure 服務的詳細資訊，對非企業協議 EA 客戶完成價格的資訊。</span><span class="sxs-lookup"><span data-stu-id="211be-107">hello RateCard API provides complete pricing information of all Azure services, for non-Enterprise Agreement (EA) customers.</span></span> <span data-ttu-id="211be-108">當這些 API 整合在一起時，會提供完整的資訊基礎給 IT 財務管理 (ITFM) 工具的輸入，例如 Cloudyn 所提供的工具。</span><span class="sxs-lookup"><span data-stu-id="211be-108">Integrated together, these APIs provide a complete information basis for input into IT Financial Management (ITFM) tools such as those provided by Cloudyn.</span></span>

## <a name="introduction"></a><span data-ttu-id="211be-109">簡介</span><span class="sxs-lookup"><span data-stu-id="211be-109">Introduction</span></span>
<span data-ttu-id="211be-110">hello 所謂 「 乘法 」 的資料從 hello RateCard API 資料 hello 使用量 API (使用 [單位] 價格 [$unit] = 詳細使用狀況和成本) 建立 hello 最細微、 精確又可靠的計費資訊可以使用 Azure 今天。</span><span class="sxs-lookup"><span data-stu-id="211be-110">hello so-called “multiplication” of data from hello Usage API with data from hello RateCard API (usage [units] price[$unit] = Detailed Usage and Cost) creates hello most granular, accurate and reliable billing information available for Azure today.</span></span>

![ITFM 概觀][1]

<span data-ttu-id="211be-112">使用這些 Api 客戶的使用量和成本，Cloudyn tooanalyze 客戶帳戶中允許的簡單、 程式設計的方式和 tooperform 各種 ITFM 工作為客戶提供重要資訊。</span><span class="sxs-lookup"><span data-stu-id="211be-112">Consuming these APIs provides key information on customers’ usage and costs, allowing Cloudyn tooanalyze customer accounts in a simple, programmatic manner, and tooperform various ITFM tasks for its customers.</span></span>

## <a name="integrating-cloudyn-with-hello-ratecard-and-usage-apis"></a><span data-ttu-id="211be-113">整合與 hello RateCard Cloudyn 和使用狀況應用程式開發介面</span><span class="sxs-lookup"><span data-stu-id="211be-113">Integrating Cloudyn with hello RateCard and Usage APIs</span></span>
<span data-ttu-id="211be-114">hello RateCard API 需要數個輸入的參數的詳細資訊-例如地區資訊、 貨幣及地區設定-但 hello 最重要的其中一個是 OfferDurableID，指定 hello Azure 提供項目 hello 客戶類型所使用 （隨用隨付、 舊版 6 和 12 個月做出的承諾計劃、 MSDN 優惠、 MPN 優惠、 促銷優惠和其他項目）。</span><span class="sxs-lookup"><span data-stu-id="211be-114">hello RateCard API requires several input parameters -- like region info, currency and locale -- but hello most important one is OfferDurableID, which specifies hello type of Azure offering hello customer is using (Pay-as-you-Go, legacy 6 and 12-month commitment plans, MSDN offers, MPN offers, promotional offers and others).</span></span> <span data-ttu-id="211be-115">hello OfferDurableID 位於 hello[使用量與計費入口網站](https://account.windowsazure.com/Subscriptions)，hello"提供 ID"hello 指定訂用帳戶底下。</span><span class="sxs-lookup"><span data-stu-id="211be-115">hello OfferDurableID can be found in hello [Azure Usage and Billing portal](https://account.windowsazure.com/Subscriptions), under hello "Offer ID" for hello given subscription.</span></span>

<span data-ttu-id="211be-116">在註冊時[azure Cloudyn](https://www.cloudyn.com/microsoft-azure/)服務，客戶可以將其 OfferDurableID 程式碼，可讓 Cloudyn toopull hello RateCard API 及其相關定價資訊。</span><span class="sxs-lookup"><span data-stu-id="211be-116">Upon registration for [Cloudyn for Azure](https://www.cloudyn.com/microsoft-azure/) services, customers can add their OfferDurableID code, which allows Cloudyn toopull their relevant pricing information through hello RateCard API.</span></span>  <span data-ttu-id="211be-117">Hello 優惠的不同型別上的資訊可以找到一個 hello [Microsoft Azure 優惠詳細資料](https://azure.microsoft.com/support/legal/offer-details/)頁面。</span><span class="sxs-lookup"><span data-stu-id="211be-117">Information on hello different types of offers can be found one hello [Microsoft Azure Offer Details](https://azure.microsoft.com/support/legal/offer-details/) page.</span></span>

![Cloudyn ITFM 引擎概觀][2]

<span data-ttu-id="211be-119">同時在加法 toohello Azure 效能 API，視覺效果，分析，toocreate 額外層級警示 hello 使用量和 RateCard Api Cloudyn 使用報告，成本管理和可採取動作的建議，提供可靠的 Azure 客戶企業雲端 ITFM 工具。</span><span class="sxs-lookup"><span data-stu-id="211be-119">Cloudyn uses both hello Usage and RateCard APIs, in addition toohello Azure Performance API, toocreate additional layers of visualization, analytics, alerting, reporting, cost management and actionable recommendations, providing Azure customers a reliable enterprise cloud ITFM tool.</span></span>

## <a name="cloudyn-itfm-use-cases-enabled-by-usage-and-ratecard-api-integration"></a><span data-ttu-id="211be-120">Cloudyn ITFM 使用由使用情況和 RateCard API 整合啟用的案例</span><span class="sxs-lookup"><span data-stu-id="211be-120">Cloudyn ITFM use cases enabled by Usage and RateCard API integration</span></span>
<span data-ttu-id="211be-121">一般 Cloudyn ITFM 所使用的案例都由使用情況和 RateCard API 啟用，包括：</span><span class="sxs-lookup"><span data-stu-id="211be-121">Common Cloudyn ITFM use cases enabled by usage and RateCard APIs include:</span></span>

* <span data-ttu-id="211be-122">**成本分析**-可讓雲端成本 toobe 細分 tooany 原生識別維度 （提供者、 服務、 帳戶、 區域等等）。</span><span class="sxs-lookup"><span data-stu-id="211be-122">**Cost Analysis** - Allows cloud costs toobe broken down tooany native identifying dimension (provider, service, account, region etc.).</span></span> <span data-ttu-id="211be-123">hello Azure 的使用量和 RateCard Api 可讓容易的工作，藉由提供使用量與成本的資料，每個帳戶，然後分組和篩選 Cloudyn 並顯示 toohello 使用者在圖形或表格式表單中的 hello 最細微分解。</span><span class="sxs-lookup"><span data-stu-id="211be-123">hello Azure Usage and RateCard APIs make this an easy task, by providing hello most granular breakdown of usage and cost data per account, which is then grouped and filtered by Cloudyn and presented toohello user, in a graphic or tabular form.</span></span>

![成本分析圓形圖][3]

* <span data-ttu-id="211be-125">**成本配置 360** -啟用財務與 IT 經理 toouncover hello 實際成本明細、 驅動程式以及其雲端部署的趨勢。</span><span class="sxs-lookup"><span data-stu-id="211be-125">**Cost Allocation 360** - Enables finance and IT managers toouncover hello actual cost breakdown, drivers and trends of their cloud deployment.</span></span> <span data-ttu-id="211be-126">它進一步允許管理員 tooeasily 關聯的部署費用與業務單位、 部門、 區域和詳細資訊，提供前所未有的深入剖析雲端成本和促進企業交易糾紛和 showbacks。</span><span class="sxs-lookup"><span data-stu-id="211be-126">It further allows managers tooeasily associate deployment expenses with business units, departments, regions, and more, providing unprecedented insights into cloud costs, and facilitating enterprise chargebacks and showbacks.</span></span> <span data-ttu-id="211be-127">hello Azure 的使用量和 RateCard 應用程式開發介面做為輸入的 tooCloudyn 成本配置引擎，補充 hello 應用程式開發介面所定義的方法和配置未標記或 untaggable 資源的商務邏輯。</span><span class="sxs-lookup"><span data-stu-id="211be-127">hello Azure Usage and RateCard APIs serve as input tooCloudyn’s cost allocation engine, which complements hello APIs by defining methods and business logic for allocating untagged or untaggable resources.</span></span>

![成本配置 360 圖表][4]

* <span data-ttu-id="211be-129">**符合成本效益的調整大小**-提供使用量過低的虛擬機器，進而降低 hello 客戶費用過大或過度佈建的電腦上的正確調整建議。</span><span class="sxs-lookup"><span data-stu-id="211be-129">**Cost-Effective Sizing** - Provides right-sizing recommendations for underutilized virtual machines, thus reducing hello customer’s expenses on oversized or over-provisioned machines.</span></span> <span data-ttu-id="211be-130">它是藉由檢查虛擬機器 CPU 和 RAM 計量 (透過效能 API)、執行階段的時數 (透過使用情況 API) 和成本 (透過 RateCard API) 來達成效果。</span><span class="sxs-lookup"><span data-stu-id="211be-130">It does so by examining virtual machine CPU and RAM metrics (via Performance API), hours of run-time (via Usage API) and cost (via RateCard API).</span></span> <span data-ttu-id="211be-131">Cloudyn 然後提供正確調整建議根據使用量過低 CPU 或 RAM 資源 （效能），並計算預估的節省量乘以 hello 價格差異 (RateCard) 之間的 hello 實際時間使用率 （使用量） 的 hello 的 hello Vm使用量過低的電腦。</span><span class="sxs-lookup"><span data-stu-id="211be-131">Cloudyn then provides right-sizing recommendations based on underutilized CPU or RAM resources (Performance), and calculates estimated savings by multiplying hello price delta (RateCard) between hello VMs by hello actual time-utilization (Usage) of hello underutilized machine.</span></span>

![符合成本效益的大小][5]

* <span data-ttu-id="211be-133">**雲端移植建議** - 提供雲端移植的財務建議。</span><span class="sxs-lookup"><span data-stu-id="211be-133">**Cloud Porting Recommendations** - Provides financial advice on cloud porting.</span></span> <span data-ttu-id="211be-134">它會檢查使用者的目前對主要雲端廠商所部署的雲端資源的成本，並比較它的對等 Azure 上部署的 toohello 成本。</span><span class="sxs-lookup"><span data-stu-id="211be-134">It examines a user's current costs of cloud resources which are deployed on major cloud vendors, and compares it toohello cost of an equivalent deployment on Azure.</span></span> <span data-ttu-id="211be-135">然後會提供精細，每個資源，以型移植建議 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="211be-135">It then provides granular, per-resource, financially-based porting recommendations tooAzure.</span></span> <span data-ttu-id="211be-136">之後評估 hello 相等 （根據效能度量和使用者偏好設定） 的 Azure 上所需的部署，Cloudyn 會在 Azure 上使用 hello 相等部署的 hello RateCard API tooevaluate hello 成本。</span><span class="sxs-lookup"><span data-stu-id="211be-136">After assessing hello equivalent deployment required on Azure (based on performance metrics and user preferences), Cloudyn uses hello RateCard API tooevaluate hello cost of hello equivalent deployment on Azure.</span></span>
* <span data-ttu-id="211be-137">**效能報告**-啟用 Azure 的效能應用程式開發介面，這些報表提供之功能的 CPU 和 RAM 使用量陣列 toooptimization 建議。</span><span class="sxs-lookup"><span data-stu-id="211be-137">**Performance Reports** - Enabled by Azure’s performance API, these reports provide an array of features from CPU and RAM utilization toooptimization recommendations.</span></span> <span data-ttu-id="211be-138">以下是執行個體使用量報告的範例，根據平均 CPU 使用量來呈現執行個體分解。</span><span class="sxs-lookup"><span data-stu-id="211be-138">Below is an instance utilization report example, presenting instance breakdown by average CPU utilization.</span></span>

![效能報告][6]

* <span data-ttu-id="211be-140">**類別目錄管理員**-Cloudyn 帶來順序 toounorganized 雲端資源的強大功能。</span><span class="sxs-lookup"><span data-stu-id="211be-140">**Category manager** - A powerful feature in Cloudyn that brings order toounorganized cloud resources.</span></span> <span data-ttu-id="211be-141">它提供使用者 hello 自由 toocreate 自己唯一的分類 （標記） 有效測量與報告，根據商業實務執行。</span><span class="sxs-lookup"><span data-stu-id="211be-141">It provides users hello freedom toocreate their own unique categories (tags) for effective measuring and reporting that is in line with business practices.</span></span> <span data-ttu-id="211be-142">此外，使用者可以輕鬆地管理和分類不一致的標記 (也就是錯字和其他不一致)，並且自動偵測未標記的資源以達成精確的成本屬性。</span><span class="sxs-lookup"><span data-stu-id="211be-142">Further, users can easily regulate and categorize inconsistent tagging (i.e. typos and other discrepancies) and automatically detect untagged resources for accurate cost attribution.</span></span>

![類別管理員][7]

## <a name="video"></a><span data-ttu-id="211be-144">影片</span><span class="sxs-lookup"><span data-stu-id="211be-144">Video</span></span>
<span data-ttu-id="211be-145">以下是示範 Azure 客戶如何針對 Azure 與 hello Azure 計費的 Api，從 Azure 耗用量資料 toogain insights 使用 Cloudyn 的短片。</span><span class="sxs-lookup"><span data-stu-id="211be-145">Here's a short video which shows how an Azure customer can use Cloudyn for Azure and hello Azure Billing APIs, toogain insights from their Azure consumption data.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Cloudyn-Provides-Cloud-ITFM-Tools-Via-Microsoft-Azure-APIs/player]
> 
> 

## <a name="next-steps"></a><span data-ttu-id="211be-146">後續步驟</span><span class="sxs-lookup"><span data-stu-id="211be-146">Next Steps</span></span>
* <span data-ttu-id="211be-147">開始免費[azure Cloudyn](https://www.cloudyn.com/microsoft-azure/)如何取得試用 toosee 成本與自訂報告和分析為您的 Microsoft Azure 雲端部署的透明度。</span><span class="sxs-lookup"><span data-stu-id="211be-147">Start a free [Cloudyn for Azure](https://www.cloudyn.com/microsoft-azure/) trial toosee how you can obtain cost transparency with customized reporting and analytics for your Microsoft Azure cloud deployment.</span></span>
* <span data-ttu-id="211be-148">請參閱[深入了解您的 Microsoft Azure 資源耗用量](billing-usage-rate-card-overview.md)hello Azure 資源使用量和 RateCard Api 的概觀。</span><span class="sxs-lookup"><span data-stu-id="211be-148">See [Gain insights into your Microsoft Azure resource consumption](billing-usage-rate-card-overview.md) for an overview of hello Azure Resource Usage and RateCard APIs.</span></span>
* <span data-ttu-id="211be-149">簽出 hello [Azure 計費 REST API 參考](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c)如需有關這兩個 Api 的詳細資訊，這是 hello 組 hello Azure 資源管理員所提供的應用程式開發介面的一部分。</span><span class="sxs-lookup"><span data-stu-id="211be-149">Check out hello [Azure Billing REST API Reference](https://msdn.microsoft.com/library/azure/1ea5b323-54bb-423d-916f-190de96c6a3c) for more information on both APIs, which are part of hello set of APIs provided by hello Azure Resource Manager.</span></span>
* <span data-ttu-id="211be-150">如果您想要 toodive 右到 hello 範例程式碼，請參閱 Microsoft Azure 計費應用程式開發介面程式碼範例上[Azure 程式碼範例](https://azure.microsoft.com/documentation/samples/?term=billing)。</span><span class="sxs-lookup"><span data-stu-id="211be-150">If you would like toodive right into hello sample code, check out our Microsoft Azure Billing API Code Samples on [Azure Code Samples](https://azure.microsoft.com/documentation/samples/?term=billing).</span></span>

## <a name="learn-more"></a><span data-ttu-id="211be-151">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="211be-151">Learn More</span></span>
* <span data-ttu-id="211be-152">toolearn 深入了解 Microsoft Azure Enterprise 合約 (EA) 提供項目，請瀏覽[授權 Azure hello 企業版](https://azure.microsoft.com/pricing/enterprise-agreement/)</span><span class="sxs-lookup"><span data-stu-id="211be-152">toolearn more about Microsoft Azure Enterprise Agreement (EA) offers, please visit [Licensing Azure for hello Enterprise](https://azure.microsoft.com/pricing/enterprise-agreement/)</span></span>
* <span data-ttu-id="211be-153">請參閱 hello [Azure 資源管理員概觀](../azure-resource-manager/resource-group-overview.md)文章 toolearn 更多關於 hello Azure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="211be-153">See hello [Azure Resource Manager Overview](../azure-resource-manager/resource-group-overview.md) article toolearn more about hello Azure Resource Manager.</span></span>
* <span data-ttu-id="211be-154">如需有關 hello 工具套件中雲端的了解必要 toohelp 支出，請參閱太 Gartner 文章[IT 財務管理 (ITFM) 工具的市場指南](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb)。</span><span class="sxs-lookup"><span data-stu-id="211be-154">For additional information on hello suite of tools necessary toohelp in gaining an understanding of cloud spend, please refer too Gartner article [Market Guide for IT Financial Management (ITFM) Tools](http://www.gartner.com/technology/reprints.do?id=1-212F7AL&ct=140909&st=sb).</span></span>

<!--Image references-->
[1]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Overview.png
[2]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-ITFM-Engine-Overview.png
[3]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Analysis-Pie-Chart.png
[4]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Allocation-360-Chart.png
[5]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Cost-Effective-Sizing.png
[6]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Performance-Reports.png
[7]: ./media/billing-usage-rate-card-partner-solution-cloudyn/Cloudyn-Category-Manager.png
