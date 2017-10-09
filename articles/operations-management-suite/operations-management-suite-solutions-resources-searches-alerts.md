---
title: "aaaSaved 搜尋和 OMS 解決方案中的警示 |Microsoft 文件"
description: "OMS 中的解決方案通常會包含已儲存的搜尋 hello 解決方案所收集的記錄分析 tooanalyze 資料中。  它們可能也定義警示 toonotify hello 使用者或自動採取動作以回應 tooa 嚴重的問題。  本文說明如何 toodefine 記錄分析儲存搜尋和警示在 ARM 範本讓它們可以包含在管理解決方案。"
services: operations-management-suite
documentationcenter: 
author: bwren
manager: carmonm
editor: tysonn
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93d7c5bbf061473833ca6c0a8e4d8e10d923f3ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-toooms-management-solution-preview"></a><span data-ttu-id="a4e2f-105">新增記錄分析儲存的搜尋和警示 tooOMS 管理方案 （預覽）</span><span class="sxs-lookup"><span data-stu-id="a4e2f-105">Adding Log Analytics saved searches and alerts tooOMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="a4e2f-106">這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="a4e2f-107">如下所述的任何結構描述是主體 toochange。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-107">Any schema described below is subject toochange.</span></span>   


<span data-ttu-id="a4e2f-108">[在 OMS 中的管理解決方案](operations-management-suite-solutions.md)通常會包含[已儲存的搜尋](../log-analytics/log-analytics-log-searches.md)hello 解決方案所收集的記錄分析 tooanalyze 資料中。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics tooanalyze data collected by hello solution.</span></span>  <span data-ttu-id="a4e2f-109">它們也必須定義[警示](../log-analytics/log-analytics-alerts.md)toonotify hello 使用者或自動採取動作以回應 tooa 嚴重的問題。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) toonotify hello user or automatically take action in response tooa critical issue.</span></span>  <span data-ttu-id="a4e2f-110">本文說明如何 toodefine 記錄分析儲存搜尋和警示中的[資源管理範本](../resource-manager-template-walkthrough.md)以便包含在[管理解決方案](operations-management-suite-solutions-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-110">This article describes how toodefine Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a4e2f-111">hello 這篇文章中的範例使用參數和變數，都是必要或常見 toomanagement 解決方案中所述[Operations Management Suite (OMS) 中建立管理方案](operations-management-suite-solutions-creating.md)</span><span class="sxs-lookup"><span data-stu-id="a4e2f-111">hello samples in this article use parameters and variables that are either required or common toomanagement solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="a4e2f-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="a4e2f-112">Prerequisites</span></span>
<span data-ttu-id="a4e2f-113">本文假設您已經熟悉如何太[建立管理方案](operations-management-suite-solutions-creating.md)和 hello 結構[ARM 範本](../resource-group-authoring-templates.md)和方案檔案。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-113">This article assumes that you're already familiar with how too[create a management solution](operations-management-suite-solutions-creating.md) and hello structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="a4e2f-114">Log Analytics 工作區</span><span class="sxs-lookup"><span data-stu-id="a4e2f-114">Log Analytics Workspace</span></span>
<span data-ttu-id="a4e2f-115">Log Analytics 中的所有資源都包含於[工作區](../log-analytics/log-analytics-manage-access.md)中。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="a4e2f-116">中所述[OMS 工作區以及自動化帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account)hello 工作區不包含在 hello 管理解決方案，但必須先安裝 hello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) hello workspace isn't included in hello management solution but must exist before hello solution is installed.</span></span>  <span data-ttu-id="a4e2f-117">如果它無法使用，hello 方案安裝將會失敗。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-117">If it isn't available, then hello solution install will fail.</span></span>

<span data-ttu-id="a4e2f-118">hello 工作區的 hello 名稱已在 hello 的每個記錄分析資源的名稱。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-118">hello name of hello workspace is in hello name of each Log Analytics resource.</span></span>  <span data-ttu-id="a4e2f-119">這是以 hello hello 方案**工作區**參數如 hello 下列 savedsearch 資源的範例所示。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-119">This is done in hello solution with hello **workspace** parameter as in hello following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="a4e2f-120">儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="a4e2f-120">Saved Searches</span></span>
<span data-ttu-id="a4e2f-121">包含[已儲存的搜尋](../log-analytics/log-analytics-log-searches.md)方案 tooallow 使用者 tooquery 資料中收集您的方案。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution tooallow users tooquery data collected by your solution.</span></span>  <span data-ttu-id="a4e2f-122">已儲存搜尋會出現在**我的最愛**hello OMS 入口網站和**已儲存的搜尋**hello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-122">Saved searches will appear under **Favorites** in hello OMS portal and **Saved Searches** in hello Azure portal .</span></span>  <span data-ttu-id="a4e2f-123">每個警示也會需要儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="a4e2f-124">[記錄分析儲存搜尋](../log-analytics/log-analytics-log-searches.md)資源有一種`Microsoft.OperationalInsights/workspaces/savedSearches`而且具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have hello following structure.</span></span>  <span data-ttu-id="a4e2f-125">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 

    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
        ],
        "tags": { },
        "properties": {
            "etag": "*",
            "query": "[variables('SavedSearch').Query]",
            "displayName": "[variables('SavedSearch').DisplayName]",
            "category": "[variables('SavedSearch').Category]"
        }
    }



<span data-ttu-id="a4e2f-126">Hello 下表說明每個儲存搜尋的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-126">Each of hello properties of a saved search are described in hello following table.</span></span> 

| <span data-ttu-id="a4e2f-127">屬性</span><span class="sxs-lookup"><span data-stu-id="a4e2f-127">Property</span></span> | <span data-ttu-id="a4e2f-128">說明</span><span class="sxs-lookup"><span data-stu-id="a4e2f-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a4e2f-129">category</span><span class="sxs-lookup"><span data-stu-id="a4e2f-129">category</span></span> | <span data-ttu-id="a4e2f-130">hello hello 已儲存搜尋的分類。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-130">hello category for hello saved search.</span></span>  <span data-ttu-id="a4e2f-131">任何已儲存的搜尋 hello 通常也會共用相同的方案中為一個分類，一起群組在 hello 主控台。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-131">Any saved searches in hello same solution will often share a single category so they are grouped together in hello console.</span></span> |
| <span data-ttu-id="a4e2f-132">displayname</span><span class="sxs-lookup"><span data-stu-id="a4e2f-132">displayname</span></span> | <span data-ttu-id="a4e2f-133">Hello 名稱 toodisplay hello 入口網站中儲存搜尋。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-133">Name toodisplay for hello saved search in hello portal.</span></span> |
| <span data-ttu-id="a4e2f-134">query</span><span class="sxs-lookup"><span data-stu-id="a4e2f-134">query</span></span> | <span data-ttu-id="a4e2f-135">查詢 toorun。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-135">Query toorun.</span></span> |

> [!NOTE]
> <span data-ttu-id="a4e2f-136">如果它包含無法解譯為 JSON 的字元，您可能需要在 hello 查詢 toouse 逸出字元。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-136">You may need toouse escape characters in hello query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="a4e2f-137">比方說，如果您的查詢已**類型： AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**，它應該要撰寫 hello 方案檔案儲存為**類型： AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in hello solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="a4e2f-138">Alerts</span><span class="sxs-lookup"><span data-stu-id="a4e2f-138">Alerts</span></span>
<span data-ttu-id="a4e2f-139">[Log Analytics 警示](../log-analytics/log-analytics-alerts.md)是由定期執行儲存之搜尋的警示規則所建立。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="a4e2f-140">如果 hello hello 查詢結果符合指定的準則，就會建立警示的記錄，並執行一或多個動作。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-140">If hello results of hello query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="a4e2f-141">Hello 下列三個不同的資源是由管理解決方案中的警示規則所組成。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-141">Alert rules in a management solution are made up of hello following three different resources.</span></span>

- <span data-ttu-id="a4e2f-142">**儲存的搜尋。**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-142">**Saved search.**</span></span>  <span data-ttu-id="a4e2f-143">定義將會執行的 hello 記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-143">Defines hello log search that will be run.</span></span>  <span data-ttu-id="a4e2f-144">多個警示規則可以共用單一儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="a4e2f-145">**排程。**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-145">**Schedule.**</span></span>  <span data-ttu-id="a4e2f-146">定義頻率 hello 記錄搜尋將會執行。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-146">Defines how often hello log search will be run.</span></span>  <span data-ttu-id="a4e2f-147">每個警示規則必須且只能有一個排程。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="a4e2f-148">**警示動作。**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-148">**Alert action.**</span></span>  <span data-ttu-id="a4e2f-149">每個警示規則不會有一個動作資源類型為**警示**，定義 hello hello 例如 hello 準則時將會建立警示的記錄，以及 hello 警示的嚴重性的警示詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-149">Each alert rule will have one action resource with a type of **Alert** that defines hello details of hello alert such as hello criteria for when an alert record will be created and hello alert's severity.</span></span>  <span data-ttu-id="a4e2f-150">hello 動作資源會選擇性地定義郵件和 runbook 的回應。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-150">hello action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="a4e2f-151">**Webhook 動作 (選擇性)。**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="a4e2f-152">如果 hello 警示規則將會呼叫 webhook，則它需要執行其他動作資源類型為**Webhook**。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-152">If hello alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="a4e2f-153">儲存的搜尋資源如上所述。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-153">Saved search resources are described above.</span></span>  <span data-ttu-id="a4e2f-154">hello 其他資源如下所述。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-154">hello other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="a4e2f-155">排程資源</span><span class="sxs-lookup"><span data-stu-id="a4e2f-155">Schedule resource</span></span>

<span data-ttu-id="a4e2f-156">儲存的搜尋可以有一或多個排程，其中每個排程均代表不同的警示規則。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="a4e2f-157">hello 排程會定義頻率 hello 搜尋執行和 hello 的 hello 透過擷取資料的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-157">hello schedule defines how often hello search is run and hello time interval over which hello data is retrieved.</span></span>  <span data-ttu-id="a4e2f-158">排程資源有一種`Microsoft.OperationalInsights/workspaces/savedSearches/schedules/`而且具有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have hello following structure.</span></span> <span data-ttu-id="a4e2f-159">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 


    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name)]"
        ],
        "properties": {
            "etag": "*",
            "interval": "[variables('Schedule').Interval]",
            "queryTimeSpan": "[variables('Schedule').TimeSpan]",
            "enabled": "[variables('Schedule').Enabled]"
        }
    }



<span data-ttu-id="a4e2f-160">排程資源的 hello 內容詳述於下表中的 hello。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-160">hello properties for schedule resources are described in hello following table.</span></span>

| <span data-ttu-id="a4e2f-161">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a4e2f-161">Element name</span></span> | <span data-ttu-id="a4e2f-162">必要</span><span class="sxs-lookup"><span data-stu-id="a4e2f-162">Required</span></span> | <span data-ttu-id="a4e2f-163">說明</span><span class="sxs-lookup"><span data-stu-id="a4e2f-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a4e2f-164">已啟用</span><span class="sxs-lookup"><span data-stu-id="a4e2f-164">enabled</span></span>       | <span data-ttu-id="a4e2f-165">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-165">Yes</span></span> | <span data-ttu-id="a4e2f-166">指定是否要在建立時，啟用 hello 警示。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-166">Specifies whether hello alert is enabled when it's created.</span></span> |
| <span data-ttu-id="a4e2f-167">interval</span><span class="sxs-lookup"><span data-stu-id="a4e2f-167">interval</span></span>      | <span data-ttu-id="a4e2f-168">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-168">Yes</span></span> | <span data-ttu-id="a4e2f-169">Hello 查詢執行的頻率以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-169">How often hello query runs in minutes.</span></span> |
| <span data-ttu-id="a4e2f-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="a4e2f-170">queryTimeSpan</span></span> | <span data-ttu-id="a4e2f-171">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-171">Yes</span></span> | <span data-ttu-id="a4e2f-172">以分鐘為單位的 tooevaluate 結果上的時間長度。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-172">Length of time in minutes over which tooevaluate results.</span></span> |

<span data-ttu-id="a4e2f-173">hello 排程資源應該依存於儲存搜尋，以便建立 hello 排程之前的 hello。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-173">hello schedule resource should depend on hello saved search so that it's created before hello schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="a4e2f-174">動作</span><span class="sxs-lookup"><span data-stu-id="a4e2f-174">Actions</span></span>
<span data-ttu-id="a4e2f-175">有兩種類型的 hello 所指定的動作資源**類型**屬性。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-175">There are two types of action resource specified by hello **Type** property.</span></span>  <span data-ttu-id="a4e2f-176">排程需要一個**警示**動作，它會定義 hello hello 警示規則，並應採取的動作時建立警示詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-176">A schedule requires one **Alert** action which defines hello details of hello alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="a4e2f-177">它也可以包含**Webhook**如果 webhook 應該呼叫 hello 警示中的動作。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-177">It may also include a **Webhook** action if a webhook should be called from hello alert.</span></span>  

<span data-ttu-id="a4e2f-178">動作資源具有 `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions` 類型。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="a4e2f-179">警示動作</span><span class="sxs-lookup"><span data-stu-id="a4e2f-179">Alert actions</span></span>

<span data-ttu-id="a4e2f-180">每個排程都會有一個**警示**動作。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="a4e2f-181">這會定義 hello hello 警示及選擇性通知和補救動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-181">This defines hello details of hello alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="a4e2f-182">通知會傳送電子郵件 tooone 或多個位址。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-182">A notification sends an email tooone or more addresses.</span></span>  <span data-ttu-id="a4e2f-183">補救啟動的 Azure 自動化 tooattempt tooremediate hello 偵測到問題。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-183">A remediation starts a runbook in Azure Automation tooattempt tooremediate hello detected issue.</span></span>

<span data-ttu-id="a4e2f-184">警示的動作有下列結構的 hello。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-184">Alert actions have hello following structure.</span></span>  <span data-ttu-id="a4e2f-185">這包括一般變數和參數，讓您可以複製並貼入您的方案檔的此程式碼片段，然後變更 hello 參數名稱。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change hello parameter names.</span></span> 



    {
        "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Alert').Name)]",
        "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
        "apiVersion": "[variables('LogAnalyticsApiVersion')]",
        "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
        ],
        "properties": {
            "etag": "*",
            "type": "Alert",
            "name": "[variables('Alert').Name]",
            "description": "[variables('Alert').Description]",
            "severity": "[variables('Alert').Severity]",
            "threshold": {
                "operator": "[variables('Alert').Threshold.Operator]",
                "value": "[variables('Alert').Threshold.Value]",
                "metricsTrigger": {
                    "triggerCondition": "[variables('Alert').Threshold.Trigger.Condition]",
                    "operator": "[variables('Alert').Trigger.Operator]",
                    "value": "[variables('Alert').Trigger.Value]"
                },
            },
            "emailNotification": {
                "recipients": [
                    "[variables('Alert').Recipients]"
                ],
                "subject": "[variables('Alert').Subject]"
            },
            "remediation": {
                "runbookName": "[variables('Alert').Remedition.RunbookName]",
                "webhookUri": "[variables('Alert').Remedition.WebhookUri]"
            }
        }
    }

<span data-ttu-id="a4e2f-186">hello 下表說明警示動作資源的 hello 內容。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-186">hello properties for Alert action resources are described in hello following tables.</span></span>

| <span data-ttu-id="a4e2f-187">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a4e2f-187">Element name</span></span> | <span data-ttu-id="a4e2f-188">必要</span><span class="sxs-lookup"><span data-stu-id="a4e2f-188">Required</span></span> | <span data-ttu-id="a4e2f-189">說明</span><span class="sxs-lookup"><span data-stu-id="a4e2f-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a4e2f-190">類型</span><span class="sxs-lookup"><span data-stu-id="a4e2f-190">Type</span></span> | <span data-ttu-id="a4e2f-191">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-191">Yes</span></span> | <span data-ttu-id="a4e2f-192">Hello 動作的類型。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-192">Type of hello action.</span></span>  <span data-ttu-id="a4e2f-193">這會是適用於警示動作的 **Alert**。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="a4e2f-194">名稱</span><span class="sxs-lookup"><span data-stu-id="a4e2f-194">Name</span></span> | <span data-ttu-id="a4e2f-195">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-195">Yes</span></span> | <span data-ttu-id="a4e2f-196">Hello 警示的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-196">Display name for hello alert.</span></span>  <span data-ttu-id="a4e2f-197">這是顯示 hello 警示規則的 hello 主控台中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-197">This is hello name that's displayed in hello console for hello alert rule.</span></span> |
| <span data-ttu-id="a4e2f-198">說明</span><span class="sxs-lookup"><span data-stu-id="a4e2f-198">Description</span></span> | <span data-ttu-id="a4e2f-199">否</span><span class="sxs-lookup"><span data-stu-id="a4e2f-199">No</span></span> | <span data-ttu-id="a4e2f-200">Hello 警示的選擇性描述。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-200">Optional description of hello alert.</span></span> |
| <span data-ttu-id="a4e2f-201">嚴重性</span><span class="sxs-lookup"><span data-stu-id="a4e2f-201">Severity</span></span> | <span data-ttu-id="a4e2f-202">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-202">Yes</span></span> | <span data-ttu-id="a4e2f-203">嚴重性 hello 警示記錄中的 hello 下列值：</span><span class="sxs-lookup"><span data-stu-id="a4e2f-203">Severity of hello alert record from hello following values:</span></span><br><br> <span data-ttu-id="a4e2f-204">**Critical**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-204">**Critical**</span></span><br><span data-ttu-id="a4e2f-205">**警告**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-205">**Warning**</span></span><br><span data-ttu-id="a4e2f-206">**Informational**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="a4e2f-207">閾值</span><span class="sxs-lookup"><span data-stu-id="a4e2f-207">Threshold</span></span>
<span data-ttu-id="a4e2f-208">此為必要區段。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-208">This section is required.</span></span>  <span data-ttu-id="a4e2f-209">它會定義 hello hello 警示臨界值的屬性。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-209">It defines hello properties for hello alert threshold.</span></span>

| <span data-ttu-id="a4e2f-210">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a4e2f-210">Element name</span></span> | <span data-ttu-id="a4e2f-211">必要</span><span class="sxs-lookup"><span data-stu-id="a4e2f-211">Required</span></span> | <span data-ttu-id="a4e2f-212">說明</span><span class="sxs-lookup"><span data-stu-id="a4e2f-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a4e2f-213">運算子</span><span class="sxs-lookup"><span data-stu-id="a4e2f-213">Operator</span></span> | <span data-ttu-id="a4e2f-214">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-214">Yes</span></span> | <span data-ttu-id="a4e2f-215">從下列值的 hello hello 比較運算子：</span><span class="sxs-lookup"><span data-stu-id="a4e2f-215">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="a4e2f-216">**gt = 大於<br>lt = 少於**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="a4e2f-217">值</span><span class="sxs-lookup"><span data-stu-id="a4e2f-217">Value</span></span> | <span data-ttu-id="a4e2f-218">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-218">Yes</span></span> | <span data-ttu-id="a4e2f-219">hello 值 toocompare hello 結果。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-219">hello value toocompare hello results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="a4e2f-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="a4e2f-220">MetricsTrigger</span></span>
<span data-ttu-id="a4e2f-221">此為選擇性區段。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-221">This section is optional.</span></span>  <span data-ttu-id="a4e2f-222">加入此區段以供計量計量警示使用。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="a4e2f-223">計量測量警示目前是處於公開預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="a4e2f-224">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a4e2f-224">Element name</span></span> | <span data-ttu-id="a4e2f-225">必要</span><span class="sxs-lookup"><span data-stu-id="a4e2f-225">Required</span></span> | <span data-ttu-id="a4e2f-226">說明</span><span class="sxs-lookup"><span data-stu-id="a4e2f-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a4e2f-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="a4e2f-227">TriggerCondition</span></span> | <span data-ttu-id="a4e2f-228">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-228">Yes</span></span> | <span data-ttu-id="a4e2f-229">指定是否 hello 臨界值是針對漏洞或連續的漏洞，從下列值的 hello 總數：</span><span class="sxs-lookup"><span data-stu-id="a4e2f-229">Specifies whether hello threshold is for total number of breaches or consecutive breaches from hello following values:</span></span><br><br><span data-ttu-id="a4e2f-230">**Total<br>Consecutive**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="a4e2f-231">運算子</span><span class="sxs-lookup"><span data-stu-id="a4e2f-231">Operator</span></span> | <span data-ttu-id="a4e2f-232">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-232">Yes</span></span> | <span data-ttu-id="a4e2f-233">從下列值的 hello hello 比較運算子：</span><span class="sxs-lookup"><span data-stu-id="a4e2f-233">Operator for hello comparison from hello following values:</span></span><br><br><span data-ttu-id="a4e2f-234">**gt = 大於<br>lt = 少於**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="a4e2f-235">值</span><span class="sxs-lookup"><span data-stu-id="a4e2f-235">Value</span></span> | <span data-ttu-id="a4e2f-236">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-236">Yes</span></span> | <span data-ttu-id="a4e2f-237">Hello hello 準則時間的數目必須符合的 tootrigger hello 警示。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-237">Number of hello times hello criteria must be met tootrigger hello alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="a4e2f-238">節流</span><span class="sxs-lookup"><span data-stu-id="a4e2f-238">Throttling</span></span>
<span data-ttu-id="a4e2f-239">此為選擇性區段。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-239">This section is optional.</span></span>  <span data-ttu-id="a4e2f-240">如果您想 toosuppress 警示 hello 從相同的一段時間後建立警示規則，請包含這一節。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-240">Include this section if you want toosuppress alerts from hello same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="a4e2f-241">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a4e2f-241">Element name</span></span> | <span data-ttu-id="a4e2f-242">必要</span><span class="sxs-lookup"><span data-stu-id="a4e2f-242">Required</span></span> | <span data-ttu-id="a4e2f-243">說明</span><span class="sxs-lookup"><span data-stu-id="a4e2f-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a4e2f-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="a4e2f-244">DurationInMinutes</span></span> | <span data-ttu-id="a4e2f-245">如果包含 Throttling 元素，即為 Yes</span><span class="sxs-lookup"><span data-stu-id="a4e2f-245">Yes if Throttling element included</span></span> | <span data-ttu-id="a4e2f-246">分鐘 toosuppress 警示之後從 hello 建立相同的警示規則的數目。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-246">Number of minutes toosuppress alerts after one from hello same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="a4e2f-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="a4e2f-247">EmailNotification</span></span>
 <span data-ttu-id="a4e2f-248">此區段是選擇性包含它，如果您想 hello 警示 toosend 郵件 tooone 或多個收件者。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-248">This section is optional  Include it if you want hello alert toosend mail tooone or more recipients.</span></span>

| <span data-ttu-id="a4e2f-249">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a4e2f-249">Element name</span></span> | <span data-ttu-id="a4e2f-250">必要</span><span class="sxs-lookup"><span data-stu-id="a4e2f-250">Required</span></span> | <span data-ttu-id="a4e2f-251">說明</span><span class="sxs-lookup"><span data-stu-id="a4e2f-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a4e2f-252">收件者</span><span class="sxs-lookup"><span data-stu-id="a4e2f-252">Recipients</span></span> | <span data-ttu-id="a4e2f-253">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-253">Yes</span></span> | <span data-ttu-id="a4e2f-254">以逗號分隔的電子郵件位址清單 toosend 通知警示 hello 下列範例中建立這類時。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-254">Comma delimited list of email addresses toosend notification when an alert is created such as in hello following example.</span></span><br><br><span data-ttu-id="a4e2f-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="a4e2f-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="a4e2f-256">主旨</span><span class="sxs-lookup"><span data-stu-id="a4e2f-256">Subject</span></span> | <span data-ttu-id="a4e2f-257">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-257">Yes</span></span> | <span data-ttu-id="a4e2f-258">Hello 郵件主旨行。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-258">Subject line of hello mail.</span></span> |
| <span data-ttu-id="a4e2f-259">附件</span><span class="sxs-lookup"><span data-stu-id="a4e2f-259">Attachment</span></span> | <span data-ttu-id="a4e2f-260">否</span><span class="sxs-lookup"><span data-stu-id="a4e2f-260">No</span></span> | <span data-ttu-id="a4e2f-261">目前不支援附件。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="a4e2f-262">如果包含此元素，就應該是 **None**。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="a4e2f-263">補救</span><span class="sxs-lookup"><span data-stu-id="a4e2f-263">Remediation</span></span>
<span data-ttu-id="a4e2f-264">此區段是選擇性包含它，如果您想要在回應 toohello 警示 runbook toostart。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-264">This section is optional  Include it if you want a runbook toostart in response toohello alert.</span></span> |

| <span data-ttu-id="a4e2f-265">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a4e2f-265">Element name</span></span> | <span data-ttu-id="a4e2f-266">必要</span><span class="sxs-lookup"><span data-stu-id="a4e2f-266">Required</span></span> | <span data-ttu-id="a4e2f-267">說明</span><span class="sxs-lookup"><span data-stu-id="a4e2f-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a4e2f-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="a4e2f-268">RunbookName</span></span> | <span data-ttu-id="a4e2f-269">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-269">Yes</span></span> | <span data-ttu-id="a4e2f-270">Hello runbook toostart 的名稱。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-270">Name of hello runbook toostart.</span></span> |
| <span data-ttu-id="a4e2f-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="a4e2f-271">WebhookUri</span></span> | <span data-ttu-id="a4e2f-272">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-272">Yes</span></span> | <span data-ttu-id="a4e2f-273">Hello runbook 的 hello webhook 的 Uri。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-273">Uri of hello webhook for hello runbook.</span></span> |
| <span data-ttu-id="a4e2f-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="a4e2f-274">Expiry</span></span> | <span data-ttu-id="a4e2f-275">否</span><span class="sxs-lookup"><span data-stu-id="a4e2f-275">No</span></span> | <span data-ttu-id="a4e2f-276">到期的日期和時間的 hello 補救。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-276">Date and time that hello remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="a4e2f-277">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="a4e2f-277">Webhook actions</span></span>

<span data-ttu-id="a4e2f-278">Webhook 動作開始的程序呼叫的 URL，同時選擇性提供裝載 toobe 傳送。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-278">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span> <span data-ttu-id="a4e2f-279">它們是類似 tooRemediation 動作，但它們一定會用於可以叫用非 Azure 自動化 runbook 的程序的 webhook。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-279">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="a4e2f-280">它們也提供其他選項可 hello 提供裝載 toobe 傳遞 toohello 遠端處理序。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-280">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="a4e2f-281">如果您的警示將會呼叫 webhook，則它需要的動作資源類型為**Webhook**中新增 toohello**警示**動作資源。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition toohello **Alert** action resource.</span></span>  

    {
      "name": "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearch').Name, '/', variables('Schedule').Name, '/', variables('Webhook').Name)]",
      "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions/",
      "apiVersion": "[variables('LogAnalyticsApiVersion')]",
      "dependsOn": [
            "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('SavedSearch').Name, '/schedules/', variables('Schedule').Name)]"
      ],
      "properties": {
        "etag": "*",
        "type": "[variables('Alert').Webhook.Type]",
        "name": "[variables('Alert').Webhook.Name]",
        "webhookUri": "[variables('Alert').Webhook.webhookUri]",
        "customPayload": "[variables('Alert').Webhook.CustomPayLoad]"
      }
    }

<span data-ttu-id="a4e2f-282">hello 下表描述 hello Webhook 動作資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-282">hello properties for Webhook action resources are described in hello following tables.</span></span>

| <span data-ttu-id="a4e2f-283">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a4e2f-283">Element name</span></span> | <span data-ttu-id="a4e2f-284">必要</span><span class="sxs-lookup"><span data-stu-id="a4e2f-284">Required</span></span> | <span data-ttu-id="a4e2f-285">說明</span><span class="sxs-lookup"><span data-stu-id="a4e2f-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a4e2f-286">類型</span><span class="sxs-lookup"><span data-stu-id="a4e2f-286">type</span></span> | <span data-ttu-id="a4e2f-287">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-287">Yes</span></span> | <span data-ttu-id="a4e2f-288">Hello 動作的類型。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-288">Type of hello action.</span></span>  <span data-ttu-id="a4e2f-289">這會是適用於 Webhook 動作的 **Webhook**。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="a4e2f-290">名稱</span><span class="sxs-lookup"><span data-stu-id="a4e2f-290">name</span></span> | <span data-ttu-id="a4e2f-291">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-291">Yes</span></span> | <span data-ttu-id="a4e2f-292">Hello 動作顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-292">Display name for hello action.</span></span>  <span data-ttu-id="a4e2f-293">這不會顯示在 hello 主控台。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-293">This is not displayed in hello console.</span></span> |
| <span data-ttu-id="a4e2f-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="a4e2f-294">wehookUri</span></span> | <span data-ttu-id="a4e2f-295">是</span><span class="sxs-lookup"><span data-stu-id="a4e2f-295">Yes</span></span> | <span data-ttu-id="a4e2f-296">Hello webhook 的 Uri。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-296">Uri for hello webhook.</span></span> |
| <span data-ttu-id="a4e2f-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="a4e2f-297">customPayload</span></span> | <span data-ttu-id="a4e2f-298">否</span><span class="sxs-lookup"><span data-stu-id="a4e2f-298">No</span></span> | <span data-ttu-id="a4e2f-299">自訂承載 toobe 傳送 toohello webhook。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-299">Custom payload toobe sent toohello webhook.</span></span> <span data-ttu-id="a4e2f-300">hello 格式將取決於哪些 hello webhook 所預期。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-300">hello format will depend on what hello webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="a4e2f-301">範例</span><span class="sxs-lookup"><span data-stu-id="a4e2f-301">Sample</span></span>

<span data-ttu-id="a4e2f-302">以下是方案的範例，包括所包含的 hello 下列資源：</span><span class="sxs-lookup"><span data-stu-id="a4e2f-302">Following is a sample of a solution that include that includes hello following resources:</span></span>

- <span data-ttu-id="a4e2f-303">儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="a4e2f-303">Saved search</span></span>
- <span data-ttu-id="a4e2f-304">排程</span><span class="sxs-lookup"><span data-stu-id="a4e2f-304">Schedule</span></span>
- <span data-ttu-id="a4e2f-305">警示動作</span><span class="sxs-lookup"><span data-stu-id="a4e2f-305">Alert action</span></span>
- <span data-ttu-id="a4e2f-306">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="a4e2f-306">Webhook action</span></span>

<span data-ttu-id="a4e2f-307">hello 範例會使用[標準方案參數](operations-management-suite-solutions-solution-file.md#parameters)通常做為方案中使用變數相對於 toohardcoding hello 資源定義中的值。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-307">hello sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed toohardcoding values in hello resource definitions.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "contentVersion": "1.0",
        "parameters": {
          "workspaceName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Log Analytics workspace"
            }
          },
          "accountName": {
            "type": "string",
            "metadata": {
              "Description": "Name of Automation account"
            }
          },
          "workspaceregionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Log Analytics workspace"
            }
          },
          "regionId": {
            "type": "string",
            "metadata": {
              "Description": "Region of Automation account"
            }
          },
          "pricingTier": {
            "type": "string",
            "metadata": {
              "Description": "Pricing tier of both Log Analytics workspace and Azure Automation account"
            }
          },
          "recipients": {
            "type": "string",
            "metadata": {
              "Description": "List of recipients for hello email alert separated by semicolon"
            }
          }
        },
        "variables": {
          "SolutionName": "MySolution",
          "SolutionVersion": "1.0",
          "SolutionPublisher": "Contoso",
          "ProductName": "SampleSolution",
    
          "LogAnalyticsApiVersion": "2015-11-01-preview",
    
          "MySearch": {
            "displayName": "Error records by hour",
            "query": "Type=MyRecord_CL | measure avg(Rating_d) by Instance_s interval 60minutes",
            "category": "Samples",
            "name": "Samples-Count of data"
          },
          "MyAlert": {
            "Name": "[toLower(concat('myalert-',uniqueString(resourceGroup().id, deployment().name)))]",
            "DisplayName": "My alert rule",
            "Description": "Sample alert.  Fires when 3 error records found over hour interval.",
            "Severity": "Critical",
            "ThresholdOperator": "gt",
            "ThresholdValue": 3,
            "Schedule": {
              "Name": "[toLower(concat('myschedule-',uniqueString(resourceGroup().id, deployment().name)))]",
              "Interval": 15,
              "TimeSpan": 60
            },
            "MetricsTrigger": {
              "TriggerCondition": "Consecutive",
              "Operator": "gt",
              "Value": 3
            },
            "ThrottleMinutes": 60,
            "Notification": {
              "Recipients": [
                "[parameters('recipients')]"
              ],
              "Subject": "Sample alert"
            },
            "Remediation": {
              "RunbookName": "MyRemediationRunbook",
              "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=TluBFH3GpX4IEAnFoImoAWLTULkjD%2bTS0yscyrr7ogw%3d"
            },
            "Webhook": {
              "Name": "MyWebhook",
              "Uri": "https://MyService.com/webhook",
              "Payload": "{\"field1\":\"value1\",\"field2\":\"value2\"}"
            }
          }
        },
        "resources": [
          {
            "name": "[concat(variables('SolutionName'), '[' ,parameters('workspacename'), ']')]",
            "location": "[parameters('workspaceRegionId')]",
            "tags": { },
            "type": "Microsoft.OperationsManagement/solutions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
              "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
            ],
            "properties": {
              "workspaceResourceId": "[resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspacename'))]",
              "referencedResources": [
              ],
              "containedResources": [
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches', parameters('workspacename'), variables('MySearch').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Name)]",
                "[resourceId('Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions', parameters('workspacename'), variables('MySearch').Name, variables('MyAlert').Schedule.Name, variables('MyAlert').Webhook.Name)]"
              ]
            },
            "plan": {
              "name": "[concat(variables('SolutionName'), '[' ,parameters('workspaceName'), ']')]",
              "Version": "[variables('SolutionVersion')]",
              "product": "[variables('ProductName')]",
              "publisher": "[variables('SolutionPublisher')]",
              "promotionCode": ""
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [ ],
            "tags": { },
            "properties": {
              "etag": "*",
              "query": "[variables('MySearch').query]",
              "displayName": "[variables('MySearch').displayName]",
              "category": "[variables('MySearch').category]"
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name)]"
            ],
            "properties": {
              "etag": "*",
              "interval": "[variables('MyAlert').Schedule.Interval]",
              "queryTimeSpan": "[variables('MyAlert').Schedule.TimeSpan]",
              "enabled": true
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/',  variables('MyAlert').Schedule.Name, '/',  variables('MyAlert').Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/',  variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Alert",
              "Name": "[variables('MyAlert').DisplayName]",
              "Description": "[variables('MyAlert').Description]",
              "Severity": "[variables('MyAlert').Severity]",
              "Threshold": {
                "Operator": "[variables('MyAlert').ThresholdOperator]",
                "Value": "[variables('MyAlert').ThresholdValue]",
                "MetricsTrigger": {
                  "TriggerCondition": "[variables('MyAlert').MetricsTrigger.TriggerCondition]",
                  "Operator": "[variables('MyAlert').MetricsTrigger.Operator]",
                  "Value": "[variables('MyAlert').MetricsTrigger.Value]"
                }
              },
              "Throttling": {
                "DurationInMinutes": "[variables('MyAlert').ThrottleMinutes]"
              },
              "EmailNotification": {
                "Recipients": "[variables('MyAlert').Notification.Recipients]",
                "Subject": "[variables('MyAlert').Notification.Subject]",
                "Attachment": "None"
              },
              "Remediation": {
                "RunbookName": "[variables('MyAlert').Remediation.RunbookName]",
                "WebhookUri": "[variables('MyAlert').Remediation.WebhookUri]"
              }
            }
          },
          {
            "name": "[concat(parameters('workspaceName'), '/', variables('MySearch').Name, '/', variables('MyAlert').Schedule.Name, '/', variables('MyAlert').Webhook.Name)]",
            "type": "Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions",
            "apiVersion": "[variables('LogAnalyticsApiVersion')]",
            "dependsOn": [
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name)]",
              "[concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName'), '/savedSearches/', variables('MySearch').Name, '/schedules/', variables('MyAlert').Schedule.Name, '/actions/',variables('MyAlert').Name)]"
            ],
            "properties": {
              "etag": "*",
              "Type": "Webhook",
              "Name": "[variables('MyAlert').Webhook.Name]",
              "WebhookUri": "[variables('MyAlert').Webhook.Uri]",
              "CustomPayload": "[variables('MyAlert').Webhook.Payload]"
            }
          }
        ]
    }


<span data-ttu-id="a4e2f-308">hello 下列參數檔會提供此解決方案的範例值。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-308">hello following parameter file provides samples values for this solution.</span></span>

    {
        "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "workspacename": {
                "value": "myWorkspace"
            },
            "accountName": {
                "value": "myAccount"
            },
            "workspaceregionId": {
                "value": "East US"
            },
            "regionId": {
                "value": "East US 2"
            },
            "pricingTier": {
                "value": "Free"
            },
            "recipients": {
                "value": "recipient1@contoso.com;recipient2@contoso.com"
            }
        }
    }


## <a name="next-steps"></a><span data-ttu-id="a4e2f-309">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a4e2f-309">Next steps</span></span>
* <span data-ttu-id="a4e2f-310">[加入檢視](operations-management-suite-solutions-resources-views.md)tooyour 管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-310">[Add views](operations-management-suite-solutions-resources-views.md) tooyour management solution.</span></span>
* <span data-ttu-id="a4e2f-311">[將自動化 runbook 及其他資源新增](operations-management-suite-solutions-resources-automation.md)tooyour 管理解決方案。</span><span class="sxs-lookup"><span data-stu-id="a4e2f-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) tooyour management solution.</span></span>

