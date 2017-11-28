---
title: "aaaAzure 記錄分析中的 SQL 分析解決方案 |Microsoft 文件"
description: "hello Azure SQL 分析解決方案，可協助您管理 Azure SQL 資料庫。"
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
ms.openlocfilehash: fe228bb3cb3f9d578a84707c3917f02fbeb8a627
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-azure-sql-database-using-azure-sql-analytics-preview-in-log-analytics"></a><span data-ttu-id="1e342-103">使用 Azure SQL Database (預覽) 監視 Log Analytics 中的 Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1e342-103">Monitor Azure SQL Database using Azure SQL Analytics (Preview) in Log Analytics</span></span>

![Azure SQL 分析符號](./media/log-analytics-azure-sql/azure-sql-symbol.png)

<span data-ttu-id="1e342-105">hello Azure SQL 分析方案中 Azure 記錄分析會收集，並以視覺化方式檢視重要的 SQL Azure 效能度量。</span><span class="sxs-lookup"><span data-stu-id="1e342-105">hello Azure SQL Analytics solution in Azure Log Analytics collects and visualizes important SQL Azure performance metrics.</span></span> <span data-ttu-id="1e342-106">藉由使用 hello 解決方案收集的 hello 度量，您可以建立自訂的監視規則和警示。</span><span class="sxs-lookup"><span data-stu-id="1e342-106">By using hello metrics that you collect with hello solution, you can create custom monitoring rules and alerts.</span></span> <span data-ttu-id="1e342-107">而且，您可以跨多個 Azure 訂用帳戶和彈性集區監視 Azure SQL Database 和彈性集區計量，並將其視覺化。</span><span class="sxs-lookup"><span data-stu-id="1e342-107">And, you can monitor Azure SQL Database and elastic pool metrics across multiple Azure subscriptions and elastic pools and visualize them.</span></span> <span data-ttu-id="1e342-108">hello 解決方案也可協助您在應用程式堆疊的每個圖層的 tooidentify 問題。</span><span class="sxs-lookup"><span data-stu-id="1e342-108">hello solution also helps you tooidentify issues at each layer of your application stack.</span></span>  <span data-ttu-id="1e342-109">它會使用[Azure 診斷度量](log-analytics-azure-storage.md)一起記錄分析檢視所有您 Azure SQL database 和彈性集區 toopresent 資料單一記錄分析工作區中。</span><span class="sxs-lookup"><span data-stu-id="1e342-109">It uses [Azure Diagnostic metrics](log-analytics-azure-storage.md) together with Log Analytics views toopresent data about all your Azure SQL databases and elastic pools in a single Log Analytics workspace.</span></span>

<span data-ttu-id="1e342-110">目前，此預覽方案最多可支援 too150 000 Azure SQL Database 和 5000 的 SQL 彈性集區，每個工作區。</span><span class="sxs-lookup"><span data-stu-id="1e342-110">Currently, this preview solution supports up too150,000 Azure SQL Databases and 5,000 SQL Elastic Pools per workspace.</span></span>

<span data-ttu-id="1e342-111">hello Azure SQL 分析解決方案，像其他可供記錄分析可協助您監視並收到通知您的 Azure 資源 hello 健全狀況 — 在此情況下，Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="1e342-111">hello Azure SQL Analytics solution, like others available for Log Analytics, helps you monitor and receive notifications about hello health of your Azure resources—in this case, Azure SQL Database.</span></span> <span data-ttu-id="1e342-112">Microsoft Azure SQL Database 會提供熟悉的 SQL Server 類似功能 tooapplications hello Azure 雲端中執行的可延展的關聯式資料庫服務。</span><span class="sxs-lookup"><span data-stu-id="1e342-112">Microsoft Azure SQL Database is a scalable relational database service that provides familiar SQL-Server-like capabilities tooapplications running in hello Azure cloud.</span></span> <span data-ttu-id="1e342-113">記錄分析可協助您 toocollect、 相互關聯，並將視覺化結構化及未結構化資料。</span><span class="sxs-lookup"><span data-stu-id="1e342-113">Log Analytics helps you toocollect, correlate, and visualize structured and unstructured data.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="1e342-114">連接的來源</span><span class="sxs-lookup"><span data-stu-id="1e342-114">Connected sources</span></span>

<span data-ttu-id="1e342-115">hello Azure SQL 分析解決方案不會使用代理程式 tooconnect toohello 記錄分析服務。</span><span class="sxs-lookup"><span data-stu-id="1e342-115">hello Azure SQL Analytics solution doesn't use agents tooconnect toohello Log Analytics service.</span></span>

<span data-ttu-id="1e342-116">hello 下表描述此解決方案所支援的 hello 連接來源。</span><span class="sxs-lookup"><span data-stu-id="1e342-116">hello following table describes hello connected sources that are supported by this solution.</span></span>

| <span data-ttu-id="1e342-117">連接的來源</span><span class="sxs-lookup"><span data-stu-id="1e342-117">Connected Source</span></span> | <span data-ttu-id="1e342-118">支援</span><span class="sxs-lookup"><span data-stu-id="1e342-118">Support</span></span> | <span data-ttu-id="1e342-119">說明</span><span class="sxs-lookup"><span data-stu-id="1e342-119">Description</span></span> |
| --- | --- | --- |
| [<span data-ttu-id="1e342-120">Windows 代理程式</span><span class="sxs-lookup"><span data-stu-id="1e342-120">Windows agents</span></span>](log-analytics-windows-agents.md) | <span data-ttu-id="1e342-121">否</span><span class="sxs-lookup"><span data-stu-id="1e342-121">No</span></span> | <span data-ttu-id="1e342-122">Hello 解決方案不會使用直接的 Windows 代理程式。</span><span class="sxs-lookup"><span data-stu-id="1e342-122">Direct Windows agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="1e342-123">Linux 代理程式</span><span class="sxs-lookup"><span data-stu-id="1e342-123">Linux agents</span></span>](log-analytics-linux-agents.md) | <span data-ttu-id="1e342-124">否</span><span class="sxs-lookup"><span data-stu-id="1e342-124">No</span></span> | <span data-ttu-id="1e342-125">Hello 解決方案不會使用直接 Linux 代理程式。</span><span class="sxs-lookup"><span data-stu-id="1e342-125">Direct Linux agents are not used by hello solution.</span></span> |
| [<span data-ttu-id="1e342-126">SCOM 管理群組</span><span class="sxs-lookup"><span data-stu-id="1e342-126">SCOM management group</span></span>](log-analytics-om-agents.md) | <span data-ttu-id="1e342-127">否</span><span class="sxs-lookup"><span data-stu-id="1e342-127">No</span></span> | <span data-ttu-id="1e342-128">從 hello SCOM 代理程式 tooLog 分析的直接連接不是由 hello 方案。</span><span class="sxs-lookup"><span data-stu-id="1e342-128">A direct connection from hello SCOM agent tooLog Analytics is not used by hello solution.</span></span> |
| [<span data-ttu-id="1e342-129">Azure 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="1e342-129">Azure storage account</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="1e342-130">否</span><span class="sxs-lookup"><span data-stu-id="1e342-130">No</span></span> | <span data-ttu-id="1e342-131">記錄分析不會從儲存體帳戶讀取 hello 的資料。</span><span class="sxs-lookup"><span data-stu-id="1e342-131">Log Analytics does not read hello data from a storage account.</span></span> |
| [<span data-ttu-id="1e342-132">Azure 診斷</span><span class="sxs-lookup"><span data-stu-id="1e342-132">Azure diagnostics</span></span>](log-analytics-azure-storage.md) | <span data-ttu-id="1e342-133">是</span><span class="sxs-lookup"><span data-stu-id="1e342-133">Yes</span></span> | <span data-ttu-id="1e342-134">Azure 的度量資料是直接由 Azure 傳送 tooLog 分析。</span><span class="sxs-lookup"><span data-stu-id="1e342-134">Azure metric data is sent tooLog Analytics directly by Azure.</span></span> |

## <a name="prerequisites"></a><span data-ttu-id="1e342-135">必要條件</span><span class="sxs-lookup"><span data-stu-id="1e342-135">Prerequisites</span></span>

- <span data-ttu-id="1e342-136">Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="1e342-136">An Azure Subscription.</span></span> <span data-ttu-id="1e342-137">如果您沒有帳戶，您可以[免費](https://azure.microsoft.com/free/)建立一個。</span><span class="sxs-lookup"><span data-stu-id="1e342-137">If you don't have one, you can create one for [free](https://azure.microsoft.com/free/).</span></span>
- <span data-ttu-id="1e342-138">Log Analytics 工作區。</span><span class="sxs-lookup"><span data-stu-id="1e342-138">A Log Analytics workspace.</span></span> <span data-ttu-id="1e342-139">您可以使用現有的帳戶，或者您可以在開始使用此解決方案之前[建立一個新的](log-analytics-get-started.md)。</span><span class="sxs-lookup"><span data-stu-id="1e342-139">You can use an existing one, or you can [create a new one](log-analytics-get-started.md) before you start using this solution.</span></span>
- <span data-ttu-id="1e342-140">啟用 Azure 診斷，您的 Azure SQL database 彈性集區和[設定它們 toosend 其資料 tooLog 分析](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="1e342-140">Enable Azure Diagnostics for your Azure SQL databases and elastic pools and [configure them toosend their data tooLog Analytics](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span>

## <a name="configuration"></a><span data-ttu-id="1e342-141">組態</span><span class="sxs-lookup"><span data-stu-id="1e342-141">Configuration</span></span>

<span data-ttu-id="1e342-142">執行下列步驟 tooadd hello Azure SQL 分析方案 tooyour 工作區的 hello。</span><span class="sxs-lookup"><span data-stu-id="1e342-142">Perform hello following steps tooadd hello Azure SQL Analytics solution tooyour workspace.</span></span>

1. <span data-ttu-id="1e342-143">新增 hello Azure SQL 分析方案 tooyour 從工作區[Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview)或使用 hello 程序中所述[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。</span><span class="sxs-lookup"><span data-stu-id="1e342-143">Add hello Azure SQL Analytics solution tooyour workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/Microsoft.AzureSQLAnalyticsOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
2. <span data-ttu-id="1e342-144">在 [hello Azure 入口網站，按一下 [**新增**（hello + 符號），然後在 [hello] 清單中的資源，選取**監視 + 管理**。</span><span class="sxs-lookup"><span data-stu-id="1e342-144">In hello Azure portal, click **New** (hello + symbol), then in hello list of resources, select **Monitoring + Management**.</span></span>  
    <span data-ttu-id="1e342-145">![監視 + 管理](./media/log-analytics-azure-sql/monitoring-management.png)</span><span class="sxs-lookup"><span data-stu-id="1e342-145">![Monitoring + Management](./media/log-analytics-azure-sql/monitoring-management.png)</span></span>
3. <span data-ttu-id="1e342-146">在 [hello**監視 + 管理**清單中按一下**查看所有**。</span><span class="sxs-lookup"><span data-stu-id="1e342-146">In hello **Monitoring + Management** list click **See all**.</span></span>
4. <span data-ttu-id="1e342-147">在 hello**建議**清單中，按一下**詳細**，然後在 hello 新清單中，尋找**Azure SQL 分析 （預覽）**並加以選取。</span><span class="sxs-lookup"><span data-stu-id="1e342-147">In hello **Recommended** list, click **More** , and then in hello new list, find **Azure SQL Analytics (Preview)** and then select it.</span></span>  
    <span data-ttu-id="1e342-148">![Azure SQL 分析解決方案](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span><span class="sxs-lookup"><span data-stu-id="1e342-148">![Azure SQL Analytics solution](./media/log-analytics-azure-sql/azure-sql-solution-portal.png)</span></span>
5. <span data-ttu-id="1e342-149">在 [hello **Azure SQL 分析 （預覽）**刀鋒視窗中，按一下 [**建立**。</span><span class="sxs-lookup"><span data-stu-id="1e342-149">In hello **Azure SQL Analytics (Preview)** blade, click **Create**.</span></span>  
    <span data-ttu-id="1e342-150">![建立](./media/log-analytics-azure-sql/portal-create.png)</span><span class="sxs-lookup"><span data-stu-id="1e342-150">![Create](./media/log-analytics-azure-sql/portal-create.png)</span></span>
6. <span data-ttu-id="1e342-151">在 [hello**建立新方案**刀鋒視窗中，選取 hello 工作區中，使用您想 tooadd hello 方案 tooand，然後按一下**建立**。</span><span class="sxs-lookup"><span data-stu-id="1e342-151">In hello **Create new solution** blade, select hello workspace that you want tooadd hello solution tooand then click **Create**.</span></span>  
    <span data-ttu-id="1e342-152">![新增 tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="1e342-152">![add tooworkspace](./media/log-analytics-azure-sql/add-to-workspace.png)</span></span>


### <a name="tooconfigure-multiple-azure-subscriptions"></a><span data-ttu-id="1e342-153">tooconfigure 多個 Azure 訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1e342-153">tooconfigure multiple Azure subscriptions</span></span>

<span data-ttu-id="1e342-154">toosupport 多個訂閱，使用中的 hello PowerShell 指令碼[使用 PowerShell 啟用 Azure 資源計量記錄](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/)。</span><span class="sxs-lookup"><span data-stu-id="1e342-154">toosupport multiple subscriptions, use hello PowerShell script from [Enable Azure resource metrics logging using PowerShell](https://blogs.technet.microsoft.com/msoms/2017/01/17/enable-azure-resource-metrics-logging-using-powershell/).</span></span> <span data-ttu-id="1e342-155">從一個 Azure 訂用帳戶 tooa] 工作區中另一個 Azure 訂用帳戶的資源執行 hello 指令碼 toosend 診斷資料時，會當做參數提供 hello 工作區的資源識別碼。</span><span class="sxs-lookup"><span data-stu-id="1e342-155">Provide hello workspace resource ID as a parameter when executing hello script toosend diagnostic data from resources in one Azure subscription tooa workspace in another Azure subscription.</span></span>

<span data-ttu-id="1e342-156">**範例**</span><span class="sxs-lookup"><span data-stu-id="1e342-156">**Example**</span></span>

```
PS C:\> $WSID = "/subscriptions/<subID>/resourcegroups/oms/providers/microsoft.operationalinsights/workspaces/omsws"
```

```
PS C:\> .\Enable-AzureRMDiagnostics.ps1 -WSID $WSID
```

## <a name="using-hello-solution"></a><span data-ttu-id="1e342-157">使用 hello 解決方案</span><span class="sxs-lookup"><span data-stu-id="1e342-157">Using hello solution</span></span>

<span data-ttu-id="1e342-158">當您新增 hello 方案 tooyour 工作區時，hello Azure SQL 分析磚加入 tooyour 工作區中，並出現在 [概觀]。</span><span class="sxs-lookup"><span data-stu-id="1e342-158">When you add hello solution tooyour workspace, hello Azure SQL Analytics tile is added tooyour workspace, and it appears in Overview.</span></span> <span data-ttu-id="1e342-159">hello 磚會顯示 hello Azure SQL database 和 hello 方案連接到 Azure SQL 彈性集區數目。</span><span class="sxs-lookup"><span data-stu-id="1e342-159">hello tile shows hello number of Azure SQL databases and Azure SQL elastic pools that hello solution is connected to.</span></span>

![Azure SQL 分析圖格](./media/log-analytics-azure-sql/azure-sql-sol-tile.png)

### <a name="viewing-azure-sql-analytics-data"></a><span data-ttu-id="1e342-161">檢視 Azure SQL 分析資料</span><span class="sxs-lookup"><span data-stu-id="1e342-161">Viewing Azure SQL Analytics data</span></span>

<span data-ttu-id="1e342-162">按一下 hello **Azure SQL 分析**磚 tooopen hello Azure SQL 分析儀表板。</span><span class="sxs-lookup"><span data-stu-id="1e342-162">Click on hello **Azure SQL Analytics** tile tooopen hello Azure SQL Analytics dashboard.</span></span> <span data-ttu-id="1e342-163">hello 儀表板包括下列定義 hello 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="1e342-163">hello dashboard includes hello blades defined below.</span></span> <span data-ttu-id="1e342-164">每個刀鋒視窗會列出 too15 資源 （訂用帳戶、 伺服器、 彈性集區，以及資料庫）。</span><span class="sxs-lookup"><span data-stu-id="1e342-164">Each blade lists up too15 resources (subscription, server, elastic pool, and database).</span></span> <span data-ttu-id="1e342-165">按一下任何 hello 資源 tooopen hello 儀表板的該特定資源。</span><span class="sxs-lookup"><span data-stu-id="1e342-165">Click any of hello resources tooopen hello dashboard for that specific resource.</span></span> <span data-ttu-id="1e342-166">彈性集區或資料庫包含 hello 與所選取資源度量的圖表。</span><span class="sxs-lookup"><span data-stu-id="1e342-166">Elastic Pool or Database contains hello charts with metrics for a selected resource.</span></span> <span data-ttu-id="1e342-167">按一下圖表 tooopen hello 記錄搜尋] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="1e342-167">Click a chart tooopen hello Log Search dialog.</span></span>

| <span data-ttu-id="1e342-168">刀鋒視窗</span><span class="sxs-lookup"><span data-stu-id="1e342-168">Blade</span></span> | <span data-ttu-id="1e342-169">說明</span><span class="sxs-lookup"><span data-stu-id="1e342-169">Description</span></span> |
|---|---|
| <span data-ttu-id="1e342-170">訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="1e342-170">Subscriptions</span></span> | <span data-ttu-id="1e342-171">具有已連線伺服器、集區及資料庫數目的訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="1e342-171">List of subscriptions with number of connected servers, pools, and databases.</span></span> |
| <span data-ttu-id="1e342-172">伺服器</span><span class="sxs-lookup"><span data-stu-id="1e342-172">Servers</span></span> | <span data-ttu-id="1e342-173">具有已連線集區和資料庫數目的伺服器清單。</span><span class="sxs-lookup"><span data-stu-id="1e342-173">List of servers with number of connected pools and databases.</span></span> |
| <span data-ttu-id="1e342-174">彈性集區</span><span class="sxs-lookup"><span data-stu-id="1e342-174">Elastic Pools</span></span> | <span data-ttu-id="1e342-175">最大的 GB 和 eDTU 中觀察到的 hello 與已連線的彈性集區的清單期間。</span><span class="sxs-lookup"><span data-stu-id="1e342-175">List of connected elastic pools with maximum GB and eDTU in hello observed period.</span></span> |
|<span data-ttu-id="1e342-176">資料庫</span><span class="sxs-lookup"><span data-stu-id="1e342-176">Databases</span></span> | <span data-ttu-id="1e342-177">連接中的資料庫清單與最大 GB DTU hello 觀察到期限。</span><span class="sxs-lookup"><span data-stu-id="1e342-177">List of connected databases with maximum GB and DTU in hello observed period.</span></span>|


### <a name="analyze-data-and-create-alerts"></a><span data-ttu-id="1e342-178">分析資料並建立警示</span><span class="sxs-lookup"><span data-stu-id="1e342-178">Analyze data and create alerts</span></span>

<span data-ttu-id="1e342-179">您可以使用 Azure SQL Database 資源從 hello 資料輕鬆建立警示。</span><span class="sxs-lookup"><span data-stu-id="1e342-179">You can easily create alerts with hello data coming from Azure SQL Database resources.</span></span> <span data-ttu-id="1e342-180">以下是您可用於警示的一些實用[記錄搜尋](log-analytics-log-searches.md)查詢：</span><span class="sxs-lookup"><span data-stu-id="1e342-180">Here are a couple of useful [log search](log-analytics-log-searches.md) queries that you can use for alerting:</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]


<span data-ttu-id="1e342-181">Azure SQL Database 上的高 DTU</span><span class="sxs-lookup"><span data-stu-id="1e342-181">*High DTU on Azure SQL Database*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/DATABASES/"* MetricName=dtu_consumption_percent | measure Avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="1e342-182">Azure SQL Database 彈性集區上的高 DTU</span><span class="sxs-lookup"><span data-stu-id="1e342-182">*High DTU on Azure SQL Database Elastic Pool*</span></span>

```
Type=AzureMetrics ResourceProvider="MICROSOFT.SQL" ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource interval 5minutes
```

<span data-ttu-id="1e342-183">您可以使用這些警示為基礎的查詢 tooalert 上特定閾值，Azure SQL Database 和彈性集區。</span><span class="sxs-lookup"><span data-stu-id="1e342-183">You can use these alert-based queries tooalert on specific thresholds for both Azure SQL Database and elastic pools.</span></span> <span data-ttu-id="1e342-184">tooconfigure OMS 工作區的警示：</span><span class="sxs-lookup"><span data-stu-id="1e342-184">tooconfigure an alert for your OMS workspace:</span></span>

#### <a name="tooconfigure-an-alert-for-your-workspace"></a><span data-ttu-id="1e342-185">tooconfigure 您的工作區的警示</span><span class="sxs-lookup"><span data-stu-id="1e342-185">tooconfigure an alert for your workspace</span></span>

1. <span data-ttu-id="1e342-186">移 toohello [OMS 入口網站](http://mms.microsoft.com/)並登入。</span><span class="sxs-lookup"><span data-stu-id="1e342-186">Go toohello [OMS portal](http://mms.microsoft.com/) and sign in.</span></span>
2. <span data-ttu-id="1e342-187">開啟您已設定為 hello 方案的 hello 工作區。</span><span class="sxs-lookup"><span data-stu-id="1e342-187">Open hello workspace that you have configured for hello solution.</span></span>
3. <span data-ttu-id="1e342-188">在 hello 概觀頁面上，按一下 [hello **Azure SQL 分析 （預覽）**磚。</span><span class="sxs-lookup"><span data-stu-id="1e342-188">On hello Overview page, click hello **Azure SQL Analytics (Preview)** tile.</span></span>
4. <span data-ttu-id="1e342-189">執行的其中一個 hello 範例查詢。</span><span class="sxs-lookup"><span data-stu-id="1e342-189">Run one of hello example queries.</span></span>
5. <span data-ttu-id="1e342-190">在記錄搜尋中，按一下 [警示]。</span><span class="sxs-lookup"><span data-stu-id="1e342-190">In Log Search, click **Alert**.</span></span>  
<span data-ttu-id="1e342-191">![在搜尋中建立警示](./media/log-analytics-azure-sql/create-alert01.png)</span><span class="sxs-lookup"><span data-stu-id="1e342-191">![create alert in search](./media/log-analytics-azure-sql/create-alert01.png)</span></span>
6. <span data-ttu-id="1e342-192">在 [hello**加入警示規則**頁面上，設定 hello 適當的屬性和 hello 特定的臨界值，然後再按一下**儲存**。</span><span class="sxs-lookup"><span data-stu-id="1e342-192">On hello **Add Alert Rule** page, configure hello appropriate properties and hello specific thresholds that you want and then click **Save**.</span></span>  
<span data-ttu-id="1e342-193">![新增警示規則](./media/log-analytics-azure-sql/create-alert02.png)</span><span class="sxs-lookup"><span data-stu-id="1e342-193">![add alert rule](./media/log-analytics-azure-sql/create-alert02.png)</span></span>

### <a name="act-on-azure-sql-analytics-data"></a><span data-ttu-id="1e342-194">對 Azure SQL 分析資料採取行動</span><span class="sxs-lookup"><span data-stu-id="1e342-194">Act on Azure SQL Analytics data</span></span>

<span data-ttu-id="1e342-195">例如，其中一個 hello 最有用的查詢，您可以執行。 所有 Azure SQL 彈性集區 toocompare hello DTU 使用率在所有 Azure 訂閱</span><span class="sxs-lookup"><span data-stu-id="1e342-195">As an example, one of hello most useful queries that you can perform is toocompare hello DTU utilization for all Azure SQL Elastic Pools across all your Azure subscriptions.</span></span> <span data-ttu-id="1e342-196">資料庫輸送量單元 (DTU) 提供方式 toodescribe hello Basic、 Standard 和 Premium 資料庫與集區的效能層級的相對容量。</span><span class="sxs-lookup"><span data-stu-id="1e342-196">Database Throughput Unit (DTU) provides a way toodescribe hello relative capacity of a performance level of Basic, Standard, and Premium databases and pools.</span></span> <span data-ttu-id="1e342-197">DTU 是根據 CPU、記憶體、讀與寫的混合測量。</span><span class="sxs-lookup"><span data-stu-id="1e342-197">DTUs are based on a blended measure of CPU, memory, reads, and writes.</span></span> <span data-ttu-id="1e342-198">當 Dtu 增加時，hello hello 的效能層級提升所提供的電源。</span><span class="sxs-lookup"><span data-stu-id="1e342-198">As DTUs increase, hello power offered by hello performance level increases.</span></span> <span data-ttu-id="1e342-199">例如，具有 5 個 DTU 的效能層級比具有 1 個 DTU 的效能層級有五倍的能力。</span><span class="sxs-lookup"><span data-stu-id="1e342-199">For example, a performance level with 5 DTUs has five times more power than a performance level with 1 DTU.</span></span> <span data-ttu-id="1e342-200">DTU 配額上限，適用於 tooeach 伺服器和彈性集區。</span><span class="sxs-lookup"><span data-stu-id="1e342-200">A maximum DTU quota applies tooeach server and elastic pool.</span></span>

<span data-ttu-id="1e342-201">藉由執行 hello 下列記錄搜尋查詢，您可以輕易地分辨您是否未充分使用或超過利用您 SQL Azure 的彈性集區。</span><span class="sxs-lookup"><span data-stu-id="1e342-201">By running hello following Log Search query, you can easily tell if you are underutilizing or over utilizing your SQL Azure elastic pools.</span></span>

```
Type=AzureMetrics ResourceId=*"/ELASTICPOOLS/"* MetricName=dtu_consumption_percent | measure avg(Average) by Resource | display LineChart
```

>[!NOTE]
> <span data-ttu-id="1e342-202">如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，然後 hello 上述查詢會變更 toohello 下列。</span><span class="sxs-lookup"><span data-stu-id="1e342-202">If your workspace has been upgraded toohello [new Log Analytics query language](log-analytics-log-search-upgrade.md), then hello above query would change toohello following.</span></span>
>
>`search in (AzureMetrics) isnotempty(ResourceId) and "/ELASTICPOOLS/" and MetricName == "dtu_consumption_percent" | summarize AggregatedValue = avg(Average) by bin(TimeGenerated, 1h), Resource | render timechart`

<span data-ttu-id="1e342-203">在下列範例的 hello，您可以看到一個彈性集區具有高使用量接近 100 %dtu 而有些則擁有非常少的使用量。</span><span class="sxs-lookup"><span data-stu-id="1e342-203">In hello following example, you can see that one elastic pool has a high usage near 100% DTU while others have very little usage.</span></span> <span data-ttu-id="1e342-204">您可以調查進一步 tootroubleshoot 潛在最近的變更，在您環境中使用 Azure 活動記錄檔。</span><span class="sxs-lookup"><span data-stu-id="1e342-204">You can investigate further tootroubleshoot potential recent changes in your environment using Azure Activity logs.</span></span>

![記錄搜尋結果 - 高使用率](./media/log-analytics-azure-sql/log-search-high-util.png)

## <a name="see-also"></a><span data-ttu-id="1e342-206">另請參閱</span><span class="sxs-lookup"><span data-stu-id="1e342-206">See also</span></span>

- <span data-ttu-id="1e342-207">使用[記錄搜尋](log-analytics-log-searches.md)記錄分析 tooview 中詳細的 Azure SQL 資料。</span><span class="sxs-lookup"><span data-stu-id="1e342-207">Use [Log Searches](log-analytics-log-searches.md) in Log Analytics tooview detailed Azure SQL data.</span></span>
- <span data-ttu-id="1e342-208">[建立您自己的儀表板](log-analytics-dashboards.md)來顯示 Azure SQL 資料。</span><span class="sxs-lookup"><span data-stu-id="1e342-208">[Create your own dashboards](log-analytics-dashboards.md) showing Azure SQL data.</span></span>
- <span data-ttu-id="1e342-209">在特定的 Azure SQL 事件發生時[建立警示](log-analytics-alerts.md)。</span><span class="sxs-lookup"><span data-stu-id="1e342-209">[Create alerts](log-analytics-alerts.md) when specific Azure SQL events occur.</span></span>
