---
title: "使用 OMS Log Analytics 警示 REST API"
description: "Log Analytics 警示 REST API 可讓您在 Log Analytics (其為 Operations Management Suite (OMS) 的一部分) 中建立及管理警示。  本文提供此 API 的詳細資料和幾個執行不同作業的範例。"
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
ms.openlocfilehash: 5ce72ffef4394bf3bbe39fa420c4fcaa965ae35c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="1d184-104">使用 REST API 在 Log Analytics 中建立及管理警示規則</span><span class="sxs-lookup"><span data-stu-id="1d184-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="1d184-105">Log Analytics 警示 REST API 可讓您在 Operations Management Suite (OMS) 中建立及管理警示。</span><span class="sxs-lookup"><span data-stu-id="1d184-105">The Log Analytics Alert REST API allows you to create and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="1d184-106">本文提供此 API 的詳細資料和幾個執行不同作業的範例。</span><span class="sxs-lookup"><span data-stu-id="1d184-106">This article provides details of the API and several examples for performing different operations.</span></span>

<span data-ttu-id="1d184-107">Log Analytics 搜尋 API 是 RESTful，可透過 Azure Resource Manager REST API 來存取。</span><span class="sxs-lookup"><span data-stu-id="1d184-107">The Log Analytics Search REST API is RESTful and can be accessed via the Azure Resource Manager REST API.</span></span> <span data-ttu-id="1d184-108">在這份文件中，您可以找到透過 [ARMClient](https://github.com/projectkudu/ARMClient) 從 PowerShell 命令列存取 API 的範例，這是一個開放原始碼命令列工具，可簡化叫用 Azure Resource Manager API。</span><span class="sxs-lookup"><span data-stu-id="1d184-108">In this document you will find examples where the API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking the Azure Resource Manager API.</span></span> <span data-ttu-id="1d184-109">使用 ARMClient 和 PowerShell 是存取 Log Analytics 搜尋 API 的許多選項之一。</span><span class="sxs-lookup"><span data-stu-id="1d184-109">The use of ARMClient and PowerShell is one of many options to access the Log Analytics Search API.</span></span> <span data-ttu-id="1d184-110">透過這些工具，您可以利用 RESTful Azure Resource Manager API 呼叫 OMS 工作區並在其中執行搜尋命令。</span><span class="sxs-lookup"><span data-stu-id="1d184-110">With these tools you can utilize the RESTful Azure Resource Manager API to make calls to OMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="1d184-111">API 會以 JSON 格式向您輸出搜尋結果，讓您以程式設計方式透過許多不同的方法使用搜尋結果。</span><span class="sxs-lookup"><span data-stu-id="1d184-111">The API will output search results to you in JSON format, allowing you to use the search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1d184-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="1d184-112">Prerequisites</span></span>
<span data-ttu-id="1d184-113">目前，在 Log Analytics 中只能使用已儲存的搜尋來建立警示。</span><span class="sxs-lookup"><span data-stu-id="1d184-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="1d184-114">如需詳細資訊，請參閱 [記錄檔搜尋 REST API](log-analytics-log-search-api.md) 。</span><span class="sxs-lookup"><span data-stu-id="1d184-114">You can refer to the [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="1d184-115">排程</span><span class="sxs-lookup"><span data-stu-id="1d184-115">Schedules</span></span>
<span data-ttu-id="1d184-116">一個已儲存的搜尋可以有一或多個排程。</span><span class="sxs-lookup"><span data-stu-id="1d184-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="1d184-117">排程中定義搜尋的執行頻率及識別準則的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="1d184-117">The schedule defines how often the search is run and the time interval over which the criteria is identified.</span></span>
<span data-ttu-id="1d184-118">排程具有下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="1d184-118">Schedules have the properties in the following table.</span></span>

| <span data-ttu-id="1d184-119">屬性</span><span class="sxs-lookup"><span data-stu-id="1d184-119">Property</span></span> | <span data-ttu-id="1d184-120">說明</span><span class="sxs-lookup"><span data-stu-id="1d184-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d184-121">間隔</span><span class="sxs-lookup"><span data-stu-id="1d184-121">Interval</span></span> |<span data-ttu-id="1d184-122">執行搜尋的頻率。</span><span class="sxs-lookup"><span data-stu-id="1d184-122">How often the search is run.</span></span> <span data-ttu-id="1d184-123">以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="1d184-123">Measured in minutes.</span></span> |
| <span data-ttu-id="1d184-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="1d184-124">QueryTimeSpan</span></span> |<span data-ttu-id="1d184-125">準則評估的時間間隔。</span><span class="sxs-lookup"><span data-stu-id="1d184-125">The time interval over which the criteria is evaluated.</span></span> <span data-ttu-id="1d184-126">必須等於或大於 Interval。</span><span class="sxs-lookup"><span data-stu-id="1d184-126">Must be equal to or greater than Interval.</span></span> <span data-ttu-id="1d184-127">以分鐘為單位。</span><span class="sxs-lookup"><span data-stu-id="1d184-127">Measured in minutes.</span></span> |
| <span data-ttu-id="1d184-128">版本</span><span class="sxs-lookup"><span data-stu-id="1d184-128">Version</span></span> |<span data-ttu-id="1d184-129">所使用的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="1d184-129">The API version being used.</span></span>  <span data-ttu-id="1d184-130">目前，這應該一律設為 1。</span><span class="sxs-lookup"><span data-stu-id="1d184-130">Currently, this should always be set to 1.</span></span> |

<span data-ttu-id="1d184-131">例如，假設事件查詢的 Interval 是 15 分鐘，而 Timespan 是 30 分鐘。</span><span class="sxs-lookup"><span data-stu-id="1d184-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="1d184-132">在此例子中，每隔 15 分鐘會執行查詢，如果準則在 30 分鐘內連續評估為 true，則會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="1d184-132">In this case, the query would be run every 15 minutes, and an alert would be triggered if the criteria continued to resolve to true over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="1d184-133">擷取排程</span><span class="sxs-lookup"><span data-stu-id="1d184-133">Retrieving schedules</span></span>
<span data-ttu-id="1d184-134">使用 Get 方法來擷取已儲存的搜尋的所有排程。</span><span class="sxs-lookup"><span data-stu-id="1d184-134">Use the Get method to retrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="1d184-135">使用 Get 方法並指定排程識別碼，以擷取已儲存的搜尋的特定排程。</span><span class="sxs-lookup"><span data-stu-id="1d184-135">Use the Get method with a schedule ID to retrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="1d184-136">以下是排程的回應範例。</span><span class="sxs-lookup"><span data-stu-id="1d184-136">Following is a sample response for a schedule.</span></span>

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

### <a name="creating-a-schedule"></a><span data-ttu-id="1d184-137">建立排程</span><span class="sxs-lookup"><span data-stu-id="1d184-137">Creating a schedule</span></span>
<span data-ttu-id="1d184-138">使用 Put 方法並指定唯一的排程識別碼，以建立新的排程。</span><span class="sxs-lookup"><span data-stu-id="1d184-138">Use the Put method with a unique schedule ID to create a new schedule.</span></span>  <span data-ttu-id="1d184-139">請注意，兩個排程即使其已儲存的相關聯搜尋不同，也不能有相同的識別碼。</span><span class="sxs-lookup"><span data-stu-id="1d184-139">Note that two schedules cannot have the same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="1d184-140">當您在 OMS 主控台中建立排程時，將會建立 GUID 做為排程識別碼。</span><span class="sxs-lookup"><span data-stu-id="1d184-140">When you create a schedule in the OMS console, a GUID is created for the schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="1d184-141">Log Analytics API 所建立並儲存的所有搜尋、排程和動作，都必須使用小寫名稱。</span><span class="sxs-lookup"><span data-stu-id="1d184-141">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="1d184-142">編輯排程</span><span class="sxs-lookup"><span data-stu-id="1d184-142">Editing a schedule</span></span>
<span data-ttu-id="1d184-143">針對已儲存的相同搜尋，使用 Put 方法並指定現有的排程識別碼，以修改該排程。</span><span class="sxs-lookup"><span data-stu-id="1d184-143">Use the Put method with an existing schedule ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="1d184-144">要求的主體必須包含排程的 etag。</span><span class="sxs-lookup"><span data-stu-id="1d184-144">The body of the request must include the etag of the schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="1d184-145">刪除排程</span><span class="sxs-lookup"><span data-stu-id="1d184-145">Deleting schedules</span></span>
<span data-ttu-id="1d184-146">使用 Delete 方法並指定排程識別碼來刪除排程。</span><span class="sxs-lookup"><span data-stu-id="1d184-146">Use the Delete method with a schedule ID to delete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="1d184-147">動作</span><span class="sxs-lookup"><span data-stu-id="1d184-147">Actions</span></span>
<span data-ttu-id="1d184-148">一個排程可以有多個動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="1d184-149">一個動作可能定義一或多個處理序來執行，例如傳送郵件或啟動 Runbook，或也可能定義臨界值來判斷搜尋結果是否符合某些準則。</span><span class="sxs-lookup"><span data-stu-id="1d184-149">An action may define one or more processes to perform such as sending a mail or starting a runbook, or it may define a threshold that determines when the results of a search match some criteria.</span></span>  <span data-ttu-id="1d184-150">某些動作會同時定義這兩者，以便符合臨界值時執行處理序。</span><span class="sxs-lookup"><span data-stu-id="1d184-150">Some actions will define both so that the processes are performed when the threshold is met.</span></span>

<span data-ttu-id="1d184-151">所有動作具有下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="1d184-151">All actions have the properties in the following table.</span></span>  <span data-ttu-id="1d184-152">不同類型的警示有不同的其他屬性，如下所述。</span><span class="sxs-lookup"><span data-stu-id="1d184-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="1d184-153">屬性</span><span class="sxs-lookup"><span data-stu-id="1d184-153">Property</span></span> | <span data-ttu-id="1d184-154">說明</span><span class="sxs-lookup"><span data-stu-id="1d184-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d184-155">類型</span><span class="sxs-lookup"><span data-stu-id="1d184-155">Type</span></span> |<span data-ttu-id="1d184-156">動作的類型。</span><span class="sxs-lookup"><span data-stu-id="1d184-156">Type of the action.</span></span>  <span data-ttu-id="1d184-157">目前可能的值為 Alert 和 Webhook。</span><span class="sxs-lookup"><span data-stu-id="1d184-157">Currently the possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="1d184-158">名稱</span><span class="sxs-lookup"><span data-stu-id="1d184-158">Name</span></span> |<span data-ttu-id="1d184-159">警示的顯示名稱。</span><span class="sxs-lookup"><span data-stu-id="1d184-159">Display name for the alert.</span></span> |
| <span data-ttu-id="1d184-160">版本</span><span class="sxs-lookup"><span data-stu-id="1d184-160">Version</span></span> |<span data-ttu-id="1d184-161">所使用的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="1d184-161">The API version being used.</span></span>  <span data-ttu-id="1d184-162">目前，這應該一律設為 1。</span><span class="sxs-lookup"><span data-stu-id="1d184-162">Currently, this should always be set to 1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="1d184-163">擷取動作</span><span class="sxs-lookup"><span data-stu-id="1d184-163">Retrieving actions</span></span>
<span data-ttu-id="1d184-164">使用 Get 方法來擷取排程的所有動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-164">Use the Get method to retrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="1d184-165">使用 Put 方法並指定動作識別碼，擷取排程的特定動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-165">Use the Get method with the action ID to retrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="1d184-166">建立或編輯動作</span><span class="sxs-lookup"><span data-stu-id="1d184-166">Creating or editing actions</span></span>
<span data-ttu-id="1d184-167">使用 Put 方法並指定排程特有的動作識別碼，以建立新的動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-167">Use the Put method with an action ID that is unique to the schedule to create a new action.</span></span>  <span data-ttu-id="1d184-168">當您在 OMS 主控台中建立動作時，動作識別碼會使用 GUID。</span><span class="sxs-lookup"><span data-stu-id="1d184-168">When you create an action in the OMS console, a GUID is for the action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="1d184-169">Log Analytics API 所建立並儲存的所有搜尋、排程和動作，都必須使用小寫名稱。</span><span class="sxs-lookup"><span data-stu-id="1d184-169">The name for all saved searches, schedules, and actions created with the Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="1d184-170">針對已儲存的相同搜尋，使用 Put 方法並指定現有的動作識別碼，以修改該排程。</span><span class="sxs-lookup"><span data-stu-id="1d184-170">Use the Put method with an existing action ID for the same saved search to modify that schedule.</span></span>  <span data-ttu-id="1d184-171">要求的主體必須包含排程的 etag。</span><span class="sxs-lookup"><span data-stu-id="1d184-171">The body of the request must include the etag of the schedule.</span></span>

<span data-ttu-id="1d184-172">建立新動作的要求格式依動作類型而不同，下列各節提供這些範例。</span><span class="sxs-lookup"><span data-stu-id="1d184-172">The request format for creating a new action varies by action type so these examples are provided in the sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="1d184-173">刪除動作</span><span class="sxs-lookup"><span data-stu-id="1d184-173">Deleting actions</span></span>
<span data-ttu-id="1d184-174">使用 Delete 方法並指定動作識別碼來刪除動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-174">Use the Delete method with the action ID to delete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="1d184-175">警示動作</span><span class="sxs-lookup"><span data-stu-id="1d184-175">Alert Actions</span></span>
<span data-ttu-id="1d184-176">一個排程應該只有一個警示動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="1d184-177">警示動作具有下表中的一或多個區段。</span><span class="sxs-lookup"><span data-stu-id="1d184-177">Alert actions have one or more of the sections in the following table.</span></span>  <span data-ttu-id="1d184-178">以下進一步詳細說明每一個區段。</span><span class="sxs-lookup"><span data-stu-id="1d184-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="1d184-179">區段</span><span class="sxs-lookup"><span data-stu-id="1d184-179">Section</span></span> | <span data-ttu-id="1d184-180">說明</span><span class="sxs-lookup"><span data-stu-id="1d184-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d184-181">閾值</span><span class="sxs-lookup"><span data-stu-id="1d184-181">Threshold</span></span> |<span data-ttu-id="1d184-182">執行動作的準則。</span><span class="sxs-lookup"><span data-stu-id="1d184-182">Criteria for when the action is run.</span></span> |
| <span data-ttu-id="1d184-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="1d184-183">EmailNotification</span></span> |<span data-ttu-id="1d184-184">將郵件傳送給多位收件者。</span><span class="sxs-lookup"><span data-stu-id="1d184-184">Send mail to multiple recipients.</span></span> |
| <span data-ttu-id="1d184-185">補救</span><span class="sxs-lookup"><span data-stu-id="1d184-185">Remediation</span></span> |<span data-ttu-id="1d184-186">在 Azure 自動化中啟動 Runbook，以嘗試更正識別的問題。</span><span class="sxs-lookup"><span data-stu-id="1d184-186">Start a runbook in Azure Automation to attempt to correct identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="1d184-187">臨界值</span><span class="sxs-lookup"><span data-stu-id="1d184-187">Thresholds</span></span>
<span data-ttu-id="1d184-188">一個警示動作應該只有一個臨界值。</span><span class="sxs-lookup"><span data-stu-id="1d184-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="1d184-189">當已儲存的搜尋結果符合與該搜尋相關聯動作中的臨界值時，將會執行該動作中的任何其他處理序。</span><span class="sxs-lookup"><span data-stu-id="1d184-189">When the results of a saved search match the threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="1d184-190">動作也可以只包含臨界值，以便與不包含臨界值的其他類型動作一起搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1d184-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="1d184-191">臨界值具有下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="1d184-191">Thresholds have the properties in the following table.</span></span>

| <span data-ttu-id="1d184-192">屬性</span><span class="sxs-lookup"><span data-stu-id="1d184-192">Property</span></span> | <span data-ttu-id="1d184-193">說明</span><span class="sxs-lookup"><span data-stu-id="1d184-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d184-194">運算子</span><span class="sxs-lookup"><span data-stu-id="1d184-194">Operator</span></span> |<span data-ttu-id="1d184-195">用於比較臨界值的運算子。</span><span class="sxs-lookup"><span data-stu-id="1d184-195">Operator for the threshold comparison.</span></span> <br> <span data-ttu-id="1d184-196">gt = 大於</span><span class="sxs-lookup"><span data-stu-id="1d184-196">gt = Greater Than</span></span> <br> <span data-ttu-id="1d184-197">lt = 小於</span><span class="sxs-lookup"><span data-stu-id="1d184-197">lt = Less Than</span></span> |
| <span data-ttu-id="1d184-198">值</span><span class="sxs-lookup"><span data-stu-id="1d184-198">Value</span></span> |<span data-ttu-id="1d184-199">臨界值。</span><span class="sxs-lookup"><span data-stu-id="1d184-199">Value for the threshold.</span></span> |

<span data-ttu-id="1d184-200">例如，假設事件查詢的間隔是 15 分鐘、時間範圍是 30 分鐘，而臨界值大於 10。</span><span class="sxs-lookup"><span data-stu-id="1d184-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="1d184-201">在此例子中，每隔 15 分鐘會執行查詢，如果傳回在 30 分鐘內建立的 10 個事件，則會觸發警示。</span><span class="sxs-lookup"><span data-stu-id="1d184-201">In this case, the query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="1d184-202">以下是一個只包含臨界值的動作的回應範例。</span><span class="sxs-lookup"><span data-stu-id="1d184-202">Following is a sample response for an action with only a threshold.</span></span>  

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

<span data-ttu-id="1d184-203">使用 Put 方法並指定唯一的動作識別碼，以建立排程的新臨界值動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-203">Use the Put method with a unique action ID to create a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="1d184-204">使用 Put 方法並指定現有的動作識別碼，以修改排程的臨界值動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-204">Use the Put method with an existing action ID to modify a threshold action for a schedule.</span></span>  <span data-ttu-id="1d184-205">要求的主體必須包含動作的 etag。</span><span class="sxs-lookup"><span data-stu-id="1d184-205">The body of the request must include the etag of the action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="1d184-206">電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="1d184-206">Email Notification</span></span>
<span data-ttu-id="1d184-207">「電子郵件通知」會將郵件傳送給一或多位收件者。</span><span class="sxs-lookup"><span data-stu-id="1d184-207">Email Notifications send mail to one or more recipients.</span></span>  <span data-ttu-id="1d184-208">它們包含下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="1d184-208">They include the properties in the following table.</span></span>

| <span data-ttu-id="1d184-209">屬性</span><span class="sxs-lookup"><span data-stu-id="1d184-209">Property</span></span> | <span data-ttu-id="1d184-210">說明</span><span class="sxs-lookup"><span data-stu-id="1d184-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d184-211">收件者</span><span class="sxs-lookup"><span data-stu-id="1d184-211">Recipients</span></span> |<span data-ttu-id="1d184-212">郵件地址清單。</span><span class="sxs-lookup"><span data-stu-id="1d184-212">List of mail addresses.</span></span> |
| <span data-ttu-id="1d184-213">主旨</span><span class="sxs-lookup"><span data-stu-id="1d184-213">Subject</span></span> |<span data-ttu-id="1d184-214">郵件的主旨。</span><span class="sxs-lookup"><span data-stu-id="1d184-214">The subject of the mail.</span></span> |
| <span data-ttu-id="1d184-215">附件</span><span class="sxs-lookup"><span data-stu-id="1d184-215">Attachment</span></span> |<span data-ttu-id="1d184-216">目前不支援附件，這個值永遠為 “None”。</span><span class="sxs-lookup"><span data-stu-id="1d184-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="1d184-217">以下是一個包含臨界值的電子郵件通知動作的回應範例。</span><span class="sxs-lookup"><span data-stu-id="1d184-217">Following is a sample response for an email notification action with a threshold.</span></span>  

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
            "Subject": "This is the subject",
            "Attachment": "None"
        },
        "Version": 1
    }

<span data-ttu-id="1d184-218">使用 Put 方法並指定唯一的動作識別碼，以建立排程的新電子郵件動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-218">Use the Put method with a unique action ID to create a new e-mail action for a schedule.</span></span>  <span data-ttu-id="1d184-219">下列範例建立一個包含臨界值的電子郵件通知，當已儲存的搜尋結果超過臨界值時，就會傳送郵件。</span><span class="sxs-lookup"><span data-stu-id="1d184-219">The following example creates an email notification with a threshold so the mail is sent when the results of the saved search exceed the threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="1d184-220">使用 Put 方法並指定現有的動作識別碼，以修改排程的電子郵件動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-220">Use the Put method with an existing action ID to modify an e-mail action for a schedule.</span></span>  <span data-ttu-id="1d184-221">要求的主體必須包含動作的 etag。</span><span class="sxs-lookup"><span data-stu-id="1d184-221">The body of the request must include the etag of the action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="1d184-222">補救動作</span><span class="sxs-lookup"><span data-stu-id="1d184-222">Remediation actions</span></span>
<span data-ttu-id="1d184-223">「補救」會在 Azure 自動化中啟動 Runbook，嘗試更正警示所識別的問題。</span><span class="sxs-lookup"><span data-stu-id="1d184-223">Remediations start a runbook in Azure Automation that attempts to correct the problem identified by the alert.</span></span>  <span data-ttu-id="1d184-224">您必須為補救動作中使用的 Runbook 建立 webhook，然後在 WebhookUri 屬性中指定 URI。</span><span class="sxs-lookup"><span data-stu-id="1d184-224">You must create a webhook for the runbook used in a remediation action and then specify the URI in the WebhookUri property.</span></span>  <span data-ttu-id="1d184-225">當您使用 OMS 主控台建立此動作時，將會自動為 Runbook 建立新的 webhook。</span><span class="sxs-lookup"><span data-stu-id="1d184-225">When you create this action using the OMS console, a new webhook is automatically created for the runbook.</span></span>

<span data-ttu-id="1d184-226">「補救」包含下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="1d184-226">Remediations include the properties in the following table.</span></span>

| <span data-ttu-id="1d184-227">屬性</span><span class="sxs-lookup"><span data-stu-id="1d184-227">Property</span></span> | <span data-ttu-id="1d184-228">說明</span><span class="sxs-lookup"><span data-stu-id="1d184-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d184-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="1d184-229">RunbookName</span></span> |<span data-ttu-id="1d184-230">Runbook 的名稱。</span><span class="sxs-lookup"><span data-stu-id="1d184-230">Name of the runbook.</span></span> <span data-ttu-id="1d184-231">這必須符合自動化帳戶 (在 OMS 工作區的自動化方案中設定) 中發佈的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="1d184-231">This must match a published runbook in the automation account configured in the Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="1d184-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="1d184-232">WebhookUri</span></span> |<span data-ttu-id="1d184-233">Webhook 的 URI。</span><span class="sxs-lookup"><span data-stu-id="1d184-233">URI of the webhook.</span></span> |
| <span data-ttu-id="1d184-234">Expiry</span><span class="sxs-lookup"><span data-stu-id="1d184-234">Expiry</span></span> |<span data-ttu-id="1d184-235">webhook 的到期日期和時間。</span><span class="sxs-lookup"><span data-stu-id="1d184-235">The expiration date and time of the webhook.</span></span>  <span data-ttu-id="1d184-236">如果 webhook 沒有到期日，這可以是任何有效的未來日期。</span><span class="sxs-lookup"><span data-stu-id="1d184-236">If the webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="1d184-237">以下是一個包含臨界值的補救動作的回應範例。</span><span class="sxs-lookup"><span data-stu-id="1d184-237">Following is a sample response for a remediation action with a threshold.</span></span>

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

<span data-ttu-id="1d184-238">使用 Put 方法並指定唯一的動作識別碼，以建立排程的新補救動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-238">Use the Put method with a unique action ID to create a new remediation action for a schedule.</span></span>  <span data-ttu-id="1d184-239">下列範例建立一個包含臨界值的補救，當已儲存的搜尋結果超過臨界值時，就會啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="1d184-239">The following example creates a remediation with a threshold so the runbook is started when the results of the saved search exceed the threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="1d184-240">使用 Put 方法並指定現有的動作識別碼，以修改排程的補救動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-240">Use the Put method with an existing action ID to modify a remediation action for a schedule.</span></span>  <span data-ttu-id="1d184-241">要求的主體必須包含動作的 etag。</span><span class="sxs-lookup"><span data-stu-id="1d184-241">The body of the request must include the etag of the action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="1d184-242">範例</span><span class="sxs-lookup"><span data-stu-id="1d184-242">Example</span></span>
<span data-ttu-id="1d184-243">以下是建立新電子郵件警示的完整範例。</span><span class="sxs-lookup"><span data-stu-id="1d184-243">Following is a complete example to create a new email alert.</span></span>  <span data-ttu-id="1d184-244">這會建立新的排程及一個包含臨界值和電子郵件的動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is the subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a><span data-ttu-id="1d184-245">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="1d184-245">Webhook actions</span></span>
<span data-ttu-id="1d184-246">Webhook 動作會呼叫 URL 並選擇性地提供要傳送的承載，以啟動處理序。</span><span class="sxs-lookup"><span data-stu-id="1d184-246">Webhook actions start a process by calling a URL and optionally providing a payload to be sent.</span></span>  <span data-ttu-id="1d184-247">這些動作類似於「補救」動作，不同之處在於它們用於可能叫用 Azure 自動化 Runbook 以外之處理序的 webhook。</span><span class="sxs-lookup"><span data-stu-id="1d184-247">They are similar to Remediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="1d184-248">它們還提供另一個選項，可指定要傳遞到遠端處理序的承載。</span><span class="sxs-lookup"><span data-stu-id="1d184-248">They also provide the additional option of providing a payload to be delivered to the remote process.</span></span>

<span data-ttu-id="1d184-249">Webhook 動作沒有臨界值，應該加入至具有警示動作和臨界值的排程。</span><span class="sxs-lookup"><span data-stu-id="1d184-249">Webhook actions do not have a threshold but instead should be added to a schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="1d184-250">您可以加入多個 Webhook 動作，在符合臨界值時全部執行。</span><span class="sxs-lookup"><span data-stu-id="1d184-250">You can add multiple Webhook actions that will all be run when the threshold is met.</span></span>

<span data-ttu-id="1d184-251">Webhook 動作包含下表中的屬性。</span><span class="sxs-lookup"><span data-stu-id="1d184-251">Webhook actions include the properties in the following table.</span></span>

| <span data-ttu-id="1d184-252">屬性</span><span class="sxs-lookup"><span data-stu-id="1d184-252">Property</span></span> | <span data-ttu-id="1d184-253">說明</span><span class="sxs-lookup"><span data-stu-id="1d184-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="1d184-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="1d184-254">WebhookUri</span></span> |<span data-ttu-id="1d184-255">郵件的主旨。</span><span class="sxs-lookup"><span data-stu-id="1d184-255">The subject of the mail.</span></span> |
| <span data-ttu-id="1d184-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="1d184-256">CustomPayload</span></span> |<span data-ttu-id="1d184-257">要傳送至 webhook 的自訂內容。</span><span class="sxs-lookup"><span data-stu-id="1d184-257">Custom payload to be sent to the webhook.</span></span>  <span data-ttu-id="1d184-258">格式取決於 webhook 需要的內容。</span><span class="sxs-lookup"><span data-stu-id="1d184-258">The format will depend on what the webhook is expecting.</span></span> |

<span data-ttu-id="1d184-259">以下是 webhook 動作及一個包含臨界值的相關聯警示動作的回應範例。</span><span class="sxs-lookup"><span data-stu-id="1d184-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

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

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="1d184-260">建立或編輯 webhook 動作</span><span class="sxs-lookup"><span data-stu-id="1d184-260">Create or edit a webhook action</span></span>
<span data-ttu-id="1d184-261">使用 Put 方法並指定唯一的動作識別碼，以建立排程的新 webhook 動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-261">Use the Put method with a unique action ID to create a new webhook action for a schedule.</span></span>  <span data-ttu-id="1d184-262">下列範例建立 Webhook 動作及一個包含臨界值的警示動作，當已儲存的搜尋結果超過臨界值時，就會啟動 webhook。</span><span class="sxs-lookup"><span data-stu-id="1d184-262">The following example creates a Webhook action and an Alert action with a threshold so that the webhook will be triggered when the results of the saved search exceed the threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="1d184-263">使用 Put 方法並指定現有的動作識別碼，以修改排程的 webhook 動作。</span><span class="sxs-lookup"><span data-stu-id="1d184-263">Use the Put method with an existing action ID to modify a webhook action for a schedule.</span></span>  <span data-ttu-id="1d184-264">要求的主體必須包含動作的 etag。</span><span class="sxs-lookup"><span data-stu-id="1d184-264">The body of the request must include the etag of the action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="1d184-265">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1d184-265">Next steps</span></span>
* <span data-ttu-id="1d184-266">在 Log Analytics 中使用 [REST API 執行記錄檔搜尋](log-analytics-log-search-api.md) 。</span><span class="sxs-lookup"><span data-stu-id="1d184-266">Use the [REST API to perform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

