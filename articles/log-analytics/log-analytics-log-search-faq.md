---
title: "aaaLog 分析新的記錄搜尋常見問題集 |Microsoft 文件"
description: "本文章提供有關 hello 升級記錄分析 toohello 新查詢語言的常見問題的解答。"
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/27/2017
ms.author: bwren
ms.openlocfilehash: b8664c8329fab0547f270793fa13e8cdd06ba637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="log-analytics-new-log-search-faq-and-known-issues"></a><span data-ttu-id="9c1f6-103">Log Analytics 新記錄搜尋常見問題集與已知問題</span><span class="sxs-lookup"><span data-stu-id="9c1f6-103">Log Analytics new log search FAQ and known issues</span></span>

<span data-ttu-id="9c1f6-104">這篇文章包含常見問題集與有關 hello 升級的已知的問題[記錄分析 toohello 新查詢語言](log-analytics-log-search-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-104">This article includes frequently asked questions and known issues regarding hello upgrade of [Log Analytics toohello new query language](log-analytics-log-search-upgrade.md).</span></span>  <span data-ttu-id="9c1f6-105">您應該閱讀這份文件之前 hello 決策 tooupgrade 您的工作區。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-105">You should read through this entire article before making hello decision tooupgrade your workspace.</span></span>


## <a name="alerts"></a><span data-ttu-id="9c1f6-106">Alerts</span><span class="sxs-lookup"><span data-stu-id="9c1f6-106">Alerts</span></span>

### <a name="question-i-have-a-lot-of-alert-rules-do-i-need-toocreate-them-again-in-hello-new-language-after-i-upgrade"></a><span data-ttu-id="9c1f6-107">問題：我有大量的警示規則。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-107">Question: I have a lot of alert rules.</span></span> <span data-ttu-id="9c1f6-108">我需要 toocreate 它們一次在升級之後 hello 新語言？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-108">Do I need toocreate them again in hello new language after I upgrade?</span></span>  
<span data-ttu-id="9c1f6-109">否，您的警示規則是新搜尋語言會自動轉換的 toohello 升級期間。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-109">No, your alert rules are automatically converted toohello new search language during upgrade.</span></span>  


## <a name="computer-groups"></a><span data-ttu-id="9c1f6-110">電腦群組</span><span class="sxs-lookup"><span data-stu-id="9c1f6-110">Computer groups</span></span>

### <a name="question-im-getting-errors-when-trying-toouse-computer-groups--has-their-syntax-changed"></a><span data-ttu-id="9c1f6-111">問題： 我會收到錯誤時嘗試 toouse 電腦群組。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-111">Question: I'm getting errors when trying toouse computer groups.</span></span>  <span data-ttu-id="9c1f6-112">其語法是否已變更？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-112">Has their syntax changed?</span></span>
<span data-ttu-id="9c1f6-113">是，hello 語法會使用電腦群組變更，升級您的工作區時。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-113">Yes, hello syntax for using computer groups changes when your workspace is upgraded.</span></span>  <span data-ttu-id="9c1f6-114">如需詳細資訊，請參閱 [Log Analytics 記錄檔搜尋中的電腦群組](log-analytics-computer-groups.md)。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-114">See [Computer groups in Log Analytics log searches](log-analytics-computer-groups.md) for details.</span></span>

### <a name="known-issue-groups-imported-from-active-directory"></a><span data-ttu-id="9c1f6-115">已知問題：從 Active Directory 匯入的群組</span><span class="sxs-lookup"><span data-stu-id="9c1f6-115">Known issue: Groups imported from Active Directory</span></span>
<span data-ttu-id="9c1f6-116">您目前無法建立使用從 Active Directory 匯入之電腦群組的查詢。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-116">You cannot currently create a query that uses a computer group imported from Active Directory.</span></span>  <span data-ttu-id="9c1f6-117">因應措施更正此問題，直到建立新的電腦群組，使用 hello 匯入 Active Directory 群組，然後在查詢中使用該新的群組。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-117">As a workaround until this issue is corrected, create a new computer group using hello imported Active Directory group and then use that new group in your query.</span></span>

<span data-ttu-id="9c1f6-118">範例查詢 toocreate 包含匯入 Active Directory 群組的新電腦群組如下所示：</span><span class="sxs-lookup"><span data-stu-id="9c1f6-118">An example query toocreate a new computer group that includes an imported Active Directory group is as follows:</span></span>

    ComputerGroup | where GroupSource == "ActiveDirectory" and Group == "AD Group Name" and TimeGenerated >= ago(24h) | distinct Computer


## <a name="dashboards"></a><span data-ttu-id="9c1f6-119">儀表板</span><span class="sxs-lookup"><span data-stu-id="9c1f6-119">Dashboards</span></span>

### <a name="question-can-i-still-use-dashboards-in-an-upgraded-workspace"></a><span data-ttu-id="9c1f6-120">問題：是否仍然可以在升級的工作區中使用儀表板？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-120">Question: Can I still use dashboards in an upgraded workspace?</span></span>
<span data-ttu-id="9c1f6-121">您可以繼續 toouse 您新增過任何磚**我的儀表板**之前已升級您的工作區，但您無法編輯這些圖格，或加入新的。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-121">You can continue toouse any tiles that you added too**My Dashboard** before your workspace was upgraded, but you cannot edit those tiles or add new ones.</span></span>  <span data-ttu-id="9c1f6-122">您可以繼續 toocreate 和編輯與檢視[檢視表設計工具](log-analytics-view-designer.md)也可以在 hello Azure 入口網站中建立儀表板。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-122">You can continue toocreate and edit views with [View Designer](log-analytics-view-designer.md) and also create dashboards in hello Azure portal.</span></span>


## <a name="log-searches"></a><span data-ttu-id="9c1f6-123">記錄檔搜尋</span><span class="sxs-lookup"><span data-stu-id="9c1f6-123">Log searches</span></span>

### <a name="question-i-have-saved-searches-outside-of-my-upgraded-workspace-can-i-convert-them-toohello-new-search-language-automatically"></a><span data-ttu-id="9c1f6-124">問題：我已在升級工作區之外儲存搜尋。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-124">Question: I have saved searches outside of my upgraded workspace.</span></span> <span data-ttu-id="9c1f6-125">可以將它們轉換 toohello 新搜尋語言會自動嗎？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-125">Can I convert them toohello new search language automatically?</span></span>
<span data-ttu-id="9c1f6-126">您可以使用每個在 hello 記錄搜尋頁面 tooconvert hello 語言轉換器工具。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-126">You can use hello language converter tool in hello log search page tooconvert each one.</span></span>  <span data-ttu-id="9c1f6-127">沒有任何方法 tooautomatically 轉換而不升級 hello 工作區的多個搜尋。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-127">There is no method tooautomatically convert multiple searches without upgrading hello workspace.</span></span>

### <a name="question-why-are-my-query-results-not-sorted"></a><span data-ttu-id="9c1f6-128">問題： 為什麼我的查詢結果未排序？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-128">Question: Why are my query results not sorted?</span></span>
<span data-ttu-id="9c1f6-129">根據預設，在 hello 新的查詢語言，不會排序結果。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-129">Results are not sorted by default in hello new query language.</span></span>  <span data-ttu-id="9c1f6-130">使用 hello [sort 運算子](https://go.microsoft.com/fwlink/?linkid=856079)toosort 您依照一個或多個屬性的結果。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-130">Use hello [sort operator](https://go.microsoft.com/fwlink/?linkid=856079) toosort your results by one or more properties.</span></span>

### <a name="known-issue-search-results-in-a-list-may-include-properties-with-no-data"></a><span data-ttu-id="9c1f6-131">已知問題：清單中的搜尋結果可能包含沒有資料的屬性</span><span class="sxs-lookup"><span data-stu-id="9c1f6-131">Known issue: Search results in a list may include properties with no data</span></span>
<span data-ttu-id="9c1f6-132">清單中的記錄搜尋結果可能會顯示沒有資料的屬性。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-132">Log search results in a list may display properties with no data.</span></span>  <span data-ttu-id="9c1f6-133">先前 tooupgrade，這些屬性就不會包含在內。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-133">Prior tooupgrade, these properties wouldn't be included.</span></span>  <span data-ttu-id="9c1f6-134">未來將修正此問題，以避免顯示空白屬性。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-134">This issue will be corrected so that empty properties are not displayed.</span></span>

### <a name="known-issue-selecting-a-value-in-a-chart-doesnt-display-detailed-results"></a><span data-ttu-id="9c1f6-135">已知問題：選取圖表中的值不會顯示詳細結果</span><span class="sxs-lookup"><span data-stu-id="9c1f6-135">Known issue: Selecting a value in a chart doesn't display detailed results</span></span>
<span data-ttu-id="9c1f6-136">先前 tooupgrade，當您在圖表中，選取值，它就會傳回符合選取的 hello 值記錄的詳細的清單。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-136">Prior tooupgrade, when you selected a value in a chart, it would return a detailed list of records matching hello selected value.</span></span>  <span data-ttu-id="9c1f6-137">升級之後，就會傳回只 hello 單一摘要的行。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-137">After upgrade, only hello single summarized line is returned.</span></span>  <span data-ttu-id="9c1f6-138">目前正在調查此問題。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-138">This issue is currently being investigated.</span></span>

## <a name="log-search-api"></a><span data-ttu-id="9c1f6-139">記錄檔搜尋 API</span><span class="sxs-lookup"><span data-stu-id="9c1f6-139">Log Search API</span></span>

### <a name="question-does-hello-log-search-api-get-updated-after-i-upgrade"></a><span data-ttu-id="9c1f6-140">問題： 未 hello Log Search API 取得更新之後升級嗎？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-140">Question: Does hello Log Search API get updated after I upgrade?</span></span>
<span data-ttu-id="9c1f6-141">hello [Log Search API](log-analytics-log-search-api.md)尚未升級的 toohello 新搜尋語言。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-141">hello [Log Search API](log-analytics-log-search-api.md) has not yet been upgraded toohello new search language.</span></span>  <span data-ttu-id="9c1f6-142">即使在工作區升級之後，請繼續 toouse hello 舊版的查詢語言，使用此 API。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-142">Continue toouse hello legacy query language with this API, even after you upgrade your workspace.</span></span>  <span data-ttu-id="9c1f6-143">當更新時，更新文件將會提供 hello Log Search API。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-143">Updated documentation will become available for hello Log Search API when it's updated.</span></span>


## <a name="portals"></a><span data-ttu-id="9c1f6-144">入口網站</span><span class="sxs-lookup"><span data-stu-id="9c1f6-144">Portals</span></span>

### <a name="question-should-i-use-hello-new-advanced-analytics-portal-or-keep-using-hello-log-search-portal"></a><span data-ttu-id="9c1f6-145">問題： 應該使用 hello 新 Advanced Analytics 入口網站或繼續使用 hello 記錄搜尋入口網站？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-145">Question: Should I use hello new Advanced Analytics portal or keep using hello Log Search portal?</span></span>
<span data-ttu-id="9c1f6-146">您可以看到在 hello 兩個入口網站的比較[入口網站來建立和編輯 Azure 記錄分析中的記錄檔查詢](log-analytics-log-search-portals.md)。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-146">You can see a comparison of hello two portals at [Portals for creating and editing log queries in Azure Log Analytics](log-analytics-log-search-portals.md).</span></span>  <span data-ttu-id="9c1f6-147">每個有不同的優點，因此您可以選擇 hello 適合您的需求。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-147">Each has distinct advantages so you can choose hello best one for your requirements.</span></span>  <span data-ttu-id="9c1f6-148">它是在 hello Advanced Analytics 入口網站中的一般 toowrite 查詢，並將它們貼至其他位置，例如檢視表設計工具。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-148">It's common toowrite queries in hello Advanced Analytics portal and paste them into other places such as View Designer.</span></span>  <span data-ttu-id="9c1f6-149">您應該閱讀[發出 tooconsider](log-analytics-log-search-portals.md#advanced-analytics-portal)執行之時。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-149">You should read about [issues tooconsider](log-analytics-log-search-portals.md#advanced-analytics-portal) when doing that.</span></span>


## <a name="power-bi"></a><span data-ttu-id="9c1f6-150">Power BI</span><span class="sxs-lookup"><span data-stu-id="9c1f6-150">Power BI</span></span>

### <a name="question-does-anything-change-with-powerbi-integration"></a><span data-ttu-id="9c1f6-151">問題：PowerBI 整合有任何變更嗎？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-151">Question: Does anything change with PowerBI integration?</span></span>
<span data-ttu-id="9c1f6-152">是。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-152">Yes.</span></span>  <span data-ttu-id="9c1f6-153">一旦升級您的工作區之後就無法再運作匯出記錄分析資料 tooPower BI hello 程序。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-153">Once your workspace has been upgraded then hello process for exporting Log Analytics data tooPower BI will no longer work.</span></span>  <span data-ttu-id="9c1f6-154">您在升級之前建立的任何現有排程將會變成停用。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-154">Any existing schedules that you created before upgrading will become disabled.</span></span>  <span data-ttu-id="9c1f6-155">升級之後，Azure 記錄分析會使用 hello Application Insights 為相同的平台，而且您使用相同的處理序 tooexport 記錄分析查詢 tooPower 為 BI hello [hello 程序 tooexport Application Insights 查詢 tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries)。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-155">After upgrade, Azure Log Analytics uses hello same platform as Application Insights, and you use hello same process tooexport Log Analytics queries tooPower BI as [hello process tooexport Application Insights queries tooPower BI](../application-insights/app-insights-export-power-bi.md#export-analytics-queries).</span></span>

### <a name="known-issue-power-bi-request-size-limit"></a><span data-ttu-id="9c1f6-156">已知問題：Power BI 要求大小限制</span><span class="sxs-lookup"><span data-stu-id="9c1f6-156">Known issue: Power BI request size limit</span></span>
<span data-ttu-id="9c1f6-157">目前沒有的記錄分析查詢，可以匯出的 tooPower BI 8 MB 的大小限制。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-157">There is currently a size limit of 8 MB for a Log Analytics query that can be exported tooPower BI.</span></span>  <span data-ttu-id="9c1f6-158">此限制即將放寬。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-158">This limit will be increased soon.</span></span>


##<a name="powershell-cmdlets"></a><span data-ttu-id="9c1f6-159">PowerShell Cmdlet</span><span class="sxs-lookup"><span data-stu-id="9c1f6-159">PowerShell cmdlets</span></span>

### <a name="question-does-hello-log-search-powershell-cmdlet-get-updated-after-i-upgrade"></a><span data-ttu-id="9c1f6-160">問題： 未 hello 記錄搜尋 PowerShell cmdlet 取得更新之後升級嗎？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-160">Question: Does hello Log Search PowerShell cmdlet get updated after I upgrade?</span></span>
<span data-ttu-id="9c1f6-161">hello [Get AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults)尚未升級的 toohello 新搜尋語言。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-161">hello [Get-AzureRmOperationalInsightsSearchResults](https://docs.microsoft.com/powershell/module/azurerm.operationalinsights/Get-AzureRmOperationalInsightsSearchResults) has not yet been upgraded toohello new search language.</span></span>  <span data-ttu-id="9c1f6-162">即使在工作區升級之後，請繼續 toouse hello 舊版的查詢語言，與這個指令程式。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-162">Continue toouse hello legacy query language with this cmdlet, even after you upgrade your workspace.</span></span>  <span data-ttu-id="9c1f6-163">當更新時，更新文件將會提供 hello 指令程式。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-163">Updated documentation will become available for hello cmdlet when it's updated.</span></span>


## <a name="resource-manager-templates"></a><span data-ttu-id="9c1f6-164">Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="9c1f6-164">Resource Manager templates</span></span>

### <a name="question-can-i-create-an-upgraded-workspace-with-a-resource-manager-template"></a><span data-ttu-id="9c1f6-165">問題：我可以使用 Resource Manager 範本建立升級工作區嗎？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-165">Question: Can I create an upgraded workspace with a Resource Manager template?</span></span>
<span data-ttu-id="9c1f6-166">是。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-166">Yes.</span></span>  <span data-ttu-id="9c1f6-167">您必須使用 2017年-03-15-預覽的應用程式開發介面版本，並包含**功能**如 hello 下列範例所示在範本中的區段。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-167">You must use an API version of 2017-03-15-preview and include a **features** section in your template as in hello following example.</span></span>

    "resources": [
        {
            "type": "Microsoft.OperationalInsights/workspaces",
            "apiVersion": "2017-03-15-preview",
            "name": "[parameters('workspaceName')]",
            "location": "[parameters('workspaceRegion')]",
            "properties": {
                "sku": {
                    "name": "Free"
                },
                "features": {
                    "legacy": 0,
                    "searchVersion": 1
                }
            }
        }
    ],



## <a name="solutions"></a><span data-ttu-id="9c1f6-168">解決方案</span><span class="sxs-lookup"><span data-stu-id="9c1f6-168">Solutions</span></span>

### <a name="question-will-my-solutions-continue-toowork"></a><span data-ttu-id="9c1f6-169">問題： 我的方案將會繼續 toowork 嗎？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-169">Question: Will my solutions continue toowork?</span></span>
<span data-ttu-id="9c1f6-170">所有方案會在升級後的工作區，都繼續 toowork，但如果它們是轉換的 toohello 新的查詢語言，可改善其效能。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-170">All solutions will continue toowork in an upgraded workspace, although their performance will improve if they are converted toohello new query language.</span></span>  <span data-ttu-id="9c1f6-171">本節中所述之現有解決方案目前已知存在問題。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-171">There are known issues with some existing solutions that are described in this section.</span></span>

### <a name="known-issue-capacity-and-performance-solution"></a><span data-ttu-id="9c1f6-172">已知問題：容量與效能解決方案</span><span class="sxs-lookup"><span data-stu-id="9c1f6-172">Known issue: Capacity and Performance solution</span></span>
<span data-ttu-id="9c1f6-173">某些 hello 組件以 hello[容量和效能](log-analytics-capacity.md)可能是空的檢視。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-173">Some of hello parts in hello [Capacity and Performance](log-analytics-capacity.md) view may be empty.</span></span>  <span data-ttu-id="9c1f6-174">修正 toothis 問題將會很快。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-174">A fix toothis issue will be available shortly.</span></span>

### <a name="known-issue-device-health-solution"></a><span data-ttu-id="9c1f6-175">已知問題：裝置健康情況解決方案</span><span class="sxs-lookup"><span data-stu-id="9c1f6-175">Known issue: Device Health solution</span></span>
<span data-ttu-id="9c1f6-176">hello[裝置健全狀況解決方案](https://docs.microsoft.com/windows/deployment/update/device-health-monitor)不會收集在升級後的工作區中的資料。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-176">hello [Device Health solution](https://docs.microsoft.com/windows/deployment/update/device-health-monitor) will not collect data in an upgraded workspace.</span></span>  <span data-ttu-id="9c1f6-177">修正 toothis 問題將會很快。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-177">A fix toothis issue will be available shortly.</span></span>

### <a name="known-issue-application-insights-connector"></a><span data-ttu-id="9c1f6-178">已知問題：Application Insights Connector</span><span class="sxs-lookup"><span data-stu-id="9c1f6-178">Known issue: Application Insights connector</span></span>
<span data-ttu-id="9c1f6-179">已升級工作區目前不支援 [Application Insights Connector 解決方案](log-analytics-app-insights-connector.md)中的檢視方塊。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-179">Perspectives in [Application Insights Connector solution](log-analytics-app-insights-connector.md) are currently not supported in an upgraded workspace.</span></span>  <span data-ttu-id="9c1f6-180">修正 toothis 問題目前正在進行分析。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-180">A fix toothis issue is currently under analysis.</span></span>

## <a name="upgrade-process"></a><span data-ttu-id="9c1f6-181">升級程序</span><span class="sxs-lookup"><span data-stu-id="9c1f6-181">Upgrade process</span></span>

### <a name="question-i-have-several-workspaces-can-i-upgrade-all-workspaces-at-hello-same-time"></a><span data-ttu-id="9c1f6-182">問題：我有數個工作區。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-182">Question: I have several workspaces.</span></span> <span data-ttu-id="9c1f6-183">我可以升級在 hello 的所有工作區相同的時間？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-183">Can I upgrade all workspaces at hello same time?</span></span>  
<span data-ttu-id="9c1f6-184">否。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-184">No.</span></span>  <span data-ttu-id="9c1f6-185">升級適用於每次 tooa 單一工作區。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-185">Upgrade applies tooa single workspace each time.</span></span> <span data-ttu-id="9c1f6-186">目前無法一次升級多個工作區。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-186">Currently there is no way of upgrading many workspaces at once.</span></span> <span data-ttu-id="9c1f6-187">請注意，將也會受到 hello 升級 工作區的其他使用者的影響。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-187">Please note that other users of hello upgraded workspace will be affected as well.</span></span>  

### <a name="question-will-existing-log-data-collected-in-my-workspace-be-modified-if-i-upgrade"></a><span data-ttu-id="9c1f6-188">問題：如果我升級，我的工作區中收集的現有記錄資料會被修改嗎？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-188">Question: Will existing log data collected in my workspace be modified if I upgrade?</span></span>  
<span data-ttu-id="9c1f6-189">否。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-189">No.</span></span> <span data-ttu-id="9c1f6-190">hello 的記錄資料可用 tooyour 工作區中搜尋不會受到 hello 升級。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-190">hello log data available tooyour workspace searches is not affected by hello upgrade.</span></span> <span data-ttu-id="9c1f6-191">已儲存的搜尋，警示和檢視都會自動轉換的 toohello 新搜尋語言。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-191">Saved searches, alerts and views will be converted toohello new search language automatically.</span></span>  

### <a name="question-what-happens-if-i-dont-upgrade-my-workspace"></a><span data-ttu-id="9c1f6-192">問題：如果不升級我的工作區會發生什麼事？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-192">Question: What happens if I don't upgrade my workspace?</span></span>  
<span data-ttu-id="9c1f6-193">hello 舊版的記錄搜尋將會取代來自數個月的 hello。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-193">hello legacy log search will be deprecated in hello coming months.</span></span> <span data-ttu-id="9c1f6-194">屆時未升級的工作區將會自動升級。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-194">Workspaces that are not upgraded by that time will be upgraded automatically.</span></span>

### <a name="question-i-didnt-choose-tooupgrade-but-my-workspace-has-been-upgraded-anyway-what-happened"></a><span data-ttu-id="9c1f6-195">問題： 未選擇 tooupgrade，但仍已升級我的工作區 ！</span><span class="sxs-lookup"><span data-stu-id="9c1f6-195">Question: I didn't choose tooupgrade, but my workspace has been upgraded anyway!</span></span> <span data-ttu-id="9c1f6-196">發生什麼情形？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-196">What happened?</span></span>  
<span data-ttu-id="9c1f6-197">此工作區的另一個系統管理員可能已經升級為 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-197">Another admin of this workspace could have upgraded hello workspace.</span></span> <span data-ttu-id="9c1f6-198">請注意，所有工作區時便會自動升級 hello 新語言正式運作。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-198">Please note that all workspaces will be automatically upgraded when hello new language reaches general availability.</span></span>  

### <a name="question-i-have-upgraded-by-mistake-and-now-need-toocancel-it-and-restore-everything-back-what-should-i-do"></a><span data-ttu-id="9c1f6-199">問題： 我有升級不小心，而且它和還原的所有項目後，現在需要 toocancel。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-199">Question: I have upgraded by mistake and now need toocancel it and restore everything back.</span></span> <span data-ttu-id="9c1f6-200">我該怎麼辦？！</span><span class="sxs-lookup"><span data-stu-id="9c1f6-200">What should I do?!</span></span>  
<span data-ttu-id="9c1f6-201">沒問題。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-201">No problem.</span></span>  <span data-ttu-id="9c1f6-202">我們會在升級時之前建立工作區的快照集，以便您可以將它還原。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-202">We create a snapshot of your workspace before upgrade, so you can restore it.</span></span> <span data-ttu-id="9c1f6-203">請記住，警示或搜尋後 hello 升級但將會遺失您所儲存的檢視。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-203">Keep in mind that searches, alerts or views you saved after hello upgrade will be lost though.</span></span>  <span data-ttu-id="9c1f6-204">toorestore 您工作區的環境，在後續 hello 程序[可以在哪裡尋求之後升級嗎？](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)</span><span class="sxs-lookup"><span data-stu-id="9c1f6-204">toorestore your workspace environment, follow hello procedure at [Can I go back after I upgrade?](log-analytics-log-search-upgrade.md#can-i-go-back-after-i-upgrade)</span></span>


## <a name="views"></a><span data-ttu-id="9c1f6-205">Views</span><span class="sxs-lookup"><span data-stu-id="9c1f6-205">Views</span></span>

### <a name="question-how-do-i-create-a-new-view-with-view-designer"></a><span data-ttu-id="9c1f6-206">問題：如何使用檢視設計工具建立新的檢視？</span><span class="sxs-lookup"><span data-stu-id="9c1f6-206">Question: How do I create a new view with View Designer?</span></span>
<span data-ttu-id="9c1f6-207">先前 tooupgrade，您可以建立新的檢視與檢視設計工具從 hello 主要儀表板上的磚。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-207">Prior tooupgrade, you could create a new view with View Designer from a tile on hello main dashboard.</span></span>  <span data-ttu-id="9c1f6-208">升級您的工作區時，會移除此圖格。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-208">When your workspace is upgraded, this tile is removed.</span></span>  <span data-ttu-id="9c1f6-209">您可以建立新的檢視與檢視設計工具 hello OMS 入口網站中按一下綠色的 hello + hello 左功能表中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-209">You can create a new view with View Designer in hello OMS portal by clicking on hello green + button in hello left menu.</span></span>

### <a name="known-issue-see-all-option-for-line-charts-in-views-doesnt-result-in-a-line-chart"></a><span data-ttu-id="9c1f6-210">已知問題：折線圖的檢視全部選項不會產生折線圖</span><span class="sxs-lookup"><span data-stu-id="9c1f6-210">Known issue: See all option for line charts in views doesn't result in a line chart</span></span>
<span data-ttu-id="9c1f6-211">當您按一下 hello*查看所有*選項在 hello 下方列圖表部分檢視中，您會看到與資料表。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-211">When you click on hello *See all* option at hello bottom of a line chart part in a view, you are presented with a table.</span></span>  <span data-ttu-id="9c1f6-212">先前 tooupgrade，就會顯示與折線圖。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-212">Prior tooupgrade, you would be presented with a line chart.</span></span>  <span data-ttu-id="9c1f6-213">目前正在分析此問題以進行可能的修改。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-213">This issue is being analyzed for a potential modification.</span></span>


## <a name="next-steps"></a><span data-ttu-id="9c1f6-214">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9c1f6-214">Next steps</span></span>

- <span data-ttu-id="9c1f6-215">深入了解[升級您的工作區 toohello 新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)。</span><span class="sxs-lookup"><span data-stu-id="9c1f6-215">Learn more about [upgrading your workspace toohello new Log Analytics query language](log-analytics-log-search-upgrade.md).</span></span>
