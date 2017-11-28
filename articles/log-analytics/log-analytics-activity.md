---
title: "使用 Log Analytics 檢視 Azure 活動記錄 | Microsoft Docs"
description: "您可以使用 Azure 活動記錄解決方案來分析和搜尋所有 Azure 訂用帳戶的 Azure 活動記錄。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 1ad56a54f094f3c314596b3a7c9fecd09647d065
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="view-azure-activity-logs"></a><span data-ttu-id="21f3c-103">檢視 Azure 活動記錄</span><span class="sxs-lookup"><span data-stu-id="21f3c-103">View Azure activity logs</span></span>

![Azure 活動記錄符號](./media/log-analytics-activity/activity-log-analytics.png)

<span data-ttu-id="21f3c-105">活動記錄分析解決方案可協助您分析和搜尋所有 Azure 訂用帳戶的 [Azure 活動記錄](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)。</span><span class="sxs-lookup"><span data-stu-id="21f3c-105">The Activity Log Analytics solution helps you analyze and search the [Azure activity log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) across all your Azure subscriptions.</span></span> <span data-ttu-id="21f3c-106">Azure 活動記錄能為您提供訂用帳戶中的資源所執行的作業有關的深入解析。</span><span class="sxs-lookup"><span data-stu-id="21f3c-106">The Azure Activity Log is a log that offers insights into the operations performed on resources in your subscriptions.</span></span> <span data-ttu-id="21f3c-107">活動記錄檔之前稱為「稽核記錄」或「作業記錄」，因為它會報告訂用帳戶的事件。</span><span class="sxs-lookup"><span data-stu-id="21f3c-107">The Activity Log was previously known as *Audit Logs* or *Operational Logs* since it reports events for your subscriptions.</span></span>

<span data-ttu-id="21f3c-108">您可以使用活動記錄檔來判斷訂用帳戶中的資源上任何寫入作業 (PUT、POST、DELETE) 的「*內容*」、「對象」和「時間」。</span><span class="sxs-lookup"><span data-stu-id="21f3c-108">Using the Activity Log, you can determine the *what*, *who*, and *when* for any write operations (PUT, POST, DELETE) made for the resources in your subscription.</span></span> <span data-ttu-id="21f3c-109">您也可以了解作業的狀態和其他相關屬性。</span><span class="sxs-lookup"><span data-stu-id="21f3c-109">You can also understand the status of the operations and other relevant properties.</span></span> <span data-ttu-id="21f3c-110">活動記錄不包含讀取 (GET) 作業，或使用傳統部署模型的資源有關的作業。</span><span class="sxs-lookup"><span data-stu-id="21f3c-110">The Activity Log does not include read (GET) operations or operations for resources that use the Classic deployment model.</span></span>

<span data-ttu-id="21f3c-111">您將 Azure 活動記錄連接至 Log Analytics 時，可以︰</span><span class="sxs-lookup"><span data-stu-id="21f3c-111">When you connect your Azure activity logs to Log Analytics, you can:</span></span>

- <span data-ttu-id="21f3c-112">使用預先定義檢視分析活動記錄</span><span class="sxs-lookup"><span data-stu-id="21f3c-112">Analyze the activity logs with pre-defined views</span></span>
- <span data-ttu-id="21f3c-113">分析和搜尋多個 Azure 訂用帳戶的活動記錄</span><span class="sxs-lookup"><span data-stu-id="21f3c-113">Analyze and search and activity logs from multiple Azure subscriptions</span></span>
- <span data-ttu-id="21f3c-114">保留活動記錄超過 90 天<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="21f3c-114">Keep activity logs for longer than 90 days<sup>1</sup></span></span>
- <span data-ttu-id="21f3c-115">使活動記錄與其他 Azure 平台和應用程式資料產生關聯</span><span class="sxs-lookup"><span data-stu-id="21f3c-115">Correlate activity logs with other Azure platform and application data</span></span>
- <span data-ttu-id="21f3c-116">請參閱依狀態彙總的作業活動</span><span class="sxs-lookup"><span data-stu-id="21f3c-116">See operational activities aggregated by status</span></span>
- <span data-ttu-id="21f3c-117">檢視每個 Azure 服務發生的活動所呈現的趨勢</span><span class="sxs-lookup"><span data-stu-id="21f3c-117">View trends of activities happening on each of your Azure services</span></span>
- <span data-ttu-id="21f3c-118">報告所有 Azure 資源的授權變更</span><span class="sxs-lookup"><span data-stu-id="21f3c-118">Report on authorization changes on all your Azure resources</span></span>
- <span data-ttu-id="21f3c-119">找出影響資源的中斷或服務健全狀況問題</span><span class="sxs-lookup"><span data-stu-id="21f3c-119">Identify outage or service health issues impacting your resources</span></span>
- <span data-ttu-id="21f3c-120">使用記錄搜尋使使用者活動、 自動調整作業、授權變更和服務健全狀況與您環境的其他記錄或度量資訊產生關聯</span><span class="sxs-lookup"><span data-stu-id="21f3c-120">Use Log Search to correlate user activities, auto-scale operations, authorization changes, and service health to other logs or metrics from your environment</span></span>

<span data-ttu-id="21f3c-121"><sup>1</sup>Log Analytics 預設會保留 Azure 活動記錄 90 天，即使您在免費層也是如此。</span><span class="sxs-lookup"><span data-stu-id="21f3c-121"><sup>1</sup>By default, Log Analytics keeps your Azure activity logs for 90 days, even if you are on the Free tier.</span></span> <span data-ttu-id="21f3c-122">或者，如果您有少於 90 天的工作區中保留期設定。</span><span class="sxs-lookup"><span data-stu-id="21f3c-122">Or, if you have a workspace retention setting of less than 90 days.</span></span> <span data-ttu-id="21f3c-123">如果工作區的保留期超過 90 天，工作區的保留期即為保留活動記錄的期間。</span><span class="sxs-lookup"><span data-stu-id="21f3c-123">If your workspace has retention that is longer than 90 days, the activity logs are kept for the retention period of your workspace.</span></span>

<span data-ttu-id="21f3c-124">Log Analytics 會免費收集活動記錄，並免費儲存記錄 90 天。</span><span class="sxs-lookup"><span data-stu-id="21f3c-124">Log Analytics collects activity logs free of charge and stores the logs for 90 days free of charge.</span></span> <span data-ttu-id="21f3c-125">如果儲存記錄超過 90 天，對於儲存超過 90 天的資料將產生資料保留期費用。</span><span class="sxs-lookup"><span data-stu-id="21f3c-125">If you store logs for longer than 90 days, you will incur data retention charges for the data stored longer than 90 days.</span></span>

<span data-ttu-id="21f3c-126">您在免費定價層時，活動記錄不適用於每日資料耗用量。</span><span class="sxs-lookup"><span data-stu-id="21f3c-126">When you're on the Free pricing tier, activity logs do not apply to your daily data consumption.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="21f3c-127">連接的來源</span><span class="sxs-lookup"><span data-stu-id="21f3c-127">Connected sources</span></span>

<span data-ttu-id="21f3c-128">不同於大部分其他 Log Analytics 解決方案，代理程式不會收集活動記錄的資料。</span><span class="sxs-lookup"><span data-stu-id="21f3c-128">Unlike most other Log Analytics solutions, data isn't collected for activity logs by agents.</span></span> <span data-ttu-id="21f3c-129">解決方案使用的所有資料直接來自於 Azure。</span><span class="sxs-lookup"><span data-stu-id="21f3c-129">All data used by the solution comes directly from Azure.</span></span>

| <span data-ttu-id="21f3c-130">連接的來源</span><span class="sxs-lookup"><span data-stu-id="21f3c-130">Connected Source</span></span> | <span data-ttu-id="21f3c-131">支援</span><span class="sxs-lookup"><span data-stu-id="21f3c-131">Supported</span></span> | <span data-ttu-id="21f3c-132">說明</span><span class="sxs-lookup"><span data-stu-id="21f3c-132">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="21f3c-133">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="21f3c-133">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="21f3c-134">否</span><span class="sxs-lookup"><span data-stu-id="21f3c-134">No</span></span> | <span data-ttu-id="21f3c-135">解決方案不會收集來自 Windows 代理程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="21f3c-135">The solution does not collect information from Windows agents.</span></span> |
| [<span data-ttu-id="21f3c-136">Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="21f3c-136">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="21f3c-137">否</span><span class="sxs-lookup"><span data-stu-id="21f3c-137">No</span></span> | <span data-ttu-id="21f3c-138">解決方案不會收集來自 Linux 代理程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="21f3c-138">The solution does not collect information from Linux agents.</span></span> |
| [<span data-ttu-id="21f3c-139">SCOM 管理群組</span><span class="sxs-lookup"><span data-stu-id="21f3c-139">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="21f3c-140">否</span><span class="sxs-lookup"><span data-stu-id="21f3c-140">No</span></span> | <span data-ttu-id="21f3c-141">解決方案不會收集來自連線 SCOM 管理群組的代理程式之中的資訊。</span><span class="sxs-lookup"><span data-stu-id="21f3c-141">The solution does not collect information from agents in a connected SCOM management group.</span></span> |
| [<span data-ttu-id="21f3c-142">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="21f3c-142">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="21f3c-143">否</span><span class="sxs-lookup"><span data-stu-id="21f3c-143">No</span></span> | <span data-ttu-id="21f3c-144">解決方案不會收集來自 Azure 儲存體的資訊。</span><span class="sxs-lookup"><span data-stu-id="21f3c-144">The solution does not collect information from Azure storage.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="21f3c-145">必要條件</span><span class="sxs-lookup"><span data-stu-id="21f3c-145">Prerequisites</span></span>

- <span data-ttu-id="21f3c-146">若要存取 Azure 活動記錄資訊，您必須有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="21f3c-146">To access Azure activity log information, you must have an Azure subscription.</span></span>

## <a name="configuration"></a><span data-ttu-id="21f3c-147">組態</span><span class="sxs-lookup"><span data-stu-id="21f3c-147">Configuration</span></span>

<span data-ttu-id="21f3c-148">執行下列步驟來設定您工作區的 Activity Log Analytics 解決方案。</span><span class="sxs-lookup"><span data-stu-id="21f3c-148">Perform the following steps to configure the Activity Log Analytics solution for your workspaces.</span></span>

1. <span data-ttu-id="21f3c-149">從 [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) 或使用[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)中所述的程序，啟用 Activity Log Analytics 解決方案。</span><span class="sxs-lookup"><span data-stu-id="21f3c-149">Enable the Activity Log Analytics solution from the [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="21f3c-150">設定活動記錄移至您的 Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="21f3c-150">Configure activity logs to go to your Log Analytics workspace.</span></span>
    1. <span data-ttu-id="21f3c-151">在 Azure 網站中，選取您的工作區，然後按一下 [Azure 活動記錄]。</span><span class="sxs-lookup"><span data-stu-id="21f3c-151">In the Azure portal, select your workspace and then click **Azure Activity log**.</span></span>
    2. <span data-ttu-id="21f3c-152">對於每個訂用帳戶，按一下訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="21f3c-152">For each subscription, click the subscription name.</span></span>  
        ![新增訂用帳戶](./media/log-analytics-activity/add-subscription.png)
    3. <span data-ttu-id="21f3c-154">在 [SubscriptionName] 刀鋒視窗中，按一下 [連接]。</span><span class="sxs-lookup"><span data-stu-id="21f3c-154">In the *SubscriptionName* blade, click **Connect**.</span></span>  
        <span data-ttu-id="21f3c-155">![connect subscription](./media/log-analytics-activity/subscription-connect.png)</span><span class="sxs-lookup"><span data-stu-id="21f3c-155">![connect subscription](./media/log-analytics-activity/subscription-connect.png)</span></span>

<span data-ttu-id="21f3c-156">如果您使用 OMS 入口網站新增解決方案，會看見下列圖格。</span><span class="sxs-lookup"><span data-stu-id="21f3c-156">If you add the solution using the OMS portal, you'll see the following tile.</span></span> <span data-ttu-id="21f3c-157">登入 Azure 入口網站，將 Azure 訂用帳戶連接至您的工作區。</span><span class="sxs-lookup"><span data-stu-id="21f3c-157">Sign in to the Azure portal to connect an Azure subscription to your workspace.</span></span>  
![執行評估](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-the-solution"></a><span data-ttu-id="21f3c-159">使用解決方案</span><span class="sxs-lookup"><span data-stu-id="21f3c-159">Using the solution</span></span>

<span data-ttu-id="21f3c-160">您將 Activity Log Analytics 解決方案新增至您的工作區時，**Azure 活動記錄**圖格會新增至概觀儀表板。</span><span class="sxs-lookup"><span data-stu-id="21f3c-160">When you add the Activity Log Analytics solution to your workspace, the **Azure Activity Logs** tile is added to your Overview dashboard.</span></span> <span data-ttu-id="21f3c-161">此圖格會顯示解決方案存取的訂用帳戶有關的 Azure 活動記錄數目計數。</span><span class="sxs-lookup"><span data-stu-id="21f3c-161">This tile displays a count of the number of Azure activity records for the Azure subscriptions that the solution has access to.</span></span>

![Azure 活動記錄圖格](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a><span data-ttu-id="21f3c-163">檢視 Azure 活動記錄</span><span class="sxs-lookup"><span data-stu-id="21f3c-163">View Azure Activity logs</span></span>

<span data-ttu-id="21f3c-164">按一下 [Azure 活動記錄] 圖格以開啟 [Azure 活動記錄] 儀表板。</span><span class="sxs-lookup"><span data-stu-id="21f3c-164">Click the **Azure Activity Logs** tile to open the **Azure Activity Logs** dashboard.</span></span> <span data-ttu-id="21f3c-165">此儀表板包含下表中的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="21f3c-165">The dashboard includes the blades in the following table.</span></span> <span data-ttu-id="21f3c-166">每個刀鋒視窗最多會列出 10 個與該刀鋒視窗中指定範圍和時間範圍的準則相符的項目。</span><span class="sxs-lookup"><span data-stu-id="21f3c-166">Each blade lists up to 10 items matching that blade's criteria for the specified scope and time range.</span></span> <span data-ttu-id="21f3c-167">您可以按一下刀鋒視窗底部的 [查看全部]，或按一下刀鋒視窗標頭，以執行記錄搜尋來傳回所有記錄。</span><span class="sxs-lookup"><span data-stu-id="21f3c-167">You can run a log search that returns all records by clicking **See all** at the bottom of the blade or by clicking the blade header.</span></span>

<span data-ttu-id="21f3c-168">您已設定您的活動記錄移至解決方案*之後*，活動記錄資料才會出現，因此您在此之前無法檢視資料。</span><span class="sxs-lookup"><span data-stu-id="21f3c-168">Activity log data only appears *after* you've configured your activity logs to go to the solution, so you can't view data before then.</span></span>

| <span data-ttu-id="21f3c-169">刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="21f3c-169">Blade</span></span> | <span data-ttu-id="21f3c-170">說明</span><span class="sxs-lookup"><span data-stu-id="21f3c-170">Description</span></span> |
| --- | --- |
| <span data-ttu-id="21f3c-171">Azure 活動記錄項目</span><span class="sxs-lookup"><span data-stu-id="21f3c-171">Azure Activity Log Entries</span></span> | <span data-ttu-id="21f3c-172">對於您選取的日期範圍，顯示最上方 Azure 活動記錄項目記錄總計的長條圖，並顯示前 10 個活動呼叫端的清單。</span><span class="sxs-lookup"><span data-stu-id="21f3c-172">Shows a bar chart of the top Azure activity log entry record totals for the date range that you have selected and shows a list of the top 10 activity callers.</span></span> <span data-ttu-id="21f3c-173">按一下橫條圖，若要執行的記錄搜尋<code>Type=AzureActivity</code>。</span><span class="sxs-lookup"><span data-stu-id="21f3c-173">Click the bar chart to run a log search for <code>Type=AzureActivity</code>.</span></span> <span data-ttu-id="21f3c-174">按一下呼叫端項目執行記錄搜尋，傳回該項目的所有活動記錄項目。</span><span class="sxs-lookup"><span data-stu-id="21f3c-174">Click a caller item to run a log search returning all activity log entries for that item.</span></span> |
| <span data-ttu-id="21f3c-175">依狀態列出的活動記錄</span><span class="sxs-lookup"><span data-stu-id="21f3c-175">Activity Logs by Status</span></span> | <span data-ttu-id="21f3c-176">對於您選取的日期範圍，顯示 Azure 活動記錄狀態的環圈圖。</span><span class="sxs-lookup"><span data-stu-id="21f3c-176">Shows a doughnut chart for Azure activity log status for the date range that you have selected.</span></span> <span data-ttu-id="21f3c-177">另外也顯示前 10 筆狀態記錄的清單。</span><span class="sxs-lookup"><span data-stu-id="21f3c-177">Also shows a list a list of the top ten status records.</span></span> <span data-ttu-id="21f3c-178">按一下圖表，即可執行的記錄搜尋<code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>。</span><span class="sxs-lookup"><span data-stu-id="21f3c-178">Click the chart to run a log search for <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>.</span></span> <span data-ttu-id="21f3c-179">按一下狀態項目執行記錄搜尋，傳回該狀態記錄的所有活動記錄項目。</span><span class="sxs-lookup"><span data-stu-id="21f3c-179">Click a status item to run a log search returning all activity log entries for that status record.</span></span> |
| <span data-ttu-id="21f3c-180">依資源列出的活動記錄</span><span class="sxs-lookup"><span data-stu-id="21f3c-180">Activity Logs by Resource</span></span> | <span data-ttu-id="21f3c-181">顯示活動記錄的資源總數，並對於各個資源列出記錄計數的前 10 個資源。</span><span class="sxs-lookup"><span data-stu-id="21f3c-181">Shows the total number of resources with activity logs and lists the top ten resources with record counts for each resource.</span></span> <span data-ttu-id="21f3c-182">按一下要執行記錄檔中的搜尋的總區域<code>Type=AzureActivity &#124; measure count() by Resource</code>，其中顯示所有的 Azure 資源可用方案。</span><span class="sxs-lookup"><span data-stu-id="21f3c-182">Click the total area to run a log search for <code>Type=AzureActivity &#124; measure count() by Resource</code>, which shows all Azure resources available to the solution.</span></span> <span data-ttu-id="21f3c-183">按一下資源來執行記錄搜尋，以傳回該資源的所有活動記錄。</span><span class="sxs-lookup"><span data-stu-id="21f3c-183">Click a resource to run a log search returning all activity records for that resource.</span></span> |
| <span data-ttu-id="21f3c-184">依資源提供者列出的活動記錄</span><span class="sxs-lookup"><span data-stu-id="21f3c-184">Activity Logs by Resource Provider</span></span> | <span data-ttu-id="21f3c-185">顯示產生活動記錄的資源提供者總數，並列出前 10 個。</span><span class="sxs-lookup"><span data-stu-id="21f3c-185">Shows the total number of resource providers that produce activity logs and lists the top ten.</span></span> <span data-ttu-id="21f3c-186">按一下要執行記錄檔中的搜尋的總區域<code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>，其中顯示所有的 Azure 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="21f3c-186">Click the total area to run a log search for <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, which shows all Azure resource providers.</span></span> <span data-ttu-id="21f3c-187">按一下資源提供者執行記錄搜尋，以傳回提供者的所有活動記錄。</span><span class="sxs-lookup"><span data-stu-id="21f3c-187">Click a resource provider to run a log search returning all activity records for the provider.</span></span> |

![Azure 活動記錄儀表板](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a><span data-ttu-id="21f3c-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="21f3c-189">Next steps</span></span>

- <span data-ttu-id="21f3c-190">特定活動時建立[警示](log-analytics-alerts-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="21f3c-190">Create an [alert](log-analytics-alerts-creating.md) when a specific activity happens.</span></span>
- <span data-ttu-id="21f3c-191">使用[記錄搜尋](log-analytics-log-searches.md)檢視活動記錄的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="21f3c-191">Use [Log Search](log-analytics-log-searches.md) to view detailed information from your activity logs.</span></span>
