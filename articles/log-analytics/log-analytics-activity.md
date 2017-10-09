---
title: "aaaView Azure 活動記錄檔記錄分析 |Microsoft 文件"
description: "您可以在所有 Azure 訂閱使用 hello Azure 活動記錄檔方案 tooanalyze 和搜尋 hello Azure 活動記錄檔。"
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
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a><span data-ttu-id="07125-103">檢視 Azure 活動記錄</span><span class="sxs-lookup"><span data-stu-id="07125-103">View Azure activity logs</span></span>

![Azure 活動記錄符號](./media/log-analytics-activity/activity-log-analytics.png)

<span data-ttu-id="07125-105">hello 活動記錄分析解決方案可協助您分析及搜尋 hello [Azure 活動記錄檔](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)跨所有您 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07125-105">hello Activity Log Analytics solution helps you analyze and search hello [Azure activity log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) across all your Azure subscriptions.</span></span> <span data-ttu-id="07125-106">hello Azure 活動記錄檔是可提供深入了解您的訂用帳戶中的資源上所執行的 hello 作業記錄。</span><span class="sxs-lookup"><span data-stu-id="07125-106">hello Azure Activity Log is a log that offers insights into hello operations performed on resources in your subscriptions.</span></span> <span data-ttu-id="07125-107">hello 活動記錄檔先前稱為*稽核記錄檔*或*操作記錄檔*因為它會報告訂用帳戶的事件。</span><span class="sxs-lookup"><span data-stu-id="07125-107">hello Activity Log was previously known as *Audit Logs* or *Operational Logs* since it reports events for your subscriptions.</span></span>

<span data-ttu-id="07125-108">使用 hello 活動記錄檔，您可以決定 hello*什麼*，*人員*，和*時*的任何寫入作業 (PUT、 POST、 DELETE) 對您的訂用帳戶中的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="07125-108">Using hello Activity Log, you can determine hello *what*, *who*, and *when* for any write operations (PUT, POST, DELETE) made for hello resources in your subscription.</span></span> <span data-ttu-id="07125-109">您也可以了解 hello 狀態 hello 作業和其他相關屬性。</span><span class="sxs-lookup"><span data-stu-id="07125-109">You can also understand hello status of hello operations and other relevant properties.</span></span> <span data-ttu-id="07125-110">hello 活動記錄檔不包括讀取 (GET) 作業或作業，以使用 hello 傳統部署模型的資源。</span><span class="sxs-lookup"><span data-stu-id="07125-110">hello Activity Log does not include read (GET) operations or operations for resources that use hello Classic deployment model.</span></span>

<span data-ttu-id="07125-111">當您連接您的 Azure 活動記錄檔 tooLog 分析時，您可以：</span><span class="sxs-lookup"><span data-stu-id="07125-111">When you connect your Azure activity logs tooLog Analytics, you can:</span></span>

- <span data-ttu-id="07125-112">分析 hello 與預先定義檢視的活動記錄檔</span><span class="sxs-lookup"><span data-stu-id="07125-112">Analyze hello activity logs with pre-defined views</span></span>
- <span data-ttu-id="07125-113">分析和搜尋多個 Azure 訂用帳戶的活動記錄</span><span class="sxs-lookup"><span data-stu-id="07125-113">Analyze and search and activity logs from multiple Azure subscriptions</span></span>
- <span data-ttu-id="07125-114">保留活動記錄超過 90 天<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="07125-114">Keep activity logs for longer than 90 days<sup>1</sup></span></span>
- <span data-ttu-id="07125-115">使活動記錄與其他 Azure 平台和應用程式資料產生關聯</span><span class="sxs-lookup"><span data-stu-id="07125-115">Correlate activity logs with other Azure platform and application data</span></span>
- <span data-ttu-id="07125-116">請參閱依狀態彙總的作業活動</span><span class="sxs-lookup"><span data-stu-id="07125-116">See operational activities aggregated by status</span></span>
- <span data-ttu-id="07125-117">檢視每個 Azure 服務發生的活動所呈現的趨勢</span><span class="sxs-lookup"><span data-stu-id="07125-117">View trends of activities happening on each of your Azure services</span></span>
- <span data-ttu-id="07125-118">報告所有 Azure 資源的授權變更</span><span class="sxs-lookup"><span data-stu-id="07125-118">Report on authorization changes on all your Azure resources</span></span>
- <span data-ttu-id="07125-119">找出影響資源的中斷或服務健全狀況問題</span><span class="sxs-lookup"><span data-stu-id="07125-119">Identify outage or service health issues impacting your resources</span></span>
- <span data-ttu-id="07125-120">使用記錄搜尋 toocorrelate 使用者活動、 自動調整規模作業、 授權變更和服務健全狀況 tooother 記錄檔或從您的環境的度量</span><span class="sxs-lookup"><span data-stu-id="07125-120">Use Log Search toocorrelate user activities, auto-scale operations, authorization changes, and service health tooother logs or metrics from your environment</span></span>

<span data-ttu-id="07125-121"><sup>1</sup>根據預設，記錄分析會保留您 Azure 活動記錄檔之 90 天，即使您是在 hello 免費層。</span><span class="sxs-lookup"><span data-stu-id="07125-121"><sup>1</sup>By default, Log Analytics keeps your Azure activity logs for 90 days, even if you are on hello Free tier.</span></span> <span data-ttu-id="07125-122">或者，如果您有少於 90 天的工作區中保留期設定。</span><span class="sxs-lookup"><span data-stu-id="07125-122">Or, if you have a workspace retention setting of less than 90 days.</span></span> <span data-ttu-id="07125-123">如果您的工作區中有超過 90 天的保留，hello 活動記錄檔會保留工作區的 hello 保留週期。</span><span class="sxs-lookup"><span data-stu-id="07125-123">If your workspace has retention that is longer than 90 days, hello activity logs are kept for hello retention period of your workspace.</span></span>

<span data-ttu-id="07125-124">記錄分析會收集免費提供的活動記錄檔，並儲存 90 天的免費的 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="07125-124">Log Analytics collects activity logs free of charge and stores hello logs for 90 days free of charge.</span></span> <span data-ttu-id="07125-125">如果您儲存的時間超過 90 天的記錄檔，就會發生資料保留 hello 資料儲存時間超過 90 天的費用。</span><span class="sxs-lookup"><span data-stu-id="07125-125">If you store logs for longer than 90 days, you will incur data retention charges for hello data stored longer than 90 days.</span></span>

<span data-ttu-id="07125-126">當您在免費定價層的 hello 時，活動記錄檔不會套用 tooyour 每日的資料使用。</span><span class="sxs-lookup"><span data-stu-id="07125-126">When you're on hello Free pricing tier, activity logs do not apply tooyour daily data consumption.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="07125-127">連接的來源</span><span class="sxs-lookup"><span data-stu-id="07125-127">Connected sources</span></span>

<span data-ttu-id="07125-128">不同於大部分其他 Log Analytics 解決方案，代理程式不會收集活動記錄的資料。</span><span class="sxs-lookup"><span data-stu-id="07125-128">Unlike most other Log Analytics solutions, data isn't collected for activity logs by agents.</span></span> <span data-ttu-id="07125-129">Hello 方案所使用的所有資料都是直接來自 Azure。</span><span class="sxs-lookup"><span data-stu-id="07125-129">All data used by hello solution comes directly from Azure.</span></span>

| <span data-ttu-id="07125-130">連接的來源</span><span class="sxs-lookup"><span data-stu-id="07125-130">Connected Source</span></span> | <span data-ttu-id="07125-131">支援</span><span class="sxs-lookup"><span data-stu-id="07125-131">Supported</span></span> | <span data-ttu-id="07125-132">說明</span><span class="sxs-lookup"><span data-stu-id="07125-132">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="07125-133">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="07125-133">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="07125-134">否</span><span class="sxs-lookup"><span data-stu-id="07125-134">No</span></span> | <span data-ttu-id="07125-135">hello 方案不會從 Windows 代理程式收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="07125-135">hello solution does not collect information from Windows agents.</span></span> |
| [<span data-ttu-id="07125-136">Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="07125-136">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="07125-137">否</span><span class="sxs-lookup"><span data-stu-id="07125-137">No</span></span> | <span data-ttu-id="07125-138">hello 解決方案不會收集從 Linux 代理程式的資訊。</span><span class="sxs-lookup"><span data-stu-id="07125-138">hello solution does not collect information from Linux agents.</span></span> |
| [<span data-ttu-id="07125-139">SCOM 管理群組</span><span class="sxs-lookup"><span data-stu-id="07125-139">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="07125-140">否</span><span class="sxs-lookup"><span data-stu-id="07125-140">No</span></span> | <span data-ttu-id="07125-141">hello 方案不會從已連線的 SCOM 管理群組中的代理程式收集的資訊。</span><span class="sxs-lookup"><span data-stu-id="07125-141">hello solution does not collect information from agents in a connected SCOM management group.</span></span> |
| [<span data-ttu-id="07125-142">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="07125-142">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="07125-143">否</span><span class="sxs-lookup"><span data-stu-id="07125-143">No</span></span> | <span data-ttu-id="07125-144">hello 方案並不會收集自 Azure 儲存體資訊。</span><span class="sxs-lookup"><span data-stu-id="07125-144">hello solution does not collect information from Azure storage.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="07125-145">必要條件</span><span class="sxs-lookup"><span data-stu-id="07125-145">Prerequisites</span></span>

- <span data-ttu-id="07125-146">tooaccess Azure 活動記錄檔資訊，您必須具有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="07125-146">tooaccess Azure activity log information, you must have an Azure subscription.</span></span>

## <a name="configuration"></a><span data-ttu-id="07125-147">組態</span><span class="sxs-lookup"><span data-stu-id="07125-147">Configuration</span></span>

<span data-ttu-id="07125-148">執行下列步驟 tooconfigure hello 您工作區的活動記錄分析解決方案的 hello。</span><span class="sxs-lookup"><span data-stu-id="07125-148">Perform hello following steps tooconfigure hello Activity Log Analytics solution for your workspaces.</span></span>

1. <span data-ttu-id="07125-149">啟用從 hello hello 活動記錄分析解決方案[Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="07125-149">Enable hello Activity Log Analytics solution from hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="07125-150">設定活動記錄檔 toogo tooyour 記錄分析工作區。</span><span class="sxs-lookup"><span data-stu-id="07125-150">Configure activity logs toogo tooyour Log Analytics workspace.</span></span>
    1. <span data-ttu-id="07125-151">在 hello Azure 入口網站，選取您的工作區，然後按一下**Azure 活動記錄檔**。</span><span class="sxs-lookup"><span data-stu-id="07125-151">In hello Azure portal, select your workspace and then click **Azure Activity log**.</span></span>
    2. <span data-ttu-id="07125-152">每個訂用帳戶中，按一下 hello 訂用帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="07125-152">For each subscription, click hello subscription name.</span></span>  
        ![新增訂用帳戶](./media/log-analytics-activity/add-subscription.png)
    3. <span data-ttu-id="07125-154">在 hello*訂用帳戶名稱*刀鋒視窗中，按一下 **連接**。</span><span class="sxs-lookup"><span data-stu-id="07125-154">In hello *SubscriptionName* blade, click **Connect**.</span></span>  
        <span data-ttu-id="07125-155">![connect subscription](./media/log-analytics-activity/subscription-connect.png)</span><span class="sxs-lookup"><span data-stu-id="07125-155">![connect subscription](./media/log-analytics-activity/subscription-connect.png)</span></span>

<span data-ttu-id="07125-156">如果您新增使用 hello OMS 入口網站的 hello 解決方案，您會看到 hello 下列磚。</span><span class="sxs-lookup"><span data-stu-id="07125-156">If you add hello solution using hello OMS portal, you'll see hello following tile.</span></span> <span data-ttu-id="07125-157">登入 Azure 入口網站 tooconnect toohello 的 Azure 訂用帳戶 tooyour 工作區。</span><span class="sxs-lookup"><span data-stu-id="07125-157">Sign in toohello Azure portal tooconnect an Azure subscription tooyour workspace.</span></span>  
![執行評估](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a><span data-ttu-id="07125-159">使用 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="07125-159">Using hello solution</span></span>

<span data-ttu-id="07125-160">當您新增 hello 活動記錄分析解決方案 tooyour 工作區時，hello **Azure 活動記錄檔**tooyour 概觀儀表板的磚加入。</span><span class="sxs-lookup"><span data-stu-id="07125-160">When you add hello Activity Log Analytics solution tooyour workspace, hello **Azure Activity Logs** tile is added tooyour Overview dashboard.</span></span> <span data-ttu-id="07125-161">此磚會顯示 hello Azure 活動記錄的數目的計數的 hello hello 方案中有 Azure 訂用帳戶的存取。</span><span class="sxs-lookup"><span data-stu-id="07125-161">This tile displays a count of hello number of Azure activity records for hello Azure subscriptions that hello solution has access to.</span></span>

![Azure 活動記錄圖格](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a><span data-ttu-id="07125-163">檢視 Azure 活動記錄</span><span class="sxs-lookup"><span data-stu-id="07125-163">View Azure Activity logs</span></span>

<span data-ttu-id="07125-164">按一下 hello **Azure 活動記錄檔**磚 tooopen hello **Azure 活動記錄檔**儀表板。</span><span class="sxs-lookup"><span data-stu-id="07125-164">Click hello **Azure Activity Logs** tile tooopen hello **Azure Activity Logs** dashboard.</span></span> <span data-ttu-id="07125-165">hello 儀表板會納入 hello 下表中的 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="07125-165">hello dashboard includes hello blades in hello following table.</span></span> <span data-ttu-id="07125-166">每個刀鋒視窗會列出 too10 hello 刀鋒視窗的準則指定領域和時間範圍比對的項目。</span><span class="sxs-lookup"><span data-stu-id="07125-166">Each blade lists up too10 items matching that blade's criteria for hello specified scope and time range.</span></span> <span data-ttu-id="07125-167">您可以執行，即可傳回的所有記錄的記錄搜尋**查看所有**底部 hello 的 hello 刀鋒視窗，或按一下 hello 刀鋒視窗中的標頭。</span><span class="sxs-lookup"><span data-stu-id="07125-167">You can run a log search that returns all records by clicking **See all** at hello bottom of hello blade or by clicking hello blade header.</span></span>

<span data-ttu-id="07125-168">活動記錄資料，才會出現*之後*您設定活動記錄檔 toogo toohello 方案，所以您無法檢視資料之前。</span><span class="sxs-lookup"><span data-stu-id="07125-168">Activity log data only appears *after* you've configured your activity logs toogo toohello solution, so you can't view data before then.</span></span>

| <span data-ttu-id="07125-169">刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="07125-169">Blade</span></span> | <span data-ttu-id="07125-170">說明</span><span class="sxs-lookup"><span data-stu-id="07125-170">Description</span></span> |
| --- | --- |
| <span data-ttu-id="07125-171">Azure 活動記錄項目</span><span class="sxs-lookup"><span data-stu-id="07125-171">Azure Activity Log Entries</span></span> | <span data-ttu-id="07125-172">顯示的橫條圖的 hello 頂端 Azure 活動記錄檔項目記錄您選取的 hello 日期範圍內的總計，並顯示一份 hello 前 10 個活動呼叫端。</span><span class="sxs-lookup"><span data-stu-id="07125-172">Shows a bar chart of hello top Azure activity log entry record totals for hello date range that you have selected and shows a list of hello top 10 activity callers.</span></span> <span data-ttu-id="07125-173">按一下橫條圖 toorun hello 的記錄搜尋<code>Type=AzureActivity</code>。</span><span class="sxs-lookup"><span data-stu-id="07125-173">Click hello bar chart toorun a log search for <code>Type=AzureActivity</code>.</span></span> <span data-ttu-id="07125-174">按一下 呼叫端的項目 toorun 記錄搜尋，傳回所有活動記錄項目，該項目。</span><span class="sxs-lookup"><span data-stu-id="07125-174">Click a caller item toorun a log search returning all activity log entries for that item.</span></span> |
| <span data-ttu-id="07125-175">依狀態列出的活動記錄</span><span class="sxs-lookup"><span data-stu-id="07125-175">Activity Logs by Status</span></span> | <span data-ttu-id="07125-176">顯示您所選取的 hello 日期範圍內的 Azure 活動記錄狀態的環圈圖。</span><span class="sxs-lookup"><span data-stu-id="07125-176">Shows a doughnut chart for Azure activity log status for hello date range that you have selected.</span></span> <span data-ttu-id="07125-177">也會顯示清單 hello 前十個狀態記錄的清單。</span><span class="sxs-lookup"><span data-stu-id="07125-177">Also shows a list a list of hello top ten status records.</span></span> <span data-ttu-id="07125-178">按一下 記錄搜尋 hello 圖表 toorun <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>。</span><span class="sxs-lookup"><span data-stu-id="07125-178">Click hello chart toorun a log search for <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>.</span></span> <span data-ttu-id="07125-179">按一下狀態項目 toorun 記錄搜尋，傳回該狀態記錄的所有活動記錄檔項目。</span><span class="sxs-lookup"><span data-stu-id="07125-179">Click a status item toorun a log search returning all activity log entries for that status record.</span></span> |
| <span data-ttu-id="07125-180">依資源列出的活動記錄</span><span class="sxs-lookup"><span data-stu-id="07125-180">Activity Logs by Resource</span></span> | <span data-ttu-id="07125-181">顯示 hello 總數的活動記錄檔的資源，並列出 hello 前十個資源記錄會計算每個資源。</span><span class="sxs-lookup"><span data-stu-id="07125-181">Shows hello total number of resources with activity logs and lists hello top ten resources with record counts for each resource.</span></span> <span data-ttu-id="07125-182">按一下 記錄搜尋 hello 總面積 toorun <code>Type=AzureActivity &#124; measure count() by Resource</code>，其中顯示所有的 Azure 資源可用 toohello 解決方案。</span><span class="sxs-lookup"><span data-stu-id="07125-182">Click hello total area toorun a log search for <code>Type=AzureActivity &#124; measure count() by Resource</code>, which shows all Azure resources available toohello solution.</span></span> <span data-ttu-id="07125-183">按一下 資源 toorun 傳回該資源的所有活動記錄的記錄搜尋。</span><span class="sxs-lookup"><span data-stu-id="07125-183">Click a resource toorun a log search returning all activity records for that resource.</span></span> |
| <span data-ttu-id="07125-184">依資源提供者列出的活動記錄</span><span class="sxs-lookup"><span data-stu-id="07125-184">Activity Logs by Resource Provider</span></span> | <span data-ttu-id="07125-185">顯示 hello 總數產生活動的資源提供者記錄檔，並列出 hello 的前十個。</span><span class="sxs-lookup"><span data-stu-id="07125-185">Shows hello total number of resource providers that produce activity logs and lists hello top ten.</span></span> <span data-ttu-id="07125-186">按一下 記錄搜尋 hello 總面積 toorun <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>，其中顯示所有的 Azure 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="07125-186">Click hello total area toorun a log search for <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, which shows all Azure resource providers.</span></span> <span data-ttu-id="07125-187">按一下 [資源提供者 toorun 傳回 hello 提供者的所有活動記錄的記錄搜尋]。</span><span class="sxs-lookup"><span data-stu-id="07125-187">Click a resource provider toorun a log search returning all activity records for hello provider.</span></span> |

![Azure 活動記錄儀表板](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a><span data-ttu-id="07125-189">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07125-189">Next steps</span></span>

- <span data-ttu-id="07125-190">特定活動時建立[警示](log-analytics-alerts-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="07125-190">Create an [alert](log-analytics-alerts-creating.md) when a specific activity happens.</span></span>
- <span data-ttu-id="07125-191">使用[記錄搜尋](log-analytics-log-searches.md)tooview 的詳細資訊，從您的活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="07125-191">Use [Log Search](log-analytics-log-searches.md) tooview detailed information from your activity logs.</span></span>
