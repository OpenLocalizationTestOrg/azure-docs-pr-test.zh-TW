---
title: "Log Analytics 中的 Azure SQL Analytics 解決方案 | Microsoft Docs"
description: "Azure SQL Analytics 解決方案可協助您管理 Azure SQL Database。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: b2712749-1ded-40c4-b211-abc51cc65171
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: banders
ms.openlocfilehash: cab45cc6dd621eb4a95ef5f1842ec38c25e980b6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="59a3d-103">使用 Azure SQL Database (預覽) 監視 Log Analytics 中的 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="59a3d-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Azure SQL 分析符號](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="59a3d-105">Azure Log Analytics 中的 Azure SQL 分析解決方案會收集並以視覺化方式檢視重要的 SQL Azure 效能計量。</span><span class="sxs-lookup"><span data-stu-id="59a3d-105">The Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="59a3d-106">藉由使用您以解決方案收集的計量，您可以建立自訂的監視規則和警示。</span><span class="sxs-lookup"><span data-stu-id="59a3d-106">By using the metrics that you collect with the solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="59a3d-107">而且，您可以跨多個 Azure 訂用帳戶和彈性集區監視 Azure SQL Database 和彈性集區計量，並將其視覺化。</span><span class="sxs-lookup"><span data-stu-id="59a3d-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="59a3d-108">解決方案也可協助您找出應用程式堆疊中每個層級的問題。</span><span class="sxs-lookup"><span data-stu-id="59a3d-108">The solution also helps you to identify issues at each layer of your application stack.</span></span>  <span data-ttu-id="59a3d-109">它會使用 [Azure 診斷計量](log-analytics-azure-storage.md)與 Log Analytics 檢視來呈現單一 Log Analytics 工作區中所有 Azure SQL Database 和彈性集區的相關資料。</span><span class="sxs-lookup"><span data-stu-id="59a3d-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views to present data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="59a3d-110">目前，此預覽解決方案針對每個工作區支援高達 150,000 個 Azure SQL Database 和 5,000 個 SQL 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="59a3d-110">Currently, this preview solution supports up to 150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="59a3d-111">Azure SQL 分析解決方案，如同其他可用的 Log Analytics，可協助您監視並接收您 Azure 資源健康情況的相關通知，在此情況下為 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="59a3d-111">The Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about the health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="59a3d-112">Microsoft Azure SQL Database 是可調整的關聯式資料庫服務，可對 Azure 雲端中執行的應用程式提供熟悉的 SQL Server 類似功能。</span><span class="sxs-lookup"><span data-stu-id="59a3d-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities to applications running in the Azure cloud.</span></span> <span data-ttu-id="59a3d-113">Log Analytics 可協助您收集、相互關聯，並以視覺化方式檢視結構化和非結構化資料。</span><span class="sxs-lookup"><span data-stu-id="59a3d-113">Log Analytics helps you to collect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="59a3d-114">連接的來源</span><span class="sxs-lookup"><span data-stu-id="59a3d-114">Connected sources</span></span>

<span data-ttu-id="59a3d-115">Azure SQL 分析解決方案不使用代理程式連線至 Log Analytics 服務。</span><span class="sxs-lookup"><span data-stu-id="59a3d-115">The Azure SQL Analytics solution doesn't use agents to connect to the Log Analytics service.</span></span>

<span data-ttu-id="59a3d-116">下表描述此方案支援的連接來源。</span><span class="sxs-lookup"><span data-stu-id="59a3d-116">The following table describes the connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="59a3d-117">連接的來源</span><span class="sxs-lookup"><span data-stu-id="59a3d-117">Connected Source</span></span> | <span data-ttu-id="59a3d-118">支援</span><span class="sxs-lookup"><span data-stu-id="59a3d-118">Support</span></span> | <span data-ttu-id="59a3d-119">說明</span><span class="sxs-lookup"><span data-stu-id="59a3d-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="59a3d-120">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="59a3d-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="59a3d-121">否</span><span class="sxs-lookup"><span data-stu-id="59a3d-121">No</span></span> | <span data-ttu-id="59a3d-122">解決方案不使用直接 Windows 代理程式。</span><span class="sxs-lookup"><span data-stu-id="59a3d-122">Direct Windows agents are not used by the solution.</span></span> |
| [<span data-ttu-id="59a3d-123">Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="59a3d-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="59a3d-124">否</span><span class="sxs-lookup"><span data-stu-id="59a3d-124">No</span></span> | <span data-ttu-id="59a3d-125">解決方案不使用直接 Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="59a3d-125">Direct Linux agents are not used by the solution.</span></span> |
| [<span data-ttu-id="59a3d-126">SCOM 管理群組</span><span class="sxs-lookup"><span data-stu-id="59a3d-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="59a3d-127">否</span><span class="sxs-lookup"><span data-stu-id="59a3d-127">No</span></span> | <span data-ttu-id="59a3d-128">解決方案不使用從 SCOM 代理程式直接連線到 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="59a3d-128">A direct connection from the SCOM agent to Log Analytics is not used by the solution.</span></span> |
| [<span data-ttu-id="59a3d-129">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="59a3d-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="59a3d-130">否</span><span class="sxs-lookup"><span data-stu-id="59a3d-130">No</span></span> | <span data-ttu-id="59a3d-131">Log Analytics 不會從儲存體帳戶讀取資料。</span><span class="sxs-lookup"><span data-stu-id="59a3d-131">Log Analytics does not read the data from a storage account.</span></span> |
| [<span data-ttu-id="59a3d-132">Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="59a3d-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="59a3d-133">是</span><span class="sxs-lookup"><span data-stu-id="59a3d-133">Yes</span></span> | <span data-ttu-id="59a3d-134">Azure 會將 Azure 計量資料直接傳送至 Log Analytics。</span><span class="sxs-lookup"><span data-stu-id="59a3d-134">Azure metric data is sent to Log Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="59a3d-135">必要條件</span><span class="sxs-lookup"><span data-stu-id="59a3d-135">Prerequisites</span></span>

- <span data-ttu-id="59a3d-136">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="59a3d-136">An Azure Subscription.</span></span> <span data-ttu-id="59a3d-137">如果您沒有帳戶，您可以[免費](https://azure.microsoft.com/free/)建立一個。</span><span class="sxs-lookup"><span data-stu-id="59a3d-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="59a3d-138">Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="59a3d-138">A Log Analytics workspace.</span></span> <span data-ttu-id="59a3d-139">您可以使用現有的帳戶，或者您可以在開始使用此解決方案之前[建立一個新的](log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="59a3d-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="59a3d-140">針對您的 Azure SQL Database 和彈性集區啟用 Azure 診斷，並[將其設定為傳送資料至 Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="59a3d-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them to send their data to Log Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="59a3d-141">組態</span><span class="sxs-lookup"><span data-stu-id="59a3d-141">Configuration</span></span>

<span data-ttu-id="59a3d-142">執行下列步驟將 Azure SQL 分析解決方案新增至您的工作區。</span><span class="sxs-lookup"><span data-stu-id="59a3d-142">Perform the following steps to add the Azure SQL Analytics solution to your workspace.</span></span>

1. <span data-ttu-id="59a3d-143">從 [Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) 或使用[從方案庫新增 Log Analytics 方案](log-analytics-add-solutions.md)中所述的程序，將 Azure SQL Analytics 解決方案新增至您的工作區。</span><span class="sxs-lookup"><span data-stu-id="59a3d-143">Add the Azure SQL Analytics solution to your workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="59a3d-144">在 Azure 入口網站中，按一下 [新增] \(+ 符號)，然後在資源的清單中，選取 [監視 + 管理]。</span><span class="sxs-lookup"><span data-stu-id="59a3d-144">In the Azure portal, click **New** (the + symbol), then in the list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="59a3d-145">![監視 + 管理](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="59a3d-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="59a3d-146">在 [監視 + 管理] 清單中，按一下 [檢視全部]。</span><span class="sxs-lookup"><span data-stu-id="59a3d-146">In the **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="59a3d-147">在 [建議]清單中，按一下 [詳細]，然後在新的清單中，尋找 **Azure SQL 分析 (預覽)**，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="59a3d-147">In the **Recommended** list, click **More** , and then in the new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="59a3d-148">![Azure SQL 分析解決方案](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="59a3d-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="59a3d-149">在 **Azure SQL 分析 (預覽)** 刀鋒視窗中，按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="59a3d-149">In the **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="59a3d-150">![建立](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="59a3d-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="59a3d-151">在 [建立新方案] 刀鋒視窗中，選取您想要新增解決方案的工作區，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="59a3d-151">In the **Create new solution** blade, select the workspace that you want to add the solution to and then click **Create**.</span></span>  
    <span data-ttu-id="59a3d-152">![新增到工作區](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="59a3d-152">![add to workspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="to-configure-multiple-azure-subscriptions"></a><span data-ttu-id="59a3d-153">若要設定多個 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="59a3d-153">To configure multiple Azure subscriptions</span></span>

<span data-ttu-id="59a3d-154">若要支援多個訂用帳戶，從[使用 PowerShell 啟用 Azure 資源計量記錄](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)使用 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="59a3d-154">To support multiple subscriptions, use the PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="59a3d-155">當執行指令碼以將診斷資料從一個 Azure 訂用帳戶中的資源傳送至另一個 Azure 訂用帳戶中的工作區時，提供工作區資源識別碼做為參數。</span><span class="sxs-lookup"><span data-stu-id="59a3d-155">Provide the workspace resource ID as a parameter when executing the script to send diagnostic data from resources in one Azure subscription to a workspace in another Azure subscription.</span></span>

<span data-ttu-id="59a3d-156">**範例**</span><span class="sxs-lookup"><span data-stu-id="59a3d-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-the-solution"></a><span data-ttu-id="59a3d-157">使用解決方案</span><span class="sxs-lookup"><span data-stu-id="59a3d-157">Using the solution</span></span>

<span data-ttu-id="59a3d-158">當您將解決方案新增至您的工作區時，Azure SQL 分析圖格會新增至您的工作區，而且會顯示在 [概觀] 中。</span><span class="sxs-lookup"><span data-stu-id="59a3d-158">When you add the solution to your workspace, the Azure SQL Analytics tile is added to your workspace, and it appears in Overview.</span></span> <span data-ttu-id="59a3d-159">圖格會顯示 Azure SQL Database 和解決方案所連接之 Azure SQL 彈性集區的數目。</span><span class="sxs-lookup"><span data-stu-id="59a3d-159">The tile shows the number of Azure SQL databases and Azure SQL elastic pools that the solution is connected to.</span></span>

![Azure SQL 分析圖格](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="59a3d-161">檢視 Azure SQL 分析資料</span><span class="sxs-lookup"><span data-stu-id="59a3d-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="59a3d-162">按一下 [Azure SQL 分析] 圖格以開啟 Azure SQL 分析儀表板。</span><span class="sxs-lookup"><span data-stu-id="59a3d-162">Click on the **Azure SQL Analytics** tile to open the Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="59a3d-163">此儀表板包含下面定義的刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="59a3d-163">The dashboard includes the blades defined below.</span></span> <span data-ttu-id="59a3d-164">每個刀鋒視窗最多可列出 15 個資源 (訂用帳戶、伺服器、彈性集區及資料庫)。</span><span class="sxs-lookup"><span data-stu-id="59a3d-164">Each blade lists up to 15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="59a3d-165">按一下任何資源，以開啟該特定資源的儀表板。</span><span class="sxs-lookup"><span data-stu-id="59a3d-165">Click any of the resources to open the dashboard for that specific resource.</span></span> <span data-ttu-id="59a3d-166">彈性集區或資料庫包含的圖表具有所選資源的計量。</span><span class="sxs-lookup"><span data-stu-id="59a3d-166">Elastic Pool or Database contains the charts with metrics for a selected resource.</span></span> <span data-ttu-id="59a3d-167">按一下圖表，以開啟 [記錄搜尋] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="59a3d-167">Click a chart to open the Log Search dialog.</span></span>

| <span data-ttu-id="59a3d-168">刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="59a3d-168">Blade</span></span> | <span data-ttu-id="59a3d-169">說明</span><span class="sxs-lookup"><span data-stu-id="59a3d-169">Description</span></span> |
|---|---|
| <span data-ttu-id="59a3d-170">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="59a3d-170">Subscriptions</span></span> | <span data-ttu-id="59a3d-171">具有已連線伺服器、集區及資料庫數目的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="59a3d-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="59a3d-172">伺服器</span><span class="sxs-lookup"><span data-stu-id="59a3d-172">Servers</span></span> | <span data-ttu-id="59a3d-173">具有已連線集區和資料庫數目的伺服器清單。</span><span class="sxs-lookup"><span data-stu-id="59a3d-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="59a3d-174">彈性集區</span><span class="sxs-lookup"><span data-stu-id="59a3d-174">Elastic Pools</span></span> | <span data-ttu-id="59a3d-175">具有觀察期間內最大 GB 和 eDTU 的已連線彈性集區清單。</span><span class="sxs-lookup"><span data-stu-id="59a3d-175">List of connected elastic pools with maximum GB and eDTU in the observed period.</span></span> |
|<span data-ttu-id="59a3d-176">資料庫</span><span class="sxs-lookup"><span data-stu-id="59a3d-176">Databases</span></span> | <span data-ttu-id="59a3d-177">具有觀察期間內最大 GB 和 DTU 的已連線資料庫清單。</span><span class="sxs-lookup"><span data-stu-id="59a3d-177">List of connected databases with maximum GB and DTU in the observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="59a3d-178">分析資料並建立警示</span><span class="sxs-lookup"><span data-stu-id="59a3d-178">Analyze data and create alerts</span></span>

<span data-ttu-id="59a3d-179">您可以使用來自 Azure SQL Database 資源的資料，輕鬆建立警示。</span><span class="sxs-lookup"><span data-stu-id="59a3d-179">You can easily create alerts with the data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="59a3d-180">以下是您可用於警示的一些實用[記錄搜尋](log-analytics-log-searches.md)查詢：</span><span class="sxs-lookup"><span data-stu-id="59a3d-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="59a3d-181">Azure SQL Database 上的高 DTU</span><span class="sxs-lookup"><span data-stu-id="59a3d-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="59a3d-182">Azure SQL Database 彈性集區上的高 DTU</span><span class="sxs-lookup"><span data-stu-id="59a3d-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="59a3d-183">您可以針對 Azure SQL Database 和彈性集區，使用這些警示型查詢發出特定閾值警示。</span><span class="sxs-lookup"><span data-stu-id="59a3d-183">You can use these alert-based queries to alert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="59a3d-184">若要設定您 OMS 工作區的警示：</span><span class="sxs-lookup"><span data-stu-id="59a3d-184">To configure an alert for your OMS workspace:</span></span>

#### <a name="to-configure-an-alert-for-your-workspace"></a><span data-ttu-id="59a3d-185">若要設定您工作區的警示</span><span class="sxs-lookup"><span data-stu-id="59a3d-185">To configure an alert for your workspace</span></span>

1. <span data-ttu-id="59a3d-186">前往 [OMS 入口網站](http://mms.microsoft.com/)並登入。</span><span class="sxs-lookup"><span data-stu-id="59a3d-186">Go to the [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="59a3d-187">開啟您針對解決方案所設定之工作區。</span><span class="sxs-lookup"><span data-stu-id="59a3d-187">Open the workspace that you have configured for the solution.</span></span>
3. <span data-ttu-id="59a3d-188">在 [概觀] 頁面上，按一下 [Azure SQL 分析 (預覽)] 圖格。</span><span class="sxs-lookup"><span data-stu-id="59a3d-188">On the Overview page, click the **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="59a3d-189">執行其中一個範例查詢。</span><span class="sxs-lookup"><span data-stu-id="59a3d-189">Run one of the example queries.</span></span>
5. <span data-ttu-id="59a3d-190">在記錄搜尋中，按一下 [警示]。</span><span class="sxs-lookup"><span data-stu-id="59a3d-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="59a3d-191">![在搜尋中建立警示](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="59a3d-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="59a3d-192">在 [新增警示規則] 頁面上，設定您要的適當屬性和特定臨界值，然後按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="59a3d-192">On the **Add Alert Rule** page, configure the appropriate properties and the specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="59a3d-193">![新增警示規則](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="59a3d-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="59a3d-194">對 Azure SQL 分析資料採取行動</span><span class="sxs-lookup"><span data-stu-id="59a3d-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="59a3d-195">做為範例，您可以執行的其中一個最有用查詢，是跨所有 Azure 訂用帳戶比較所有 Azure SQL 彈性集區的 DTU 使用量。</span><span class="sxs-lookup"><span data-stu-id="59a3d-195">As an example, one of the most useful queries that you can perform is to compare the DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="59a3d-196">資料庫輸送量單位 (DTU) 提供說明 Basic、Standard 和 Premium 資料庫與集區的效能層級相對容量。</span><span class="sxs-lookup"><span data-stu-id="59a3d-196">Database Throughput Unit (DTU) provides a way to describe the relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="59a3d-197">DTU 是根據 CPU、記憶體、讀與寫的混合測量。</span><span class="sxs-lookup"><span data-stu-id="59a3d-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="59a3d-198">當 DTU 增加時，會增加效能層級所提供的強大功能。</span><span class="sxs-lookup"><span data-stu-id="59a3d-198">As DTUs increase, the power offered by the performance level increases.</span></span> <span data-ttu-id="59a3d-199">例如，具有 5 個 DTU 的效能層級比具有 1 個 DTU 的效能層級有五倍的能力。</span><span class="sxs-lookup"><span data-stu-id="59a3d-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="59a3d-200">最大 DTU 配額適用於每個伺服器和彈性集區。</span><span class="sxs-lookup"><span data-stu-id="59a3d-200">A maximum DTU quota applies to each server and elastic pool.</span></span>

<span data-ttu-id="59a3d-201">藉由執行下列記錄搜尋查詢，您可以輕易地分辨是否未充分使用或過度使用您的 SQL Azure 彈性集區。</span><span class="sxs-lookup"><span data-stu-id="59a3d-201">By running the following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="59a3d-202">如果您的工作區已升級為[新的 Log Analytics 查詢語言](log-analytics-log-search-upgrade.md)，則以上查詢會變更如下。</span><span class="sxs-lookup"><span data-stu-id="59a3d-202">If your workspace has been upgraded to the [new Log Analytics query language](log-analytics-log-search-upgrade.md), then the above query would change to the following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="59a3d-203">在下列範例中，您可以看到一個彈性集區有接近 100 % DTU 的高使用量，而有些則有極少的使用量。</span><span class="sxs-lookup"><span data-stu-id="59a3d-203">In the following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="59a3d-204">您可以進一步調查以在您環境中使用 Azure 活動記錄疑難排解潛在的最新變更。</span><span class="sxs-lookup"><span data-stu-id="59a3d-204">You can investigate further to troubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![記錄搜尋結果 - 高使用率](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="59a3d-206">另請參閱</span><span class="sxs-lookup"><span data-stu-id="59a3d-206">See also</span></span>

- <span data-ttu-id="59a3d-207">使用 Log Analytics 中的[記錄搜尋](log-analytics-log-searches.md)來檢視詳細的 Azure SQL 資料。</span><span class="sxs-lookup"><span data-stu-id="59a3d-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics to view detailed Azure SQL data.</span></span>
- <span data-ttu-id="59a3d-208">[建立您自己的儀表板](log-analytics-dashboards.md)來顯示 Azure SQL 資料。</span><span class="sxs-lookup"><span data-stu-id="59a3d-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="59a3d-209">在特定的 Azure SQL 事件發生時[建立警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="59a3d-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
