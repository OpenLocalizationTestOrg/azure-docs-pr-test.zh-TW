---
title: "OMS 解決方案中儲存的搜尋和警示 | Microsoft Docs"
description: "OMS 中的解決方案通常會包含 Log Analytics 中儲存的搜尋，來分析解決方案所收集的資料。  它們可能也會定義警示來通知使用者，或自動採取動作以回應重大的問題。  本文說明如何在 ARM 範本中定義 Log Analytics 儲存的搜尋與警示，讓它們能夠包含於管理解決方案中。"
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
ms.openlocfilehash: 21c42a747a08c5386c65d10190baf0054a7adef8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="adding-log-analytics-saved-searches-and-alerts-to-oms-management-solution-preview"></a><span data-ttu-id="a5a42-105">將 Log Analytics 儲存的搜尋和警告新增到 OMS 管理解決方案 (預覽)</span><span class="sxs-lookup"><span data-stu-id="a5a42-105">Adding Log Analytics saved searches and alerts to OMS management solution (Preview)</span></span>

> [!NOTE]
> <span data-ttu-id="a5a42-106">這是在 OMS 中建立管理解決方案 (目前處於預覽狀態) 的預備文件。</span><span class="sxs-lookup"><span data-stu-id="a5a42-106">This is preliminary documentation for creating management solutions in OMS which are currently in preview.</span></span> <span data-ttu-id="a5a42-107">以下所述的任何結構描述可能會有所變更。</span><span class="sxs-lookup"><span data-stu-id="a5a42-107">Any schema described below is subject to change.</span></span>   


<span data-ttu-id="a5a42-108">[OMS 中的管理解決方案](operations-management-suite-solutions.md)通常會包含 Log Analytics 中[儲存的搜尋](../log-analytics/log-analytics-log-searches.md)，來分析解決方案所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="a5a42-108">[Management solutions in OMS](operations-management-suite-solutions.md) will typically include [saved searches](../log-analytics/log-analytics-log-searches.md) in Log Analytics to analyze data collected by the solution.</span></span>  <span data-ttu-id="a5a42-109">它們可能也會定義[警示](../log-analytics/log-analytics-alerts.md)來通知使用者，或自動採取動作以回應重大的問題。</span><span class="sxs-lookup"><span data-stu-id="a5a42-109">They may also define [alerts](../log-analytics/log-analytics-alerts.md) to notify the user or automatically take action in response to a critical issue.</span></span>  <span data-ttu-id="a5a42-110">本文說明如何在[資源範本範本](../resource-manager-template-walkthrough.md)中定義 Log Analytics 儲存的搜尋與警示，讓它們能夠包含於[管理解決方案](operations-management-suite-solutions-creating.md)中。</span><span class="sxs-lookup"><span data-stu-id="a5a42-110">This article describes how to define Log Analytics saved searches and alerts in a [Resource Management template](../resource-manager-template-walkthrough.md) so they can be included in [management solutions](operations-management-suite-solutions-creating.md).</span></span>

> [!NOTE]
> <span data-ttu-id="a5a42-111">本文中的範例使用管理解決方案所必要或通用的參數和變數，如[在 Operations Management Suite (OMS) 中建立管理解決方案](operations-management-suite-solutions-creating.md)所述。</span><span class="sxs-lookup"><span data-stu-id="a5a42-111">The samples in this article use parameters and variables that are either required or common to management solutions  and described in [Creating management solutions in Operations Management Suite (OMS)](operations-management-suite-solutions-creating.md)</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="a5a42-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="a5a42-112">Prerequisites</span></span>
<span data-ttu-id="a5a42-113">本文假設您已經熟悉如何[建立管理解決方案](operations-management-suite-solutions-creating.md)，以及 [ARM 範本](../resource-group-authoring-templates.md)和方案檔的結構。</span><span class="sxs-lookup"><span data-stu-id="a5a42-113">This article assumes that you're already familiar with how to [create a management solution](operations-management-suite-solutions-creating.md) and the structure of an [ARM template](../resource-group-authoring-templates.md) and solution file.</span></span>


## <a name="log-analytics-workspace"></a><span data-ttu-id="a5a42-114">Log Analytics 工作區</span><span class="sxs-lookup"><span data-stu-id="a5a42-114">Log Analytics Workspace</span></span>
<span data-ttu-id="a5a42-115">Log Analytics 中的所有資源都包含於[工作區](../log-analytics/log-analytics-manage-access.md)中。</span><span class="sxs-lookup"><span data-stu-id="a5a42-115">All resources in Log Analytics are contained in a [workspace](../log-analytics/log-analytics-manage-access.md).</span></span>  <span data-ttu-id="a5a42-116">如 [OMS 工作區和自動化帳戶](operations-management-suite-solutions.md#oms-workspace-and-automation-account)所述，工作區不會包含於管理解決方案中，但在安裝解決方案前就必須存在。</span><span class="sxs-lookup"><span data-stu-id="a5a42-116">As described in [OMS workspace and Automation account](operations-management-suite-solutions.md#oms-workspace-and-automation-account) the workspace isn't included in the management solution but must exist before the solution is installed.</span></span>  <span data-ttu-id="a5a42-117">如果無法使用，則解決方案會安裝失敗。</span><span class="sxs-lookup"><span data-stu-id="a5a42-117">If it isn't available, then the solution install will fail.</span></span>

<span data-ttu-id="a5a42-118">工作區的名稱位於每個 Log Analytics 資源的名稱中。</span><span class="sxs-lookup"><span data-stu-id="a5a42-118">The name of the workspace is in the name of each Log Analytics resource.</span></span>  <span data-ttu-id="a5a42-119">這可在解決方案中使用**工作區**參數來完成，如下列 savedsearch 資源範例所示。</span><span class="sxs-lookup"><span data-stu-id="a5a42-119">This is done in the solution with the **workspace** parameter as in the following example of a savedsearch resource.</span></span>

    "name": "[concat(parameters('workspaceName'), '/', variables('SavedSearchId'))]"


## <a name="saved-searches"></a><span data-ttu-id="a5a42-120">儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="a5a42-120">Saved Searches</span></span>
<span data-ttu-id="a5a42-121">在解決方案中包含[儲存的搜尋](../log-analytics/log-analytics-log-searches.md)，可讓使用者查詢您解決方案所收集的資料。</span><span class="sxs-lookup"><span data-stu-id="a5a42-121">Include [saved searches](../log-analytics/log-analytics-log-searches.md) in a solution to allow users to query data collected by your solution.</span></span>  <span data-ttu-id="a5a42-122">儲存的搜尋將出現在 OMS 入口網站中的 [我的最愛] 下方，以及 Azure 入口網站中 [儲存的搜尋] 下方。</span><span class="sxs-lookup"><span data-stu-id="a5a42-122">Saved searches will appear under **Favorites** in the OMS portal and **Saved Searches** in the Azure portal .</span></span>  <span data-ttu-id="a5a42-123">每個警示也會需要儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="a5a42-123">A saved search is also required for each alert.</span></span>   

<span data-ttu-id="a5a42-124">[Log Analytics 儲存的搜尋](../log-analytics/log-analytics-log-searches.md)資源都具有 `Microsoft.OperationalInsights/workspaces/savedSearches` 類型，並具備下列結構。</span><span class="sxs-lookup"><span data-stu-id="a5a42-124">[Log Analytics saved search](../log-analytics/log-analytics-log-searches.md) resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches` and have the following structure.</span></span>  <span data-ttu-id="a5a42-125">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="a5a42-125">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 

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



<span data-ttu-id="a5a42-126">下表說明儲存的搜尋的每個屬性。</span><span class="sxs-lookup"><span data-stu-id="a5a42-126">Each of the properties of a saved search are described in the following table.</span></span> 

| <span data-ttu-id="a5a42-127">屬性</span><span class="sxs-lookup"><span data-stu-id="a5a42-127">Property</span></span> | <span data-ttu-id="a5a42-128">說明</span><span class="sxs-lookup"><span data-stu-id="a5a42-128">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="a5a42-129">category</span><span class="sxs-lookup"><span data-stu-id="a5a42-129">category</span></span> | <span data-ttu-id="a5a42-130">儲存的搜尋的類別。</span><span class="sxs-lookup"><span data-stu-id="a5a42-130">The category for the saved search.</span></span>  <span data-ttu-id="a5a42-131">同一個解決方案中所有儲存的搜尋通常都會共用單一類別，因此它們會在主控台中群組在一起。</span><span class="sxs-lookup"><span data-stu-id="a5a42-131">Any saved searches in the same solution will often share a single category so they are grouped together in the console.</span></span> |
| <span data-ttu-id="a5a42-132">displayname</span><span class="sxs-lookup"><span data-stu-id="a5a42-132">displayname</span></span> | <span data-ttu-id="a5a42-133">要在入口網站中顯示之儲存的搜尋名稱。</span><span class="sxs-lookup"><span data-stu-id="a5a42-133">Name to display for the saved search in the portal.</span></span> |
| <span data-ttu-id="a5a42-134">query</span><span class="sxs-lookup"><span data-stu-id="a5a42-134">query</span></span> | <span data-ttu-id="a5a42-135">要執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="a5a42-135">Query to run.</span></span> |

> [!NOTE]
> <span data-ttu-id="a5a42-136">如果查詢包含可解譯為 JSON 的字元，您可能需要在查詢中使用逸出字元。</span><span class="sxs-lookup"><span data-stu-id="a5a42-136">You may need to use escape characters in the query if it includes characters that could be interpreted as JSON.</span></span>  <span data-ttu-id="a5a42-137">例如，如果查詢為 **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**，就應該在方案檔中撰寫為 **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**。</span><span class="sxs-lookup"><span data-stu-id="a5a42-137">For example, if your query was **Type:AzureActivity OperationName:"Microsoft.Compute/virtualMachines/write"**, it should be written in the solution file as **Type:AzureActivity OperationName:\"Microsoft.Compute/virtualMachines/write\"**.</span></span>

## <a name="alerts"></a><span data-ttu-id="a5a42-138">警示</span><span class="sxs-lookup"><span data-stu-id="a5a42-138">Alerts</span></span>
<span data-ttu-id="a5a42-139">[Log Analytics 警示](../log-analytics/log-analytics-alerts.md)是由定期執行儲存之搜尋的警示規則所建立。</span><span class="sxs-lookup"><span data-stu-id="a5a42-139">[Log Analytics alerts](../log-analytics/log-analytics-alerts.md) are created by alert rules that run a saved search on a regular interval.</span></span>  <span data-ttu-id="a5a42-140">如果查詢的結果符合指定的準則，就會建立警示記錄，並執行一或多個動作。</span><span class="sxs-lookup"><span data-stu-id="a5a42-140">If the results of the query match specified criteria, an alert record is created and one or more actions are run.</span></span>  

<span data-ttu-id="a5a42-141">管理解決方案中的警示規則是由下列三個不同資源所組成。</span><span class="sxs-lookup"><span data-stu-id="a5a42-141">Alert rules in a management solution are made up of the following three different resources.</span></span>

- <span data-ttu-id="a5a42-142">**儲存的搜尋。**</span><span class="sxs-lookup"><span data-stu-id="a5a42-142">**Saved search.**</span></span>  <span data-ttu-id="a5a42-143">定義將執行的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="a5a42-143">Defines the log search that will be run.</span></span>  <span data-ttu-id="a5a42-144">多個警示規則可以共用單一儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="a5a42-144">Multiple alert rules can share a single saved search.</span></span>
- <span data-ttu-id="a5a42-145">**排程。**</span><span class="sxs-lookup"><span data-stu-id="a5a42-145">**Schedule.**</span></span>  <span data-ttu-id="a5a42-146">定義記錄搜尋的執行頻率。</span><span class="sxs-lookup"><span data-stu-id="a5a42-146">Defines how often the log search will be run.</span></span>  <span data-ttu-id="a5a42-147">每個警示規則必須且只能有一個排程。</span><span class="sxs-lookup"><span data-stu-id="a5a42-147">Each alert rule will have one and only one schedule.</span></span>
- <span data-ttu-id="a5a42-148">**警示動作。**</span><span class="sxs-lookup"><span data-stu-id="a5a42-148">**Alert action.**</span></span>  <span data-ttu-id="a5a42-149">每個警示規則都會有一個具有一種**警示**類型的動作資源，該類型會定義警示的詳細資料，像是建立警示記錄的時機及警示的嚴重性等準則。</span><span class="sxs-lookup"><span data-stu-id="a5a42-149">Each alert rule will have one action resource with a type of **Alert** that defines the details of the alert such as the criteria for when an alert record will be created and the alert's severity.</span></span>  <span data-ttu-id="a5a42-150">動作資源將會選擇性地定義郵件和 runbook 回應。</span><span class="sxs-lookup"><span data-stu-id="a5a42-150">The action resource will optionally define a mail and runbook response.</span></span>
- <span data-ttu-id="a5a42-151">**Webhook 動作 (選擇性)。**</span><span class="sxs-lookup"><span data-stu-id="a5a42-151">**Webhook action (optional).**</span></span>  <span data-ttu-id="a5a42-152">如果警示規則將會呼叫 webhook，則它需要執行類型為 **Webhook** 的其他動作資源。</span><span class="sxs-lookup"><span data-stu-id="a5a42-152">If the alert rule will call a webhook, then it requires an additional action resource with a type of **Webhook**.</span></span>    

<span data-ttu-id="a5a42-153">儲存的搜尋資源如上所述。</span><span class="sxs-lookup"><span data-stu-id="a5a42-153">Saved search resources are described above.</span></span>  <span data-ttu-id="a5a42-154">其他資源將在後續內容中加以說明。</span><span class="sxs-lookup"><span data-stu-id="a5a42-154">The other resources are described below.</span></span>


### <a name="schedule-resource"></a><span data-ttu-id="a5a42-155">排程資源</span><span class="sxs-lookup"><span data-stu-id="a5a42-155">Schedule resource</span></span>

<span data-ttu-id="a5a42-156">儲存的搜尋可以有一或多個排程，其中每個排程均代表不同的警示規則。</span><span class="sxs-lookup"><span data-stu-id="a5a42-156">A saved search can have one or more schedules with each schedule representing a separate alert rule.</span></span> <span data-ttu-id="a5a42-157">排程會定義搜尋的執行頻率，以及擷取資料的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="a5a42-157">The schedule defines how often the search is run and the time interval over which the data is retrieved.</span></span>  <span data-ttu-id="a5a42-158">排程資源具有 `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` 類型，並具備下列結構。</span><span class="sxs-lookup"><span data-stu-id="a5a42-158">Schedule resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/` and have the following structure.</span></span> <span data-ttu-id="a5a42-159">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="a5a42-159">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 


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



<span data-ttu-id="a5a42-160">下表會說明排程資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="a5a42-160">The properties for schedule resources are described in the following table.</span></span>

| <span data-ttu-id="a5a42-161">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a5a42-161">Element name</span></span> | <span data-ttu-id="a5a42-162">必要</span><span class="sxs-lookup"><span data-stu-id="a5a42-162">Required</span></span> | <span data-ttu-id="a5a42-163">說明</span><span class="sxs-lookup"><span data-stu-id="a5a42-163">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a5a42-164">已啟用</span><span class="sxs-lookup"><span data-stu-id="a5a42-164">enabled</span></span>       | <span data-ttu-id="a5a42-165">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-165">Yes</span></span> | <span data-ttu-id="a5a42-166">指定在建立警示時是否要加以啟用。</span><span class="sxs-lookup"><span data-stu-id="a5a42-166">Specifies whether the alert is enabled when it's created.</span></span> |
| <span data-ttu-id="a5a42-167">interval</span><span class="sxs-lookup"><span data-stu-id="a5a42-167">interval</span></span>      | <span data-ttu-id="a5a42-168">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-168">Yes</span></span> | <span data-ttu-id="a5a42-169">查詢的執行頻率，以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="a5a42-169">How often the query runs in minutes.</span></span> |
| <span data-ttu-id="a5a42-170">queryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="a5a42-170">queryTimeSpan</span></span> | <span data-ttu-id="a5a42-171">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-171">Yes</span></span> | <span data-ttu-id="a5a42-172">評估結果的時間長度，以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="a5a42-172">Length of time in minutes over which to evaluate results.</span></span> |

<span data-ttu-id="a5a42-173">排程資源應該相依於儲存的搜尋，如此就會在排程之前建立該資源。</span><span class="sxs-lookup"><span data-stu-id="a5a42-173">The schedule resource should depend on the saved search so that it's created before the schedule.</span></span>


### <a name="actions"></a><span data-ttu-id="a5a42-174">動作</span><span class="sxs-lookup"><span data-stu-id="a5a42-174">Actions</span></span>
<span data-ttu-id="a5a42-175">**Type** 屬性會指定兩種類型的動作資源。</span><span class="sxs-lookup"><span data-stu-id="a5a42-175">There are two types of action resource specified by the **Type** property.</span></span>  <span data-ttu-id="a5a42-176">排程需要一個**警示**動作，其會定義警示規則的詳細資料，以及建立警示時要採取哪些動作。</span><span class="sxs-lookup"><span data-stu-id="a5a42-176">A schedule requires one **Alert** action which defines the details of the alert rule and what actions are taken when an alert is created.</span></span>  <span data-ttu-id="a5a42-177">如果必須從警示呼叫 Webhook，則它也可以包含 **Webhook** 動作。</span><span class="sxs-lookup"><span data-stu-id="a5a42-177">It may also include a **Webhook** action if a webhook should be called from the alert.</span></span>  

<span data-ttu-id="a5a42-178">動作資源具有 `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions` 類型。</span><span class="sxs-lookup"><span data-stu-id="a5a42-178">Action resources have a type of `Microsoft.OperationalInsights/workspaces/savedSearches/schedules/actions`.</span></span>  

#### <a name="alert-actions"></a><span data-ttu-id="a5a42-179">警示動作</span><span class="sxs-lookup"><span data-stu-id="a5a42-179">Alert actions</span></span>

<span data-ttu-id="a5a42-180">每個排程都會有一個**警示**動作。</span><span class="sxs-lookup"><span data-stu-id="a5a42-180">Every schedule will have one **Alert** action.</span></span>  <span data-ttu-id="a5a42-181">這會定義警示的詳細資料，以及選擇性地定義通知和修復動作的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a5a42-181">This defines the details of the alert and optionally notification and remediation actions.</span></span>  <span data-ttu-id="a5a42-182">通知會將電子郵件傳送到一或多個地址。</span><span class="sxs-lookup"><span data-stu-id="a5a42-182">A notification sends an email to one or more addresses.</span></span>  <span data-ttu-id="a5a42-183">修復會在 Azure 自動化中啟動 Runbook，以嘗試修復偵測到的問題。</span><span class="sxs-lookup"><span data-stu-id="a5a42-183">A remediation starts a runbook in Azure Automation to attempt to remediate the detected issue.</span></span>

<span data-ttu-id="a5a42-184">警示動作具備下列結構。</span><span class="sxs-lookup"><span data-stu-id="a5a42-184">Alert actions have the following structure.</span></span>  <span data-ttu-id="a5a42-185">這包括一般變數和參數，因此您可以將此程式碼片段複製並貼到您的解決方案檔，然後變更參數名稱。</span><span class="sxs-lookup"><span data-stu-id="a5a42-185">This includes common variables and parameters so that you can copy and paste this code snippet into your solution file and change the parameter names.</span></span> 



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

<span data-ttu-id="a5a42-186">下表會說明警示動作資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="a5a42-186">The properties for Alert action resources are described in the following tables.</span></span>

| <span data-ttu-id="a5a42-187">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a5a42-187">Element name</span></span> | <span data-ttu-id="a5a42-188">必要</span><span class="sxs-lookup"><span data-stu-id="a5a42-188">Required</span></span> | <span data-ttu-id="a5a42-189">說明</span><span class="sxs-lookup"><span data-stu-id="a5a42-189">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a5a42-190">類型</span><span class="sxs-lookup"><span data-stu-id="a5a42-190">Type</span></span> | <span data-ttu-id="a5a42-191">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-191">Yes</span></span> | <span data-ttu-id="a5a42-192">動作的類型。</span><span class="sxs-lookup"><span data-stu-id="a5a42-192">Type of the action.</span></span>  <span data-ttu-id="a5a42-193">這會是適用於警示動作的 **Alert**。</span><span class="sxs-lookup"><span data-stu-id="a5a42-193">This will be **Alert** for alert actions.</span></span> |
| <span data-ttu-id="a5a42-194">名稱</span><span class="sxs-lookup"><span data-stu-id="a5a42-194">Name</span></span> | <span data-ttu-id="a5a42-195">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-195">Yes</span></span> | <span data-ttu-id="a5a42-196">警示的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="a5a42-196">Display name for the alert.</span></span>  <span data-ttu-id="a5a42-197">這是顯示於主控台中的警示規則名稱。</span><span class="sxs-lookup"><span data-stu-id="a5a42-197">This is the name that's displayed in the console for the alert rule.</span></span> |
| <span data-ttu-id="a5a42-198">說明</span><span class="sxs-lookup"><span data-stu-id="a5a42-198">Description</span></span> | <span data-ttu-id="a5a42-199">否</span><span class="sxs-lookup"><span data-stu-id="a5a42-199">No</span></span> | <span data-ttu-id="a5a42-200">警示的選擇性描述。</span><span class="sxs-lookup"><span data-stu-id="a5a42-200">Optional description of the alert.</span></span> |
| <span data-ttu-id="a5a42-201">嚴重性</span><span class="sxs-lookup"><span data-stu-id="a5a42-201">Severity</span></span> | <span data-ttu-id="a5a42-202">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-202">Yes</span></span> | <span data-ttu-id="a5a42-203">警示記錄的嚴重性有下列值：</span><span class="sxs-lookup"><span data-stu-id="a5a42-203">Severity of the alert record from the following values:</span></span><br><br> <span data-ttu-id="a5a42-204">**Critical**</span><span class="sxs-lookup"><span data-stu-id="a5a42-204">**Critical**</span></span><br><span data-ttu-id="a5a42-205">**警告**</span><span class="sxs-lookup"><span data-stu-id="a5a42-205">**Warning**</span></span><br><span data-ttu-id="a5a42-206">**Informational**</span><span class="sxs-lookup"><span data-stu-id="a5a42-206">**Informational**</span></span> |


##### <a name="threshold"></a><span data-ttu-id="a5a42-207">閾值</span><span class="sxs-lookup"><span data-stu-id="a5a42-207">Threshold</span></span>
<span data-ttu-id="a5a42-208">此為必要區段。</span><span class="sxs-lookup"><span data-stu-id="a5a42-208">This section is required.</span></span>  <span data-ttu-id="a5a42-209">它會定義警示臨界值的屬性。</span><span class="sxs-lookup"><span data-stu-id="a5a42-209">It defines the properties for the alert threshold.</span></span>

| <span data-ttu-id="a5a42-210">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a5a42-210">Element name</span></span> | <span data-ttu-id="a5a42-211">必要</span><span class="sxs-lookup"><span data-stu-id="a5a42-211">Required</span></span> | <span data-ttu-id="a5a42-212">說明</span><span class="sxs-lookup"><span data-stu-id="a5a42-212">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a5a42-213">運算子</span><span class="sxs-lookup"><span data-stu-id="a5a42-213">Operator</span></span> | <span data-ttu-id="a5a42-214">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-214">Yes</span></span> | <span data-ttu-id="a5a42-215">比較運算子具有下列值：</span><span class="sxs-lookup"><span data-stu-id="a5a42-215">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="a5a42-216">**gt = 大於<br>lt = 少於**</span><span class="sxs-lookup"><span data-stu-id="a5a42-216">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="a5a42-217">值</span><span class="sxs-lookup"><span data-stu-id="a5a42-217">Value</span></span> | <span data-ttu-id="a5a42-218">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-218">Yes</span></span> | <span data-ttu-id="a5a42-219">要比較結果的值。</span><span class="sxs-lookup"><span data-stu-id="a5a42-219">The value to compare the results.</span></span> |


##### <a name="metricstrigger"></a><span data-ttu-id="a5a42-220">MetricsTrigger</span><span class="sxs-lookup"><span data-stu-id="a5a42-220">MetricsTrigger</span></span>
<span data-ttu-id="a5a42-221">此為選擇性區段。</span><span class="sxs-lookup"><span data-stu-id="a5a42-221">This section is optional.</span></span>  <span data-ttu-id="a5a42-222">加入此區段以供計量計量警示使用。</span><span class="sxs-lookup"><span data-stu-id="a5a42-222">Include it for a metric measurement alert.</span></span>

> [!NOTE]
> <span data-ttu-id="a5a42-223">計量測量警示目前是處於公開預覽狀態。</span><span class="sxs-lookup"><span data-stu-id="a5a42-223">Metric measurement alerts are currently in public preview.</span></span> 

| <span data-ttu-id="a5a42-224">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a5a42-224">Element name</span></span> | <span data-ttu-id="a5a42-225">必要</span><span class="sxs-lookup"><span data-stu-id="a5a42-225">Required</span></span> | <span data-ttu-id="a5a42-226">說明</span><span class="sxs-lookup"><span data-stu-id="a5a42-226">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a5a42-227">TriggerCondition</span><span class="sxs-lookup"><span data-stu-id="a5a42-227">TriggerCondition</span></span> | <span data-ttu-id="a5a42-228">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-228">Yes</span></span> | <span data-ttu-id="a5a42-229">使用下列值來指定臨界值為違反次數總和或連續違反次數：</span><span class="sxs-lookup"><span data-stu-id="a5a42-229">Specifies whether the threshold is for total number of breaches or consecutive breaches from the following values:</span></span><br><br><span data-ttu-id="a5a42-230">**Total<br>Consecutive**</span><span class="sxs-lookup"><span data-stu-id="a5a42-230">**Total<br>Consecutive**</span></span> |
| <span data-ttu-id="a5a42-231">運算子</span><span class="sxs-lookup"><span data-stu-id="a5a42-231">Operator</span></span> | <span data-ttu-id="a5a42-232">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-232">Yes</span></span> | <span data-ttu-id="a5a42-233">比較運算子具有下列值：</span><span class="sxs-lookup"><span data-stu-id="a5a42-233">Operator for the comparison from the following values:</span></span><br><br><span data-ttu-id="a5a42-234">**gt = 大於<br>lt = 少於**</span><span class="sxs-lookup"><span data-stu-id="a5a42-234">**gt = greater than<br>lt = less than**</span></span> |
| <span data-ttu-id="a5a42-235">值</span><span class="sxs-lookup"><span data-stu-id="a5a42-235">Value</span></span> | <span data-ttu-id="a5a42-236">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-236">Yes</span></span> | <span data-ttu-id="a5a42-237">必須符合準則以觸發警示的次數。</span><span class="sxs-lookup"><span data-stu-id="a5a42-237">Number of the times the criteria must be met to trigger the alert.</span></span> |

##### <a name="throttling"></a><span data-ttu-id="a5a42-238">節流</span><span class="sxs-lookup"><span data-stu-id="a5a42-238">Throttling</span></span>
<span data-ttu-id="a5a42-239">此為選擇性區段。</span><span class="sxs-lookup"><span data-stu-id="a5a42-239">This section is optional.</span></span>  <span data-ttu-id="a5a42-240">如果您想要在建立警示之後的某一段時間內隱藏相同規則所產生的警示，請加入此區段。</span><span class="sxs-lookup"><span data-stu-id="a5a42-240">Include this section if you want to suppress alerts from the same rule for some amount of time after an alert is created.</span></span>

| <span data-ttu-id="a5a42-241">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a5a42-241">Element name</span></span> | <span data-ttu-id="a5a42-242">必要</span><span class="sxs-lookup"><span data-stu-id="a5a42-242">Required</span></span> | <span data-ttu-id="a5a42-243">說明</span><span class="sxs-lookup"><span data-stu-id="a5a42-243">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a5a42-244">DurationInMinutes</span><span class="sxs-lookup"><span data-stu-id="a5a42-244">DurationInMinutes</span></span> | <span data-ttu-id="a5a42-245">如果包含 Throttling 元素，即為 Yes</span><span class="sxs-lookup"><span data-stu-id="a5a42-245">Yes if Throttling element included</span></span> | <span data-ttu-id="a5a42-246">從同一個警示規則中建立一個警示之後隱藏警示的分鐘數。</span><span class="sxs-lookup"><span data-stu-id="a5a42-246">Number of minutes to suppress alerts after one from the same alert rule is created.</span></span> |

##### <a name="emailnotification"></a><span data-ttu-id="a5a42-247">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="a5a42-247">EmailNotification</span></span>
 <span data-ttu-id="a5a42-248">此為選擇性區段  如果您想要警示將郵件傳送給一或多位收件者，請包含此區段。</span><span class="sxs-lookup"><span data-stu-id="a5a42-248">This section is optional  Include it if you want the alert to send mail to one or more recipients.</span></span>

| <span data-ttu-id="a5a42-249">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a5a42-249">Element name</span></span> | <span data-ttu-id="a5a42-250">必要</span><span class="sxs-lookup"><span data-stu-id="a5a42-250">Required</span></span> | <span data-ttu-id="a5a42-251">說明</span><span class="sxs-lookup"><span data-stu-id="a5a42-251">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a5a42-252">收件者</span><span class="sxs-lookup"><span data-stu-id="a5a42-252">Recipients</span></span> | <span data-ttu-id="a5a42-253">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-253">Yes</span></span> | <span data-ttu-id="a5a42-254">以逗號分隔的電子郵件地址清單，以便在建立警示時傳送通知，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="a5a42-254">Comma delimited list of email addresses to send notification when an alert is created such as in the following example.</span></span><br><br><span data-ttu-id="a5a42-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span><span class="sxs-lookup"><span data-stu-id="a5a42-255">**[ "recipient1@contoso.com", "recipient2@contoso.com" ]**</span></span> |
| <span data-ttu-id="a5a42-256">主旨</span><span class="sxs-lookup"><span data-stu-id="a5a42-256">Subject</span></span> | <span data-ttu-id="a5a42-257">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-257">Yes</span></span> | <span data-ttu-id="a5a42-258">郵件的主旨列。</span><span class="sxs-lookup"><span data-stu-id="a5a42-258">Subject line of the mail.</span></span> |
| <span data-ttu-id="a5a42-259">附件</span><span class="sxs-lookup"><span data-stu-id="a5a42-259">Attachment</span></span> | <span data-ttu-id="a5a42-260">否</span><span class="sxs-lookup"><span data-stu-id="a5a42-260">No</span></span> | <span data-ttu-id="a5a42-261">目前不支援附件。</span><span class="sxs-lookup"><span data-stu-id="a5a42-261">Attachments are not currently supported.</span></span>  <span data-ttu-id="a5a42-262">如果包含此元素，就應該是 **None**。</span><span class="sxs-lookup"><span data-stu-id="a5a42-262">If this element is included, it should be **None**.</span></span> |


##### <a name="remediation"></a><span data-ttu-id="a5a42-263">補救</span><span class="sxs-lookup"><span data-stu-id="a5a42-263">Remediation</span></span>
<span data-ttu-id="a5a42-264">此為選擇性區段  如果您想要讓 Runbook 啟動以回應警示，請包含此區段。</span><span class="sxs-lookup"><span data-stu-id="a5a42-264">This section is optional  Include it if you want a runbook to start in response to the alert.</span></span> |

| <span data-ttu-id="a5a42-265">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a5a42-265">Element name</span></span> | <span data-ttu-id="a5a42-266">必要</span><span class="sxs-lookup"><span data-stu-id="a5a42-266">Required</span></span> | <span data-ttu-id="a5a42-267">說明</span><span class="sxs-lookup"><span data-stu-id="a5a42-267">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a5a42-268">RunbookName</span><span class="sxs-lookup"><span data-stu-id="a5a42-268">RunbookName</span></span> | <span data-ttu-id="a5a42-269">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-269">Yes</span></span> | <span data-ttu-id="a5a42-270">要啟動的 Runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="a5a42-270">Name of the runbook to start.</span></span> |
| <span data-ttu-id="a5a42-271">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="a5a42-271">WebhookUri</span></span> | <span data-ttu-id="a5a42-272">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-272">Yes</span></span> | <span data-ttu-id="a5a42-273">Runbook 的 Webhook 的 Uri。</span><span class="sxs-lookup"><span data-stu-id="a5a42-273">Uri of the webhook for the runbook.</span></span> |
| <span data-ttu-id="a5a42-274">Expiry</span><span class="sxs-lookup"><span data-stu-id="a5a42-274">Expiry</span></span> | <span data-ttu-id="a5a42-275">否</span><span class="sxs-lookup"><span data-stu-id="a5a42-275">No</span></span> | <span data-ttu-id="a5a42-276">補救到期的日期和時間。</span><span class="sxs-lookup"><span data-stu-id="a5a42-276">Date and time that the remediation expires.</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="a5a42-277">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="a5a42-277">Webhook actions</span></span>

<span data-ttu-id="a5a42-278">Webhook 動作會呼叫 URL 並選擇性地提供要傳送的承載，以啟動處理序。</span><span class="sxs-lookup"><span data-stu-id="a5a42-278">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span> <span data-ttu-id="a5a42-279">這些動作類似於「補救」動作，不同之處在於它們用於可能叫用 Azure 自動化 Runbook 以外之處理序的 webhook。</span><span class="sxs-lookup"><span data-stu-id="a5a42-279">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span> <span data-ttu-id="a5a42-280">它們還提供另一個選項，可指定要傳遞到遠端處理序的承載。</span><span class="sxs-lookup"><span data-stu-id="a5a42-280">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="a5a42-281">如果您的警示會呼叫 webhook，則除了**警示**動作資源之外，還需要一種 **Webhook** 類型的動作資源。</span><span class="sxs-lookup"><span data-stu-id="a5a42-281">If your alert will call a webhook, then it will need an action resource with a type of **Webhook** in addition to the **Alert** action resource.</span></span>  

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

<span data-ttu-id="a5a42-282">下表會說明 Webhook 動作資源的屬性。</span><span class="sxs-lookup"><span data-stu-id="a5a42-282">The properties for Webhook action resources are described in the following tables.</span></span>

| <span data-ttu-id="a5a42-283">元素名稱</span><span class="sxs-lookup"><span data-stu-id="a5a42-283">Element name</span></span> | <span data-ttu-id="a5a42-284">必要</span><span class="sxs-lookup"><span data-stu-id="a5a42-284">Required</span></span> | <span data-ttu-id="a5a42-285">說明</span><span class="sxs-lookup"><span data-stu-id="a5a42-285">Description</span></span> |
|:--|:--|:--|
| <span data-ttu-id="a5a42-286">類型</span><span class="sxs-lookup"><span data-stu-id="a5a42-286">type</span></span> | <span data-ttu-id="a5a42-287">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-287">Yes</span></span> | <span data-ttu-id="a5a42-288">動作的類型。</span><span class="sxs-lookup"><span data-stu-id="a5a42-288">Type of the action.</span></span>  <span data-ttu-id="a5a42-289">這會是適用於 Webhook 動作的 **Webhook**。</span><span class="sxs-lookup"><span data-stu-id="a5a42-289">This will be **Webhook** for webhook actions.</span></span> |
| <span data-ttu-id="a5a42-290">名稱</span><span class="sxs-lookup"><span data-stu-id="a5a42-290">name</span></span> | <span data-ttu-id="a5a42-291">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-291">Yes</span></span> | <span data-ttu-id="a5a42-292">動作的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="a5a42-292">Display name for the action.</span></span>  <span data-ttu-id="a5a42-293">這不會顯示在主控台中。</span><span class="sxs-lookup"><span data-stu-id="a5a42-293">This is not displayed in the console.</span></span> |
| <span data-ttu-id="a5a42-294">wehookUri</span><span class="sxs-lookup"><span data-stu-id="a5a42-294">wehookUri</span></span> | <span data-ttu-id="a5a42-295">是</span><span class="sxs-lookup"><span data-stu-id="a5a42-295">Yes</span></span> | <span data-ttu-id="a5a42-296">Webhook 的 Uri。</span><span class="sxs-lookup"><span data-stu-id="a5a42-296">Uri for the webhook.</span></span> |
| <span data-ttu-id="a5a42-297">customPayload</span><span class="sxs-lookup"><span data-stu-id="a5a42-297">customPayload</span></span> | <span data-ttu-id="a5a42-298">否</span><span class="sxs-lookup"><span data-stu-id="a5a42-298">No</span></span> | <span data-ttu-id="a5a42-299">要傳送至 webhook 的自訂內容。</span><span class="sxs-lookup"><span data-stu-id="a5a42-299">Custom payload to be sent to the webhook.</span></span> <span data-ttu-id="a5a42-300">格式取決於 webhook 需要的內容。</span><span class="sxs-lookup"><span data-stu-id="a5a42-300">The format will depend on what the webhook is expecting.</span></span> |




## <a name="sample"></a><span data-ttu-id="a5a42-301">範例</span><span class="sxs-lookup"><span data-stu-id="a5a42-301">Sample</span></span>

<span data-ttu-id="a5a42-302">以下是解決方案的範例，其中包含下列資源：</span><span class="sxs-lookup"><span data-stu-id="a5a42-302">Following is a sample of a solution that include that includes the following resources:</span></span>

- <span data-ttu-id="a5a42-303">儲存的搜尋</span><span class="sxs-lookup"><span data-stu-id="a5a42-303">Saved search</span></span>
- <span data-ttu-id="a5a42-304">排程</span><span class="sxs-lookup"><span data-stu-id="a5a42-304">Schedule</span></span>
- <span data-ttu-id="a5a42-305">警示動作</span><span class="sxs-lookup"><span data-stu-id="a5a42-305">Alert action</span></span>
- <span data-ttu-id="a5a42-306">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="a5a42-306">Webhook action</span></span>

<span data-ttu-id="a5a42-307">此範例會使用[標準的解決方案參數](operations-management-suite-solutions-solution-file.md#parameters)變數，相對於資源定義中的硬式編碼值，這類變數常用於解決方案中。</span><span class="sxs-lookup"><span data-stu-id="a5a42-307">The sample uses [standard solution parameters](operations-management-suite-solutions-solution-file.md#parameters) variables that would commonly be used in a solution as opposed to hardcoding values in the resource definitions.</span></span>

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
              "Description": "List of recipients for the email alert separated by semicolon"
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


<span data-ttu-id="a5a42-308">下列參數檔會提供此解決方案的範例值。</span><span class="sxs-lookup"><span data-stu-id="a5a42-308">The following parameter file provides samples values for this solution.</span></span>

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


## <a name="next-steps"></a><span data-ttu-id="a5a42-309">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a5a42-309">Next steps</span></span>
* <span data-ttu-id="a5a42-310">在您的管理解決方案中[新增檢視](operations-management-suite-solutions-resources-views.md)。</span><span class="sxs-lookup"><span data-stu-id="a5a42-310">[Add views](operations-management-suite-solutions-resources-views.md) to your management solution.</span></span>
* <span data-ttu-id="a5a42-311">在您的管理解決方案中[新增自動化 Runbook 及其他資源](operations-management-suite-solutions-resources-automation.md)。</span><span class="sxs-lookup"><span data-stu-id="a5a42-311">[Add Automation runbooks and other resources](operations-management-suite-solutions-resources-automation.md) to your management solution.</span></span>

