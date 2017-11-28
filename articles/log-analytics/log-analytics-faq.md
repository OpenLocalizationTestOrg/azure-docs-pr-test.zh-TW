---
title: "aaaLog Analytics 常見問題集 |Microsoft 文件"
description: "Hello Azure 記錄分析服務相關常見問題的解答 toofrequently。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ad536ff7-2c60-4850-a46d-230bc9e1ab45
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte
ms.openlocfilehash: 25931f521cbb6ec840184221c6c1a5794b3445f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-faq"></a><span data-ttu-id="e6c47-103">Log Analytics 常見問題集</span><span class="sxs-lookup"><span data-stu-id="e6c47-103">Log Analytics FAQ</span></span>
<span data-ttu-id="e6c47-104">此 Microsoft 常見問題集是 Microsoft Operations Management Suite (OMS) 中 Log Analytics 常見問題的清單。</span><span class="sxs-lookup"><span data-stu-id="e6c47-104">This Microsoft FAQ is a list of commonly asked questions about Log Analytics in Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="e6c47-105">如果您有任何關於記錄分析的其他問題，請移至 toohello[討論區論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights)並張貼您的問題。</span><span class="sxs-lookup"><span data-stu-id="e6c47-105">If you have any additional questions about Log Analytics, go toohello [discussion forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) and post your questions.</span></span> <span data-ttu-id="e6c47-106">當常見問題集問題時，我們將其新增 toothis 發行項，讓它可以快速且輕鬆地找到。</span><span class="sxs-lookup"><span data-stu-id="e6c47-106">When a question is frequently asked, we add it toothis article so that it can be found quickly and easily.</span></span>

## <a name="general"></a><span data-ttu-id="e6c47-107">一般</span><span class="sxs-lookup"><span data-stu-id="e6c47-107">General</span></span>

### <a name="q-does-log-analytics-use-hello-same-agent-as-azure-security-center"></a><span data-ttu-id="e6c47-108">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-108">Q.</span></span> <span data-ttu-id="e6c47-109">記錄分析會使用 hello 以 Azure 資訊安全中心的相同代理程式嗎？</span><span class="sxs-lookup"><span data-stu-id="e6c47-109">Does Log Analytics use hello same agent as Azure Security Center?</span></span>

<span data-ttu-id="e6c47-110">A.</span><span class="sxs-lookup"><span data-stu-id="e6c47-110">A.</span></span> <span data-ttu-id="e6c47-111">Azure 資訊安全中心早期年 6 月 2017，開始使用 hello Microsoft Monitoring Agent toocollect 和存放區資料。</span><span class="sxs-lookup"><span data-stu-id="e6c47-111">In early June 2017, Azure Security Center began using hello Microsoft Monitoring Agent toocollect and store data.</span></span> <span data-ttu-id="e6c47-112">詳細資訊，請參閱 toolearn [Azure 安全性 Center 平台移轉常見問題集](../security-center/security-center-platform-migration-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="e6c47-112">toolearn more, see [Azure Security Center Platform Migration FAQ](../security-center/security-center-platform-migration-faq.md).</span></span>

### <a name="q-what-checks-are-performed-by-hello-ad-and-sql-assessment-solutions"></a><span data-ttu-id="e6c47-113">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-113">Q.</span></span> <span data-ttu-id="e6c47-114">Hello AD 和 SQL 評估解決方案會執行哪些檢查？</span><span class="sxs-lookup"><span data-stu-id="e6c47-114">What checks are performed by hello AD and SQL Assessment solutions?</span></span>

<span data-ttu-id="e6c47-115">A.</span><span class="sxs-lookup"><span data-stu-id="e6c47-115">A.</span></span> <span data-ttu-id="e6c47-116">hello 下列查詢顯示目前執行的所有檢查的描述：</span><span class="sxs-lookup"><span data-stu-id="e6c47-116">hello following query shows a description of all checks currently performed:</span></span>

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

<span data-ttu-id="e6c47-117">hello 結果可以匯出的 tooExcel 供進一步檢閱。</span><span class="sxs-lookup"><span data-stu-id="e6c47-117">hello results can then be exported tooExcel for further review.</span></span>

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a><span data-ttu-id="e6c47-118">問：為什麼我在 System Center Operations Manager 主控台中看到與 *OMS* 不同的項目？</span><span class="sxs-lookup"><span data-stu-id="e6c47-118">Q: Why do I see something different than *OMS* in System Center Operations Manager console?</span></span>

<span data-ttu-id="e6c47-119">答：根據您所採用的 Operations Manager 更新彙總套件而定，您可能會看到 *System Center Advisor*、*Operational Insights* 或 *Log Analytics* 節點。</span><span class="sxs-lookup"><span data-stu-id="e6c47-119">A: Depending on what Update Rollup of Operations Manager you are on, you may see a node for *System Center Advisor*, *Operational Insights*, or *Log Analytics*.</span></span>

<span data-ttu-id="e6c47-120">太 hello 文字字串更新*OMS*包含需要 toobe 手動方式匯入管理組件中。</span><span class="sxs-lookup"><span data-stu-id="e6c47-120">hello text string update too*OMS* is included in a management pack, which needs toobe imported manually.</span></span> <span data-ttu-id="e6c47-121">toosee hello 目前的文字和功能，依照 hello 指示 hello 最新版 System Center Operations Manager 更新彙總套件知識庫文件並重新整理 hello 主控台。</span><span class="sxs-lookup"><span data-stu-id="e6c47-121">toosee hello current text and functionality, follow hello instructions on hello latest System Center Operations Manager Update Rollup KB article and refresh hello console.</span></span>

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a><span data-ttu-id="e6c47-122">問：Log Analytics 是否有「內部部署」版本？</span><span class="sxs-lookup"><span data-stu-id="e6c47-122">Q: Is there an *on-premises* version of Log Analytics?</span></span>

<span data-ttu-id="e6c47-123">答：否。</span><span class="sxs-lookup"><span data-stu-id="e6c47-123">A: No.</span></span> <span data-ttu-id="e6c47-124">Log Analytics 可以處理並儲存大量資料。</span><span class="sxs-lookup"><span data-stu-id="e6c47-124">Log Analytics processes and stores large amounts of data.</span></span> <span data-ttu-id="e6c47-125">為雲端服務時，記錄分析會無法 tooscale 接如有必要，並避免任何效能影響 tooyour 環境。</span><span class="sxs-lookup"><span data-stu-id="e6c47-125">As a cloud service, Log Analytics is able tooscale-up if necessary and avoid any performance impact tooyour environment.</span></span>

<span data-ttu-id="e6c47-126">其他優點包括：</span><span class="sxs-lookup"><span data-stu-id="e6c47-126">Additional benefits include:</span></span>
- <span data-ttu-id="e6c47-127">Microsoft 執行 hello 記錄分析基礎結構，您節省成本</span><span class="sxs-lookup"><span data-stu-id="e6c47-127">Microsoft runs hello Log Analytics infrastructure, saving you costs</span></span>
- <span data-ttu-id="e6c47-128">定期部署功能更新和修正程式。</span><span class="sxs-lookup"><span data-stu-id="e6c47-128">Regular deployment of feature updates and fixes.</span></span>

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a><span data-ttu-id="e6c47-129">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-129">Q.</span></span> <span data-ttu-id="e6c47-130">如何針對 Log Analytics 不再收集資料的問題進行疑難排解？</span><span class="sxs-lookup"><span data-stu-id="e6c47-130">How do I troubleshoot that Log Analytics is no longer collecting data?</span></span>

<span data-ttu-id="e6c47-131">答： 如果您是 hello 免費定價層上，而且已在一天傳送超過 500 MB 的資料，就會停止 hello rest hello 一天的資料收集。</span><span class="sxs-lookup"><span data-stu-id="e6c47-131">A: If you are on hello free pricing tier and have sent more than 500 MB of data in a day, data collection stops for hello rest of hello day.</span></span> <span data-ttu-id="e6c47-132">到達 hello 每日限制為記錄分析會停止收集資料，一個常見原因，或出現 toobe 資料遺失。</span><span class="sxs-lookup"><span data-stu-id="e6c47-132">Reaching hello daily limit is a common reason that Log Analytics stops collecting data, or data appears toobe missing.</span></span>

<span data-ttu-id="e6c47-133">當資料收集開始及停止時，Log Analytics 會建立 *Operation* 類型的事件。</span><span class="sxs-lookup"><span data-stu-id="e6c47-133">Log Analytics creates an event of type *Operation* when data collection starts and stops.</span></span> 

<span data-ttu-id="e6c47-134">執行下列查詢中搜尋 toocheck，如果您是達到 hello 每日限制，而且找不到資料的 hello:`Type=Operation OperationCategory="Data Collection Status"`</span><span class="sxs-lookup"><span data-stu-id="e6c47-134">Run hello following query in search toocheck if you are reaching hello daily limit and missing data: `Type=Operation OperationCategory="Data Collection Status"`</span></span>

<span data-ttu-id="e6c47-135">當資料收集會停止，hello *OperationStatus*是**警告**。</span><span class="sxs-lookup"><span data-stu-id="e6c47-135">When data collection stops, hello *OperationStatus* is **Warning**.</span></span> <span data-ttu-id="e6c47-136">當資料收集開始，hello *OperationStatus*是**Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="e6c47-136">When data collection starts, hello *OperationStatus* is **Succeeded**.</span></span> 

<span data-ttu-id="e6c47-137">hello 下表描述停止資料收集的原因和建議的動作 tooresume 資料收集：</span><span class="sxs-lookup"><span data-stu-id="e6c47-137">hello following table describes reasons that data collection stops and a suggested action tooresume data collection:</span></span>

| <span data-ttu-id="e6c47-138">資料收集停止的原因</span><span class="sxs-lookup"><span data-stu-id="e6c47-138">Reason data collection stops</span></span>                       | <span data-ttu-id="e6c47-139">tooresume 資料收集</span><span class="sxs-lookup"><span data-stu-id="e6c47-139">tooresume data collection</span></span> |
| -------------------------------------------------- | ----------------  |
| <span data-ttu-id="e6c47-140">已達免費資料的每日限制<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="e6c47-140">Daily limit of free data reached<sup>1</sup></span></span>       | <span data-ttu-id="e6c47-141">等候 hello 下列天集合 tooautomatically 重新啟動，或</span><span class="sxs-lookup"><span data-stu-id="e6c47-141">Wait until hello following day for collection tooautomatically restart, or</span></span><br> <span data-ttu-id="e6c47-142">變更 tooa 付費定價層</span><span class="sxs-lookup"><span data-stu-id="e6c47-142">Change tooa paid pricing tier</span></span> |
| <span data-ttu-id="e6c47-143">Azure 訂用帳戶處於暫停狀態，原因如下：</span><span class="sxs-lookup"><span data-stu-id="e6c47-143">Azure subscription is in a suspended state due to:</span></span> <br> <span data-ttu-id="e6c47-144">免費試用已結束</span><span class="sxs-lookup"><span data-stu-id="e6c47-144">Free trial ended</span></span> <br> <span data-ttu-id="e6c47-145">Azure Pass 已過期</span><span class="sxs-lookup"><span data-stu-id="e6c47-145">Azure pass expired</span></span> <br> <span data-ttu-id="e6c47-146">已達每月消費限制 (例如 MSDN 或 Visual Studio 訂閱)</span><span class="sxs-lookup"><span data-stu-id="e6c47-146">Monthly spending limit reached (for example on an MSDN or Visual Studio subscription)</span></span>                          | <span data-ttu-id="e6c47-147">轉換 tooa 付費訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e6c47-147">Convert tooa paid subscription</span></span> <br> <span data-ttu-id="e6c47-148">轉換 tooa 付費訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="e6c47-148">Convert tooa paid subscription</span></span> <br> <span data-ttu-id="e6c47-149">移除限制，或等到限制重設</span><span class="sxs-lookup"><span data-stu-id="e6c47-149">Remove limit, or wait until limit resets</span></span> |

<span data-ttu-id="e6c47-150"><sup>1</sup>如果您的工作區在 hello 免費定價層，您只能 toosending 500 MB 的每個日期 toohello 服務的資料。</span><span class="sxs-lookup"><span data-stu-id="e6c47-150"><sup>1</sup> If your workspace is on hello free pricing tier, you're limited toosending 500 MB of data per day toohello service.</span></span> <span data-ttu-id="e6c47-151">達到 hello 每日限制，就會停止資料收集直到隔天 hello。</span><span class="sxs-lookup"><span data-stu-id="e6c47-151">When you reach hello daily limit, data collection stops until hello next day.</span></span> <span data-ttu-id="e6c47-152">在資料收集停止時所傳送的資料不會編製索引，而且無法供搜尋使用。</span><span class="sxs-lookup"><span data-stu-id="e6c47-152">Data sent while data collection is stopped is not indexed and is not available for searching.</span></span> <span data-ttu-id="e6c47-153">當資料收集繼續時，只會處理傳送的新資料。</span><span class="sxs-lookup"><span data-stu-id="e6c47-153">When data collection resumes, processing occurs only for new data sent.</span></span> 

<span data-ttu-id="e6c47-154">Log Analytics 使用 UTC 時間，而且每天從午夜 UTC 開始。</span><span class="sxs-lookup"><span data-stu-id="e6c47-154">Log Analytics uses UTC time and each day starts at midnight UTC.</span></span> <span data-ttu-id="e6c47-155">如果 hello 工作區已達到 hello 每日限制，處理會繼續在 hello 第一個小時的 hello 下一步的 UTC 日。</span><span class="sxs-lookup"><span data-stu-id="e6c47-155">If hello workspace reaches hello daily limit, processing resumes during hello first hour of hello next UTC day.</span></span>

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a><span data-ttu-id="e6c47-156">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-156">Q.</span></span> <span data-ttu-id="e6c47-157">如何在資料收集停止時收到通知？</span><span class="sxs-lookup"><span data-stu-id="e6c47-157">How can I be notified when data collection stops?</span></span>

<span data-ttu-id="e6c47-158">答： 請使用 hello 中所述的步驟[建立警示規則](log-analytics-alerts-creating.md#create-an-alert-rule)toobe 通知時停止資料收集。</span><span class="sxs-lookup"><span data-stu-id="e6c47-158">A: Use hello steps described in [create an alert rule](log-analytics-alerts-creating.md#create-an-alert-rule) toobe notified when data collection stops.</span></span>

<span data-ttu-id="e6c47-159">在建立 hello 警示停止資料收集時，設定:</span><span class="sxs-lookup"><span data-stu-id="e6c47-159">When creating hello alert for when data collection stops, set the:</span></span>
- <span data-ttu-id="e6c47-160">**名稱**太*停止資料收集*</span><span class="sxs-lookup"><span data-stu-id="e6c47-160">**Name** too*Data collection stopped*</span></span>
- <span data-ttu-id="e6c47-161">**嚴重性**太*警告*</span><span class="sxs-lookup"><span data-stu-id="e6c47-161">**Severity** too*Warning*</span></span>
- <span data-ttu-id="e6c47-162">**搜尋查詢**太`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`</span><span class="sxs-lookup"><span data-stu-id="e6c47-162">**Search query** too`Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`</span></span>
- <span data-ttu-id="e6c47-163">**時間間隔**太*2 小時*。</span><span class="sxs-lookup"><span data-stu-id="e6c47-163">**Time window** too*2 Hours*.</span></span>
- <span data-ttu-id="e6c47-164">**警示頻率**toobe 一小時後 hello 使用量資料只會更新每小時一次。</span><span class="sxs-lookup"><span data-stu-id="e6c47-164">**Alert frequency** toobe one hour since hello usage data only updates once per hour.</span></span>
- <span data-ttu-id="e6c47-165">**產生警示根據**toobe*的結果數目*</span><span class="sxs-lookup"><span data-stu-id="e6c47-165">**Generate alert based on** toobe *number of results*</span></span>
- <span data-ttu-id="e6c47-166">**結果數目**toobe*大於 0*</span><span class="sxs-lookup"><span data-stu-id="e6c47-166">**Number of results** toobe *Greater than 0*</span></span>

<span data-ttu-id="e6c47-167">使用中所述的 hello 步驟[新增動作 tooalert 規則](log-analytics-alerts-actions.md)設定電子郵件、 webhook 或 runbook hello 警示規則的動作。</span><span class="sxs-lookup"><span data-stu-id="e6c47-167">Use hello steps described in [add actions tooalert rules](log-analytics-alerts-actions.md) configure an e-mail, webhook, or runbook action for hello alert rule.</span></span>


## <a name="configuration"></a><span data-ttu-id="e6c47-168">組態</span><span class="sxs-lookup"><span data-stu-id="e6c47-168">Configuration</span></span>
### <a name="q-can-i-change-hello-name-of-hello-tableblob-container-used-tooread-from-azure-diagnostics-wad"></a><span data-ttu-id="e6c47-169">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-169">Q.</span></span> <span data-ttu-id="e6c47-170">我可以變更 hello 資料表 /blob 容器使用 tooread hello 名稱從 Azure 診斷 (WAD)？</span><span class="sxs-lookup"><span data-stu-id="e6c47-170">Can I change hello name of hello table/blob container used tooread from Azure Diagnostics (WAD)?</span></span>

<span data-ttu-id="e6c47-171">A.</span><span class="sxs-lookup"><span data-stu-id="e6c47-171">A.</span></span> <span data-ttu-id="e6c47-172">否，它不是目前 tooread 任意的資料表或容器中的 Azure 儲存體中。</span><span class="sxs-lookup"><span data-stu-id="e6c47-172">No, it is not currently possible tooread from arbitrary tables or containers in Azure storage.</span></span>

### <a name="q-what-ip-addresses-does-hello-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-toohello-log-analytics-service"></a><span data-ttu-id="e6c47-173">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-173">Q.</span></span> <span data-ttu-id="e6c47-174">IP 的位址沒有 hello 記錄分析服務使用嗎？</span><span class="sxs-lookup"><span data-stu-id="e6c47-174">What IP addresses does hello Log Analytics service use?</span></span> <span data-ttu-id="e6c47-175">如何確定我的防火牆只允許流量 toohello 記錄分析服務？</span><span class="sxs-lookup"><span data-stu-id="e6c47-175">How do I ensure that my firewall only allows traffic toohello Log Analytics service?</span></span>

<span data-ttu-id="e6c47-176">A.</span><span class="sxs-lookup"><span data-stu-id="e6c47-176">A.</span></span> <span data-ttu-id="e6c47-177">hello 記錄分析服務建置在 Azure 之上。</span><span class="sxs-lookup"><span data-stu-id="e6c47-177">hello Log Analytics service is built on top of Azure.</span></span> <span data-ttu-id="e6c47-178">記錄分析 IP 位址皆位於 hello [Microsoft Azure Datacenter IP 範圍](http://www.microsoft.com/download/details.aspx?id=41653)。</span><span class="sxs-lookup"><span data-stu-id="e6c47-178">Log Analytics IP addresses are in hello [Microsoft Azure Datacenter IP Ranges](http://www.microsoft.com/download/details.aspx?id=41653).</span></span>

<span data-ttu-id="e6c47-179">進行服務部署時，變更的記錄分析服務 hello hello 實際 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e6c47-179">As service deployments are made, hello actual IP addresses of hello Log Analytics service change.</span></span> <span data-ttu-id="e6c47-180">hello DNS 名稱 tooallow 通過防火牆會記載於[中記錄分析設定 proxy 和防火牆設定](log-analytics-proxy-firewall.md)。</span><span class="sxs-lookup"><span data-stu-id="e6c47-180">hello DNS names tooallow through your firewall are documented at [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md).</span></span>

### <a name="q-i-use-expressroute-for-connecting-tooazure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a><span data-ttu-id="e6c47-181">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-181">Q.</span></span> <span data-ttu-id="e6c47-182">我使用 ExpressRoute 連線 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="e6c47-182">I use ExpressRoute for connecting tooAzure.</span></span> <span data-ttu-id="e6c47-183">我的 Log Analytics 流量是否會使用我的 ExpressRoute 連線？</span><span class="sxs-lookup"><span data-stu-id="e6c47-183">Does my Log Analytics traffic use my ExpressRoute connection?</span></span>

<span data-ttu-id="e6c47-184">A.</span><span class="sxs-lookup"><span data-stu-id="e6c47-184">A.</span></span> <span data-ttu-id="e6c47-185">hello 不同類型的 ExpressRoute 流量描述 hello [ExpressRoute 文件](../expressroute/expressroute-faqs.md#supported-services)。</span><span class="sxs-lookup"><span data-stu-id="e6c47-185">hello different types of ExpressRoute traffic are described in hello [ExpressRoute documentation](../expressroute/expressroute-faqs.md#supported-services).</span></span>

<span data-ttu-id="e6c47-186">流量 tooLog 分析會使用 hello 公用對等 ExpressRoute 循環。</span><span class="sxs-lookup"><span data-stu-id="e6c47-186">Traffic tooLog Analytics uses hello public-peering ExpressRoute circuit.</span></span>

### <a name="q-is-there-a-simple-and-easy-way-toomove-an-existing-log-analytics-workspace-tooanother-log-analytics-workspaceazure-subscription"></a><span data-ttu-id="e6c47-187">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-187">Q.</span></span> <span data-ttu-id="e6c47-188">是否有簡單輕鬆的方式 toomove 現有的記錄分析工作區 tooanother 記錄分析工作區 /azure 訂用帳戶？</span><span class="sxs-lookup"><span data-stu-id="e6c47-188">Is there a simple and easy way toomove an existing Log Analytics workspace tooanother Log Analytics workspace/Azure subscription?</span></span>

<span data-ttu-id="e6c47-189">A.</span><span class="sxs-lookup"><span data-stu-id="e6c47-189">A.</span></span> <span data-ttu-id="e6c47-190">hello `Move-AzureRmResource` cmdlet 可讓您從一個 Azure 訂用帳戶 tooanother 移動記錄分析工作區以及自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="e6c47-190">hello `Move-AzureRmResource` cmdlet lets you move a Log Analytics workspace, and also an Automation account from one Azure subscription tooanother.</span></span> <span data-ttu-id="e6c47-191">如需詳細資訊，請參閱 [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx)。</span><span class="sxs-lookup"><span data-stu-id="e6c47-191">For more information, see [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).</span></span>

<span data-ttu-id="e6c47-192">這項變更也進行 hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="e6c47-192">This change can also be made in hello Azure portal.</span></span>

<span data-ttu-id="e6c47-193">您無法將資料從一個記錄分析工作區 tooanother，移動或變更記錄分析資料會儲存在 hello 區域。</span><span class="sxs-lookup"><span data-stu-id="e6c47-193">You can’t move data from one Log Analytics workspace tooanother, or change hello region that Log Analytics data is stored in.</span></span>

### <a name="q-how-do-i-add-log-analytics-toosystem-center-operations-manager"></a><span data-ttu-id="e6c47-194">問： 如何加入記錄分析 tooSystem Center Operations Manager？</span><span class="sxs-lookup"><span data-stu-id="e6c47-194">Q: How do I add Log Analytics tooSystem Center Operations Manager?</span></span>

<span data-ttu-id="e6c47-195">答： 更新 toohello 最新的更新彙總，以及匯入管理組件可讓您 tooconnect Operations Manager tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="e6c47-195">A:  Updating toohello latest update rollup and importing management packs enables you tooconnect Operations Manager tooLog Analytics.</span></span>

>[!NOTE]
><span data-ttu-id="e6c47-196">hello Operations Manager 連線 tooLog 分析才可使用 System Center Operations Manager 2012 SP1 和更新版本。</span><span class="sxs-lookup"><span data-stu-id="e6c47-196">hello Operations Manager connection tooLog Analytics is only available for System Center Operations Manager 2012 SP1 and later.</span></span>

### <a name="q-how-can-i-confirm-that-an-agent-is-able-toocommunicate-with-log-analytics"></a><span data-ttu-id="e6c47-197">問： 如何確認代理程式是可以 toocommunicate 記錄分析？</span><span class="sxs-lookup"><span data-stu-id="e6c47-197">Q: How can I confirm that an agent is able toocommunicate with Log Analytics?</span></span>

<span data-ttu-id="e6c47-198">答： tooensure hello 代理程式可以與 OMS 通訊，請移至： 控制台、 安全性和設定， **Microsoft Monitoring Agent**。</span><span class="sxs-lookup"><span data-stu-id="e6c47-198">A: tooensure that hello agent can communicate with OMS, go to: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span></span>

<span data-ttu-id="e6c47-199">在 hello **Azure 記錄分析 (OMS)**索引標籤中，找出綠色的核取記號。</span><span class="sxs-lookup"><span data-stu-id="e6c47-199">Under hello **Azure Log Analytics (OMS)** tab, look for a green check mark.</span></span> <span data-ttu-id="e6c47-200">綠色核取記號圖示可確認該 hello 代理程式無法 toocommunicate 以 hello OMS 服務。</span><span class="sxs-lookup"><span data-stu-id="e6c47-200">A green check mark icon confirms that hello agent is able toocommunicate with hello OMS service.</span></span>

<span data-ttu-id="e6c47-201">黃色警告圖示表示 hello 代理程式的通訊出現問題與 OMS。</span><span class="sxs-lookup"><span data-stu-id="e6c47-201">A yellow warning icon means hello agent is having issues communication with OMS.</span></span> <span data-ttu-id="e6c47-202">一個常見的原因是 hello Microsoft Monitoring Agent 服務已停止。</span><span class="sxs-lookup"><span data-stu-id="e6c47-202">One common reason is hello Microsoft Monitoring Agent service has stopped.</span></span> <span data-ttu-id="e6c47-203">使用服務控制管理員 toorestart hello 服務。</span><span class="sxs-lookup"><span data-stu-id="e6c47-203">Use service control manager toorestart hello service.</span></span>

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a><span data-ttu-id="e6c47-204">問：如何阻止代理程式與 Log Analytics 通訊？</span><span class="sxs-lookup"><span data-stu-id="e6c47-204">Q: How do I stop an agent from communicating with Log Analytics?</span></span>

<span data-ttu-id="e6c47-205">答： 在 System Center Operations Manager，會移除 hello Advisor 受管理的電腦清單中的 hello 電腦。</span><span class="sxs-lookup"><span data-stu-id="e6c47-205">A: In System Center Operations Manager, remove hello computer from hello Advisor managed computer list.</span></span> <span data-ttu-id="e6c47-206">Operations Manager 更新 hello hello 代理程式 toono 長報表 tooLog Analytics 的組態。</span><span class="sxs-lookup"><span data-stu-id="e6c47-206">Operations Manager updates hello configuration of hello agent toono longer report tooLog Analytics.</span></span> <span data-ttu-id="e6c47-207">代理程式已直接連接 tooLog 分析，您可以停止其通訊透過： 控制台、 安全性和設定， **Microsoft Monitoring Agent**。</span><span class="sxs-lookup"><span data-stu-id="e6c47-207">For agents connected tooLog Analytics directly, you can stop them from communicating through: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span></span>
<span data-ttu-id="e6c47-208">在 **Azure Log Analytics (OMS)** 下，移除所有列出的工作區。</span><span class="sxs-lookup"><span data-stu-id="e6c47-208">Under **Azure Log Analytics (OMS)**, remove all workspaces listed.</span></span>

### <a name="q-why-am-i-getting-an-error-when-i-try-toomove-my-workspace-from-one-azure-subscription-tooanother"></a><span data-ttu-id="e6c47-209">問： 為什麼我會收到錯誤當我嘗試 toomove 我的工作區，從一個 Azure 訂用帳戶 tooanother？</span><span class="sxs-lookup"><span data-stu-id="e6c47-209">Q: Why am I getting an error when I try toomove my workspace from one Azure subscription tooanother?</span></span>

<span data-ttu-id="e6c47-210">答： 如果您使用 hello Azure 入口網站，確定只 hello 工作區中已選取 hello 移動。</span><span class="sxs-lookup"><span data-stu-id="e6c47-210">A: If you are using hello Azure portal, ensure only hello workspace is selected for hello move.</span></span> <span data-ttu-id="e6c47-211">未選取 hello 解決方案--它們會自動移動 hello 工作區中移動之後。</span><span class="sxs-lookup"><span data-stu-id="e6c47-211">Do not select hello solutions -- they will automatically move after hello workspace moves.</span></span> 

<span data-ttu-id="e6c47-212">請確定您具有這兩個 Azure 訂用帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="e6c47-212">Ensure you have permission in both Azure subscriptions.</span></span>

## <a name="agent-data"></a><span data-ttu-id="e6c47-213">代理程式資料</span><span class="sxs-lookup"><span data-stu-id="e6c47-213">Agent data</span></span>
### <a name="q-how-much-data-can-i-send-through-hello-agent-toolog-analytics-is-there-a-maximum-amount-of-data-per-customer"></a><span data-ttu-id="e6c47-214">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-214">Q.</span></span> <span data-ttu-id="e6c47-215">透過 hello 代理程式 tooLog 分析可以傳送多少資料？</span><span class="sxs-lookup"><span data-stu-id="e6c47-215">How much data can I send through hello agent tooLog Analytics?</span></span> <span data-ttu-id="e6c47-216">是否有每位客戶最大的資料量？</span><span class="sxs-lookup"><span data-stu-id="e6c47-216">Is there a maximum amount of data per customer?</span></span>
<span data-ttu-id="e6c47-217">A.</span><span class="sxs-lookup"><span data-stu-id="e6c47-217">A.</span></span> <span data-ttu-id="e6c47-218">hello 免費方案設定每個工作區的每日最高量為 500 MB。</span><span class="sxs-lookup"><span data-stu-id="e6c47-218">hello free plan sets a daily cap of 500 MB per workspace.</span></span> <span data-ttu-id="e6c47-219">hello 標準和高階計劃對 hello 上傳的資料量沒有限制。</span><span class="sxs-lookup"><span data-stu-id="e6c47-219">hello standard and premium plans have no limit on hello amount of data that is uploaded.</span></span> <span data-ttu-id="e6c47-220">記錄分析作為雲端服務，其設計 toohandle hello 磁碟區的小數位數 tooautomatically 來自客戶 – 即使它是每日 tb。</span><span class="sxs-lookup"><span data-stu-id="e6c47-220">As a cloud service, Log Analytics is designed tooautomatically scale up toohandle hello volume coming from a customer – even if it is terabytes per day.</span></span>

<span data-ttu-id="e6c47-221">hello 記錄分析代理程式已設計的 tooensure 其使用量很小。</span><span class="sxs-lookup"><span data-stu-id="e6c47-221">hello Log Analytics agent was designed tooensure it has a small footprint.</span></span> <span data-ttu-id="e6c47-222">我們的客戶的其中一個有關 hello 測試他們對我們的代理程式 」 和 「 如何它們深刻撰寫部落格。</span><span class="sxs-lookup"><span data-stu-id="e6c47-222">One of our customers wrote a blog about hello tests they performed against our agent and how impressed they were.</span></span> <span data-ttu-id="e6c47-223">hello 資料量會根據您啟用的 hello 解決方案而異。</span><span class="sxs-lookup"><span data-stu-id="e6c47-223">hello data volume varies based on hello solutions you enable.</span></span> <span data-ttu-id="e6c47-224">您可以尋找 hello 資料磁碟區上的詳細的資訊，並依據解決方案 hello 查看 hello 各部分[使用量](log-analytics-usage.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="e6c47-224">You can find detailed information on hello data volume and see hello breakup by solution in hello [Usage](log-analytics-usage.md) page.</span></span>

<span data-ttu-id="e6c47-225">如需詳細資訊，您可以閱讀[客戶部落格](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html)有關 hello hello OMS 代理程式的低使用量。</span><span class="sxs-lookup"><span data-stu-id="e6c47-225">For more information, you can read a [customer blog](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) about hello low footprint of hello OMS agent.</span></span>

### <a name="q-how-much-network-bandwidth-is-used-by-hello-microsoft-management-agent-mma-when-sending-data-toolog-analytics"></a><span data-ttu-id="e6c47-226">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-226">Q.</span></span> <span data-ttu-id="e6c47-227">傳送資料 tooLog 分析時 hello Microsoft 管理代理程式 (MMA) 會使用多少網路頻寬？</span><span class="sxs-lookup"><span data-stu-id="e6c47-227">How much network bandwidth is used by hello Microsoft Management Agent (MMA) when sending data tooLog Analytics?</span></span>

<span data-ttu-id="e6c47-228">A.</span><span class="sxs-lookup"><span data-stu-id="e6c47-228">A.</span></span> <span data-ttu-id="e6c47-229">頻寬是傳送資料的 hello 數量上的函式。</span><span class="sxs-lookup"><span data-stu-id="e6c47-229">Bandwidth is a function on hello amount of data sent.</span></span> <span data-ttu-id="e6c47-230">透過 hello 網路傳送時會受到壓縮資料。</span><span class="sxs-lookup"><span data-stu-id="e6c47-230">Data is compressed as it is sent over hello network.</span></span>

### <a name="q-how-much-data-is-sent-per-agent"></a><span data-ttu-id="e6c47-231">問：</span><span class="sxs-lookup"><span data-stu-id="e6c47-231">Q.</span></span> <span data-ttu-id="e6c47-232">每個代理程式會傳送多少資料？</span><span class="sxs-lookup"><span data-stu-id="e6c47-232">How much data is sent per agent?</span></span>

<span data-ttu-id="e6c47-233">A.</span><span class="sxs-lookup"><span data-stu-id="e6c47-233">A.</span></span> <span data-ttu-id="e6c47-234">每個代理程式傳送資料的 hello 數量而定：</span><span class="sxs-lookup"><span data-stu-id="e6c47-234">hello amount of data sent per agent depends on:</span></span>

* <span data-ttu-id="e6c47-235">您已啟用的 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="e6c47-235">hello solutions you have enabled</span></span>
* <span data-ttu-id="e6c47-236">正在收集計數器的記錄檔和效能的 hello 數目</span><span class="sxs-lookup"><span data-stu-id="e6c47-236">hello number of logs and performance counters being collected</span></span>
* <span data-ttu-id="e6c47-237">hello hello 記錄檔中的資料量</span><span class="sxs-lookup"><span data-stu-id="e6c47-237">hello volume of data in hello logs</span></span>

<span data-ttu-id="e6c47-238">hello 免費定價層是很好的方式 tooonboard 幾部量測計與 hello 一般資料量。</span><span class="sxs-lookup"><span data-stu-id="e6c47-238">hello free pricing tier is a good way tooonboard several servers and gauge hello typical data volume.</span></span> <span data-ttu-id="e6c47-239">整體使用量會顯示在 hello[使用量](log-analytics-usage.md)頁面。</span><span class="sxs-lookup"><span data-stu-id="e6c47-239">Overall usage is shown on hello [Usage](log-analytics-usage.md) page.</span></span>

<span data-ttu-id="e6c47-240">無法 toorun hello WireData 代理程式電腦，使用下列查詢 toosee 正在傳送多少資料 hello:</span><span class="sxs-lookup"><span data-stu-id="e6c47-240">For computers that are able toorun hello WireData agent, use hello following query toosee how much data is being sent:</span></span>

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a><span data-ttu-id="e6c47-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e6c47-241">Next steps</span></span>
* <span data-ttu-id="e6c47-242">[開始使用記錄分析](log-analytics-get-started.md)toolearn 深入了解記錄分析，以及如何取得最新且正在執行，以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="e6c47-242">[Get started with Log Analytics](log-analytics-get-started.md) toolearn more about Log Analytics and get up and running in minutes.</span></span>
