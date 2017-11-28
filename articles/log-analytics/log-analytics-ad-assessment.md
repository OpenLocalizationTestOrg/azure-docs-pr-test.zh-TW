---
title: "使用 Azure Log Analytics 最佳化 Active Directory 環境 | Microsoft Docs"
description: "您可以使用 Active Directory 評估方案定期評估伺服器環境的風險和健全狀況。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 81eb41b8-eb62-4eb2-9f7b-fde5c89c9b47
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 97368f0b9e89ffd0cd982b6e8670d5a1f62ad42c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="optimize-your-active-directory-environment-with-the-active-directory-assessment-solution-in-log-analytics"></a><span data-ttu-id="0a8ab-103">在 Log Analytics 中使用 Active Directory 評估方案來最佳化 Active Directory 環境</span><span class="sxs-lookup"><span data-stu-id="0a8ab-103">Optimize your Active Directory environment with the Active Directory Assessment solution in Log Analytics</span></span>

![AD 評定符號](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

<span data-ttu-id="0a8ab-105">您可以使用 Active Directory 評估方案定期評估伺服器環境的風險和健全狀況。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-105">You can use the Active Directory Assessment solution to assess the risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="0a8ab-106">本文協助您安裝和使用此解決方案，讓您可以針對潛在問題採取修正動作。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-106">This article helps you install and use the solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="0a8ab-107">此方案能針對已部署的伺服器基礎結構提供依照優先順序排列的具體建議清單。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-107">This solution provides a prioritized list of recommendations specific to your deployed server infrastructure.</span></span> <span data-ttu-id="0a8ab-108">建議分為四個焦點區域，它們可以幫助您快速了解風險並採取動作。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-108">The recommendations are categorized across four focus areas, which help you quickly understand the risk and take action.</span></span>

<span data-ttu-id="0a8ab-109">建議乃源自 Microsoft 工程師數千次客戶拜訪所得到的知識和經驗。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-109">The recommendations are based on the knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="0a8ab-110">每項建議均提供問題的影響層面，以及如何實作建議變更等相關指引。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-110">Each recommendation provides guidance about why an issue might matter to you and how to implement the suggested changes.</span></span>

<span data-ttu-id="0a8ab-111">您可以選擇對組織而言最重要的焦點區域，同時追蹤經營無風險且健康狀態良好之環境的進度。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-111">You can choose focus areas that are most important to your organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="0a8ab-112">加入方案且評估完成之後，系統會將焦點區域的摘要資訊顯示在環境之基礎結構的 [AD 評估]  儀表板中。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-112">After you've added the solution and an assessment is completed, summary information for focus areas is shown on the **AD Assessment** dashboard for the infrastructure in your environment.</span></span> <span data-ttu-id="0a8ab-113">下列章節說明如何使用 [AD 評估]  儀表板上的資訊，您可以在這裡檢視 Active Directory 伺服器基礎結構的建議動作並予以實施。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-113">The following sections describe how to use the information on the **AD Assessment** dashboard, where you can view and then take recommended actions for your Active Directory server infrastructure.</span></span>

![SQL 評估磚的影像](./media/log-analytics-ad-assessment/ad-tile.png)

![SQL 評估儀表板的影像](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="0a8ab-116">安裝和設定方案</span><span class="sxs-lookup"><span data-stu-id="0a8ab-116">Installing and configuring the solution</span></span>
<span data-ttu-id="0a8ab-117">請使用下列資訊來安裝和設定方案。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-117">Use the following information to install and configure the solutions.</span></span>

* <span data-ttu-id="0a8ab-118">代理程式必須安裝在隸屬於要評估之網域成員的網域控制站上。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-118">Agents must be installed on domain controllers that are members of the domain to be evaluated.</span></span>
* <span data-ttu-id="0a8ab-119">Active Directory 評估方案需要在具有 OMS 代理程式的每部電腦上都安裝 .NET Framework 4 (4.5.2 或以上) 的支援版本。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-119">The Active Directory Assessment solution requires a supported version of .NET Framework 4 (4.5.2 or above) installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="0a8ab-120">從 [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) 或使用[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)中所述的程序，將 Active Directory 評估方案新增至您的 OMS 工作區。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-120">Add the Active Directory Assessment solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>  <span data-ttu-id="0a8ab-121">不需要進一步的組態。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-121">There is no further configuration required.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0a8ab-122">您加入方案之後，AdvisorAssessment.exe 檔案會以代理程式加入伺服器中。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-122">After you've added the solution, the AdvisorAssessment.exe file is added to servers with agents.</span></span> <span data-ttu-id="0a8ab-123">組態資料會先讀取後再傳送至雲端中的 OMS 服務，以便進行處理。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-123">Configuration data is read and then sent to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="0a8ab-124">會將邏輯套用至接收的資料，且雲端服務會記錄資料。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-124">Logic is applied to the received data and the cloud service records the data.</span></span>
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a><span data-ttu-id="0a8ab-125">Active Directory 評估資料收集詳細資訊</span><span class="sxs-lookup"><span data-stu-id="0a8ab-125">Active Directory Assessment data collection details</span></span>

<span data-ttu-id="0a8ab-126">Active Directory 評定會使用您已啟用的代理程式，從下列來源收集資料：</span><span class="sxs-lookup"><span data-stu-id="0a8ab-126">Active Directory Assessment collects data from the following sources using the agents that you have enabled:</span></span>

- <span data-ttu-id="0a8ab-127">登錄收集器</span><span class="sxs-lookup"><span data-stu-id="0a8ab-127">Registry collectors</span></span>
- <span data-ttu-id="0a8ab-128">LDAP 收集器</span><span class="sxs-lookup"><span data-stu-id="0a8ab-128">LDAP collectors</span></span>
- <span data-ttu-id="0a8ab-129">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="0a8ab-129">.NET Framework</span></span>
- <span data-ttu-id="0a8ab-130">事件記錄檔收集器</span><span class="sxs-lookup"><span data-stu-id="0a8ab-130">Event log collectors</span></span>
- <span data-ttu-id="0a8ab-131">Active Directory 服務介面 (ADSI)</span><span class="sxs-lookup"><span data-stu-id="0a8ab-131">Active Directory Service interfaces (ADSI)</span></span>
- <span data-ttu-id="0a8ab-132">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="0a8ab-132">Windows PowerShell</span></span>
- <span data-ttu-id="0a8ab-133">檔案資料收集器</span><span class="sxs-lookup"><span data-stu-id="0a8ab-133">File data collectors</span></span>
- <span data-ttu-id="0a8ab-134">Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="0a8ab-134">Windows Management Instrumentation (WMI)</span></span>
- <span data-ttu-id="0a8ab-135">DCDIAG 工具 API</span><span class="sxs-lookup"><span data-stu-id="0a8ab-135">DCDIAG tool API</span></span>
- <span data-ttu-id="0a8ab-136">檔案複寫服務 (NTFRS) API</span><span class="sxs-lookup"><span data-stu-id="0a8ab-136">File Replication Service (NTFRS) API</span></span>
- <span data-ttu-id="0a8ab-137">自訂 C# 程式碼</span><span class="sxs-lookup"><span data-stu-id="0a8ab-137">Custom C# code</span></span>


<span data-ttu-id="0a8ab-138">下表顯示代理程式的資料收集方法、是否需要 Operations Manager (SCOM)，以及如何代理程式收集資料的頻率。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-138">The following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="0a8ab-139">平台</span><span class="sxs-lookup"><span data-stu-id="0a8ab-139">platform</span></span> | <span data-ttu-id="0a8ab-140">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="0a8ab-140">Direct Agent</span></span> | <span data-ttu-id="0a8ab-141">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="0a8ab-141">SCOM agent</span></span> | <span data-ttu-id="0a8ab-142">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="0a8ab-142">Azure Storage</span></span> | <span data-ttu-id="0a8ab-143">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="0a8ab-143">SCOM required?</span></span> | <span data-ttu-id="0a8ab-144">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="0a8ab-144">SCOM agent data sent via management group</span></span> | <span data-ttu-id="0a8ab-145">收集頻率</span><span class="sxs-lookup"><span data-stu-id="0a8ab-145">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0a8ab-146">Windows</span><span class="sxs-lookup"><span data-stu-id="0a8ab-146">Windows</span></span> |<span data-ttu-id="0a8ab-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="0a8ab-147">&#8226;</span></span> |<span data-ttu-id="0a8ab-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="0a8ab-148">&#8226;</span></span> |  |  |<span data-ttu-id="0a8ab-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="0a8ab-149">&#8226;</span></span> |<span data-ttu-id="0a8ab-150">7 天</span><span class="sxs-lookup"><span data-stu-id="0a8ab-150">7 days</span></span> |

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="0a8ab-151">了解建議的排列方式</span><span class="sxs-lookup"><span data-stu-id="0a8ab-151">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="0a8ab-152">智慧套件會為每項建議指派加權值，該值能顯現建議的相對重要性。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-152">Every recommendation made is given a weighting value that identifies the relative importance of the recommendation.</span></span> <span data-ttu-id="0a8ab-153">只會顯示最重要的 10 個建議。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-153">Only the 10 most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="0a8ab-154">加權的計算方式</span><span class="sxs-lookup"><span data-stu-id="0a8ab-154">How weights are calculated</span></span>
<span data-ttu-id="0a8ab-155">加權是彙集以下三個重要因素的值：</span><span class="sxs-lookup"><span data-stu-id="0a8ab-155">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="0a8ab-156">識別之疑難引發問題的機率。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-156">The *probability* that an issue identified causes problems.</span></span> <span data-ttu-id="0a8ab-157">機率較高等同於建議的整體分數較高。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-157">A higher probability equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="0a8ab-158">疑難對組織的 *影響力* (如果確實引發問題)。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-158">The *impact* of the issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="0a8ab-159">影響力較高等同於建議的整體分數較高。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-159">A higher impact equates to a larger overall score for the recommendation.</span></span>
* <span data-ttu-id="0a8ab-160">實作建議所需的 *勞力* 。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-160">The *effort* required to implement the recommendation.</span></span> <span data-ttu-id="0a8ab-161">勞力較高等同於建議的整體分數較低。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-161">A higher effort equates to a smaller overall score for the recommendation.</span></span>

<span data-ttu-id="0a8ab-162">每項建議之加權的表示採用每個焦點區域之總分的百分比。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-162">The weighting for each recommendation is expressed as a percentage of the total score available for each focus area.</span></span> <span data-ttu-id="0a8ab-163">例如，如果針對安全性和法務遵循焦點區域之建議的分數為 5%，代表實作該項建議能增加 5% 的安全性和法務遵循整體分數。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-163">For example, if a recommendation in the Security and Compliance focus area has a score of 5%, implementing that recommendation increases your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="0a8ab-164">焦點區域</span><span class="sxs-lookup"><span data-stu-id="0a8ab-164">Focus areas</span></span>
<span data-ttu-id="0a8ab-165">**安全性和法務遵循** - 這個重點區域會顯示下列項目的建議：潛在安全性威脅和填補缺口、公司原則，以及技術、法律和法務遵循要求。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-165">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="0a8ab-166">**可用性和業務續航力** - 這個重點區域會顯示下列項目的建議：服務可用性、基礎結構備援和企業保護。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-166">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="0a8ab-167">**效能和延展性** - 這個重點區域會顯示建議來協助貴組織的 IT 基礎結構成長、確定您的 IT 環境是否符合目前的效能需求，而且能夠回應不斷變動的基礎結構需求。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-167">**Performance and Scalability** - This focus area shows recommendations to help your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able to respond to changing infrastructure needs.</span></span>

<span data-ttu-id="0a8ab-168">**升級、移轉和部署** - 這個焦點區域顯示建議來協助您升級、移轉和部署 Active Directory 到您的現有基礎結構。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-168">**Upgrade, Migration and Deployment** - This focus area shows recommendations to help you upgrade, migrate, and deploy Active Directory to your existing infrastructure.</span></span>

### <a name="should-you-aim-to-score-100-in-every-focus-area"></a><span data-ttu-id="0a8ab-169">我應該為每個焦點區域訂定 100% 的分數嗎？</span><span class="sxs-lookup"><span data-stu-id="0a8ab-169">Should you aim to score 100% in every focus area?</span></span>
<span data-ttu-id="0a8ab-170">不一定。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-170">Not necessarily.</span></span> <span data-ttu-id="0a8ab-171">建議乃源自 Microsoft 工程師上千次客戶拜訪所得到的知識和經驗。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-171">The recommendations are based on the knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="0a8ab-172">然而，世界上沒有兩個一模一樣的伺服器基礎結構，因此特定建議與您的關聯性可能會有所增減。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-172">However, no two server infrastructures are the same, and specific recommendations may be more or less relevant to you.</span></span> <span data-ttu-id="0a8ab-173">例如，如果您的虛擬機器並未暴露在網際網路中，某些安全性建議的關聯性就會降低。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-173">For example, some security recommendations might be less relevant if your virtual machines are not exposed to the Internet.</span></span> <span data-ttu-id="0a8ab-174">對於提供低優先順序臨機操作資料收集和報告的服務來說，某些可用性建議的關聯性就會降低。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-174">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="0a8ab-175">會對成熟企業造成重大影響的問題，不見得會對新公司造成同等嚴重的影響。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-175">Issues that are important to a mature business may be less important to a start-up.</span></span> <span data-ttu-id="0a8ab-176">因此，建議您先找出自己的優先焦點區域，然後觀察一段時間內的分數變化。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-176">You may want to identify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="0a8ab-177">每項建議都包含其重要性的指引。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-177">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="0a8ab-178">在已知 IT 服務之本質和組織之商務需求的情況下，您應使用該指引來評估實作建議的適當性。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-178">You should use this guidance to evaluate whether implementing the recommendation is appropriate for you, given the nature of your IT services and the business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="0a8ab-179">使用評估焦點區域建議</span><span class="sxs-lookup"><span data-stu-id="0a8ab-179">Use assessment focus area recommendations</span></span>
<span data-ttu-id="0a8ab-180">在使用 OMS 中的評估方案之前，您必須先安裝方案。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-180">Before you can use an assessment solution in OMS, you must have the solution installed.</span></span> <span data-ttu-id="0a8ab-181">如需閱讀安裝方案的更多資訊，請參閱 [從方案庫加入 Log Analytics 方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-181">To read more about installing solutions, see [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="0a8ab-182">安裝之後，您可以在 OMS 中使用 [概觀] 頁面上的 [評估] 圖格檢視建議摘要。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-182">After it is installed, you can view the summary of recommendations by using the Assessment tile on the Overview page in OMS.</span></span>

<span data-ttu-id="0a8ab-183">檢視基礎結構的總結法務遵循評估結果，然後再深入鑽研建議事項。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-183">View the summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="to-view-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="0a8ab-184">檢視的焦點區域的建議並採取更正措施</span><span class="sxs-lookup"><span data-stu-id="0a8ab-184">To view recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="0a8ab-185">在 [概觀] 頁面中，按一下伺服器基礎結構的 [評估] 圖格。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-185">On the **Overview** page, click the **Assessment** tile for your server infrastructure.</span></span>
2. <span data-ttu-id="0a8ab-186">在 [ **評估** ] 頁面中檢閱任一焦點區域分葉中的摘要資訊，然後按一下焦點區域以檢視建議。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-186">On the **Assessment** page, review the summary information in one of the focus area blades and then click one to view recommendations for that focus area.</span></span>
3. <span data-ttu-id="0a8ab-187">在任一焦點區域頁面中，您可以檢視針對環境且按照優先順序排列的建議。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-187">On any of the focus area pages, you can view the prioritized recommendations made for your environment.</span></span> <span data-ttu-id="0a8ab-188">按一下 [受影響的物件]  下方的建議，可檢視建議提出原因的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-188">Click a recommendation under **Affected Objects** to view details about why the recommendation is made.</span></span>  
    <span data-ttu-id="0a8ab-189">![評估建議的影像](./media/log-analytics-ad-assessment/ad-focus.png)</span><span class="sxs-lookup"><span data-stu-id="0a8ab-189">![image of Assessment recommendations](./media/log-analytics-ad-assessment/ad-focus.png)</span></span>
4. <span data-ttu-id="0a8ab-190">您可以採取 [建議動作] 中所建議的更正動作。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-190">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="0a8ab-191">當您解決某個項目後，後續評估會記錄您實施的建議動作並提高法務遵循分數。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-191">When the item has been addressed, later assessments records that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="0a8ab-192">更正後的項目將以**通過的物件**呈現。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-192">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="0a8ab-193">忽略建議</span><span class="sxs-lookup"><span data-stu-id="0a8ab-193">Ignore recommendations</span></span>
<span data-ttu-id="0a8ab-194">如果您有想要忽略的建議，則可以建立 OMS 將用來防止建議出現在您評估結果的文字檔。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-194">If you have recommendations that you want to ignore, you can create a text file that OMS will use to prevent recommendations from appearing in your assessment results.</span></span>

### <a name="to-identify-recommendations-that-you-will-ignore"></a><span data-ttu-id="0a8ab-195">識別您將忽略的建議</span><span class="sxs-lookup"><span data-stu-id="0a8ab-195">To identify recommendations that you will ignore</span></span>
1. <span data-ttu-id="0a8ab-196">登入您的工作區，並開啟記錄檔搜尋。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-196">Sign in to your workspace and open Log Search.</span></span> <span data-ttu-id="0a8ab-197">使用下列查詢來列出您環境中電腦的失敗建議。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-197">Use the following query to list recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> <span data-ttu-id="0a8ab-198">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則以上查詢會變更如下。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-198">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   <span data-ttu-id="0a8ab-199">以下是顯示記錄檔搜尋查詢的螢幕擷取畫面︰![失敗的建議](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="0a8ab-199">Here's a screen shot showing the Log Search query: ![failed recommendations](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)</span></span>
2. <span data-ttu-id="0a8ab-200">選擇您想要忽略的建議。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-200">Choose recommendations that you want to ignore.</span></span> <span data-ttu-id="0a8ab-201">您將使用下一個程序中的 RecommendationId 值。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-201">You’ll use the values for RecommendationId in the next procedure.</span></span>

### <a name="to-create-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="0a8ab-202">建立及使用 IgnoreRecommendations.txt 文字檔案</span><span class="sxs-lookup"><span data-stu-id="0a8ab-202">To create and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="0a8ab-203">建立名為 IgnoreRecommendations.txt 的檔案。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-203">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="0a8ab-204">在個別行上貼上或輸入您想要 Log Analytics 忽略之每個建議的各個 RecommendationId，然後儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-204">Paste or type each RecommendationId for each recommendation that you want Log Analytics to ignore on a separate line and then save and close the file.</span></span>
3. <span data-ttu-id="0a8ab-205">將檔案放在您想要 OMS 忽略建議之每一部電腦的下列資料夾中。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-205">Put the file in the following folder on each computer where you want OMS to ignore recommendations.</span></span>
   * <span data-ttu-id="0a8ab-206">在具有 Microsoft Monitoring Agent 的電腦 (直接連線或透過 Operations Manager 連線) 上 - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="0a8ab-206">On computers with the Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="0a8ab-207">在 Operations Manager 管理伺服器上 - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="0a8ab-207">On the Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="to-verify-that-recommendations-are-ignored"></a><span data-ttu-id="0a8ab-208">驗證已忽略建議</span><span class="sxs-lookup"><span data-stu-id="0a8ab-208">To verify that recommendations are ignored</span></span>
<span data-ttu-id="0a8ab-209">在執行下一個排定的評估之後，依預設是每隔 7 天執行一次，指定的建議會標示為「忽略」  ，且不會出現在評估儀表板上。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-209">After the next scheduled assessment runs, by default every 7 days, the specified recommendations are marked *Ignored* and will not appear on the assessment dashboard.</span></span>

1. <span data-ttu-id="0a8ab-210">您可以使用下列記錄搜尋查詢列出所有已忽略的建議。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-210">You can use the following Log Search queries to list all the ignored recommendations.</span></span>

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> <span data-ttu-id="0a8ab-211">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則以上查詢會變更如下。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-211">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. <span data-ttu-id="0a8ab-212">如果您稍後決定想要查看忽略的建議，請移除任何 IgnoreRecommendations.txt 檔案，或從中移除 RecommendationID。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-212">If you decide later that you want to see ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="ad-assessment-solutions-faq"></a><span data-ttu-id="0a8ab-213">AD 評估方案常見問題集</span><span class="sxs-lookup"><span data-stu-id="0a8ab-213">AD Assessment solutions FAQ</span></span>
<span data-ttu-id="0a8ab-214">*評估的執行頻率為何？*</span><span class="sxs-lookup"><span data-stu-id="0a8ab-214">*How often does an assessment run?*</span></span>

* <span data-ttu-id="0a8ab-215">評估會每隔 7 天執行一次。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-215">The assessment runs every 7 days.</span></span>

<span data-ttu-id="0a8ab-216">*是否有設定評估執行頻率的方法？*</span><span class="sxs-lookup"><span data-stu-id="0a8ab-216">*Is there a way to configure how often the assessment runs?*</span></span>

* <span data-ttu-id="0a8ab-217">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-217">Not at this time.</span></span>

<span data-ttu-id="0a8ab-218">*如果我在加入評估方案後探索到另一部伺服器，方案也會評估這部伺服器嗎？*</span><span class="sxs-lookup"><span data-stu-id="0a8ab-218">*If another server for is discovered after I’ve added an assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="0a8ab-219">是的。智慧套件會在探索到該伺服器之後每隔 7 天評估一次。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-219">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="0a8ab-220">*如果把伺服器除役，何時能將它從評估中移除？*</span><span class="sxs-lookup"><span data-stu-id="0a8ab-220">*If a server is decommissioned, when will it be removed from the assessment?*</span></span>

* <span data-ttu-id="0a8ab-221">如果伺服器在 3 週內未提交任何資料，智慧套件便會將其移除。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-221">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="0a8ab-222">*負責收集資料之處理序的名稱為何？*</span><span class="sxs-lookup"><span data-stu-id="0a8ab-222">*What is the name of the process that does the data collection?*</span></span>

* <span data-ttu-id="0a8ab-223">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="0a8ab-223">AdvisorAssessment.exe</span></span>

<span data-ttu-id="0a8ab-224">*收集資料需要花費多少時間？*</span><span class="sxs-lookup"><span data-stu-id="0a8ab-224">*How long does it take for data to be collected?*</span></span>

* <span data-ttu-id="0a8ab-225">伺服器上的實際資料收集需費時約 1 小時。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-225">The actual data collection on the server takes about 1 hour.</span></span> <span data-ttu-id="0a8ab-226">對於擁有大量 Active Directory 伺服器的伺服器，資料收集可能需要花費更久的時間。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-226">It may take longer on servers that have a large number of Active Directory servers.</span></span>

<span data-ttu-id="0a8ab-227">*是否有設定資料收集時間的方法？*</span><span class="sxs-lookup"><span data-stu-id="0a8ab-227">*Is there a way to configure when data is collected?*</span></span>

* <span data-ttu-id="0a8ab-228">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-228">Not at this time.</span></span>

<span data-ttu-id="0a8ab-229">*為什麼只顯示前 10 項建議？*</span><span class="sxs-lookup"><span data-stu-id="0a8ab-229">*Why display only the top 10 recommendations?*</span></span>

* <span data-ttu-id="0a8ab-230">與其提供鉅細靡遺的工作清單，我們建議您先著重於解決優先建議事項。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-230">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing the prioritized recommendations first.</span></span> <span data-ttu-id="0a8ab-231">解決後，智慧套件將會提供其他建議。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-231">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="0a8ab-232">如果您想要查看詳細清單，可以使用記錄檔搜尋來檢視所有建議。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-232">If you prefer to see the detailed list, you can view all recommendations using Log Search.</span></span>

<span data-ttu-id="0a8ab-233">*是否有忽略建議的方法？*</span><span class="sxs-lookup"><span data-stu-id="0a8ab-233">*Is there a way to ignore a recommendation?*</span></span>

* <span data-ttu-id="0a8ab-234">是，請參閱上面的 [忽略建議](#ignore-recommendations) 一節。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-234">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0a8ab-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0a8ab-235">Next steps</span></span>
* <span data-ttu-id="0a8ab-236">使用 [Log Analytics 中的記錄檔搜尋](log-analytics-log-searches.md) ，可檢視詳細的 AD 評估資料和建議。</span><span class="sxs-lookup"><span data-stu-id="0a8ab-236">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed AD Assessment data and recommendations.</span></span>
