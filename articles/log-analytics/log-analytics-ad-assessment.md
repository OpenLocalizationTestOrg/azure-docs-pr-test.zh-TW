---
title: "aaaOptimize Active Directory 環境與 Azure Log Analytics |Microsoft 文件"
description: "您可以使用 Active Directory 評估解決方案 tooassess hello 定期的風險和健全狀況，伺服器環境的 hello。"
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
ms.openlocfilehash: 63290d95302a9e1d243cd993ac50556ed42b97bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-active-directory-environment-with-hello-active-directory-assessment-solution-in-log-analytics"></a><span data-ttu-id="3d1cb-103">最佳化您的 Active Directory 環境，以 hello Active Directory 評估記錄分析解決方案</span><span class="sxs-lookup"><span data-stu-id="3d1cb-103">Optimize your Active Directory environment with hello Active Directory Assessment solution in Log Analytics</span></span>

![AD 評定符號](./media/log-analytics-ad-assessment/ad-assessment-symbol.png)

<span data-ttu-id="3d1cb-105">您可以使用 Active Directory 評估解決方案 tooassess hello 定期的風險和健全狀況，伺服器環境的 hello。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-105">You can use hello Active Directory Assessment solution tooassess hello risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="3d1cb-106">這篇文章可協助您安裝及使用 hello 解決方案，讓您可以採取修正動作，可能的問題。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-106">This article helps you install and use hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="3d1cb-107">此解決方案提供建議特定 tooyour 部署的伺服器基礎結構的優先順序的清單。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="3d1cb-108">hello 建議是跨四個焦點區域，幫助您快速了解 hello 風險並採取動作分類。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-108">hello recommendations are categorized across four focus areas, which help you quickly understand hello risk and take action.</span></span>

<span data-ttu-id="3d1cb-109">hello 建議根據 hello 知識和乃源自 Microsoft 工程師上千個客戶拜訪所得到的體驗。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-109">hello recommendations are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="3d1cb-110">每項建議均提供問題可能 tooyou 層面，以及如何 tooimplement hello 建議變更的相關指引。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="3d1cb-111">您可以選擇的是最重要的 tooyour 組織及追蹤經營無風險且狀況良好環境的進度焦點區域。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="3d1cb-112">焦點區域的資訊之後您加入 hello 解決方案，並且評估為已完成，摘要顯示 hello **AD 評估**hello 基礎結構，您的環境中的儀表板。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **AD Assessment** dashboard for hello infrastructure in your environment.</span></span> <span data-ttu-id="3d1cb-113">hello 下列各節說明如何 toouse hello 有關 hello **AD 評估**儀表板，您可以在此檢視，並接著採取建議的動作為您的 Active Directory 伺服器基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-113">hello following sections describe how toouse hello information on hello **AD Assessment** dashboard, where you can view and then take recommended actions for your Active Directory server infrastructure.</span></span>

![SQL 評估磚的影像](./media/log-analytics-ad-assessment/ad-tile.png)

![SQL 評估儀表板的影像](./media/log-analytics-ad-assessment/ad-assessment.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="3d1cb-116">安裝和設定 hello 方案</span><span class="sxs-lookup"><span data-stu-id="3d1cb-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="3d1cb-117">使用下列資訊 tooinstall hello 並設定 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-117">Use hello following information tooinstall and configure hello solutions.</span></span>

* <span data-ttu-id="3d1cb-118">必須是評估 hello 網域 toobe 的成員的網域控制站上安裝代理程式。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-118">Agents must be installed on domain controllers that are members of hello domain toobe evaluated.</span></span>
* <span data-ttu-id="3d1cb-119">解決方案需要.NET Framework 4 的支援的版本的 Active Directory 評估 hello (4.5.2 或更新版本) 內含的 OMS 代理程式的每部電腦上安裝。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-119">hello Active Directory Assessment solution requires a supported version of .NET Framework 4 (4.5.2 or above) installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="3d1cb-120">新增 hello Active Directory 評估解決方案 tooyour OMS 工作區從[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-120">Add hello Active Directory Assessment solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ADAssessmentOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>  <span data-ttu-id="3d1cb-121">不需要進一步的組態。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-121">There is no further configuration required.</span></span>

  > [!NOTE]
  > <span data-ttu-id="3d1cb-122">您加入 hello 方案之後，hello AdvisorAssessment.exe 檔案加入 tooservers 與代理程式。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-122">After you've added hello solution, hello AdvisorAssessment.exe file is added tooservers with agents.</span></span> <span data-ttu-id="3d1cb-123">讀取組態資料及傳送 toohello OMS 服務進行處理的 hello 雲端中。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-123">Configuration data is read and then sent toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="3d1cb-124">邏輯是套用的 toohello 接收資料，而 hello 雲端服務會記錄 hello 資料。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-124">Logic is applied toohello received data and hello cloud service records hello data.</span></span>
  >
  >

## <a name="active-directory-assessment-data-collection-details"></a><span data-ttu-id="3d1cb-125">Active Directory 評估資料收集詳細資訊</span><span class="sxs-lookup"><span data-stu-id="3d1cb-125">Active Directory Assessment data collection details</span></span>

<span data-ttu-id="3d1cb-126">Active Directory 評估收集資料，從下列來源使用您已啟用的 hello 代理程式的 hello:</span><span class="sxs-lookup"><span data-stu-id="3d1cb-126">Active Directory Assessment collects data from hello following sources using hello agents that you have enabled:</span></span>

- <span data-ttu-id="3d1cb-127">登錄收集器</span><span class="sxs-lookup"><span data-stu-id="3d1cb-127">Registry collectors</span></span>
- <span data-ttu-id="3d1cb-128">LDAP 收集器</span><span class="sxs-lookup"><span data-stu-id="3d1cb-128">LDAP collectors</span></span>
- <span data-ttu-id="3d1cb-129">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="3d1cb-129">.NET Framework</span></span>
- <span data-ttu-id="3d1cb-130">事件記錄檔收集器</span><span class="sxs-lookup"><span data-stu-id="3d1cb-130">Event log collectors</span></span>
- <span data-ttu-id="3d1cb-131">Active Directory 服務介面 (ADSI)</span><span class="sxs-lookup"><span data-stu-id="3d1cb-131">Active Directory Service interfaces (ADSI)</span></span>
- <span data-ttu-id="3d1cb-132">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3d1cb-132">Windows PowerShell</span></span>
- <span data-ttu-id="3d1cb-133">檔案資料收集器</span><span class="sxs-lookup"><span data-stu-id="3d1cb-133">File data collectors</span></span>
- <span data-ttu-id="3d1cb-134">Windows Management Instrumentation (WMI)</span><span class="sxs-lookup"><span data-stu-id="3d1cb-134">Windows Management Instrumentation (WMI)</span></span>
- <span data-ttu-id="3d1cb-135">DCDIAG 工具 API</span><span class="sxs-lookup"><span data-stu-id="3d1cb-135">DCDIAG tool API</span></span>
- <span data-ttu-id="3d1cb-136">檔案複寫服務 (NTFRS) API</span><span class="sxs-lookup"><span data-stu-id="3d1cb-136">File Replication Service (NTFRS) API</span></span>
- <span data-ttu-id="3d1cb-137">自訂 C# 程式碼</span><span class="sxs-lookup"><span data-stu-id="3d1cb-137">Custom C# code</span></span>


<span data-ttu-id="3d1cb-138">hello 下表顯示資料收集方法，代理程式是否 Operations Manager (SCOM) 為必要項，以及如何通常資料會收集代理程式。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-138">hello following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="3d1cb-139">平台</span><span class="sxs-lookup"><span data-stu-id="3d1cb-139">platform</span></span> | <span data-ttu-id="3d1cb-140">直接代理程式</span><span class="sxs-lookup"><span data-stu-id="3d1cb-140">Direct Agent</span></span> | <span data-ttu-id="3d1cb-141">SCOM 代理程式</span><span class="sxs-lookup"><span data-stu-id="3d1cb-141">SCOM agent</span></span> | <span data-ttu-id="3d1cb-142">Azure 儲存體</span><span class="sxs-lookup"><span data-stu-id="3d1cb-142">Azure Storage</span></span> | <span data-ttu-id="3d1cb-143">SCOM 是否為必要項目？</span><span class="sxs-lookup"><span data-stu-id="3d1cb-143">SCOM required?</span></span> | <span data-ttu-id="3d1cb-144">透過管理群組傳送的 SCOM 代理程式資料</span><span class="sxs-lookup"><span data-stu-id="3d1cb-144">SCOM agent data sent via management group</span></span> | <span data-ttu-id="3d1cb-145">收集頻率</span><span class="sxs-lookup"><span data-stu-id="3d1cb-145">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="3d1cb-146">Windows</span><span class="sxs-lookup"><span data-stu-id="3d1cb-146">Windows</span></span> |<span data-ttu-id="3d1cb-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="3d1cb-147">&#8226;</span></span> |<span data-ttu-id="3d1cb-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="3d1cb-148">&#8226;</span></span> |  |  |<span data-ttu-id="3d1cb-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="3d1cb-149">&#8226;</span></span> |<span data-ttu-id="3d1cb-150">7 天</span><span class="sxs-lookup"><span data-stu-id="3d1cb-150">7 days</span></span> |

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="3d1cb-151">了解建議的排列方式</span><span class="sxs-lookup"><span data-stu-id="3d1cb-151">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="3d1cb-152">每個所做的建議是指定加權值可識別 hello hello 提供建議的相對重要性。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-152">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="3d1cb-153">只有 hello 10 最重要的建議會出現。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-153">Only hello 10 most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="3d1cb-154">加權的計算方式</span><span class="sxs-lookup"><span data-stu-id="3d1cb-154">How weights are calculated</span></span>
<span data-ttu-id="3d1cb-155">加權是彙集以下三個重要因素的值：</span><span class="sxs-lookup"><span data-stu-id="3d1cb-155">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="3d1cb-156">hello*機率*識別問題會造成問題。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-156">hello *probability* that an issue identified causes problems.</span></span> <span data-ttu-id="3d1cb-157">較高的機率等同 tooa 的整體分數較 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-157">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="3d1cb-158">hello*影響*hello 問題如果確實引發問題對您組織。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-158">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="3d1cb-159">較高的影響等同 tooa 的整體分數較 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-159">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="3d1cb-160">hello*投入時間*需要 tooimplement hello 建議。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-160">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="3d1cb-161">勞力較高 tooa 整體分數較低的 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-161">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="3d1cb-162">每個建議的加權 hello hello 總分每個焦點區域的百分比表示。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-162">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="3d1cb-163">例如，如果 hello 安全性和相容性的焦點區域建議的分數為 5%，實作該項建議會增加您整體安全性和法規遵循分數 5%。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-163">For example, if a recommendation in hello Security and Compliance focus area has a score of 5%, implementing that recommendation increases your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="3d1cb-164">焦點區域</span><span class="sxs-lookup"><span data-stu-id="3d1cb-164">Focus areas</span></span>
<span data-ttu-id="3d1cb-165">**安全性和法務遵循** - 這個重點區域會顯示下列項目的建議：潛在安全性威脅和填補缺口、公司原則，以及技術、法律和法務遵循要求。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-165">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="3d1cb-166">**可用性和業務續航力** - 這個重點區域會顯示下列項目的建議：服務可用性、基礎結構備援和企業保護。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-166">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="3d1cb-167">**效能和延展性**-這個焦點區域會顯示建議 toohelp 貴組織的 IT 基礎結構的成長，確保 IT 環境滿足當前的效能需求，以及是無法 toorespond toochanging必須基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-167">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="3d1cb-168">**升級、 移轉和部署**-這個焦點區域會顯示建議 toohelp 升級、 移轉以及部署 Active Directory tooyour 現有基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-168">**Upgrade, Migration and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy Active Directory tooyour existing infrastructure.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="3d1cb-169">您的目標應該 tooscore 100%中每個焦點區域？</span><span class="sxs-lookup"><span data-stu-id="3d1cb-169">Should you aim tooscore 100% in every focus area?</span></span>
<span data-ttu-id="3d1cb-170">不一定。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-170">Not necessarily.</span></span> <span data-ttu-id="3d1cb-171">hello 建議根據 hello 知識和 Microsoft 工程師上千次客戶拜訪而獲得的經驗。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-171">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="3d1cb-172">不過，任何兩個伺服器基礎結構不是 hello 相同，且特定建議可能會增加或減少相關 tooyou。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-172">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="3d1cb-173">例如，某些安全性建議可能比較不相關，如果您的虛擬機器不公開的 toohello 網際網路。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-173">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="3d1cb-174">對於提供低優先順序臨機操作資料收集和報告的服務來說，某些可用性建議的關聯性就會降低。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-174">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="3d1cb-175">重要 tooa 成熟商務問題可能是較不重要的 tooa 啟動。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-175">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="3d1cb-176">您可能想的 tooidentify 哪些個重點是您的優先順序，並再看看分數如何隨著時間變更。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-176">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="3d1cb-177">每項建議都包含其重要性的指引。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-177">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="3d1cb-178">您應該使用此指南 tooevaluate 是否實作 hello 建議適用於您，提供您 IT 服務和 hello 的商務需求的組織的 hello 性質。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-178">You should use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="3d1cb-179">使用評估焦點區域建議</span><span class="sxs-lookup"><span data-stu-id="3d1cb-179">Use assessment focus area recommendations</span></span>
<span data-ttu-id="3d1cb-180">您可以在 OMS 中使用了評估解決方案之前，您必須先安裝的 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-180">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="3d1cb-181">tooread 進一步了解安裝解決方案的更多資訊，請參閱[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-181">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="3d1cb-182">安裝之後，您就可以使用 OMS hello 概觀 頁面上的 hello 評估磚來檢視建議 hello 摘要。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-182">After it is installed, you can view hello summary of recommendations by using hello Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="3d1cb-183">檢視 hello 摘要說明您基礎結構，然後切入到建議的法務遵循。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-183">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="3d1cb-184">tooview 焦點區域，並採取修正動作的建議</span><span class="sxs-lookup"><span data-stu-id="3d1cb-184">tooview recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="3d1cb-185">在 hello**概觀**頁面上，按一下 hello**評估**磚伺服器基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-185">On hello **Overview** page, click hello **Assessment** tile for your server infrastructure.</span></span>
2. <span data-ttu-id="3d1cb-186">在 hello**評估**頁面上，檢閱 hello 其中一種 hello 焦點區域刀鋒的摘要資訊，然後按一下其中一個 tooview 針對該焦點區域的建議。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-186">On hello **Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="3d1cb-187">在任何 hello 焦點區域頁面，您可以檢視針對環境設定優先權的 hello 建議。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-187">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="3d1cb-188">按一下下方的建議**受影響的物件**tooview 有關為何提出 hello 該項建議的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-188">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="3d1cb-189">![評估建議的影像](./media/log-analytics-ad-assessment/ad-focus.png)</span><span class="sxs-lookup"><span data-stu-id="3d1cb-189">![image of Assessment recommendations](./media/log-analytics-ad-assessment/ad-focus.png)</span></span>
4. <span data-ttu-id="3d1cb-190">您可以採取 [建議動作] 中所建議的更正動作。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-190">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="3d1cb-191">Hello 項目已獲得解決之後，已採取建議動作的更新評估記錄，並提高法務遵循分數。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-191">When hello item has been addressed, later assessments records that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="3d1cb-192">更正後的項目將以**通過的物件**呈現。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-192">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="3d1cb-193">忽略建議</span><span class="sxs-lookup"><span data-stu-id="3d1cb-193">Ignore recommendations</span></span>
<span data-ttu-id="3d1cb-194">如果您有想 tooignore 的建議，您可以建立 OMS 將會使用您的評估結果中出現 tooprevent 建議的文字檔。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-194">If you have recommendations that you want tooignore, you can create a text file that OMS will use tooprevent recommendations from appearing in your assessment results.</span></span>

### <a name="tooidentify-recommendations-that-you-will-ignore"></a><span data-ttu-id="3d1cb-195">tooidentify，建議您將會忽略</span><span class="sxs-lookup"><span data-stu-id="3d1cb-195">tooidentify recommendations that you will ignore</span></span>
1. <span data-ttu-id="3d1cb-196">登入 tooyour 工作區，並開啟 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-196">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="3d1cb-197">使用下列查詢 toolist 失敗建議您的環境中電腦的 hello。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-197">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=ADAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
>[!NOTE]
> <span data-ttu-id="3d1cb-198">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-198">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
> `ADAssessmentRecommendation | where RecommendationResult == "Failed" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

   <span data-ttu-id="3d1cb-199">以下是螢幕擷取畫面顯示 hello 記錄搜尋查詢：![失敗的建議](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="3d1cb-199">Here's a screen shot showing hello Log Search query: ![failed recommendations](./media/log-analytics-ad-assessment/ad-failed-recommendations.png)</span></span>
2. <span data-ttu-id="3d1cb-200">選擇您想 tooignore 的建議。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-200">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="3d1cb-201">您會在 hello 下一個程序中使用 RecommendationId hello 值。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-201">You’ll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="3d1cb-202">toocreate 及使用 IgnoreRecommendations.txt 文字檔</span><span class="sxs-lookup"><span data-stu-id="3d1cb-202">toocreate and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="3d1cb-203">建立名為 IgnoreRecommendations.txt 的檔案。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-203">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="3d1cb-204">貼上或輸入您想要記錄分析 tooignore 單獨的一行，然後儲存並關閉 hello 檔案的每個建議的每個 RecommendationId。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-204">Paste or type each RecommendationId for each recommendation that you want Log Analytics tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="3d1cb-205">將 hello 檔案放在 hello 想 OMS tooignore 建議每台電腦上下列資料夾中。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-205">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
   * <span data-ttu-id="3d1cb-206">以 hello Microsoft Monitoring Agent （直接或透過 Operations Manager 連線） 的電腦上*SystemDrive*: \Program Files\Microsoft Monitoring Agent\Agent</span><span class="sxs-lookup"><span data-stu-id="3d1cb-206">On computers with hello Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="3d1cb-207">Hello Operations Manager 管理伺服器- *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="3d1cb-207">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="3d1cb-208">tooverify 建議已忽略</span><span class="sxs-lookup"><span data-stu-id="3d1cb-208">tooverify that recommendations are ignored</span></span>
<span data-ttu-id="3d1cb-209">Hello hello 下一個排程評估執行時，預設每隔 7 天之後, 指定的建議會標示*忽略*並不會出現在 hello 評估儀表板上。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-209">After hello next scheduled assessment runs, by default every 7 days, hello specified recommendations are marked *Ignored* and will not appear on hello assessment dashboard.</span></span>

1. <span data-ttu-id="3d1cb-210">您可以使用下列記錄搜尋查詢 toolist hello 所有 hello 忽略建議。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-210">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

    ```
    Type=ADAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```
>[!NOTE]
> <span data-ttu-id="3d1cb-211">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-211">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
> `ADAssessmentRecommendation | where RecommendationResult == "Ignored" | sort by Computer asc | project Computer, RecommendationId, Recommendation`

2. <span data-ttu-id="3d1cb-212">如果您稍後決定您想要忽略 toosee 建議，移除所有的 IgnoreRecommendations.txt 檔案，或您可以移除其中的 recommendationid。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-212">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="ad-assessment-solutions-faq"></a><span data-ttu-id="3d1cb-213">AD 評估方案常見問題集</span><span class="sxs-lookup"><span data-stu-id="3d1cb-213">AD Assessment solutions FAQ</span></span>
<span data-ttu-id="3d1cb-214">*評估的執行頻率為何？*</span><span class="sxs-lookup"><span data-stu-id="3d1cb-214">*How often does an assessment run?*</span></span>

* <span data-ttu-id="3d1cb-215">hello 評估每 7 天執行。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-215">hello assessment runs every 7 days.</span></span>

<span data-ttu-id="3d1cb-216">*有方法 tooconfigure 頻率 hello 評估執行嗎？*</span><span class="sxs-lookup"><span data-stu-id="3d1cb-216">*Is there a way tooconfigure how often hello assessment runs?*</span></span>

* <span data-ttu-id="3d1cb-217">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-217">Not at this time.</span></span>

<span data-ttu-id="3d1cb-218">*如果我在加入評估方案後探索到另一部伺服器，方案也會評估這部伺服器嗎？*</span><span class="sxs-lookup"><span data-stu-id="3d1cb-218">*If another server for is discovered after I’ve added an assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="3d1cb-219">是的。智慧套件會在探索到該伺服器之後每隔 7 天評估一次。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-219">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="3d1cb-220">*如果伺服器除役，何時將它會移除來自 hello 評估？*</span><span class="sxs-lookup"><span data-stu-id="3d1cb-220">*If a server is decommissioned, when will it be removed from hello assessment?*</span></span>

* <span data-ttu-id="3d1cb-221">如果伺服器在 3 週內未提交任何資料，智慧套件便會將其移除。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-221">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="3d1cb-222">*Hello 沒有 hello 資料收集的 hello 程序的名稱為何？*</span><span class="sxs-lookup"><span data-stu-id="3d1cb-222">*What is hello name of hello process that does hello data collection?*</span></span>

* <span data-ttu-id="3d1cb-223">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="3d1cb-223">AdvisorAssessment.exe</span></span>

<span data-ttu-id="3d1cb-224">*如何花費時間的資料收集的 toobe？*</span><span class="sxs-lookup"><span data-stu-id="3d1cb-224">*How long does it take for data toobe collected?*</span></span>

* <span data-ttu-id="3d1cb-225">hello hello 伺服器上的實際資料收集需費時約 1 小時。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-225">hello actual data collection on hello server takes about 1 hour.</span></span> <span data-ttu-id="3d1cb-226">對於擁有大量 Active Directory 伺服器的伺服器，資料收集可能需要花費更久的時間。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-226">It may take longer on servers that have a large number of Active Directory servers.</span></span>

<span data-ttu-id="3d1cb-227">*有方法 tooconfigure 時收集資料嗎？*</span><span class="sxs-lookup"><span data-stu-id="3d1cb-227">*Is there a way tooconfigure when data is collected?*</span></span>

* <span data-ttu-id="3d1cb-228">目前沒有。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-228">Not at this time.</span></span>

<span data-ttu-id="3d1cb-229">*為什麼只顯示 hello 前 10 項建議？*</span><span class="sxs-lookup"><span data-stu-id="3d1cb-229">*Why display only hello top 10 recommendations?*</span></span>

* <span data-ttu-id="3d1cb-230">與其提供鉅細靡遺的工作清單，我們建議您著重於解決設定優先權的 hello 建議事項第一次。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-230">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="3d1cb-231">解決後，智慧套件將會提供其他建議。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-231">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="3d1cb-232">如果您偏好 toosee hello 詳細的清單，您可以檢視所有建議使用記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-232">If you prefer toosee hello detailed list, you can view all recommendations using Log Search.</span></span>

<span data-ttu-id="3d1cb-233">*是否有方法 tooignore 建議？*</span><span class="sxs-lookup"><span data-stu-id="3d1cb-233">*Is there a way tooignore a recommendation?*</span></span>

* <span data-ttu-id="3d1cb-234">是，請參閱上面的 [忽略建議](#ignore-recommendations) 一節。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-234">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d1cb-235">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d1cb-235">Next steps</span></span>
* <span data-ttu-id="3d1cb-236">使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細 AD 評估資料和建議。</span><span class="sxs-lookup"><span data-stu-id="3d1cb-236">Use [Log searches in Log Analytics](log-analytics-log-searches.md) tooview detailed AD Assessment data and recommendations.</span></span>
