---
title: "aaaUsing OMS 記錄分析警示 REST API"
description: "hello 記錄分析警示 REST API 可讓您 toocreate 和管理記錄分析是一部分的 Operations Management Suite (OMS) 中的警示。  本文章提供 hello API 和幾個範例的詳細資料，執行不同的作業。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="3d446-104">使用 REST API 在 Log Analytics 中建立及管理警示規則</span><span class="sxs-lookup"><span data-stu-id="3d446-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="3d446-105">hello 記錄分析警示 REST API 可讓您 toocreate 和管理警示在 Operations Management Suite (OMS)。</span><span class="sxs-lookup"><span data-stu-id="3d446-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="3d446-106">本文章提供 hello API 和幾個範例的詳細資料，執行不同的作業。</span><span class="sxs-lookup"><span data-stu-id="3d446-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="3d446-107">hello 記錄分析搜尋 REST API 是 RESTful，而且可以透過 hello Azure 資源管理員 REST API 存取。</span><span class="sxs-lookup"><span data-stu-id="3d446-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="3d446-108">本文件中您會發現範例 hello 應用程式開發介面透過 PowerShell 命令列使用[ARMClient](https://github.com/projectkudu/ARMClient)，簡化叫用的開放原始碼命令列工具 hello Azure 資源管理員 API。</span><span class="sxs-lookup"><span data-stu-id="3d446-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="3d446-109">hello 使用 ARMClient 和 PowerShell 是許多選項 tooaccess hello 記錄分析搜尋 API 的其中一個。</span><span class="sxs-lookup"><span data-stu-id="3d446-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="3d446-110">這些工具，您可以利用 hello RESTful Azure 資源管理員 API toomake 呼叫 tooOMS 工作區，以及它們在執行搜尋命令。</span><span class="sxs-lookup"><span data-stu-id="3d446-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="3d446-111">hello API 會輸出搜尋結果 tooyou JSON 格式，可讓您 toouse hello 搜尋結果中許多不同的方式以程式設計的方式。</span><span class="sxs-lookup"><span data-stu-id="3d446-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d446-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="3d446-112">Prerequisites</span></span>
<span data-ttu-id="3d446-113">目前，在 Log Analytics 中只能使用已儲存的搜尋來建立警示。</span><span class="sxs-lookup"><span data-stu-id="3d446-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="3d446-114">您可以使用參照 toohello[記錄搜尋 REST API](log-analytics-log-search-api.md)如需詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="3d446-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="3d446-115">排程</span><span class="sxs-lookup"><span data-stu-id="3d446-115">Schedules</span></span>
<span data-ttu-id="3d446-116">一個已儲存的搜尋可以有一或多個排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="3d446-117">hello 排程會定義 hello 搜尋執行的頻率，並識別哪一個準則，hello 透過 hello 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="3d446-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="3d446-118">排程 hello 下表中都有 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="3d446-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="3d446-119">屬性</span><span class="sxs-lookup"><span data-stu-id="3d446-119">Property</span></span> | <span data-ttu-id="3d446-120">說明</span><span class="sxs-lookup"><span data-stu-id="3d446-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d446-121">間隔</span><span class="sxs-lookup"><span data-stu-id="3d446-121">Interval</span></span> |<span data-ttu-id="3d446-122">Hello 搜尋是的執行頻率。</span><span class="sxs-lookup"><span data-stu-id="3d446-122">How often hello search is run.</span></span> <span data-ttu-id="3d446-123">以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="3d446-123">Measured in minutes.</span></span> |
| <span data-ttu-id="3d446-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="3d446-124">QueryTimeSpan</span></span> |<span data-ttu-id="3d446-125">哪些 hello 準則評估 hello 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="3d446-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="3d446-126">必須大於等於 tooor 間隔。</span><span class="sxs-lookup"><span data-stu-id="3d446-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="3d446-127">以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="3d446-127">Measured in minutes.</span></span> |
| <span data-ttu-id="3d446-128">版本</span><span class="sxs-lookup"><span data-stu-id="3d446-128">Version</span></span> |<span data-ttu-id="3d446-129">hello 所使用的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="3d446-129">hello API version being used.</span></span>  <span data-ttu-id="3d446-130">目前，這應一律設 too1。</span><span class="sxs-lookup"><span data-stu-id="3d446-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="3d446-131">例如，假設事件查詢的 Interval 是 15 分鐘，而 Timespan 是 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="3d446-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="3d446-132">在此情況下，hello 查詢會執行每隔 15 分鐘，且如果 hello 準則 tooresolve tootrue 透過在 30 分鐘的時間範圍，就會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="3d446-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="3d446-133">擷取排程</span><span class="sxs-lookup"><span data-stu-id="3d446-133">Retrieving schedules</span></span>
<span data-ttu-id="3d446-134">使用 hello 取得方法 tooretrieve 將已儲存搜尋的所有排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="3d446-135">使用 hello 取得排程識別碼 tooretrieve 方法將已儲存搜尋的特定排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="3d446-136">以下是排程的回應範例。</span><span class="sxs-lookup"><span data-stu-id="3d446-136">Following is a sample response for a schedule.</span></span>

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a><span data-ttu-id="3d446-137">建立排程</span><span class="sxs-lookup"><span data-stu-id="3d446-137">Creating a schedule</span></span>
<span data-ttu-id="3d446-138">使用新的排程的排程唯一識別碼 toocreate hello Put 方法。</span><span class="sxs-lookup"><span data-stu-id="3d446-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="3d446-139">請注意，兩個排程不能有 hello 相同識別碼即使它們與相關聯不同儲存的搜尋。</span><span class="sxs-lookup"><span data-stu-id="3d446-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="3d446-140">當您建立排程在 hello OMS 主控台中時，GUID 被建立 hello 排程識別碼。</span><span class="sxs-lookup"><span data-stu-id="3d446-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="3d446-141">所有已儲存的搜尋、 排程和動作以 hello 記錄分析 API 所建立的 hello 名稱必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="3d446-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="3d446-142">編輯排程</span><span class="sxs-lookup"><span data-stu-id="3d446-142">Editing a schedule</span></span>
<span data-ttu-id="3d446-143">使用現有的排程識別碼 hello 相同儲存搜尋排程的 toomodify hello Put 方法。</span><span class="sxs-lookup"><span data-stu-id="3d446-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="3d446-144">hello hello 要求主體必須包含 hello 排程 hello 的 etag。</span><span class="sxs-lookup"><span data-stu-id="3d446-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="3d446-145">刪除排程</span><span class="sxs-lookup"><span data-stu-id="3d446-145">Deleting schedules</span></span>
<span data-ttu-id="3d446-146">使用排程的排程識別碼 toodelete hello Delete 方法。</span><span class="sxs-lookup"><span data-stu-id="3d446-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="3d446-147">動作</span><span class="sxs-lookup"><span data-stu-id="3d446-147">Actions</span></span>
<span data-ttu-id="3d446-148">一個排程可以有多個動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="3d446-149">動作可以定義一個或多個處理程序 tooperform，例如傳送郵件，或啟動 runbook，或它可能會定義的臨界值會決定當 hello 搜尋的結果符合某些準則。</span><span class="sxs-lookup"><span data-stu-id="3d446-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="3d446-150">使 hello 處理程序將會符合 hello 臨界值時，某些動作會同時定義。</span><span class="sxs-lookup"><span data-stu-id="3d446-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="3d446-151">所有動作都有 hello 屬性 hello 下表中。</span><span class="sxs-lookup"><span data-stu-id="3d446-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="3d446-152">不同類型的警示有不同的其他屬性，如下所述。</span><span class="sxs-lookup"><span data-stu-id="3d446-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="3d446-153">屬性</span><span class="sxs-lookup"><span data-stu-id="3d446-153">Property</span></span> | <span data-ttu-id="3d446-154">說明</span><span class="sxs-lookup"><span data-stu-id="3d446-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d446-155">類型</span><span class="sxs-lookup"><span data-stu-id="3d446-155">Type</span></span> |<span data-ttu-id="3d446-156">Hello 動作的類型。</span><span class="sxs-lookup"><span data-stu-id="3d446-156">Type of hello action.</span></span>  <span data-ttu-id="3d446-157">目前 hello 可能的值已設定警示和 Webhook。</span><span class="sxs-lookup"><span data-stu-id="3d446-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="3d446-158">名稱</span><span class="sxs-lookup"><span data-stu-id="3d446-158">Name</span></span> |<span data-ttu-id="3d446-159">Hello 警示的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="3d446-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="3d446-160">版本</span><span class="sxs-lookup"><span data-stu-id="3d446-160">Version</span></span> |<span data-ttu-id="3d446-161">hello 所使用的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="3d446-161">hello API version being used.</span></span>  <span data-ttu-id="3d446-162">目前，這應一律設 too1。</span><span class="sxs-lookup"><span data-stu-id="3d446-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="3d446-163">擷取動作</span><span class="sxs-lookup"><span data-stu-id="3d446-163">Retrieving actions</span></span>
<span data-ttu-id="3d446-164">使用 hello 取得方法 tooretrieve 排程的所有動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="3d446-165">使用 hello 取得 hello 動作識別碼 tooretrieve 方法排程的特定動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="3d446-166">建立或編輯動作</span><span class="sxs-lookup"><span data-stu-id="3d446-166">Creating or editing actions</span></span>
<span data-ttu-id="3d446-167">使用唯一 toohello 排程 toocreate 新動作的動作識別碼 hello Put 方法。</span><span class="sxs-lookup"><span data-stu-id="3d446-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="3d446-168">當您建立動作 hello OMS 主控台中時，GUID 是 hello 動作識別碼。</span><span class="sxs-lookup"><span data-stu-id="3d446-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="3d446-169">所有已儲存的搜尋、 排程和動作以 hello 記錄分析 API 所建立的 hello 名稱必須是小寫。</span><span class="sxs-lookup"><span data-stu-id="3d446-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="3d446-170">使用現有的動作識別碼 hello 相同儲存搜尋排程的 toomodify hello Put 方法。</span><span class="sxs-lookup"><span data-stu-id="3d446-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="3d446-171">hello hello 要求主體必須包含 hello 排程 hello 的 etag。</span><span class="sxs-lookup"><span data-stu-id="3d446-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="3d446-172">hello 要求格式來建立新的動作會因動作類型，因此 hello 的以下各節會提供這些範例。</span><span class="sxs-lookup"><span data-stu-id="3d446-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="3d446-173">刪除動作</span><span class="sxs-lookup"><span data-stu-id="3d446-173">Deleting actions</span></span>
<span data-ttu-id="3d446-174">使用 hello 動作識別碼 toodelete 動作 hello Delete 方法。</span><span class="sxs-lookup"><span data-stu-id="3d446-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="3d446-175">警示動作</span><span class="sxs-lookup"><span data-stu-id="3d446-175">Alert Actions</span></span>
<span data-ttu-id="3d446-176">一個排程應該只有一個警示動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="3d446-177">警示的動作都有一或多個 hello 下表中的 hello 區段。</span><span class="sxs-lookup"><span data-stu-id="3d446-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="3d446-178">以下進一步詳細說明每一個區段。</span><span class="sxs-lookup"><span data-stu-id="3d446-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="3d446-179">區段</span><span class="sxs-lookup"><span data-stu-id="3d446-179">Section</span></span> | <span data-ttu-id="3d446-180">說明</span><span class="sxs-lookup"><span data-stu-id="3d446-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d446-181">閾值</span><span class="sxs-lookup"><span data-stu-id="3d446-181">Threshold</span></span> |<span data-ttu-id="3d446-182">Hello 動作執行時的準則。</span><span class="sxs-lookup"><span data-stu-id="3d446-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="3d446-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="3d446-183">EmailNotification</span></span> |<span data-ttu-id="3d446-184">傳送郵件 toomultiple 收件者。</span><span class="sxs-lookup"><span data-stu-id="3d446-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="3d446-185">補救</span><span class="sxs-lookup"><span data-stu-id="3d446-185">Remediation</span></span> |<span data-ttu-id="3d446-186">在 Azure 自動化 tooattempt toocorrect 識別問題中啟動 runbook。</span><span class="sxs-lookup"><span data-stu-id="3d446-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="3d446-187">臨界值</span><span class="sxs-lookup"><span data-stu-id="3d446-187">Thresholds</span></span>
<span data-ttu-id="3d446-188">一個警示動作應該只有一個臨界值。</span><span class="sxs-lookup"><span data-stu-id="3d446-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="3d446-189">當儲存搜尋的 hello 結果符合 hello 臨界值中搜尋相關聯的動作時，會執行該動作中的任何其他處理序。</span><span class="sxs-lookup"><span data-stu-id="3d446-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="3d446-190">動作也可以只包含臨界值，以便與不包含臨界值的其他類型動作一起搭配使用。</span><span class="sxs-lookup"><span data-stu-id="3d446-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="3d446-191">臨界值 hello 下表中都有 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="3d446-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="3d446-192">屬性</span><span class="sxs-lookup"><span data-stu-id="3d446-192">Property</span></span> | <span data-ttu-id="3d446-193">說明</span><span class="sxs-lookup"><span data-stu-id="3d446-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d446-194">運算子</span><span class="sxs-lookup"><span data-stu-id="3d446-194">Operator</span></span> |<span data-ttu-id="3d446-195">Hello 臨界值比較運算子。</span><span class="sxs-lookup"><span data-stu-id="3d446-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="3d446-196">gt = 大於</span><span class="sxs-lookup"><span data-stu-id="3d446-196">gt = Greater Than</span></span> <br> <span data-ttu-id="3d446-197">lt = 小於</span><span class="sxs-lookup"><span data-stu-id="3d446-197">lt = Less Than</span></span> |
| <span data-ttu-id="3d446-198">值</span><span class="sxs-lookup"><span data-stu-id="3d446-198">Value</span></span> |<span data-ttu-id="3d446-199">Hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="3d446-199">Value for hello threshold.</span></span> |

<span data-ttu-id="3d446-200">例如，假設事件查詢的間隔是 15 分鐘、時間範圍是 30 分鐘，而臨界值大於 10。</span><span class="sxs-lookup"><span data-stu-id="3d446-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="3d446-201">在此情況下，hello 執行查詢，會每隔 15 分鐘，並會觸發警示，如果它傳回 10 個透過在 30 分鐘的時間範圍所建立的事件。</span><span class="sxs-lookup"><span data-stu-id="3d446-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="3d446-202">以下是一個只包含臨界值的動作的回應範例。</span><span class="sxs-lookup"><span data-stu-id="3d446-202">Following is a sample response for an action with only a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

<span data-ttu-id="3d446-203">使用唯一的動作識別碼 toocreate 新臨界值的動作的 hello Put 方法的排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="3d446-204">使用現有的動作識別碼 toomodify 閾值動作的 hello Put 方法排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="3d446-205">hello hello 要求主體必須包含 hello etag 的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="3d446-206">電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="3d446-206">Email Notification</span></span>
<span data-ttu-id="3d446-207">電子郵件通知傳送郵件 tooone 或多個收件者。</span><span class="sxs-lookup"><span data-stu-id="3d446-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="3d446-208">其中包含下表中的 hello hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="3d446-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="3d446-209">屬性</span><span class="sxs-lookup"><span data-stu-id="3d446-209">Property</span></span> | <span data-ttu-id="3d446-210">說明</span><span class="sxs-lookup"><span data-stu-id="3d446-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d446-211">收件者</span><span class="sxs-lookup"><span data-stu-id="3d446-211">Recipients</span></span> |<span data-ttu-id="3d446-212">郵件地址清單。</span><span class="sxs-lookup"><span data-stu-id="3d446-212">List of mail addresses.</span></span> |
| <span data-ttu-id="3d446-213">主旨</span><span class="sxs-lookup"><span data-stu-id="3d446-213">Subject</span></span> |<span data-ttu-id="3d446-214">hello hello 郵件主旨。</span><span class="sxs-lookup"><span data-stu-id="3d446-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="3d446-215">附件</span><span class="sxs-lookup"><span data-stu-id="3d446-215">Attachment</span></span> |<span data-ttu-id="3d446-216">目前不支援附件，這個值永遠為 “None”。</span><span class="sxs-lookup"><span data-stu-id="3d446-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="3d446-217">以下是一個包含臨界值的電子郵件通知動作的回應範例。</span><span class="sxs-lookup"><span data-stu-id="3d446-217">Following is a sample response for an email notification action with a threshold.</span></span>  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="3d446-218">使用唯一的動作識別碼 toocreate 新的電子郵件動作的 hello Put 方法的排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="3d446-219">hello 下列範例會建立電子郵件通知與臨界值讓 hello hello 已儲存的搜尋結果超過 hello 臨界值時，會傳送 hello 郵件。</span><span class="sxs-lookup"><span data-stu-id="3d446-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="3d446-220">使用現有的動作識別碼 toomodify 電子郵件動作的 hello Put 方法的排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="3d446-221">hello hello 要求主體必須包含 hello etag 的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="3d446-222">補救動作</span><span class="sxs-lookup"><span data-stu-id="3d446-222">Remediation actions</span></span>
<span data-ttu-id="3d446-223">修復會嘗試識別 hello 警示 toocorrect hello 問題的 Azure 自動化中啟動 runbook。</span><span class="sxs-lookup"><span data-stu-id="3d446-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="3d446-224">您必須建立 webhook hello runbook 使用的修復動作，然後 hello URI hello WebhookUri 屬性中。</span><span class="sxs-lookup"><span data-stu-id="3d446-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="3d446-225">當您建立使用 hello OMS 主控台，此動作時，hello runbook 自動建立新的 webhook。</span><span class="sxs-lookup"><span data-stu-id="3d446-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="3d446-226">補救 hello 下表中包含 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="3d446-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="3d446-227">屬性</span><span class="sxs-lookup"><span data-stu-id="3d446-227">Property</span></span> | <span data-ttu-id="3d446-228">說明</span><span class="sxs-lookup"><span data-stu-id="3d446-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d446-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="3d446-229">RunbookName</span></span> |<span data-ttu-id="3d446-230">Hello runbook 名稱。</span><span class="sxs-lookup"><span data-stu-id="3d446-230">Name of hello runbook.</span></span> <span data-ttu-id="3d446-231">這必須符合設定 hello OMS 工作區中的自動化方案中的 hello 自動化帳戶中已發佈的 runbook。</span><span class="sxs-lookup"><span data-stu-id="3d446-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="3d446-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="3d446-232">WebhookUri</span></span> |<span data-ttu-id="3d446-233">Hello webhook 的 URI。</span><span class="sxs-lookup"><span data-stu-id="3d446-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="3d446-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="3d446-234">Expiry</span></span> |<span data-ttu-id="3d446-235">hello 到期日期和時間的 hello webhook。</span><span class="sxs-lookup"><span data-stu-id="3d446-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="3d446-236">如果 hello webhook 沒有到期日，這可以是任何有效的未來日期。</span><span class="sxs-lookup"><span data-stu-id="3d446-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="3d446-237">以下是一個包含臨界值的補救動作的回應範例。</span><span class="sxs-lookup"><span data-stu-id="3d446-237">Following is a sample response for a remediation action with a threshold.</span></span>

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

<span data-ttu-id="3d446-238">使用唯一的動作識別碼 toocreate 新的補救動作的 hello Put 方法的排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="3d446-239">hello 下列範例會建立修復與臨界值讓 hello runbook 在啟動時的儲存搜尋的 hello hello 結果超過 hello 臨界值。</span><span class="sxs-lookup"><span data-stu-id="3d446-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="3d446-240">使用現有的動作識別碼 toomodify 的修復動作的 hello Put 方法的排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="3d446-241">hello hello 要求主體必須包含 hello etag 的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="3d446-242">範例</span><span class="sxs-lookup"><span data-stu-id="3d446-242">Example</span></span>
<span data-ttu-id="3d446-243">以下是完整的範例 toocreate 新的電子郵件警示。</span><span class="sxs-lookup"><span data-stu-id="3d446-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="3d446-244">這會建立新的排程及一個包含臨界值和電子郵件的動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="3d446-245">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="3d446-245">Webhook actions</span></span>
<span data-ttu-id="3d446-246">Webhook 動作開始的程序呼叫的 URL，同時選擇性提供裝載 toobe 傳送。</span><span class="sxs-lookup"><span data-stu-id="3d446-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="3d446-247">它們是類似 tooRemediation 動作，但它們一定會用於可以叫用非 Azure 自動化 runbook 的程序的 webhook。</span><span class="sxs-lookup"><span data-stu-id="3d446-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="3d446-248">它們也提供其他選項可 hello 提供裝載 toobe 傳遞 toohello 遠端處理序。</span><span class="sxs-lookup"><span data-stu-id="3d446-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="3d446-249">Webhook 動作沒有臨界值，但應該改為加入 tooa 排程，其與臨界值警示動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="3d446-250">您可以新增將會執行所有符合 hello 臨界值時的多個 Webhook 動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="3d446-251">Webhook 動作會併入 hello 下表中的 hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="3d446-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="3d446-252">屬性</span><span class="sxs-lookup"><span data-stu-id="3d446-252">Property</span></span> | <span data-ttu-id="3d446-253">說明</span><span class="sxs-lookup"><span data-stu-id="3d446-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="3d446-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="3d446-254">WebhookUri</span></span> |<span data-ttu-id="3d446-255">hello hello 郵件主旨。</span><span class="sxs-lookup"><span data-stu-id="3d446-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="3d446-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="3d446-256">CustomPayload</span></span> |<span data-ttu-id="3d446-257">自訂承載 toobe 傳送 toohello webhook。</span><span class="sxs-lookup"><span data-stu-id="3d446-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="3d446-258">hello 格式將取決於哪些 hello webhook 所預期。</span><span class="sxs-lookup"><span data-stu-id="3d446-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="3d446-259">以下是 webhook 動作及一個包含臨界值的相關聯警示動作的回應範例。</span><span class="sxs-lookup"><span data-stu-id="3d446-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="3d446-260">建立或編輯 webhook 動作</span><span class="sxs-lookup"><span data-stu-id="3d446-260">Create or edit a webhook action</span></span>
<span data-ttu-id="3d446-261">使用唯一的動作識別碼 toocreate 新 webhook 動作的 hello Put 方法的排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="3d446-262">hello 下列範例會建立 Webhook 動作和警示的動作與臨界值，以便 hello hello 已儲存的搜尋結果超過 hello 臨界值時，將會觸發 hello webhook。</span><span class="sxs-lookup"><span data-stu-id="3d446-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="3d446-263">使用現有的動作識別碼 toomodify webhook 動作的 hello Put 方法的排程。</span><span class="sxs-lookup"><span data-stu-id="3d446-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="3d446-264">hello hello 要求主體必須包含 hello etag 的 hello 動作。</span><span class="sxs-lookup"><span data-stu-id="3d446-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="3d446-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d446-265">Next steps</span></span>
* <span data-ttu-id="3d446-266">使用 hello [REST API tooperform 記錄搜尋](log-analytics-log-search-api.md)記錄分析中。</span><span class="sxs-lookup"><span data-stu-id="3d446-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

