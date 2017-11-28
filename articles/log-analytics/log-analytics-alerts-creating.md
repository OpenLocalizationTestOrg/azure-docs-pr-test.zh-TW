---
title: "在 OMS 記錄分析 aaaCreating 警示 |Microsoft 文件"
description: "警示記錄分析中的識別您的 OMS 儲存機制中的重要資訊和可以主動通知您的問題或叫用動作 tooattempt toocorrect 它們。  本文說明如何 toocreate 警示的規則和詳細資料 hello 不同動作才會。"
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
ms.openlocfilehash: 3d035b2426dda9645b19e6c993dc26a2d95a2a78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="working-with-alert-rules-in-log-analytics"></a><span data-ttu-id="e8547-104">使用 Log Analytics 中的警示規則</span><span class="sxs-lookup"><span data-stu-id="e8547-104">Working with alert rules in Log Analytics</span></span>
<span data-ttu-id="e8547-105">警示會由自動定期執行記錄搜尋的警示規則所建立。</span><span class="sxs-lookup"><span data-stu-id="e8547-105">Alerts are created by alert rules that automatically run log searches at regular intervals.</span></span>  <span data-ttu-id="e8547-106">如果 hello 結果符合特定準則，他們就會建立警示的記錄。</span><span class="sxs-lookup"><span data-stu-id="e8547-106">They create an alert record if hello results match particular criteria.</span></span>  <span data-ttu-id="e8547-107">hello 規則然後就可以自動執行一個或多個動作 tooproactively 通知您 hello 警示，或叫用另一個處理序。</span><span class="sxs-lookup"><span data-stu-id="e8547-107">hello rule can then automatically run one or more actions tooproactively notify you of hello alert or invoke another process.</span></span>   

<span data-ttu-id="e8547-108">本文描述 hello 處理程序 toocreate，並編輯使用 hello OMS 入口網站的警示規則。</span><span class="sxs-lookup"><span data-stu-id="e8547-108">This article describes hello processes toocreate and edit alert rules using hello OMS portal.</span></span>  <span data-ttu-id="e8547-109">如需 hello 不同的設定，以及如何 tooimplement 所需的邏輯的詳細資訊，請參閱[中記錄分析了解警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="e8547-109">For details about hello different settings and how tooimplement required logic, see [Understanding alerts in Log Analytics](log-analytics-alerts.md).</span></span>

>[!NOTE]
> <span data-ttu-id="e8547-110">您目前無法建立或修改使用 hello Azure 入口網站警示規則。</span><span class="sxs-lookup"><span data-stu-id="e8547-110">You cannot currently create or modify an alert rule using hello Azure portal.</span></span> 

## <a name="create-an-alert-rule"></a><span data-ttu-id="e8547-111">建立警示規則</span><span class="sxs-lookup"><span data-stu-id="e8547-111">Create an alert rule</span></span>

<span data-ttu-id="e8547-112">toocreate 使用 hello OMS 入口網站警示規則，先建立記錄檔搜尋應該叫用 hello 警示的 hello 記錄。</span><span class="sxs-lookup"><span data-stu-id="e8547-112">toocreate an alert rule using hello OMS portal, you start by creating a log search for hello records that should invoke hello alert.</span></span>  <span data-ttu-id="e8547-113">hello**警示**按鈕將可以讓您可以建立並設定 hello 警示規則。</span><span class="sxs-lookup"><span data-stu-id="e8547-113">hello **Alert** button will then be available so you can create and configure hello alert rule.</span></span>

>[!NOTE]
> <span data-ttu-id="e8547-114">目前最多可以在 OMS 工作區中建立 250 個警示規則。</span><span class="sxs-lookup"><span data-stu-id="e8547-114">A maximum of 250 alert rules can currently be created in an OMS workspace.</span></span> 

1. <span data-ttu-id="e8547-115">從 hello OMS 的 概觀 頁面上，按一下 **記錄搜尋**。</span><span class="sxs-lookup"><span data-stu-id="e8547-115">From hello OMS Overview page, click **Log Search**.</span></span>
2. <span data-ttu-id="e8547-116">建立新的記錄檔搜尋查詢，或選取已儲存的記錄檔搜尋。</span><span class="sxs-lookup"><span data-stu-id="e8547-116">Either create a new log search query or select a saved log search.</span></span> 
3. <span data-ttu-id="e8547-117">按一下**警示**頂端的 hello 頁面 tooopen hello hello**加入警示規則**螢幕。</span><span class="sxs-lookup"><span data-stu-id="e8547-117">Click **Alert** at hello top of hello page tooopen hello **Add Alert Rule** screen.</span></span>
4. <span data-ttu-id="e8547-118">設定使用中的資訊 hello 警示規則[警示規則的詳細資料](#details-of-alert-rules)下方。</span><span class="sxs-lookup"><span data-stu-id="e8547-118">Configure hello alert rule using information in [Details of alert rules](#details-of-alert-rules) below.</span></span>
6. <span data-ttu-id="e8547-119">按一下**儲存**toocomplete hello 警示規則。</span><span class="sxs-lookup"><span data-stu-id="e8547-119">Click **Save** toocomplete hello alert rule.</span></span>  <span data-ttu-id="e8547-120">該警示規則會立即開始執行。</span><span class="sxs-lookup"><span data-stu-id="e8547-120">It will start running immediately.</span></span>


## <a name="edit-an-alert-rule"></a><span data-ttu-id="e8547-121">編輯警示規則</span><span class="sxs-lookup"><span data-stu-id="e8547-121">Edit an alert rule</span></span>
<span data-ttu-id="e8547-122">您可以取得所有的警示規則的清單中 hello**警示**記錄分析中的功能表**設定**。</span><span class="sxs-lookup"><span data-stu-id="e8547-122">You can get a list of all alert rules in hello **Alerts** menu in Log Analytics **Settings**.</span></span>  

![管理警示](./media/log-analytics-alerts/configure.png)

1. <span data-ttu-id="e8547-124">在 hello OMS 主控台選取 hello**設定**磚。</span><span class="sxs-lookup"><span data-stu-id="e8547-124">In hello OMS console select hello **Settings** tile.</span></span>
2. <span data-ttu-id="e8547-125">選取 [警示] 。</span><span class="sxs-lookup"><span data-stu-id="e8547-125">Select **Alerts**.</span></span>

<span data-ttu-id="e8547-126">您可以在此檢視中執行多個動作。</span><span class="sxs-lookup"><span data-stu-id="e8547-126">You can perform multiple actions from this view.</span></span>

* <span data-ttu-id="e8547-127">選取 [停用規則**關閉**tooit 下一步]。</span><span class="sxs-lookup"><span data-stu-id="e8547-127">Disable a rule by selecting **Off** next tooit.</span></span>
* <span data-ttu-id="e8547-128">按一下 hello 鉛筆圖示下一步 tooit 編輯警示規則。</span><span class="sxs-lookup"><span data-stu-id="e8547-128">Edit an alert rule by clicking hello pencil icon next tooit.</span></span>
* <span data-ttu-id="e8547-129">移除警示規則，依序按一下 hello **X**圖示下一步 tooit。</span><span class="sxs-lookup"><span data-stu-id="e8547-129">Remove an alert rule by clicking hello **X** icon next tooit.</span></span> 

## <a name="details-of-alert-rules"></a><span data-ttu-id="e8547-130">警示規則詳細資訊</span><span class="sxs-lookup"><span data-stu-id="e8547-130">Details of alert rules</span></span>
<span data-ttu-id="e8547-131">當您建立或編輯警示規則 hello OMS 入口網站中的時，搭配 hello**加入警示規則**或**編輯警示規則**頁面。</span><span class="sxs-lookup"><span data-stu-id="e8547-131">When you create or edit an alert rule in hello OMS portal, you work with hello **Add Alert Rule** or **Edit Alert Rule** page.</span></span>  <span data-ttu-id="e8547-132">hello 下表描述在此畫面中的 hello 欄位。</span><span class="sxs-lookup"><span data-stu-id="e8547-132">hello following tables describe hello fields in this screen.</span></span>

![警示規則](media/log-analytics-alerts/add-alert-rule.png)

### <a name="alert-information"></a><span data-ttu-id="e8547-134">警示資訊</span><span class="sxs-lookup"><span data-stu-id="e8547-134">Alert information</span></span>
<span data-ttu-id="e8547-135">這些是基本 hello 警示規則，它會建立 hello 警示設定。</span><span class="sxs-lookup"><span data-stu-id="e8547-135">These are basic settings for hello alert rule and hello alerts it creates.</span></span>

| <span data-ttu-id="e8547-136">屬性</span><span class="sxs-lookup"><span data-stu-id="e8547-136">Property</span></span> | <span data-ttu-id="e8547-137">說明</span><span class="sxs-lookup"><span data-stu-id="e8547-137">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="e8547-138">名稱</span><span class="sxs-lookup"><span data-stu-id="e8547-138">Name</span></span> | <span data-ttu-id="e8547-139">唯一名稱 tooidentify hello 的警示規則。</span><span class="sxs-lookup"><span data-stu-id="e8547-139">Unique name tooidentify hello alert rule.</span></span> <span data-ttu-id="e8547-140">這個名稱會包含在 hello 規則所建立的任何警示。</span><span class="sxs-lookup"><span data-stu-id="e8547-140">This name is included in any alerts created by hello rule.</span></span>  |
| <span data-ttu-id="e8547-141">說明</span><span class="sxs-lookup"><span data-stu-id="e8547-141">Description</span></span> | <span data-ttu-id="e8547-142">Hello 警示規則的選擇性描述。</span><span class="sxs-lookup"><span data-stu-id="e8547-142">Optional description of hello alert rule.</span></span> |
| <span data-ttu-id="e8547-143">嚴重性</span><span class="sxs-lookup"><span data-stu-id="e8547-143">Severity</span></span> |<span data-ttu-id="e8547-144">此規則所建立之任何警示的嚴重性。</span><span class="sxs-lookup"><span data-stu-id="e8547-144">Severity of any alerts created by this rule.</span></span> |

### <a name="search-query-and-time-window"></a><span data-ttu-id="e8547-145">搜尋查詢和時間範圍</span><span class="sxs-lookup"><span data-stu-id="e8547-145">Search query and time window</span></span>
<span data-ttu-id="e8547-146">傳回會評估的 toodetermine，如果應建立任何警示的 hello 記錄 hello 搜尋查詢和時間範圍。</span><span class="sxs-lookup"><span data-stu-id="e8547-146">hello search query and time window that return hello records that are evaluated toodetermine if any alerts should be created.</span></span>

| <span data-ttu-id="e8547-147">屬性</span><span class="sxs-lookup"><span data-stu-id="e8547-147">Property</span></span> | <span data-ttu-id="e8547-148">說明</span><span class="sxs-lookup"><span data-stu-id="e8547-148">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="e8547-149">搜尋查詢</span><span class="sxs-lookup"><span data-stu-id="e8547-149">Search query</span></span> | <span data-ttu-id="e8547-150">這是將執行的 hello 查詢。</span><span class="sxs-lookup"><span data-stu-id="e8547-150">This is hello query that will be run.</span></span>  <span data-ttu-id="e8547-151">此查詢所傳回的 hello 記錄將會使用的 toodetermine 是否建立警示。</span><span class="sxs-lookup"><span data-stu-id="e8547-151">hello records returned by this query will be used toodetermine whether an alert is created.</span></span><br><br><span data-ttu-id="e8547-152">選取**使用目前的搜尋查詢**toouse hello 目前的查詢，或選取現有的儲存搜尋從 hello 清單。</span><span class="sxs-lookup"><span data-stu-id="e8547-152">Select **Use current search query** toouse hello current query or select an existing saved search from hello list.</span></span>  <span data-ttu-id="e8547-153">其中您可以視需要修改它的 hello 文字方塊中提供 hello 查詢語法。</span><span class="sxs-lookup"><span data-stu-id="e8547-153">hello query syntax is provided in hello text box where you can modify it if necessary.</span></span> |
| <span data-ttu-id="e8547-154">時間範圍</span><span class="sxs-lookup"><span data-stu-id="e8547-154">Time window</span></span> |<span data-ttu-id="e8547-155">指定 hello hello 查詢的時間範圍。</span><span class="sxs-lookup"><span data-stu-id="e8547-155">Specifies hello time range for hello query.</span></span>  <span data-ttu-id="e8547-156">hello 查詢會傳回目前時間的 hello 這個範圍內所建立的記錄。</span><span class="sxs-lookup"><span data-stu-id="e8547-156">hello query returns only records that were created within this range of  hello current time.</span></span>  <span data-ttu-id="e8547-157">可以是介於 5 分鐘與 24 小時之間的任何值。</span><span class="sxs-lookup"><span data-stu-id="e8547-157">This can be any value between 5 minutes and 24 hours.</span></span>  <span data-ttu-id="e8547-158">它應該是大於或等於 toohello 警示的頻率。</span><span class="sxs-lookup"><span data-stu-id="e8547-158">It should be greater than or equal toohello alert frequency.</span></span>  <br><br> <span data-ttu-id="e8547-159">例如，如果 hello too60 分鐘和 hello 查詢設定 視窗的時間執行在下午 1:15，將傳回 12:15 PM 和 1:15 PM 之間建立的記錄。</span><span class="sxs-lookup"><span data-stu-id="e8547-159">For example, If hello time window is set too60 minutes, and hello query is run at 1:15 PM, only records created between 12:15 PM and 1:15 PM will be returned.</span></span> |

<span data-ttu-id="e8547-160">當您提供 hello 時段 hello 警示規則時，會顯示 hello 數目符合該時間視窗的 hello 搜尋條件的現有記錄。</span><span class="sxs-lookup"><span data-stu-id="e8547-160">When you provide hello time window for hello alert rule, hello number of existing records that match hello search criteria for that time window will be displayed.</span></span>  <span data-ttu-id="e8547-161">這可協助您判斷 hello 頻率，以提供您 hello 您預期的結果數目。</span><span class="sxs-lookup"><span data-stu-id="e8547-161">This can help you determine hello frequency that will give you hello number of results that you expect.</span></span>

### <a name="schedule"></a><span data-ttu-id="e8547-162">排程</span><span class="sxs-lookup"><span data-stu-id="e8547-162">Schedule</span></span>
<span data-ttu-id="e8547-163">定義頻率 hello 搜尋執行查詢。</span><span class="sxs-lookup"><span data-stu-id="e8547-163">Defines how often hello search query is run.</span></span>

| <span data-ttu-id="e8547-164">屬性</span><span class="sxs-lookup"><span data-stu-id="e8547-164">Property</span></span> | <span data-ttu-id="e8547-165">說明</span><span class="sxs-lookup"><span data-stu-id="e8547-165">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="e8547-166">警示頻率</span><span class="sxs-lookup"><span data-stu-id="e8547-166">Alert frequency</span></span> | <span data-ttu-id="e8547-167">指定頻率 hello 應該執行查詢。</span><span class="sxs-lookup"><span data-stu-id="e8547-167">Specifies how often hello query should be run.</span></span> <span data-ttu-id="e8547-168">可以是介於 5 分鐘與 24 小時之間的任何值。</span><span class="sxs-lookup"><span data-stu-id="e8547-168">Can be any value between 5 minutes and 24 hours.</span></span> <span data-ttu-id="e8547-169">應該是等於 tooor 小於 hello 時間間隔。</span><span class="sxs-lookup"><span data-stu-id="e8547-169">Should be equal tooor less than hello time window.</span></span>  <span data-ttu-id="e8547-170">如果 hello 值大於 hello 的時段，然後可能會遺漏的記錄。</span><span class="sxs-lookup"><span data-stu-id="e8547-170">If hello value is greater than hello time window, then you risk records being missed.</span></span><br><br><span data-ttu-id="e8547-171">例如，請考慮 30 分鐘的時間範圍，以及 60 分鐘的頻率。</span><span class="sxs-lookup"><span data-stu-id="e8547-171">For example, consider a time window of 30 minutes and a frequency of 60 minutes.</span></span>  <span data-ttu-id="e8547-172">如果 hello 查詢 1:00 執行，它會傳回 12:30 下午 1:00 之間的記錄。</span><span class="sxs-lookup"><span data-stu-id="e8547-172">If hello query is run at 1:00, it returns records between 12:30 and 1:00 PM.</span></span>  <span data-ttu-id="e8547-173">hello hello 查詢就會執行下一次為 2:00 時，它就會傳回 1:30 到 2:00 之間的記錄。</span><span class="sxs-lookup"><span data-stu-id="e8547-173">hello next time hello query would run is 2:00 when it would return records between 1:30 and 2:00.</span></span>  <span data-ttu-id="e8547-174">1:00 和 1:30 之間建立的任何記錄一律不會評估。</span><span class="sxs-lookup"><span data-stu-id="e8547-174">Any records created between 1:00 and 1:30 would never be evaluated.</span></span> |


### <a name="generate-alert-based-on"></a><span data-ttu-id="e8547-175">產生警示的依據</span><span class="sxs-lookup"><span data-stu-id="e8547-175">Generate alert based on</span></span>
<span data-ttu-id="e8547-176">定義的 hello 應該建立將會評估 hello hello 的搜尋查詢 toodetermine 如果警示結果的準則。</span><span class="sxs-lookup"><span data-stu-id="e8547-176">Defines hello criteria that will be evaluated against hello results of hello search query toodetermine if an alert should be created.</span></span>  <span data-ttu-id="e8547-177">這些詳細資料會根據您選取的警示規則的 hello 類型而不同。</span><span class="sxs-lookup"><span data-stu-id="e8547-177">These details will be different depending on hello type of alert rule that you select.</span></span>  <span data-ttu-id="e8547-178">您可以取得詳細資料 hello 從不同的警示規則類型[中記錄分析了解警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="e8547-178">You can get details for hello different alert rule types from [Understanding alerts in Log Analytics](log-analytics-alerts.md).</span></span>

| <span data-ttu-id="e8547-179">屬性</span><span class="sxs-lookup"><span data-stu-id="e8547-179">Property</span></span> | <span data-ttu-id="e8547-180">說明</span><span class="sxs-lookup"><span data-stu-id="e8547-180">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="e8547-181">隱藏警示</span><span class="sxs-lookup"><span data-stu-id="e8547-181">Suppress alerts</span></span> | <span data-ttu-id="e8547-182">當您開啟 hello 警示規則隱藏項目時，定義建立新的警示之後的時間長度的 hello 規則的動作會停用。</span><span class="sxs-lookup"><span data-stu-id="e8547-182">When you turn on suppression for hello alert rule, actions for hello rule are disabled for a defined length of time after creating a new alert.</span></span> <span data-ttu-id="e8547-183">hello 規則仍在執行，並符合 hello 準則，則會建立警示記錄。</span><span class="sxs-lookup"><span data-stu-id="e8547-183">hello rule is still running and will create alert records if hello criteria is met.</span></span> <span data-ttu-id="e8547-184">這是 tooallow toocorrect hello 問題的時間而不需執行重複的動作。</span><span class="sxs-lookup"><span data-stu-id="e8547-184">This is tooallow you time toocorrect hello problem without running duplicate actions.</span></span> |

#### <a name="number-of-results-alert-rules"></a><span data-ttu-id="e8547-185">結果數目警示規則</span><span class="sxs-lookup"><span data-stu-id="e8547-185">Number of results alert rules</span></span>

| <span data-ttu-id="e8547-186">屬性</span><span class="sxs-lookup"><span data-stu-id="e8547-186">Property</span></span> | <span data-ttu-id="e8547-187">說明</span><span class="sxs-lookup"><span data-stu-id="e8547-187">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="e8547-188">結果數目</span><span class="sxs-lookup"><span data-stu-id="e8547-188">Number of results</span></span> |<span data-ttu-id="e8547-189">如果 hello hello 查詢所傳回的記錄數目可能是建立警示**大於**或**小於**hello 您提供的值。</span><span class="sxs-lookup"><span data-stu-id="e8547-189">An alert is created if hello number of records returned by hello query is either **greater than** or **less than** hello value you provide.</span></span>  |

#### <a name="metric-measurement-alert-rules"></a><span data-ttu-id="e8547-190">公制度量單位的警示規則</span><span class="sxs-lookup"><span data-stu-id="e8547-190">Metric measurement alert rules</span></span>

| <span data-ttu-id="e8547-191">屬性</span><span class="sxs-lookup"><span data-stu-id="e8547-191">Property</span></span> | <span data-ttu-id="e8547-192">說明</span><span class="sxs-lookup"><span data-stu-id="e8547-192">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="e8547-193">彙總值</span><span class="sxs-lookup"><span data-stu-id="e8547-193">Aggregate value</span></span> | <span data-ttu-id="e8547-194">Hello 結果中每個彙總的值必須超過 toobe 臨界值會被視為有入侵。</span><span class="sxs-lookup"><span data-stu-id="e8547-194">Threshold value that each aggregate value in hello results must exceed toobe considered a breach.</span></span> |
| <span data-ttu-id="e8547-195">觸發警示的依據</span><span class="sxs-lookup"><span data-stu-id="e8547-195">Trigger alert based on</span></span> | <span data-ttu-id="e8547-196">建立警示 toobe 的漏洞的 hello 數目。</span><span class="sxs-lookup"><span data-stu-id="e8547-196">hello number of breaches for an alert toobe created.</span></span>  <span data-ttu-id="e8547-197">您可以指定**總計漏洞**漏洞 hello 結果之間的任何組合的設定或**連續漏洞**hello 漏洞的 toorequire 必須位於連續取樣。</span><span class="sxs-lookup"><span data-stu-id="e8547-197">You can specify **Total breaches** for any combination of breaches across hello results set or **Consecutive breaches** toorequire that hello breaches must occur in consecutive samples.</span></span> |

### <a name="actions"></a><span data-ttu-id="e8547-198">動作</span><span class="sxs-lookup"><span data-stu-id="e8547-198">Actions</span></span>
<span data-ttu-id="e8547-199">永遠會建立警示規則[警示記錄](#alert-records)hello 臨界值到達時。</span><span class="sxs-lookup"><span data-stu-id="e8547-199">Alert rules will always create an [alert record](#alert-records) when hello threshold is met.</span></span>  <span data-ttu-id="e8547-200">您也可以定義一個或多個回應 toobe 執行，例如傳送電子郵件或啟動 runbook。</span><span class="sxs-lookup"><span data-stu-id="e8547-200">You can also define one or more responses toobe run such as sending an email or starting a runbook.</span></span>



#### <a name="email-actions"></a><span data-ttu-id="e8547-201">電子郵件動作</span><span class="sxs-lookup"><span data-stu-id="e8547-201">Email actions</span></span>
<span data-ttu-id="e8547-202">電子郵件動作會傳送 hello 的 hello 警示 tooone 或多個收件者的詳細資料的電子郵件。</span><span class="sxs-lookup"><span data-stu-id="e8547-202">Email actions send an e-mail with hello details of hello alert tooone or more recipients.</span></span>

| <span data-ttu-id="e8547-203">屬性</span><span class="sxs-lookup"><span data-stu-id="e8547-203">Property</span></span> | <span data-ttu-id="e8547-204">說明</span><span class="sxs-lookup"><span data-stu-id="e8547-204">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="e8547-205">電子郵件通知</span><span class="sxs-lookup"><span data-stu-id="e8547-205">Email notification</span></span> |<span data-ttu-id="e8547-206">指定**是**如果您想 hello 在警示觸發時傳送電子郵件 toobe。</span><span class="sxs-lookup"><span data-stu-id="e8547-206">Specify **Yes** if you want an email toobe sent when hello alert is triggered.</span></span> |
| <span data-ttu-id="e8547-207">主旨</span><span class="sxs-lookup"><span data-stu-id="e8547-207">Subject</span></span> |<span data-ttu-id="e8547-208">Hello 電子郵件的主旨。</span><span class="sxs-lookup"><span data-stu-id="e8547-208">Subject in hello email.</span></span>  <span data-ttu-id="e8547-209">您無法修改 hello 郵件 hello 主體。</span><span class="sxs-lookup"><span data-stu-id="e8547-209">You cannot modify hello body of hello mail.</span></span> |
| <span data-ttu-id="e8547-210">收件者</span><span class="sxs-lookup"><span data-stu-id="e8547-210">Recipients</span></span> |<span data-ttu-id="e8547-211">所有電子郵件收件者的地址。</span><span class="sxs-lookup"><span data-stu-id="e8547-211">Addresses of all e-mail recipients.</span></span>  <span data-ttu-id="e8547-212">如果您指定一個以上的地址，然後個別 hello 位址以分號 （;）。</span><span class="sxs-lookup"><span data-stu-id="e8547-212">If you specify more than one address, then separate hello addresses with a semicolon (;).</span></span> |

#### <a name="webhook-actions"></a><span data-ttu-id="e8547-213">Webhook 動作</span><span class="sxs-lookup"><span data-stu-id="e8547-213">Webhook actions</span></span>
<span data-ttu-id="e8547-214">Webhook 動作可讓您 tooinvoke 外部處理序，透過單一的 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="e8547-214">Webhook actions allow you tooinvoke an external process through a single HTTP POST request.</span></span>

| <span data-ttu-id="e8547-215">屬性</span><span class="sxs-lookup"><span data-stu-id="e8547-215">Property</span></span> | <span data-ttu-id="e8547-216">說明</span><span class="sxs-lookup"><span data-stu-id="e8547-216">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="e8547-217">Webhook</span><span class="sxs-lookup"><span data-stu-id="e8547-217">Webhook</span></span> |<span data-ttu-id="e8547-218">指定**是**如果 hello 在警示觸發時，您會想 toocall webhook。</span><span class="sxs-lookup"><span data-stu-id="e8547-218">Specify **Yes** if you want toocall a webhook when hello alert is triggered.</span></span> |
| <span data-ttu-id="e8547-219">Webhook URL</span><span class="sxs-lookup"><span data-stu-id="e8547-219">Webhook URL</span></span> |<span data-ttu-id="e8547-220">hello hello webhook URL。</span><span class="sxs-lookup"><span data-stu-id="e8547-220">hello URL of hello webhook.</span></span> |
| <span data-ttu-id="e8547-221">包含自訂 JSON 承載</span><span class="sxs-lookup"><span data-stu-id="e8547-221">Include custom JSON payload</span></span> |<span data-ttu-id="e8547-222">如果您想要使用自訂承載 tooreplace hello 預設內容，請選取此選項。</span><span class="sxs-lookup"><span data-stu-id="e8547-222">Select this option if you want tooreplace hello default payload with a custom payload.</span></span> |
| <span data-ttu-id="e8547-223">輸入您的自訂 JSON 承載</span><span class="sxs-lookup"><span data-stu-id="e8547-223">Enter your custom JSON payload</span></span> |<span data-ttu-id="e8547-224">hello webhook hello 自訂裝載。</span><span class="sxs-lookup"><span data-stu-id="e8547-224">hello custom payload for hello webhook.</span></span>  <span data-ttu-id="e8547-225">如需詳細資料，請參閱上一節。</span><span class="sxs-lookup"><span data-stu-id="e8547-225">See previous section for details.</span></span> |

#### <a name="runbook-actions"></a><span data-ttu-id="e8547-226">Runbook 動作</span><span class="sxs-lookup"><span data-stu-id="e8547-226">Runbook actions</span></span>
<span data-ttu-id="e8547-227">Runbook 動作可在 Azure 自動化中啟動 Runbook。</span><span class="sxs-lookup"><span data-stu-id="e8547-227">Runbook actions start a runbook in Azure Automation.</span></span> 

>[!NOTE]
> <span data-ttu-id="e8547-228">您必須安裝在您的工作區的 啟用這個動作 toobe hello 自動化解決方案。</span><span class="sxs-lookup"><span data-stu-id="e8547-228">You must have hello Automation solution installed in your workspace for this action toobe enabled.</span></span> 


| <span data-ttu-id="e8547-229">屬性</span><span class="sxs-lookup"><span data-stu-id="e8547-229">Property</span></span> | <span data-ttu-id="e8547-230">說明</span><span class="sxs-lookup"><span data-stu-id="e8547-230">Description</span></span> |
|:--- |:---|
| <span data-ttu-id="e8547-231">Runbook</span><span class="sxs-lookup"><span data-stu-id="e8547-231">Runbook</span></span> | <span data-ttu-id="e8547-232">指定**是**如果 hello 在警示觸發時，您會想 toostart Azure 自動化 runbook。</span><span class="sxs-lookup"><span data-stu-id="e8547-232">Specify **Yes** if you want toostart an Azure Automation runbook when hello alert is triggered.</span></span>  |
| <span data-ttu-id="e8547-233">自動化帳戶</span><span class="sxs-lookup"><span data-stu-id="e8547-233">Automation account</span></span> | <span data-ttu-id="e8547-234">指定 hello runbook 會從選取的自動化帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8547-234">Specifies hello Automation account that runbooks are selected from.</span></span>  <span data-ttu-id="e8547-235">這是已連結 toohello 工作區中的 hello 動作帳戶。</span><span class="sxs-lookup"><span data-stu-id="e8547-235">This is hello Action account that's linked toohello workspace.</span></span> |
| <span data-ttu-id="e8547-236">啟動 Runbook</span><span class="sxs-lookup"><span data-stu-id="e8547-236">Select a runbook</span></span> | <span data-ttu-id="e8547-237">選取您在建立警示時要 toostart hello runbook。</span><span class="sxs-lookup"><span data-stu-id="e8547-237">Select hello runbook that you want toostart when an alert is created.</span></span> |
| <span data-ttu-id="e8547-238">執行位置</span><span class="sxs-lookup"><span data-stu-id="e8547-238">Run on</span></span> | <span data-ttu-id="e8547-239">選取**Azure** toorun hello runbook hello 雲端中的。</span><span class="sxs-lookup"><span data-stu-id="e8547-239">Select **Azure** toorun hello runbook in hello cloud.</span></span>  <span data-ttu-id="e8547-240">選取**Hybrid worker** toorun hello runbook 上的代理程式[Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md )安裝。</span><span class="sxs-lookup"><span data-stu-id="e8547-240">Select **Hybrid worker** toorun hello runbook on an agent with [Hybrid Runbook Worker](../automation/automation-hybrid-runbook-worker.md ) installed.</span></span>  |




## <a name="next-steps"></a><span data-ttu-id="e8547-241">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e8547-241">Next steps</span></span>
* <span data-ttu-id="e8547-242">安裝 hello[警示管理解決方案](log-analytics-solution-alert-management.md)tooanalyze 警示與警示一起建立記錄分析中收集從 System Center Operations Manager (SCOM)。</span><span class="sxs-lookup"><span data-stu-id="e8547-242">Install hello [Alert Management solution](log-analytics-solution-alert-management.md) tooanalyze alerts created in Log Analytics along with alerts collected from System Center Operations Manager (SCOM).</span></span>
* <span data-ttu-id="e8547-243">深入了解可產生警示的 [記錄檔搜尋](log-analytics-log-searches.md) 。</span><span class="sxs-lookup"><span data-stu-id="e8547-243">Read more about [log searches](log-analytics-log-searches.md) that can generate alerts.</span></span>
* <span data-ttu-id="e8547-244">完成 [設定 Webook](log-analytics-alerts-webhooks.md) 和警示規則的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="e8547-244">Complete a walkthrough for [configuring a webook](log-analytics-alerts-webhooks.md) with an alert rule.</span></span>  
* <span data-ttu-id="e8547-245">深入了解如何 toowrite [Azure 自動化中的 runbook](https://azure.microsoft.com/documentation/services/automation) tooremediate 警示所識別的問題。</span><span class="sxs-lookup"><span data-stu-id="e8547-245">Learn how toowrite [runbooks in Azure Automation](https://azure.microsoft.com/documentation/services/automation) tooremediate problems identified by alerts.</span></span>

