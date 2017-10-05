---
title: "建立 OMS Log Analytics 中的警示 | Microsoft Docs"
description: "Log Analytics 中的警示會識別您的 OMS 儲存機制中的重要資訊，並可主動通知您相關問題或叫用動作以嘗試更正問題。  本文描述如何建立警示規則及詳細說明可以採取的各種動作。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 6cfd2a46-b6a2-4f79-a67b-08ce488f9a91
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/23/2017
ms.author: bwren
ms.openlocfilehash: c34fb7295e8f386f0e7cf2c1db6b26a3e49eae98
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a><span data-ttu-id="7e18a-104">使用 Log Analytics 中的警示規則</span><span class="sxs-lookup"><span data-stu-id="7e18a-104">Working with alert rules in Log Analytics</span></span>
<span data-ttu-id="7e18a-105">警示會由自動定期執行記錄搜尋的警示規則所建立。</span><span class="sxs-lookup"><span data-stu-id="7e18a-105">Alerts are created by alert rules that automatically run log searches at regular intervals.</span></span>  <span data-ttu-id="7e18a-106">如果結果符合特定準則，則會建立警示記錄。</span><span class="sxs-lookup"><span data-stu-id="7e18a-106">They create an alert record if the results match particular criteria.</span></span>  <span data-ttu-id="7e18a-107">此規則接著可以自動執行一或多個動作，以主動通知警示或叫用另一個處理序。</span><span class="sxs-lookup"><span data-stu-id="7e18a-107">The rule can then automatically run one or more actions to proactively notify you of the alert or invoke another process.</span></span>   

<span data-ttu-id="7e18a-108">本文說明使用 OMS 入口網站建立和編輯警示規則的程序。</span><span class="sxs-lookup"><span data-stu-id="7e18a-108">This article describes the processes to create and edit alert rules using the OMS portal.</span></span>  <span data-ttu-id="7e18a-109">如需不同設定以及如何實作必要邏輯的詳細資訊，請參閱[了解 Log Analytics 中的警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="7e18a-109">For details about the different settings and how to implement required logic, see [Understanding alerts in Log Analytics](log-analytics-alerts.md).</span></span>

>[!NOTE]
> <span data-ttu-id="7e18a-110">您目前無法使用 Azure 入口網站建立或修改警示規則。</span><span class="sxs-lookup"><span data-stu-id="7e18a-110">You cannot currently create or modify an alert rule using the Azure portal.</span></span> 

## <a name="create-an-alert-rule"></a><span data-ttu-id="7e18a-111">建立警示規則</span><span class="sxs-lookup"><span data-stu-id="7e18a-111">Create an alert rule</span></span>

<span data-ttu-id="7e18a-112">若要使用 OMS 入口網站建立警示規則，首先針對應叫用警示的記錄，建立記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="7e18a-112">To create an alert rule using the OMS portal, you start by creating a log search for the records that should invoke the alert.</span></span>  <span data-ttu-id="7e18a-113">[警示]  按鈕將可供您使用，以便建立和設定警示規則。</span><span class="sxs-lookup"><span data-stu-id="7e18a-113">The **Alert** button will then be available so you can create and configure the alert rule.</span></span>

>[!NOTE]
> <span data-ttu-id="7e18a-114">目前最多可以在 OMS 工作區中建立 250 個警示規則。</span><span class="sxs-lookup"><span data-stu-id="7e18a-114">A maximum of 250 alert rules can currently be created in an OMS workspace.</span></span> 

1. <span data-ttu-id="7e18a-115">從 [OMS 概觀] 頁面，按一下 [記錄檔搜尋] 。</span><span class="sxs-lookup"><span data-stu-id="7e18a-115">From the OMS Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="7e18a-116">建立新的記錄檔搜尋查詢，或選取已儲存的記錄檔搜尋。</span><span class="sxs-lookup"><span data-stu-id="7e18a-116">Either create a new log search query or select a saved log search.</span></span> 
3. <span data-ttu-id="7e18a-117">按一下頁面頂端的 [警示] 以開啟 [新增警示規則] 畫面。</span><span class="sxs-lookup"><span data-stu-id="7e18a-117">Click **Alert** at the top of the page to open the **Add Alert Rule** screen.</span></span>
4. <span data-ttu-id="7e18a-118">使用底下[警示規則詳細資訊](#details-of-alert-rules)中的資訊，設定警示規則。</span><span class="sxs-lookup"><span data-stu-id="7e18a-118">Configure the alert rule using information in [Details of alert rules](#details-of-alert-rules) below.</span></span>
6. <span data-ttu-id="7e18a-119">按一下 [儲存]  完成警示規則。</span><span class="sxs-lookup"><span data-stu-id="7e18a-119">Click **Save** to complete the alert rule.</span></span>  <span data-ttu-id="7e18a-120">該警示規則會立即開始執行。</span><span class="sxs-lookup"><span data-stu-id="7e18a-120">It will start running immediately.</span></span>


## <a name="edit-an-alert-rule"></a><span data-ttu-id="7e18a-121">編輯警示規則</span><span class="sxs-lookup"><span data-stu-id="7e18a-121">Edit an alert rule</span></span>
<span data-ttu-id="7e18a-122">您可以在 Log Analytics [設定] 的 [警示] 功能表中，取得所有警示規則的清單。</span><span class="sxs-lookup"><span data-stu-id="7e18a-122">You can get a list of all alert rules in the **Alerts** menu in Log Analytics **Settings**.</span></span>  

![管理警示](./media/log-analytics-alerts/configure.png)

1. <span data-ttu-id="7e18a-124">在 OMS 主控台中選取 [設定]  圖格。</span><span class="sxs-lookup"><span data-stu-id="7e18a-124">In the OMS console select the **Settings** tile.</span></span>
2. <span data-ttu-id="7e18a-125">選取 [警示] 。</span><span class="sxs-lookup"><span data-stu-id="7e18a-125">Select **Alerts**.</span></span>

<span data-ttu-id="7e18a-126">您可以在此檢視中執行多個動作。</span><span class="sxs-lookup"><span data-stu-id="7e18a-126">You can perform multiple actions from this view.</span></span>

* <span data-ttu-id="7e18a-127">選取旁邊的 [關閉]  來停用規則。</span><span class="sxs-lookup"><span data-stu-id="7e18a-127">Disable a rule by selecting **Off** next to it.</span></span>
* <span data-ttu-id="7e18a-128">按一下旁邊的鉛筆圖示以編輯警示規則。</span><span class="sxs-lookup"><span data-stu-id="7e18a-128">Edit an alert rule by clicking the pencil icon next to it.</span></span>
* <span data-ttu-id="7e18a-129">按一下旁邊的 **X** 圖示以移除警示規則。</span><span class="sxs-lookup"><span data-stu-id="7e18a-129">Remove an alert rule by clicking the **X** icon next to it.</span></span> 

## <a name="details-of-alert-rules"></a><span data-ttu-id="7e18a-130">警示規則詳細資訊</span><span class="sxs-lookup"><span data-stu-id="7e18a-130">Details of alert rules</span></span>
<span data-ttu-id="7e18a-131">當您在 OMS 入口網站中建立或編輯警示規則時，您可使用 [新增警示規則] 或 [編輯警示規則] 頁面。</span><span class="sxs-lookup"><span data-stu-id="7e18a-131">When you create or edit an alert rule in the OMS portal, you work with the **Add Alert Rule** or **Edit Alert Rule** page.</span></span>  <span data-ttu-id="7e18a-132">下表說明此畫面中的欄位。</span><span class="sxs-lookup"><span data-stu-id="7e18a-132">The following tables describe the fields in this screen.</span></span>

![警示規則](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a><span data-ttu-id="7e18a-134">警示資訊</span><span class="sxs-lookup"><span data-stu-id="7e18a-134">Alert information</span></span>
<span data-ttu-id="7e18a-135">這些是警示規則的基本設定及其建立的警示。</span><span class="sxs-lookup"><span data-stu-id="7e18a-135">These are basic settings for the alert rule and the alerts it creates.</span></span>

| <span data-ttu-id="7e18a-136">屬性</span><span class="sxs-lookup"><span data-stu-id="7e18a-136">Property</span></span> | <span data-ttu-id="7e18a-137">說明</span><span class="sxs-lookup"><span data-stu-id="7e18a-137">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="7e18a-138">名稱</span><span class="sxs-lookup"><span data-stu-id="7e18a-138">Name</span></span> | <span data-ttu-id="7e18a-139">用以識別警示規則的唯一名稱。</span><span class="sxs-lookup"><span data-stu-id="7e18a-139">Unique name to identify the alert rule.</span></span> <span data-ttu-id="7e18a-140">此名稱包含在規則所建立的任何警示中。</span><span class="sxs-lookup"><span data-stu-id="7e18a-140">This name is included in any alerts created by the rule.</span></span>  |
| <span data-ttu-id="7e18a-141">說明</span><span class="sxs-lookup"><span data-stu-id="7e18a-141">Description</span></span> | <span data-ttu-id="7e18a-142">警示規則的選擇性描述。</span><span class="sxs-lookup"><span data-stu-id="7e18a-142">Optional description of the alert rule.</span></span> |
| <span data-ttu-id="7e18a-143">嚴重性</span><span class="sxs-lookup"><span data-stu-id="7e18a-143">Severity</span></span> |<span data-ttu-id="7e18a-144">此規則所建立之任何警示的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="7e18a-144">Severity of any alerts created by this rule.</span></span> |

### <a name="search-query-and-time-window"></a><span data-ttu-id="7e18a-145">搜尋查詢和時間範圍</span><span class="sxs-lookup"><span data-stu-id="7e18a-145">Search query and time window</span></span>
<span data-ttu-id="7e18a-146">系統會評估可傳回記錄的搜尋查詢和時間範圍，以判斷是否應建立任何警示。</span><span class="sxs-lookup"><span data-stu-id="7e18a-146">The search query and time window that return the records that are evaluated to determine if any alerts should be created.</span></span>

| <span data-ttu-id="7e18a-147">屬性</span><span class="sxs-lookup"><span data-stu-id="7e18a-147">Property</span></span> | <span data-ttu-id="7e18a-148">說明</span><span class="sxs-lookup"><span data-stu-id="7e18a-148">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="7e18a-149">搜尋查詢</span><span class="sxs-lookup"><span data-stu-id="7e18a-149">Search query</span></span> | <span data-ttu-id="7e18a-150">這是將要執行的查詢。</span><span class="sxs-lookup"><span data-stu-id="7e18a-150">This is the query that will be run.</span></span>  <span data-ttu-id="7e18a-151">此查詢所傳回的記錄將會用來判斷是否要建立警示。</span><span class="sxs-lookup"><span data-stu-id="7e18a-151">The records returned by this query will be used to determine whether an alert is created.</span></span><br><br><span data-ttu-id="7e18a-152">選取 [使用目前搜尋查詢]  以使用目前的查詢，或從清單中選取現有的已儲存搜尋。</span><span class="sxs-lookup"><span data-stu-id="7e18a-152">Select **Use current search query** to use the current query or select an existing saved search from the list.</span></span>  <span data-ttu-id="7e18a-153">查詢語法會提供於文字方塊中，您可以視需要加以修改。</span><span class="sxs-lookup"><span data-stu-id="7e18a-153">The query syntax is provided in the text box where you can modify it if necessary.</span></span> |
| <span data-ttu-id="7e18a-154">時間範圍</span><span class="sxs-lookup"><span data-stu-id="7e18a-154">Time window</span></span> |<span data-ttu-id="7e18a-155">指定查詢的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="7e18a-155">Specifies the time range for the query.</span></span>  <span data-ttu-id="7e18a-156">查詢只會傳回在此目前時間範圍內建立的記錄。</span><span class="sxs-lookup"><span data-stu-id="7e18a-156">The query returns only records that were created within this range of  the current time.</span></span>  <span data-ttu-id="7e18a-157">可以是介於 5 分鐘與 24 小時之間的任何值。</span><span class="sxs-lookup"><span data-stu-id="7e18a-157">This can be any value between 5 minutes and 24 hours.</span></span>  <span data-ttu-id="7e18a-158">應大於或等於警示頻率。</span><span class="sxs-lookup"><span data-stu-id="7e18a-158">It should be greater than or equal to the alert frequency.</span></span>  <br><br> <span data-ttu-id="7e18a-159">例如，如果時間範圍設定為 60 分鐘，則查詢會在下午 1:15 執行，只會傳回在下午 12:15 與下午 1:15 之間建立的記錄。</span><span class="sxs-lookup"><span data-stu-id="7e18a-159">For example, If the time window is set to 60 minutes, and the query is run at 1:15 PM, only records created between 12:15 PM and 1:15 PM will be returned.</span></span> |

<span data-ttu-id="7e18a-160">當您提供警示規則的時間範圍時，將會顯示該時間範圍內符合搜尋準則的現有記錄數目。</span><span class="sxs-lookup"><span data-stu-id="7e18a-160">When you provide the time window for the alert rule, the number of existing records that match the search criteria for that time window will be displayed.</span></span>  <span data-ttu-id="7e18a-161">這可以協助您判斷可為您提供預期結果數目的頻率。</span><span class="sxs-lookup"><span data-stu-id="7e18a-161">This can help you determine the frequency that will give you the number of results that you expect.</span></span>

### <a name="schedule"></a><span data-ttu-id="7e18a-162">排程</span><span class="sxs-lookup"><span data-stu-id="7e18a-162">Schedule</span></span>
<span data-ttu-id="7e18a-163">定義搜尋查詢的執行頻率。</span><span class="sxs-lookup"><span data-stu-id="7e18a-163">Defines how often the search query is run.</span></span>

| <span data-ttu-id="7e18a-164">屬性</span><span class="sxs-lookup"><span data-stu-id="7e18a-164">Property</span></span> | <span data-ttu-id="7e18a-165">說明</span><span class="sxs-lookup"><span data-stu-id="7e18a-165">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="7e18a-166">警示頻率</span><span class="sxs-lookup"><span data-stu-id="7e18a-166">Alert frequency</span></span> | <span data-ttu-id="7e18a-167">指定應執行查詢的頻率。</span><span class="sxs-lookup"><span data-stu-id="7e18a-167">Specifies how often the query should be run.</span></span> <span data-ttu-id="7e18a-168">可以是介於 5 分鐘與 24 小時之間的任何值。</span><span class="sxs-lookup"><span data-stu-id="7e18a-168">Can be any value between 5 minutes and 24 hours.</span></span> <span data-ttu-id="7e18a-169">應等於或小於此時間範圍。</span><span class="sxs-lookup"><span data-stu-id="7e18a-169">Should be equal to or less than the time window.</span></span>  <span data-ttu-id="7e18a-170">如果值大於時間範圍，則您可能有遺漏記錄的風險。</span><span class="sxs-lookup"><span data-stu-id="7e18a-170">If the value is greater than the time window, then you risk records being missed.</span></span><br><br><span data-ttu-id="7e18a-171">例如，請考慮 30 分鐘的時間範圍，以及 60 分鐘的頻率。</span><span class="sxs-lookup"><span data-stu-id="7e18a-171">For example, consider a time window of 30 minutes and a frequency of 60 minutes.</span></span>  <span data-ttu-id="7e18a-172">如果在 1:00 執行查詢，它會傳回 12:30 到下午 1:00 之間的記錄。</span><span class="sxs-lookup"><span data-stu-id="7e18a-172">If the query is run at 1:00, it returns records between 12:30 and 1:00 PM.</span></span>  <span data-ttu-id="7e18a-173">下一次執行查詢就是 2:00 時，它會傳回 1:30 至 2:00 之間的記錄。</span><span class="sxs-lookup"><span data-stu-id="7e18a-173">The next time the query would run is 2:00 when it would return records between 1:30 and 2:00.</span></span>  <span data-ttu-id="7e18a-174">1:00 和 1:30 之間建立的任何記錄一律不會評估。</span><span class="sxs-lookup"><span data-stu-id="7e18a-174">Any records created between 1:00 and 1:30 would never be evaluated.</span></span> |


### <a name="generate-alert-based-on"></a><span data-ttu-id="7e18a-175">產生警示的依據</span><span class="sxs-lookup"><span data-stu-id="7e18a-175">Generate alert based on</span></span>
<span data-ttu-id="7e18a-176">定義將根據搜尋查詢的結果進行評估以判斷是否應該建立警示的準則。</span><span class="sxs-lookup"><span data-stu-id="7e18a-176">Defines the criteria that will be evaluated against the results of the search query to determine if an alert should be created.</span></span>  <span data-ttu-id="7e18a-177">這些詳細資料將根據您選取的警示規則類型而不同。</span><span class="sxs-lookup"><span data-stu-id="7e18a-177">These details will be different depending on the type of alert rule that you select.</span></span>  <span data-ttu-id="7e18a-178">您可以從[了解 Log Analytics 中的警示](log-analytics-alerts.md)中取得不同警示規則類型的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="7e18a-178">You can get details for the different alert rule types from [Understanding alerts in Log Analytics](log-analytics-alerts.md).</span></span>

| <span data-ttu-id="7e18a-179">屬性</span><span class="sxs-lookup"><span data-stu-id="7e18a-179">Property</span></span> | <span data-ttu-id="7e18a-180">說明</span><span class="sxs-lookup"><span data-stu-id="7e18a-180">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="7e18a-181">隱藏警示</span><span class="sxs-lookup"><span data-stu-id="7e18a-181">Suppress alerts</span></span> | <span data-ttu-id="7e18a-182">當您開啟警示規則的隱藏功能時，此規則的動作會在建立新警示後停用並持續一段您所定義的時間。</span><span class="sxs-lookup"><span data-stu-id="7e18a-182">When you turn on suppression for the alert rule, actions for the rule are disabled for a defined length of time after creating a new alert.</span></span> <span data-ttu-id="7e18a-183">採規則仍在執行中，並且會在符合準則時建立警示記錄。</span><span class="sxs-lookup"><span data-stu-id="7e18a-183">The rule is still running and will create alert records if the criteria is met.</span></span> <span data-ttu-id="7e18a-184">這可讓您有時間更正問題，而不需執行重複的動作。</span><span class="sxs-lookup"><span data-stu-id="7e18a-184">This is to allow you time to correct the problem without running duplicate actions.</span></span> |

#### <a name="number-of-results-alert-rules"></a><span data-ttu-id="7e18a-185">結果數目的警示規則</span><span class="sxs-lookup"><span data-stu-id="7e18a-185">Number of results alert rules</span></span>

| <span data-ttu-id="7e18a-186">屬性</span><span class="sxs-lookup"><span data-stu-id="7e18a-186">Property</span></span> | <span data-ttu-id="7e18a-187">說明</span><span class="sxs-lookup"><span data-stu-id="7e18a-187">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="7e18a-188">結果數目</span><span class="sxs-lookup"><span data-stu-id="7e18a-188">Number of results</span></span> |<span data-ttu-id="7e18a-189">如果查詢所傳回的記錄數目**大於**或**小於**您所提供的值，則會建立警示。</span><span class="sxs-lookup"><span data-stu-id="7e18a-189">An alert is created if the number of records returned by the query is either **greater than** or **less than** the value you provide.</span></span>  |

#### <a name="metric-measurement-alert-rules"></a><span data-ttu-id="7e18a-190">公制度量單位的警示規則</span><span class="sxs-lookup"><span data-stu-id="7e18a-190">Metric measurement alert rules</span></span>

| <span data-ttu-id="7e18a-191">屬性</span><span class="sxs-lookup"><span data-stu-id="7e18a-191">Property</span></span> | <span data-ttu-id="7e18a-192">說明</span><span class="sxs-lookup"><span data-stu-id="7e18a-192">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="7e18a-193">彙總值</span><span class="sxs-lookup"><span data-stu-id="7e18a-193">Aggregate value</span></span> | <span data-ttu-id="7e18a-194">結果中的每個彙總值必須超過才會被視為違規的臨界值。</span><span class="sxs-lookup"><span data-stu-id="7e18a-194">Threshold value that each aggregate value in the results must exceed to be considered a breach.</span></span> |
| <span data-ttu-id="7e18a-195">觸發警示的依據</span><span class="sxs-lookup"><span data-stu-id="7e18a-195">Trigger alert based on</span></span> | <span data-ttu-id="7e18a-196">要針對警示建立的違規數。</span><span class="sxs-lookup"><span data-stu-id="7e18a-196">The number of breaches for an alert to be created.</span></span>  <span data-ttu-id="7e18a-197">您可以跨結果集針對任何違規組合指定 [違規數總計]，或指定 [連續違規] 以要求違規必須發生於連續取樣中。</span><span class="sxs-lookup"><span data-stu-id="7e18a-197">You can specify **Total breaches** for any combination of breaches across the results set or **Consecutive breaches** to require that the breaches must occur in consecutive samples.</span></span> |

### <a name="actions"></a><span data-ttu-id="7e18a-198">動作</span><span class="sxs-lookup"><span data-stu-id="7e18a-198">Actions</span></span>
<span data-ttu-id="7e18a-199">警示規則一律會在達到閾值時建立[警示記錄](#alert-records)。</span><span class="sxs-lookup"><span data-stu-id="7e18a-199">Alert rules will always create an [alert record](#alert-records) when the threshold is met.</span></span>  <span data-ttu-id="7e18a-200">您也可以定義一或多個要執行的回應，例如傳送電子郵件或啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7e18a-200">You can also define one or more responses to be run such as sending an email or starting a runbook.</span></span>



#### <a name="email-actions"></a><span data-ttu-id="7e18a-201">電子郵件動作</span><span class="sxs-lookup"><span data-stu-id="7e18a-201">Email actions</span></span>
<span data-ttu-id="7e18a-202">電子郵件動作會傳送內含警示詳細資料的電子郵件給一或多位收件者。</span><span class="sxs-lookup"><span data-stu-id="7e18a-202">Email actions send an e-mail with the details of the alert to one or more recipients.</span></span>

| <span data-ttu-id="7e18a-203">屬性</span><span class="sxs-lookup"><span data-stu-id="7e18a-203">Property</span></span> | <span data-ttu-id="7e18a-204">說明</span><span class="sxs-lookup"><span data-stu-id="7e18a-204">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="7e18a-205">電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="7e18a-205">Email notification</span></span> |<span data-ttu-id="7e18a-206">如果您要在警示觸發時傳送電子郵件，請指定 [是]  。</span><span class="sxs-lookup"><span data-stu-id="7e18a-206">Specify **Yes** if you want an email to be sent when the alert is triggered.</span></span> |
| <span data-ttu-id="7e18a-207">主旨</span><span class="sxs-lookup"><span data-stu-id="7e18a-207">Subject</span></span> |<span data-ttu-id="7e18a-208">電子郵件的主旨。</span><span class="sxs-lookup"><span data-stu-id="7e18a-208">Subject in the email.</span></span>  <span data-ttu-id="7e18a-209">您無法修改郵件的內文。</span><span class="sxs-lookup"><span data-stu-id="7e18a-209">You cannot modify the body of the mail.</span></span> |
| <span data-ttu-id="7e18a-210">收件者</span><span class="sxs-lookup"><span data-stu-id="7e18a-210">Recipients</span></span> |<span data-ttu-id="7e18a-211">所有電子郵件收件者的地址。</span><span class="sxs-lookup"><span data-stu-id="7e18a-211">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="7e18a-212">如果您指定多個地址，則使用分號 (;) 分隔這些地址。</span><span class="sxs-lookup"><span data-stu-id="7e18a-212">If you specify more than one address, then separate the addresses with a semicolon (;).</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="7e18a-213">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="7e18a-213">Webhook actions</span></span>
<span data-ttu-id="7e18a-214">Webhook 動作可讓您透過單一 HTTP POST 要求叫用外部處理序。</span><span class="sxs-lookup"><span data-stu-id="7e18a-214">Webhook actions allow you to invoke an external process through a single HTTP POST request.</span></span>

| <span data-ttu-id="7e18a-215">屬性</span><span class="sxs-lookup"><span data-stu-id="7e18a-215">Property</span></span> | <span data-ttu-id="7e18a-216">說明</span><span class="sxs-lookup"><span data-stu-id="7e18a-216">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="7e18a-217">Webhook</span><span class="sxs-lookup"><span data-stu-id="7e18a-217">Webhook</span></span> |<span data-ttu-id="7e18a-218">如果您要在警示觸發時呼叫 Webhook，請指定 [是]  。</span><span class="sxs-lookup"><span data-stu-id="7e18a-218">Specify **Yes** if you want to call a webhook when the alert is triggered.</span></span> |
| <span data-ttu-id="7e18a-219">Webhook URL</span><span class="sxs-lookup"><span data-stu-id="7e18a-219">Webhook URL</span></span> |<span data-ttu-id="7e18a-220">Webhook 的 URL。</span><span class="sxs-lookup"><span data-stu-id="7e18a-220">The URL of the webhook.</span></span> |
| <span data-ttu-id="7e18a-221">包含自訂 JSON 承載</span><span class="sxs-lookup"><span data-stu-id="7e18a-221">Include custom JSON payload</span></span> |<span data-ttu-id="7e18a-222">如果您要使用自訂承載取代預設承載，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="7e18a-222">Select this option if you want to replace the default payload with a custom payload.</span></span> |
| <span data-ttu-id="7e18a-223">輸入您的自訂 JSON 承載</span><span class="sxs-lookup"><span data-stu-id="7e18a-223">Enter your custom JSON payload</span></span> |<span data-ttu-id="7e18a-224">Webhook 的自訂承載。</span><span class="sxs-lookup"><span data-stu-id="7e18a-224">The custom payload for the webhook.</span></span>  <span data-ttu-id="7e18a-225">如需詳細資料，請參閱上一節。</span><span class="sxs-lookup"><span data-stu-id="7e18a-225">See previous section for details.</span></span> |

#### <a name="runbook-actions"></a><span data-ttu-id="7e18a-226">Runbook 動作</span><span class="sxs-lookup"><span data-stu-id="7e18a-226">Runbook actions</span></span>
<span data-ttu-id="7e18a-227">Runbook 動作可在 Azure 自動化中啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7e18a-227">Runbook actions start a runbook in Azure Automation.</span></span> 

>[!NOTE]
> <span data-ttu-id="7e18a-228">您必須在工作區中安裝自動化解決方案，才能啟用這個動作。</span><span class="sxs-lookup"><span data-stu-id="7e18a-228">You must have the Automation solution installed in your workspace for this action to be enabled.</span></span> 


| <span data-ttu-id="7e18a-229">屬性</span><span class="sxs-lookup"><span data-stu-id="7e18a-229">Property</span></span> | <span data-ttu-id="7e18a-230">說明</span><span class="sxs-lookup"><span data-stu-id="7e18a-230">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="7e18a-231">Runbook</span><span class="sxs-lookup"><span data-stu-id="7e18a-231">Runbook</span></span> | <span data-ttu-id="7e18a-232">如果您要在警示觸發時啟動 Azure 自動化，請指定 [是]  。</span><span class="sxs-lookup"><span data-stu-id="7e18a-232">Specify **Yes** if you want to start an Azure Automation runbook when the alert is triggered.</span></span>  |
| <span data-ttu-id="7e18a-233">自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="7e18a-233">Automation account</span></span> | <span data-ttu-id="7e18a-234">指定從中選取 Runbook 的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="7e18a-234">Specifies the Automation account that runbooks are selected from.</span></span>  <span data-ttu-id="7e18a-235">這是連結至工作區的動作帳戶。</span><span class="sxs-lookup"><span data-stu-id="7e18a-235">This is the Action account that's linked to the workspace.</span></span> |
| <span data-ttu-id="7e18a-236">啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="7e18a-236">Select a runbook</span></span> | <span data-ttu-id="7e18a-237">建立警示後，選取您想要啟動的 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7e18a-237">Select the runbook that you want to start when an alert is created.</span></span> |
| <span data-ttu-id="7e18a-238">執行位置</span><span class="sxs-lookup"><span data-stu-id="7e18a-238">Run on</span></span> | <span data-ttu-id="7e18a-239">選取 [Azure] 以在雲端執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7e18a-239">Select **Azure** to run the runbook in the cloud.</span></span>  <span data-ttu-id="7e18a-240">選取 [Hybrid Worker]，以在已安裝 [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) 的代理程式上執行 Runbook。</span><span class="sxs-lookup"><span data-stu-id="7e18a-240">Select **Hybrid worker** to run the runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |




## <a name="next-steps"></a><span data-ttu-id="7e18a-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7e18a-241">Next steps</span></span>
* <span data-ttu-id="7e18a-242">安裝 [警示管理解決方案](log-analytics-solution-alert-management.md) ，以分析在 Log Analytics 中建立的警示以及從 System Center Operations Manager (SCOM) 收集的警示。</span><span class="sxs-lookup"><span data-stu-id="7e18a-242">Install the [Alert Management solution](log-analytics-solution-alert-management.md) to analyze alerts created in Log Analytics along with alerts collected from System Center Operations Manager (SCOM).</span></span>
* <span data-ttu-id="7e18a-243">深入了解可產生警示的 [記錄檔搜尋](log-analytics-log-searches.md) 。</span><span class="sxs-lookup"><span data-stu-id="7e18a-243">Read more about [log searches](log-analytics-log-searches.md) that can generate alerts.</span></span>
* <span data-ttu-id="7e18a-244">完成 [設定 Webook](log-analytics-alerts-webhooks.md) 和警示規則的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="7e18a-244">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
* <span data-ttu-id="7e18a-245">了解如何在 [Azure 自動化中撰寫 Runbook](https://azure.microsoft.com/documentation/services/automation) 以補救警示所識別的問題。</span><span class="sxs-lookup"><span data-stu-id="7e18a-245">Learn how to write [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) to remediate problems identified by alerts.</span></span>

