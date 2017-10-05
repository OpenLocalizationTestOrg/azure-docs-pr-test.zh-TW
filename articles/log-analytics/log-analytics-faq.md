---
title: "Log Analytics 常見問題集 | Microsoft Docs"
description: "Azure Log Analytics 服務的相關常見問題的解答。"
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
ms.openlocfilehash: 8ddea06b1a90e9b1599466ad4d1c3af7a6dc8ba9
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="log-analytics-faq"></a><span data-ttu-id="654b9-103">Log Analytics 常見問題集</span><span class="sxs-lookup"><span data-stu-id="654b9-103">Log Analytics FAQ</span></span>
<span data-ttu-id="654b9-104">此 Microsoft 常見問題集是 Microsoft Operations Management Suite (OMS) 中 Log Analytics 常見問題的清單。</span><span class="sxs-lookup"><span data-stu-id="654b9-104">This Microsoft FAQ is a list of commonly asked questions about Log Analytics in Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="654b9-105">若您有任何關於 Log Analytics 的其他問題，請前往[討論論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights)並張貼您的問題。</span><span class="sxs-lookup"><span data-stu-id="654b9-105">If you have any additional questions about Log Analytics, go to the [discussion forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=opinsights) and post your questions.</span></span> <span data-ttu-id="654b9-106">當問到常見問題時，我們會將其新增至此文章，以便其他人可以快速輕鬆地找到此問題。</span><span class="sxs-lookup"><span data-stu-id="654b9-106">When a question is frequently asked, we add it to this article so that it can be found quickly and easily.</span></span>

## <a name="general"></a><span data-ttu-id="654b9-107">一般</span><span class="sxs-lookup"><span data-stu-id="654b9-107">General</span></span>

### <a name="q-does-log-analytics-use-the-same-agent-as-azure-security-center"></a><span data-ttu-id="654b9-108">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-108">Q.</span></span> <span data-ttu-id="654b9-109">Log Analytics 會使用相同的代理程式作為 Azure 資訊安全中心嗎？</span><span class="sxs-lookup"><span data-stu-id="654b9-109">Does Log Analytics use the same agent as Azure Security Center?</span></span>

<span data-ttu-id="654b9-110">A.</span><span class="sxs-lookup"><span data-stu-id="654b9-110">A.</span></span> <span data-ttu-id="654b9-111">在 2017 年 6 月初，Azure 資訊安全中心開始使用 Microsoft Monitoring Agent 來收集與儲存資料。</span><span class="sxs-lookup"><span data-stu-id="654b9-111">In early June 2017, Azure Security Center began using the Microsoft Monitoring Agent to collect and store data.</span></span> <span data-ttu-id="654b9-112">若要深入了解，請參閱 [Azure 資訊安全中心平台移轉常見問題集](../security-center/security-center-platform-migration-faq.md)。</span><span class="sxs-lookup"><span data-stu-id="654b9-112">To learn more, see [Azure Security Center Platform Migration FAQ](../security-center/security-center-platform-migration-faq.md).</span></span>

### <a name="q-what-checks-are-performed-by-the-ad-and-sql-assessment-solutions"></a><span data-ttu-id="654b9-113">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-113">Q.</span></span> <span data-ttu-id="654b9-114">AD 和 SQL 評估解決方案會執行哪些檢查？</span><span class="sxs-lookup"><span data-stu-id="654b9-114">What checks are performed by the AD and SQL Assessment solutions?</span></span>

<span data-ttu-id="654b9-115">A.</span><span class="sxs-lookup"><span data-stu-id="654b9-115">A.</span></span> <span data-ttu-id="654b9-116">下列查詢會顯示目前執行的所有檢查的描述：</span><span class="sxs-lookup"><span data-stu-id="654b9-116">The following query shows a description of all checks currently performed:</span></span>

```
(Type=SQLAssessmentRecommendation OR Type=ADAssessmentRecommendation) | dedup RecommendationId | select FocusArea, ActionArea, Recommendation, Description | sort Type, FocusArea,ActionArea, Recommendation
```

<span data-ttu-id="654b9-117">然後可將結果匯出至 Excel 供進一步檢閱。</span><span class="sxs-lookup"><span data-stu-id="654b9-117">The results can then be exported to Excel for further review.</span></span>

### <a name="q-why-do-i-see-something-different-than-oms-in-system-center-operations-manager-console"></a><span data-ttu-id="654b9-118">問：為什麼我在 System Center Operations Manager 主控台中看到與 *OMS* 不同的項目？</span><span class="sxs-lookup"><span data-stu-id="654b9-118">Q: Why do I see something different than *OMS* in System Center Operations Manager console?</span></span>

<span data-ttu-id="654b9-119">答：根據您所採用的 Operations Manager 更新彙總套件而定，您可能會看到 *System Center Advisor*、*Operational Insights* 或 *Log Analytics* 節點。</span><span class="sxs-lookup"><span data-stu-id="654b9-119">A: Depending on what Update Rollup of Operations Manager you are on, you may see a node for *System Center Advisor*, *Operational Insights*, or *Log Analytics*.</span></span>

<span data-ttu-id="654b9-120">對 *OMS* 文字字串的更新包含在管理組件西，必須手動匯入它。</span><span class="sxs-lookup"><span data-stu-id="654b9-120">The text string update to *OMS* is included in a management pack, which needs to be imported manually.</span></span> <span data-ttu-id="654b9-121">若要查看目前文字和功能，請遵循最新 System Center Operations Manager 更新彙總套件知識庫文章中的指示，並重新整理主控台。</span><span class="sxs-lookup"><span data-stu-id="654b9-121">To see the current text and functionality, follow the instructions on the latest System Center Operations Manager Update Rollup KB article and refresh the console.</span></span>

### <a name="q-is-there-an-on-premises-version-of-log-analytics"></a><span data-ttu-id="654b9-122">問：Log Analytics 是否有「內部部署」版本？</span><span class="sxs-lookup"><span data-stu-id="654b9-122">Q: Is there an *on-premises* version of Log Analytics?</span></span>

<span data-ttu-id="654b9-123">答：否。</span><span class="sxs-lookup"><span data-stu-id="654b9-123">A: No.</span></span> <span data-ttu-id="654b9-124">Log Analytics 可以處理並儲存大量資料。</span><span class="sxs-lookup"><span data-stu-id="654b9-124">Log Analytics processes and stores large amounts of data.</span></span> <span data-ttu-id="654b9-125">作為一項雲端服務，Log Analytics 在必要時可以向上延展，並避免對您的環境效能的任何影響。</span><span class="sxs-lookup"><span data-stu-id="654b9-125">As a cloud service, Log Analytics is able to scale-up if necessary and avoid any performance impact to your environment.</span></span>

<span data-ttu-id="654b9-126">其他優點包括：</span><span class="sxs-lookup"><span data-stu-id="654b9-126">Additional benefits include:</span></span>
- <span data-ttu-id="654b9-127">Microsoft 執行 Log Analytics 基礎結構，為您節省成本</span><span class="sxs-lookup"><span data-stu-id="654b9-127">Microsoft runs the Log Analytics infrastructure, saving you costs</span></span>
- <span data-ttu-id="654b9-128">定期部署功能更新和修正程式。</span><span class="sxs-lookup"><span data-stu-id="654b9-128">Regular deployment of feature updates and fixes.</span></span>

### <a name="q-how-do-i-troubleshoot-that-log-analytics-is-no-longer-collecting-data"></a><span data-ttu-id="654b9-129">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-129">Q.</span></span> <span data-ttu-id="654b9-130">如何針對 Log Analytics 不再收集資料的問題進行疑難排解？</span><span class="sxs-lookup"><span data-stu-id="654b9-130">How do I troubleshoot that Log Analytics is no longer collecting data?</span></span>

<span data-ttu-id="654b9-131">答：如果您在免費定價層並在某天傳送了超過 500 MB 的資料，就會停止收集當天其餘資料。</span><span class="sxs-lookup"><span data-stu-id="654b9-131">A: If you are on the free pricing tier and have sent more than 500 MB of data in a day, data collection stops for the rest of the day.</span></span> <span data-ttu-id="654b9-132">達到每日限制是 Log Analytics 停止收集資料或資料似乎遺失的常見原因。</span><span class="sxs-lookup"><span data-stu-id="654b9-132">Reaching the daily limit is a common reason that Log Analytics stops collecting data, or data appears to be missing.</span></span>

<span data-ttu-id="654b9-133">當資料收集開始及停止時，Log Analytics 會建立 *Operation* 類型的事件。</span><span class="sxs-lookup"><span data-stu-id="654b9-133">Log Analytics creates an event of type *Operation* when data collection starts and stops.</span></span> 

<span data-ttu-id="654b9-134">在搜尋中執行下列查詢，即可檢查您是否達到每日限制並遺失資料：`Type=Operation OperationCategory="Data Collection Status"`</span><span class="sxs-lookup"><span data-stu-id="654b9-134">Run the following query in search to check if you are reaching the daily limit and missing data: `Type=Operation OperationCategory="Data Collection Status"`</span></span>

<span data-ttu-id="654b9-135">當資料收集停止時，*OperationStatus* 為 **Warning**。</span><span class="sxs-lookup"><span data-stu-id="654b9-135">When data collection stops, the *OperationStatus* is **Warning**.</span></span> <span data-ttu-id="654b9-136">當資料收集開始時，*OperationStatus* 為 **Succeeded**。</span><span class="sxs-lookup"><span data-stu-id="654b9-136">When data collection starts, the *OperationStatus* is **Succeeded**.</span></span> 

<span data-ttu-id="654b9-137">下表描述資料收集停止的原因，並建議為繼續資料收集所要採取的動作：</span><span class="sxs-lookup"><span data-stu-id="654b9-137">The following table describes reasons that data collection stops and a suggested action to resume data collection:</span></span>

| <span data-ttu-id="654b9-138">資料收集停止的原因</span><span class="sxs-lookup"><span data-stu-id="654b9-138">Reason data collection stops</span></span>                       | <span data-ttu-id="654b9-139">若要繼續資料收集</span><span class="sxs-lookup"><span data-stu-id="654b9-139">To resume data collection</span></span> |
| -------------------------------------------------- | ----------------  |
| <span data-ttu-id="654b9-140">已達免費資料的每日限制<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="654b9-140">Daily limit of free data reached<sup>1</sup></span></span>       | <span data-ttu-id="654b9-141">請等到隔天自動重新開始收集，或</span><span class="sxs-lookup"><span data-stu-id="654b9-141">Wait until the following day for collection to automatically restart, or</span></span><br> <span data-ttu-id="654b9-142">變更為付費定價層</span><span class="sxs-lookup"><span data-stu-id="654b9-142">Change to a paid pricing tier</span></span> |
| <span data-ttu-id="654b9-143">Azure 訂用帳戶處於暫停狀態，原因如下：</span><span class="sxs-lookup"><span data-stu-id="654b9-143">Azure subscription is in a suspended state due to:</span></span> <br> <span data-ttu-id="654b9-144">免費試用已結束</span><span class="sxs-lookup"><span data-stu-id="654b9-144">Free trial ended</span></span> <br> <span data-ttu-id="654b9-145">Azure Pass 已過期</span><span class="sxs-lookup"><span data-stu-id="654b9-145">Azure pass expired</span></span> <br> <span data-ttu-id="654b9-146">已達每月消費限制 (例如 MSDN 或 Visual Studio 訂閱)</span><span class="sxs-lookup"><span data-stu-id="654b9-146">Monthly spending limit reached (for example on an MSDN or Visual Studio subscription)</span></span>                          | <span data-ttu-id="654b9-147">轉換成付費訂閱</span><span class="sxs-lookup"><span data-stu-id="654b9-147">Convert to a paid subscription</span></span> <br> <span data-ttu-id="654b9-148">轉換成付費訂閱</span><span class="sxs-lookup"><span data-stu-id="654b9-148">Convert to a paid subscription</span></span> <br> <span data-ttu-id="654b9-149">移除限制，或等到限制重設</span><span class="sxs-lookup"><span data-stu-id="654b9-149">Remove limit, or wait until limit resets</span></span> |

<span data-ttu-id="654b9-150"><sup>1</sup> 如果您的工作區在免費定價層，您每天最多可傳送 500 MB 的資料至服務。</span><span class="sxs-lookup"><span data-stu-id="654b9-150"><sup>1</sup> If your workspace is on the free pricing tier, you're limited to sending 500 MB of data per day to the service.</span></span> <span data-ttu-id="654b9-151">當您達到每日限制時，資料收集就會停止，直到隔天再開始。</span><span class="sxs-lookup"><span data-stu-id="654b9-151">When you reach the daily limit, data collection stops until the next day.</span></span> <span data-ttu-id="654b9-152">在資料收集停止時所傳送的資料不會編製索引，而且無法供搜尋使用。</span><span class="sxs-lookup"><span data-stu-id="654b9-152">Data sent while data collection is stopped is not indexed and is not available for searching.</span></span> <span data-ttu-id="654b9-153">當資料收集繼續時，只會處理傳送的新資料。</span><span class="sxs-lookup"><span data-stu-id="654b9-153">When data collection resumes, processing occurs only for new data sent.</span></span> 

<span data-ttu-id="654b9-154">Log Analytics 使用 UTC 時間，而且每天從午夜 UTC 開始。</span><span class="sxs-lookup"><span data-stu-id="654b9-154">Log Analytics uses UTC time and each day starts at midnight UTC.</span></span> <span data-ttu-id="654b9-155">如果工作區達到每日限制，會在隔天 UTC 的第一個小時繼續處理。</span><span class="sxs-lookup"><span data-stu-id="654b9-155">If the workspace reaches the daily limit, processing resumes during the first hour of the next UTC day.</span></span>

### <a name="q-how-can-i-be-notified-when-data-collection-stops"></a><span data-ttu-id="654b9-156">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-156">Q.</span></span> <span data-ttu-id="654b9-157">如何在資料收集停止時收到通知？</span><span class="sxs-lookup"><span data-stu-id="654b9-157">How can I be notified when data collection stops?</span></span>

<span data-ttu-id="654b9-158">答：請使用[建立警示規則](log-analytics-alerts-creating.md#create-an-alert-rule)中所述的步驟，以在資料收集停止時收到通知。</span><span class="sxs-lookup"><span data-stu-id="654b9-158">A: Use the steps described in [create an alert rule](log-analytics-alerts-creating.md#create-an-alert-rule) to be notified when data collection stops.</span></span>

<span data-ttu-id="654b9-159">建立要在資料收集停止發出的警示時：</span><span class="sxs-lookup"><span data-stu-id="654b9-159">When creating the alert for when data collection stops, set the:</span></span>
- <span data-ttu-id="654b9-160">將 [名稱] 設定為「資料收集已停止」</span><span class="sxs-lookup"><span data-stu-id="654b9-160">**Name** to *Data collection stopped*</span></span>
- <span data-ttu-id="654b9-161">將 [嚴重性] 設定為「警告」</span><span class="sxs-lookup"><span data-stu-id="654b9-161">**Severity** to *Warning*</span></span>
- <span data-ttu-id="654b9-162">將 [搜尋查詢] 設定為 `Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`</span><span class="sxs-lookup"><span data-stu-id="654b9-162">**Search query** to `Type=Operation OperationCategory="Data Collection Status" OperationStatus=Warning`</span></span>
- <span data-ttu-id="654b9-163">將 [時間範圍] 設定為「2 小時」。</span><span class="sxs-lookup"><span data-stu-id="654b9-163">**Time window** to *2 Hours*.</span></span>
- <span data-ttu-id="654b9-164">將 [警示頻率] 設定為一小時，因為使用量資料每小時只會更新一次。</span><span class="sxs-lookup"><span data-stu-id="654b9-164">**Alert frequency** to be one hour since the usage data only updates once per hour.</span></span>
- <span data-ttu-id="654b9-165">將 [產生警示的依據] 設定為「結果數目」</span><span class="sxs-lookup"><span data-stu-id="654b9-165">**Generate alert based on** to be *number of results*</span></span>
- <span data-ttu-id="654b9-166">將 [結果數目] 設定為「大於 0」</span><span class="sxs-lookup"><span data-stu-id="654b9-166">**Number of results** to be *Greater than 0*</span></span>

<span data-ttu-id="654b9-167">使用[將動作新增至警示規則](log-analytics-alerts-actions.md)中所述的步驟來設定警示規則的電子郵件、Webhook 或 Runbook 動作。</span><span class="sxs-lookup"><span data-stu-id="654b9-167">Use the steps described in [add actions to alert rules](log-analytics-alerts-actions.md) configure an e-mail, webhook, or runbook action for the alert rule.</span></span>


## <a name="configuration"></a><span data-ttu-id="654b9-168">組態</span><span class="sxs-lookup"><span data-stu-id="654b9-168">Configuration</span></span>
### <a name="q-can-i-change-the-name-of-the-tableblob-container-used-to-read-from-azure-diagnostics-wad"></a><span data-ttu-id="654b9-169">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-169">Q.</span></span> <span data-ttu-id="654b9-170">可以變更用來從 Azure 診斷 (WAD) 讀取的資料表/Blob 容器的名稱嗎？</span><span class="sxs-lookup"><span data-stu-id="654b9-170">Can I change the name of the table/blob container used to read from Azure Diagnostics (WAD)?</span></span>

<span data-ttu-id="654b9-171">A.</span><span class="sxs-lookup"><span data-stu-id="654b9-171">A.</span></span> <span data-ttu-id="654b9-172">不可以，目前無法讀取 Azure 儲存體中的任意資料表或容器。</span><span class="sxs-lookup"><span data-stu-id="654b9-172">No, it is not currently possible to read from arbitrary tables or containers in Azure storage.</span></span>

### <a name="q-what-ip-addresses-does-the-log-analytics-service-use-how-do-i-ensure-that-my-firewall-only-allows-traffic-to-the-log-analytics-service"></a><span data-ttu-id="654b9-173">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-173">Q.</span></span> <span data-ttu-id="654b9-174">Log Analytics 服務使用哪些 IP 位址？</span><span class="sxs-lookup"><span data-stu-id="654b9-174">What IP addresses does the Log Analytics service use?</span></span> <span data-ttu-id="654b9-175">如何確保我的防火牆只允許對 Log Analytics 服務的流量？</span><span class="sxs-lookup"><span data-stu-id="654b9-175">How do I ensure that my firewall only allows traffic to the Log Analytics service?</span></span>

<span data-ttu-id="654b9-176">A.</span><span class="sxs-lookup"><span data-stu-id="654b9-176">A.</span></span> <span data-ttu-id="654b9-177">Log Analytics 服務以 Azure 為建置基礎。</span><span class="sxs-lookup"><span data-stu-id="654b9-177">The Log Analytics service is built on top of Azure.</span></span> <span data-ttu-id="654b9-178">Log Analytics IP 位址位於 [Microsoft Azure 資料中心 IP 範圍](http://www.microsoft.com/download/details.aspx?id=41653)內。</span><span class="sxs-lookup"><span data-stu-id="654b9-178">Log Analytics IP addresses are in the [Microsoft Azure Datacenter IP Ranges](http://www.microsoft.com/download/details.aspx?id=41653).</span></span>

<span data-ttu-id="654b9-179">進行服務部署時，Log Analytics 服務的實際 IP 位址會變更。</span><span class="sxs-lookup"><span data-stu-id="654b9-179">As service deployments are made, the actual IP addresses of the Log Analytics service change.</span></span> <span data-ttu-id="654b9-180">[在 Log Analytics 中設定 Proxy 和防火牆設定](log-analytics-proxy-firewall.md)中記載要允許通過防火牆的 DNS 名稱。</span><span class="sxs-lookup"><span data-stu-id="654b9-180">The DNS names to allow through your firewall are documented at [Configure proxy and firewall settings in Log Analytics](log-analytics-proxy-firewall.md).</span></span>

### <a name="q-i-use-expressroute-for-connecting-to-azure-does-my-log-analytics-traffic-use-my-expressroute-connection"></a><span data-ttu-id="654b9-181">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-181">Q.</span></span> <span data-ttu-id="654b9-182">我可以使用 ExpressRoute 連接到 Azure。</span><span class="sxs-lookup"><span data-stu-id="654b9-182">I use ExpressRoute for connecting to Azure.</span></span> <span data-ttu-id="654b9-183">我的 Log Analytics 流量是否會使用我的 ExpressRoute 連線？</span><span class="sxs-lookup"><span data-stu-id="654b9-183">Does my Log Analytics traffic use my ExpressRoute connection?</span></span>

<span data-ttu-id="654b9-184">A.</span><span class="sxs-lookup"><span data-stu-id="654b9-184">A.</span></span> <span data-ttu-id="654b9-185">[ExpressRoute 文件](../expressroute/expressroute-faqs.md#supported-services)中描述不同類型的 ExpressRoute 流量。</span><span class="sxs-lookup"><span data-stu-id="654b9-185">The different types of ExpressRoute traffic are described in the [ExpressRoute documentation](../expressroute/expressroute-faqs.md#supported-services).</span></span>

<span data-ttu-id="654b9-186">通往 Log Analytics 的流量都會使用公用互連 ExpressRoute 電路。</span><span class="sxs-lookup"><span data-stu-id="654b9-186">Traffic to Log Analytics uses the public-peering ExpressRoute circuit.</span></span>

### <a name="q-is-there-a-simple-and-easy-way-to-move-an-existing-log-analytics-workspace-to-another-log-analytics-workspaceazure-subscription"></a><span data-ttu-id="654b9-187">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-187">Q.</span></span> <span data-ttu-id="654b9-188">有簡單且輕鬆的方法，可將現有的 Log Analytics 工作區移至另一個 Log Analytics 工作區/Azure 訂用帳戶嗎？</span><span class="sxs-lookup"><span data-stu-id="654b9-188">Is there a simple and easy way to move an existing Log Analytics workspace to another Log Analytics workspace/Azure subscription?</span></span>

<span data-ttu-id="654b9-189">A.</span><span class="sxs-lookup"><span data-stu-id="654b9-189">A.</span></span> <span data-ttu-id="654b9-190">`Move-AzureRmResource` Cmdlet 可讓您將 Log Analytics 工作區及自動化帳戶從一個 Azure 訂用帳戶移至另一個 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="654b9-190">The `Move-AzureRmResource` cmdlet lets you move a Log Analytics workspace, and also an Automation account from one Azure subscription to another.</span></span> <span data-ttu-id="654b9-191">如需詳細資訊，請參閱 [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx)。</span><span class="sxs-lookup"><span data-stu-id="654b9-191">For more information, see [Move-AzureRmResource](http://msdn.microsoft.com/library/mt652516.aspx).</span></span>

<span data-ttu-id="654b9-192">這項變更也可在 Azure 入口網站進行。</span><span class="sxs-lookup"><span data-stu-id="654b9-192">This change can also be made in the Azure portal.</span></span>

<span data-ttu-id="654b9-193">您無法將資料在不同一個 Log Analytics 工作區間移動，或是變更 Log Analytics 資料儲存所在的區域。</span><span class="sxs-lookup"><span data-stu-id="654b9-193">You can’t move data from one Log Analytics workspace to another, or change the region that Log Analytics data is stored in.</span></span>

### <a name="q-how-do-i-add-log-analytics-to-system-center-operations-manager"></a><span data-ttu-id="654b9-194">問：如何將 Log Analytics 新增至 System Center Operations Manager？</span><span class="sxs-lookup"><span data-stu-id="654b9-194">Q: How do I add Log Analytics to System Center Operations Manager?</span></span>

<span data-ttu-id="654b9-195">答：更新為最新的更新彙總套件和匯入管理組件可讓您將 Operations Manager 連線到 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="654b9-195">A:  Updating to the latest update rollup and importing management packs enables you to connect Operations Manager to Log Analytics.</span></span>

>[!NOTE]
><span data-ttu-id="654b9-196">只有 System Center Operations Manager 2012 SP1 和更新版本才能將 Operations Manager 連線到 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="654b9-196">The Operations Manager connection to Log Analytics is only available for System Center Operations Manager 2012 SP1 and later.</span></span>

### <a name="q-how-can-i-confirm-that-an-agent-is-able-to-communicate-with-log-analytics"></a><span data-ttu-id="654b9-197">問：如何確認代理程式可與 Log Analytics 通訊？</span><span class="sxs-lookup"><span data-stu-id="654b9-197">Q: How can I confirm that an agent is able to communicate with Log Analytics?</span></span>

<span data-ttu-id="654b9-198">答：若要確保代理程式可以與 OMS 通訊，請移至：[控制台] > [安全性和設定] > [Microsoft Monitoring Agent]。</span><span class="sxs-lookup"><span data-stu-id="654b9-198">A: To ensure that the agent can communicate with OMS, go to: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span></span>

<span data-ttu-id="654b9-199">在 [Azure Log Analytics (OMS)]  索引標籤中，找出綠色的核取記號。</span><span class="sxs-lookup"><span data-stu-id="654b9-199">Under the **Azure Log Analytics (OMS)** tab, look for a green check mark.</span></span> <span data-ttu-id="654b9-200">綠色核取記號圖示可確認代理程式能夠與 OMS 服務進行通訊。</span><span class="sxs-lookup"><span data-stu-id="654b9-200">A green check mark icon confirms that the agent is able to communicate with the OMS service.</span></span>

<span data-ttu-id="654b9-201">黃色警告圖示表示代理程式有與 OMS 通訊的問題。</span><span class="sxs-lookup"><span data-stu-id="654b9-201">A yellow warning icon means the agent is having issues communication with OMS.</span></span> <span data-ttu-id="654b9-202">一個常見原因是 Microsoft Monitoring Agent 服務已停止。</span><span class="sxs-lookup"><span data-stu-id="654b9-202">One common reason is the Microsoft Monitoring Agent service has stopped.</span></span> <span data-ttu-id="654b9-203">使用服務控制管理員來重新啟動服務。</span><span class="sxs-lookup"><span data-stu-id="654b9-203">Use service control manager to restart the service.</span></span>

### <a name="q-how-do-i-stop-an-agent-from-communicating-with-log-analytics"></a><span data-ttu-id="654b9-204">問：如何阻止代理程式與 Log Analytics 通訊？</span><span class="sxs-lookup"><span data-stu-id="654b9-204">Q: How do I stop an agent from communicating with Log Analytics?</span></span>

<span data-ttu-id="654b9-205">答：在 System Center Operations Manager 中，從 Advisor 受管理的電腦清單中移除該電腦。</span><span class="sxs-lookup"><span data-stu-id="654b9-205">A: In System Center Operations Manager, remove the computer from the Advisor managed computer list.</span></span> <span data-ttu-id="654b9-206">Operations Manager 會將代理程式的設定更新為不再向 Log Analytics 回報。</span><span class="sxs-lookup"><span data-stu-id="654b9-206">Operations Manager updates the configuration of the agent to no longer report to Log Analytics.</span></span> <span data-ttu-id="654b9-207">針對直接連線到 Log Analytics 的代理程式，您可以透過 [控制台] > [安全性和設定] > [Microsoft Monitoring Agent] 來阻止其通訊。</span><span class="sxs-lookup"><span data-stu-id="654b9-207">For agents connected to Log Analytics directly, you can stop them from communicating through: Control Panel, Security & Settings, **Microsoft Monitoring Agent**.</span></span>
<span data-ttu-id="654b9-208">在 **Azure Log Analytics (OMS)** 下，移除所有列出的工作區。</span><span class="sxs-lookup"><span data-stu-id="654b9-208">Under **Azure Log Analytics (OMS)**, remove all workspaces listed.</span></span>

### <a name="q-why-am-i-getting-an-error-when-i-try-to-move-my-workspace-from-one-azure-subscription-to-another"></a><span data-ttu-id="654b9-209">問︰當我試著將工作區從某個 Azure 訂用帳戶移到另一個時，為什麼會發生錯誤？</span><span class="sxs-lookup"><span data-stu-id="654b9-209">Q: Why am I getting an error when I try to move my workspace from one Azure subscription to another?</span></span>

<span data-ttu-id="654b9-210">答：如果您使用 Azure 入口網站，請確定只選取要移動的工作區。</span><span class="sxs-lookup"><span data-stu-id="654b9-210">A: If you are using the Azure portal, ensure only the workspace is selected for the move.</span></span> <span data-ttu-id="654b9-211">請勿選取解決方案，移動工作區之後會自動移動解決方案。</span><span class="sxs-lookup"><span data-stu-id="654b9-211">Do not select the solutions -- they will automatically move after the workspace moves.</span></span> 

<span data-ttu-id="654b9-212">請確定您具有這兩個 Azure 訂用帳戶的權限。</span><span class="sxs-lookup"><span data-stu-id="654b9-212">Ensure you have permission in both Azure subscriptions.</span></span>

## <a name="agent-data"></a><span data-ttu-id="654b9-213">代理程式資料</span><span class="sxs-lookup"><span data-stu-id="654b9-213">Agent data</span></span>
### <a name="q-how-much-data-can-i-send-through-the-agent-to-log-analytics-is-there-a-maximum-amount-of-data-per-customer"></a><span data-ttu-id="654b9-214">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-214">Q.</span></span> <span data-ttu-id="654b9-215">我可以透過代理程式傳送多少資料到 Log Analytics？</span><span class="sxs-lookup"><span data-stu-id="654b9-215">How much data can I send through the agent to Log Analytics?</span></span> <span data-ttu-id="654b9-216">是否有每位客戶最大的資料量？</span><span class="sxs-lookup"><span data-stu-id="654b9-216">Is there a maximum amount of data per customer?</span></span>
<span data-ttu-id="654b9-217">A.</span><span class="sxs-lookup"><span data-stu-id="654b9-217">A.</span></span> <span data-ttu-id="654b9-218">免費方案每個工作區的每日容量設定為 500 MB。</span><span class="sxs-lookup"><span data-stu-id="654b9-218">The free plan sets a daily cap of 500 MB per workspace.</span></span> <span data-ttu-id="654b9-219">標準和進階計畫對於所上傳的資料量沒有限制。</span><span class="sxs-lookup"><span data-stu-id="654b9-219">The standard and premium plans have no limit on the amount of data that is uploaded.</span></span> <span data-ttu-id="654b9-220">作為一項雲端服務，Log Analytics 的設計可自動相應增加，以處理來自客戶的資料量，即使是每日數 TB。</span><span class="sxs-lookup"><span data-stu-id="654b9-220">As a cloud service, Log Analytics is designed to automatically scale up to handle the volume coming from a customer – even if it is terabytes per day.</span></span>

<span data-ttu-id="654b9-221">Log Analytics 代理程式的設計是為了確保它的使用量很小。</span><span class="sxs-lookup"><span data-stu-id="654b9-221">The Log Analytics agent was designed to ensure it has a small footprint.</span></span> <span data-ttu-id="654b9-222">我們的其中一個客戶撰寫了一篇部落格，內容是有關他們為我們的代理程式執行的測試以及如何讓其印象深刻。</span><span class="sxs-lookup"><span data-stu-id="654b9-222">One of our customers wrote a blog about the tests they performed against our agent and how impressed they were.</span></span> <span data-ttu-id="654b9-223">資料量會視您啟用的解決方案而不同。</span><span class="sxs-lookup"><span data-stu-id="654b9-223">The data volume varies based on the solutions you enable.</span></span> <span data-ttu-id="654b9-224">您可以在[使用量](log-analytics-usage.md)頁面中找到有關資料量的詳細資訊，並依解決方案查看劃分。</span><span class="sxs-lookup"><span data-stu-id="654b9-224">You can find detailed information on the data volume and see the breakup by solution in the [Usage](log-analytics-usage.md) page.</span></span>

<span data-ttu-id="654b9-225">如需詳細資訊，您可以閱讀 [客戶部落格](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) 以了解 OMS 代理程式的低使用量。</span><span class="sxs-lookup"><span data-stu-id="654b9-225">For more information, you can read a [customer blog](http://thoughtsonopsmgr.blogspot.com/2015/09/one-small-footprint-for-server-one.html) about the low footprint of the OMS agent.</span></span>

### <a name="q-how-much-network-bandwidth-is-used-by-the-microsoft-management-agent-mma-when-sending-data-to-log-analytics"></a><span data-ttu-id="654b9-226">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-226">Q.</span></span> <span data-ttu-id="654b9-227">傳送資料到 Log Analytics 時，Microsoft 管理代理程式 (MMA) 使用多少網路頻寬？</span><span class="sxs-lookup"><span data-stu-id="654b9-227">How much network bandwidth is used by the Microsoft Management Agent (MMA) when sending data to Log Analytics?</span></span>

<span data-ttu-id="654b9-228">A.</span><span class="sxs-lookup"><span data-stu-id="654b9-228">A.</span></span> <span data-ttu-id="654b9-229">頻寬是關於傳送的資料量的功能。</span><span class="sxs-lookup"><span data-stu-id="654b9-229">Bandwidth is a function on the amount of data sent.</span></span> <span data-ttu-id="654b9-230">透過網路傳送資料時，會壓縮資料。</span><span class="sxs-lookup"><span data-stu-id="654b9-230">Data is compressed as it is sent over the network.</span></span>

### <a name="q-how-much-data-is-sent-per-agent"></a><span data-ttu-id="654b9-231">問：</span><span class="sxs-lookup"><span data-stu-id="654b9-231">Q.</span></span> <span data-ttu-id="654b9-232">每個代理程式會傳送多少資料？</span><span class="sxs-lookup"><span data-stu-id="654b9-232">How much data is sent per agent?</span></span>

<span data-ttu-id="654b9-233">A.</span><span class="sxs-lookup"><span data-stu-id="654b9-233">A.</span></span> <span data-ttu-id="654b9-234">每個代理程式所傳送的資料量取決於：</span><span class="sxs-lookup"><span data-stu-id="654b9-234">The amount of data sent per agent depends on:</span></span>

* <span data-ttu-id="654b9-235">您已啟用的解決方案</span><span class="sxs-lookup"><span data-stu-id="654b9-235">The solutions you have enabled</span></span>
* <span data-ttu-id="654b9-236">記錄檔和要收集之效能計數器的數目</span><span class="sxs-lookup"><span data-stu-id="654b9-236">The number of logs and performance counters being collected</span></span>
* <span data-ttu-id="654b9-237">記錄檔中的資料量</span><span class="sxs-lookup"><span data-stu-id="654b9-237">The volume of data in the logs</span></span>

<span data-ttu-id="654b9-238">免費定價層是將數個伺服器上架和量測典型資料量的好方法。</span><span class="sxs-lookup"><span data-stu-id="654b9-238">The free pricing tier is a good way to onboard several servers and gauge the typical data volume.</span></span> <span data-ttu-id="654b9-239">[使用量] [](log-analytics-usage.md) 頁面會顯示整體使用方式。</span><span class="sxs-lookup"><span data-stu-id="654b9-239">Overall usage is shown on the [Usage](log-analytics-usage.md) page.</span></span>

<span data-ttu-id="654b9-240">對於可執行 WireData 代理程式的電腦，請使用下列查詢查看正在傳送的資料量：</span><span class="sxs-lookup"><span data-stu-id="654b9-240">For computers that are able to run the WireData agent, use the following query to see how much data is being sent:</span></span>

```
Type=WireData (ProcessName="C:\\Program Files\\Microsoft Monitoring Agent\\Agent\\MonitoringHost.exe") (Direction=Outbound) | measure Sum(TotalBytes) by Computer
```



## <a name="next-steps"></a><span data-ttu-id="654b9-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="654b9-241">Next steps</span></span>
* <span data-ttu-id="654b9-242">[開始使用 Log Analytics](log-analytics-get-started.md) 以深入了解 Log Analytics，並幾分鐘內就啟動並執行。</span><span class="sxs-lookup"><span data-stu-id="654b9-242">[Get started with Log Analytics](log-analytics-get-started.md) to learn more about Log Analytics and get up and running in minutes.</span></span>
